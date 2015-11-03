#summary Recommended coding guidelines for Tryton
#labels Phase-Implementation,Phase-Design

The Tryton Project strongly recommends the following guidelines for code contributed to the Tryton framework and modules:
  * Code style follows in general [PEP 8](http://www.python.org/dev/peps/pep-0008/)
    * Use 4 spaces for indentation.
    * Avoid the usage of `from M import *`, except for the `__init__.py` of modules.
    * If unsure about PEP 8 conformity use [pep8](http://pypi.python.org/pypi/pep8) to check the code (with `ignore=E123,E124,E126,E128`)
    * Breaking lines:
      * Use 4 spaces per bracket pair.
      * Prefer parenthesis over backslash.
      * Break around a binary operator before the operator. (exception to PEP 8)
    * Imitate the existing code, follow conventions you notice when modifying existing code. For example, use the string formatting operator `%` instead of `str.format` when `%` is already used.
  * Good practices for coding in Tryton:
    * Use doc-strings and comments in your code
    * Only use keyword arguments when defining a constructor method.
    * Never pass keyword arguments as positional arguments when calling a method.
    * In the very beginning (right under the doc-string) of a method definition, define all your objects you will use (`self.pool.get(...)`).
    * Try to use the `browse` instead of the `read` method.
  * Naming of modules, classes, variables
    * A name should be as descriptive and as short as possible
    * Naming structure of a model or module must follow these rules:
      * First part left of the name is the general functioning of the module or model,
      * after this comes the less general name parts (= the more specific name parts) of the module or model
      * If you are unsure with naming, please request first on the mailing list or on the IRC channel #tryton
    * For naming modules we use underscore for separating the name parts
    * For naming classes we use [CamelCase](http://en.wikipedia.org/wiki/CamelCase)
    * For naming methods we use underscore for separating the name parts