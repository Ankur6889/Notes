# Class Based Unit Test in Matlab
The purpose of these notes is to simplify the process of navigating MATLAB documentation. The official documentation can be quite cumbersome, often directing you to various links, resulting in a fragmented learning experience. By consolidating everything sequentially, with examples and key points clearly presented, this document makes it much easier to review and study the concepts. Each section includes links to the original documentation, providing clear references to the source material. This organized approach ensures that all necessary information is easily accessible and comprehensible.

## [Author classed Based Unit Test in MATLAB](https://uk.mathworks.com/help/matlab/matlab_prog/author-class-based-unit-tests-in-matlab.html)
* A test class must inherit from `matlab.unittest.TestCase` and contain a methods block with the `Test` attribute . 
* The methods block contains functions, each of which is a unit test.
* Each unit test is contained within a methods block. The function must accept a TestCase instance as an input.
* Qualifications are methods for testing values and responding to failures. 
``` matlab 
%% Test Class Definition
classdef MyComponentTest < matlab.unittest.TestCase
    
    %% Test Method Block
    methods (Test)
        
        %% Test Function
        function testASolution(testCase)      
            %% Exercise function under test
            % act = the value from the function under test

            %% Verify using test qualification
            % exp = your expected value
            % testCase.<qualification method>(act,exp);
        end
    end
end
```

[List of Qualifications to be used](https://uk.mathworks.com/help/matlab/matlab_prog/types-of-qualifications.html)

## [Write Simple Test Case Using Classes](https://uk.mathworks.com/help/matlab/matlab_prog/write-simple-test-case-using-classes.html)

* This example shows how to write class-based unit tests to qualify the correctness of a function `defined in a file in your current folder.`    
###  quadraticSolver.m
```matlab
function r = quadraticSolver(a,b,c)
% quadraticSolver returns solutions to the
% quadratic equation a*x^2 + b*x + c = 0.

if ~isa(a,'numeric') || ~isa(b,'numeric') || ~isa(c,'numeric')
    error('quadraticSolver:InputMustBeNumeric', ...
        'Coefficients must be numeric.');
end

r(1) = (-b + sqrt(b^2 - 4*a*c)) / (2*a);
r(2) = (-b - sqrt(b^2 - 4*a*c)) / (2*a);

end
```
### SolverTest.m
```matlab
classdef SolverTest < matlab.unittest.TestCase
    methods(Test)
        function realSolution(testCase)
            actSolution = quadraticSolver(1,-3,2);
            expSolution = [2 1];
            testCase.verifyEqual(actSolution,expSolution)
        end
        function imaginarySolution(testCase)
            actSolution = quadraticSolver(1,2,10);
            expSolution = [-1+3i -1-3i];
            testCase.verifyEqual(actSolution,expSolution)
        end
        function nonnumericInput(testCase)
            testCase.verifyError(@()quadraticSolver(1,'-3',2), ...
                'quadraticSolver:InputMustBeNumeric')
        end
    end
end
```
To run all of the tests in the SolverTest class, create a TestCase object from the class and then call the run method on the object.
```matlab
testCase = SolverTest;
results = testCase.run
```
You also can run a single test specified by one of the Test methods. To run a specific Test method, pass the name of the method to run. For example, run the realSolution method.
```matlab
result = run(testCase,'realSolution')
```
## [Analyze Test Case Results](https://uk.mathworks.com/help/matlab/matlab_prog/analyze-testsolver-results.html)
* This example shows how to combine tests into test suites, using the SolverTest test case. 
* Use the static from* methods in the `matlab.unittest.TestSuite` class to create suites for combinations of your tests
### Create Suite from SolverTest class
```matlab
quadTests = matlab.unittest.TestSuite.fromClass(?SolverTest);
result = run(quadTests);
rt = table(result)
```
### Create Suite from SolverTest Calss Definition File 
```matlab
suiteFile = TestSuite.fromFile('SolverTest.m');
result = run(suiteFile);
```
### Create Suite from All Test Case Files in Current Folder
```matlab
suiteFolder = TestSuite.fromFolder(pwd);
result = run(suiteFolder);
```
### Create Suite from Single Test Method
```matlab 
suiteMethod = TestSuite.fromMethod(?SolverTest,'testRealSolution')'
result = run(suiteMethod);
```
## [Write Setup and Teardown Code Using Classes](https://uk.mathworks.com/help/matlab/matlab_prog/write-setup-and-teardown-code-using-classes.html)

### Test Fixtures 
Test fixtures are setup and teardown code that sets up the pretest state of the system and returns it to the original state after running the test. Setup and teardown methods are defined in the TestCase class by these method attributes:
* TestMethodSetup and TestMethodTeardown methods run before and after each Test method.
* TestClassSetup and TestClassTeardown methods run before and after all Test methods in the test class.

Also testing framework executes TestMethodSetup and TestClassSetup, methods of superclasses before those in subclasses. 
`It is good practice to perform all teardown actions from within the TestMethodSetup and TestClassSetup methods blocks using the addTeardown method instead of implementing corresponding teardown methods in the TestMethodTeardown and TestClassTeardown methods blocks. Call addTeardown immediately before or after the original state change, without any other code in between that can throw an exception. Using addTeardown this way allows the testing framework to execute the teardown code in the reverse order of the setup code and also creates exception-safe test content.`

## [Use Parameters in Class-Based Tests](https://uk.mathworks.com/help/matlab/matlab_prog/use-parameters-in-class-based-tests.html)
* With parameterized testing, you can implement code to iteratively run tests using different data values.
* When a method is parameterized, the testing framework automatically invokes the method for each parameter value.
### How to Write Parameterized Tests
* To provide data as parameters in your class-based test, specify the data using a properties block with an appropriate parameterization attribute.
*  Consider the SampleTest class. The class defines a parameterized test because it specifies properties within a properties block with the TestParameter attribute. The properties are passed to Test methods and are used to perform qualifications.
### Example 
```matlab
classdef SampleTest < matlab.unittest.TestCase
    properties (TestParameter)
        numericArray = {int16(1),single(zeros(1,4)),magic(3)};
        functionHandle = {@false,@() size([])};
    end
    methods (Test)
        function test1(testCase,numericArray)
            testCase.verifyNotEmpty(numericArray)
        end
        function test2(testCase,functionHandle)
            testCase.verifyWarningFree(functionHandle)
        end
    end
end
```
The test class results in a parameterized test suite with five elements.
```matlab
suite = testsuite("SampleTest");
{suite.Name}'
```
```ans =

  5×1 cell array

    {'SampleTest/test1(numericArray=int16_1)'          }
    {'SampleTest/test1(numericArray=1x4_single)'       }
    {'SampleTest/test1(numericArray=3x3_double)'       }
    {'SampleTest/test2(functionHandle=@false)'         }
    {'SampleTest/test2(functionHandle=function_handle)'}
```
The value assigned to a parameterization property must be either a nonempty cell array or a scalar structure with at least one field.
### Cell Array as Parameterization Property 
```matlab 
classdef MyTest < matlab.unittest.TestCase
    properties (TestParameter)
        % Define parameterization property as a nonempty cell array
        Value = {1, 2, 3; 'A', 'B', 'C'; true, false, true}
    end
    
    methods (Test)
        function testWithValue(testCase, Value)
            disp(['Testing with Value: ', mat2str(Value)]);
        end
    end
end
```
### Structure as Parameterization Property
```matlab
classdef MyTest < matlab.unittest.TestCase
    properties (TestParameter)
        % Define parameterization property as a structure
        Param = struct('One', 1, 'Two', 2, 'Three', 3)
    end
    
    methods (Test)
        function testWithParam(testCase, Param)
            disp(['Testing with Param: ', num2str(Param)]);
        end
    end
end
```
The Param property is a structure where field names (One, Two, Three) represent parameter names and the corresponding values (1, 2, 3) are the parameter values.

 You can initialize the property at either test class load time or test suite creation time
 * Class Load Time 
 * Suite Creation Time

` To better understand this part use chatgpt`

### Parameterization Levels
---
There are three levels at which you can parameterize a test class: class setup, method setup, and test. Each level requires specific method and property attributes.

1. Class-Setup Level
    * Method Attribute: TestClassSetup
    * Property Attribute: ClassSetupParameter

Example :
```matlab
classdef MyTestClass < matlab.unittest.TestCase
    properties (ClassSetupParameter)
        Param1 = {1, 2, 3}; % Class setup parameter
    end

    methods (TestClassSetup)
        function setupOnce(testCase, Param1)
            disp(['Class setup with Param1: ', num2str(Param1)]);
        end
    end
    
    methods (Test)
        function testExample(testCase)
            disp('Running a test...');
        end
    end
end
```
2. Method-Setup Level
    * Method Attribute: TestMethodSetup
    * Property Attribute: MethodSetupParameter or ClassSetupParameter

A method with the TestMethodSetup attribute runs before each test method. If parameterized, it can access properties defined with MethodSetupParameter or ClassSetupParameter.

Example:
``` matlab 
classdef MyTestClass < matlab.unittest.TestCase
    properties (ClassSetupParameter)
        Param1 = {1, 2}; % Class setup parameter
    end

    properties (MethodSetupParameter)
        Param2 = {'A', 'B'}; % Method setup parameter
    end

    methods (TestClassSetup)
        function setupOnce(testCase, Param1)
            disp(['Class setup with Param1: ', num2str(Param1)]);
        end
    end

    methods (TestMethodSetup)
        function setupEach(testCase, Param2)
            disp(['Method setup with Param2: ', Param2]);
        end
    end
    
    methods (Test)
        function testExample(testCase)
            disp('Running a test...');
        end
    end
end
```
3. Test Level
    * Method Attribute: Test
    * Property Attribute: TestParameter, MethodSetupParameter, or ClassSetupParameter

A method with the Test attribute is a test method. If parameterized, it can access properties defined with TestParameter, MethodSetupParameter, or ClassSetupParameter.

Example: 
```matlab 
classdef MyTestClass < matlab.unittest.TestCase
    properties (ClassSetupParameter)
        Param1 = {1, 2}; % Class setup parameter
    end

    properties (MethodSetupParameter)
        Param2 = {'A', 'B'}; % Method setup parameter
    end

    properties (TestParameter)
        Param3 = {true, false}; % Test parameter
    end

    methods (TestClassSetup)
        function setupOnce(testCase, Param1)
            disp(['Class setup with Param1: ', num2str(Param1)]);
        end
    end

    methods (TestMethodSetup)
        function setupEach(testCase, Param2)
            disp(['Method setup with Param2: ', Param2]);
        end
    end
    
    methods (Test)
        function testExample(testCase, Param3)
            disp(['Running test with Param3: ', num2str(Param3)]);
        end
    end
end
```

## Specify How Parameters Are Combined
* When you pass more than one parameterization property to a method, you can use the ParameterCombination method attribute to specify how parameters are combined.

### 1. Exhaustive Combination
The testing framework uses this as default combination if you do not specify the ParameterCombination attribute.

Example: 
```matlab 
classdef ExhaustiveTest < matlab.unittest.TestCase
    properties (TestParameter)
        a = {1, 2, 3};
        b = {4, 5};
    end
    methods (Test, ParameterCombination="exhaustive")
        function testAddition(testCase, a, b)
            % Perform addition
            result = a + b;
            % Verify the result
            expected = a + b;
            testCase.verifyEqual(result, expected);
        end
    end
end
```
```
suite = testsuite("ExhaustiveTest");
{suite.Name}'
```
Output: 
```
ans =

  6×1 cell array

    {'ExhaustiveTest/testAddition(a=1,b=4)'}
    {'ExhaustiveTest/testAddition(a=1,b=5)'}
    {'ExhaustiveTest/testAddition(a=2,b=4)'}
    {'ExhaustiveTest/testAddition(a=2,b=5)'}
    {'ExhaustiveTest/testAddition(a=3,b=4)'}
    {'ExhaustiveTest/testAddition(a=3,b=5)'}
```
### 2. Sequential Combination 

The parameterization properties must specify the same number of parameter values. For example, if a method is provided with two parameterization properties and each property specifies three parameter values, then the framework invokes the method three times.

Example: 
```matlab
classdef SequentialTest < matlab.unittest.TestCase
    properties (TestParameter)
        x = {1, 2, 3};
        y = {4, 5, 6};
    end
    methods (Test, ParameterCombination="sequential")
        function testMultiplication(testCase, x, y)
            % Perform multiplication
            result = x * y;
            % Verify the result
            expected = x * y;
            testCase.verifyEqual(result, expected);
        end
    end
end
```
```
suite = testsuite("SequentialTest");
{suite.Name}'
```
Output:
ans =

  3×1 cell array

    {'SequentialTest/testMultiplication(x=1,y=4)'}
    {'SequentialTest/testMultiplication(x=2,y=5)'}
    {'SequentialTest/testMultiplication(x=3,y=6)'}

### 3.Pairwise Combination 
The pairwise combination strategy is designed to reduce the number of test cases by ensuring that every pair of parameter values is tested at least once. This is different from the exhaustive combination strategy, which would test every possible combination of all parameter values, resulting in 27 tests (3 rowCounts × 3 columnCounts × 3 types).

In pairwise testing, the testing framework selects a minimal set of test cases that covers all possible pairs of values for any two parameters, while not necessarily covering all possible triples. This approach reduces the number of tests significantly while still providing good coverage.
```matlab
classdef ZerosTest < matlab.unittest.TestCase
    properties (TestParameter)
        rowCount = struct("r1",1,"r2",2,"r3",3);
        columnCount = struct("c1",2,"c2",3,"c3",4);
        type = {'single','double','uint16'};
    end
    methods (Test,ParameterCombination="pairwise")
        function testSize(testCase,rowCount,columnCount,type)
            testCase.verifySize(zeros(rowCount,columnCount,type), ...
                [rowCount columnCount])
        end
    end
end
```


