# Unit testing in python 
## module unittest

### Import module unit test
```python 
import unittest
```
### import the py file you are testing
```python 
import calc
# assuing calc is in the same folder 
```
### create a class with name Test<Name>
```python
class TestCalc(unitTest.TestCase):
```

### create a method for testing the method
```python 
    def test_add(self):
        result = add(10,15)
        self.assertEqual(result, 15)
```

### running the unit test
```bash 
python -m unittest test_calc.py
```

### to run unit test with a simpler command include the unit test file
```python 
if __name__ == "__main__":
    unittest.main()
```

### to test a exception

code 
```python
def divide(x,y):
    # divide function
    if y == 0:
        raise ValueError("Cannot divide by zero")
    return x / y
```
unit test
```python
self.assertRaises(ValueError, calc.divide, 10, 0)
# only the function name is specified and the arguments of the functions are passed seperately
```

#### another way of testing exception
```python
with self.assertRaises(ValueError):
    calc.divide(10, 0)
```

### Setup and tear down methods
```python
# pay close attention to camel case
# setUp will create the data before every test case
def setUp(self):
    self.emp_1 = Employee("firstname","lastname",29384)
def tearDown(self):
    print('teardown')
```
refer the variables in the functions 
```python
def test_email(self):
        self.assertEqual(self.emp_1.email, "Corey.Sampson@gmail.com")
```

### setUpClass and tearDownClass
use these to setup and tear down data at the start and end of all the test cases
```python
@classmethod
def setUpClass(cls):
    print('Setup stuff here')
@classmethod
def tearDownClass(cls):
    print('this class method tears down at the end')
```


### Mocking

code
```python
def monthly_schedule(self,month):
        response = requests.get(f'http://company.com/{self.last}/{month}')
        if response.ok:
            return response.text
        else:
            return 'Bad Request'
```
unit test
```python
from unittest.mock import patch

with patch('employee.requests.get') as mocked_get:
            mocked_get.return_value.ok = True
            mocked_get.return_value.text = "Success"
            schedule = self.emp_1.monthly_schedule('May')
            # to make sure the right url was called
            mocked_get.assert_called_with('http://company.com/Sampson/May')
            self.assertEqual(schedule,"Success")
            # invalid response
            mocked_get.return_value.ok = False
            schedule = self.emp_2.monthly_schedule('June')
            # to make sure the right url was called
            mocked_get.assert_called_with('http://company.com/Smith/j')
            self.assertEqual(schedule,"Bad Request")
```

## module pytest
```bash
pip install pytest
```
### file and the methods should start with test_

### To run the unit test using pytest
```bash
python -m pytest filename.py
```
### To run all the test recursively in all the subfolders user
```bash
python -m pytest
```
### second way of running it is 
```bash
py.test
```
#### see more details
```bash 
py.test -v
``` 
skip a test
```python
import pytest
@pytest.mark.skip(reason="message why the test was skipped")
```
to see why the test was skipped
```bash 
pytest -v -rxs
```
skip with a condition
```python
import pytest
@pytest.mark.skipif(condition,reason="message why the test was skipped")
```
To run tests with a substring in the method name
```bash
pytest -k <name>
```
tagging and running tests
```python
import pytest
@pytest.mark.tagname
def somefunction()
```
```bash
pytest -m tagname
```
run everything other than tag
```bash
pytest -m "not tagname"
```

#### fixtures
Use this instead of writing functions to setup and teardown

```python
import pytest

@pytest.fixture
def function1():
    # do stuff and 
    return something
def test_method1(function1):
    function1.somemethod
```

to see the print messages use
```bash
pytest -v --capture=no
```
to make the fixture run only once set the scope as follows
```python
import pytest

@pytest.fixture(scope="module")
def function1():
```

to tear down use yield
```python
def function1():
    # do stuff and 
    yield something
    object1.close()
    object1.disconnect()
```
use parametrize to test the same method with mutiple values
