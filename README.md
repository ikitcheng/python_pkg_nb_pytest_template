# Python Project template
This repo shows a generic template that incorporates python packages, tests, notebooks and config files for pytest. 

## Scenario 1 (preferred)
```
./
my_pkg/
	__init__.py
    my_script.py
    my_script_2.py
    main.py
tests/
    __init__.py
    test_multiply.py
    test_myscript.py
__init__.py
multiply.py
my_notebook.ipynb
pytest.ini           <- Use so pytest can locate pkgs from ./
.env                 <- Use so VsCode and its extention can locate pkgs from ./
```
* If we don't want to keep writing the package name when importing our own scripts in your module files, then create a pytest config file `pytest.ini` file in the root directory. Inside, write 
```ini
[pytest]
pythonpath = . my_pkg
```
This allows pytest to locate module files in `my_pkg`. In the test files, you would still need to import your scripts prefixed with the package name. You may now run `python -m pytest` or `pytest` in the root directory. If the root directory is also a package itself (i.e. there is an `__init__.py` file) and it contains modules, then in your test files you could use relative imports (e.g. using `..moduleName`). 

To invoke `main.py`, run `python my_pkg/main.py` in the root. 

For the notebook, located outside of `my_pkg` folder, create a `.env` file so VsCode and its extention can locate files inside from `./my_pkg`
```bash
PYTHONPATH="${PYTHONPATH};./my_pkg;"
```

[Source](https://stackoverflow.com/a/72132699/8902929)

## Scenario 2

* If we write import statements as `my_pkg.script_name` in scripts then in the root of the project (i.e. in `./`) invoke  `main.py` using `python -m my_pkg.main`. Run pytest using `python -m pytest` or simply `pytest` in the root directory. This scenario does not require `pytest.ini`.
