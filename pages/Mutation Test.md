
- mutpyを使う
    - [https://pypi.python.org/pypi/MutPy/0.4.0](https://pypi.python.org/pypi/MutPy/0.4.0)
- mutpyを使うために雑にunittestを作る
- 2系で書いてるなら3系にする必要があるので2to3とかする
python

```
import doctest
from unittest import TestCase
import core

def load_tests(loader, tests, ignore):
    tests.addTests(doctest.DocTestSuite(core))
    return tests 

class SameOutputTest(TestCase):
    def test_output(self):
        import subprocess
        out = subprocess.check_output("python entrypoint.py --algo=algo2 --data=data/data6.csv", shell=True)
        self.assertEqual(file('test_output.txt').read(), out)                                                                                 
```



`mut.py --target core --unit-test test_geister -m -r report.yaml > log.txt`
