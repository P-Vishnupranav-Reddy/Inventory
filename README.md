# Issue Table

Issue	Type	Line(s)	Description	Fix Approach
Use of eval	Security	59	eval("...") can execute arbitrary code (Bandit B307). This is a major security vulnerability.	Removing the eval call.
Mutable Default Argument	Bug	8	logs=[] is a mutable default argument. This list will be shared and persist across all calls to addItem.	Changing the default to logs=None and initializing logs = [] inside the function.
Missing Input Validation	Bug / Robustness	8, 51	addItem accepts invalid types (like 123, "ten") and negative quantities, which can corrupt the stock_data.	Adding type checks (isinstance) and value checks (qty >= 0) and raise a ValueError.
Potential KeyError	Bug	23	getQty directly accesses stock_data[item], which will crash if the item doesn't exist.	Use of stock_data.get(item, 0) to safely return 0 for missing items.
Bare except	Reliability	19-20	except: pass catches all exceptions (including SystemExit) and silently ignores them, hiding bugs.	Catching the specific exception you expect (e.g., KeyError).
Unsafe File Handling	Reliability	26-34	open() is used without a with block, risking resource leaks if an error occurs. No file encoding ("utf-8") is specified.	Using the with open(file, mode, encoding="utf-8") as f: context manager.
Global Variable	Design	6, 28	The code relies on a mutable global stock_data. loadData rebinds it with the global keyword. This makes the code hard to test and reason about.	Passing stock_data as a parameter to functions that need it. Having loadData return the dictionary.
PEP8 Naming	Style	8, 14, 22	Functions use camelCase (e.g., addItem) instead of the PEP8 standard snake_case (e.g., add_item).	Renaming all functions to snake_case.
Missing Docstrings	Maintainability	All	No module or function docstrings exist, making the code's purpose and usage unclear.	Adding a module docstring and docstrings to all functions describing their purpose, arguments, and return values.
Unused Import	Style	2	import logging is included but the logging module is never used.	Removing the import (or, preferably, use it for logging errors instead of print).
Old-Style Formatting	Style	12	Uses old %-style string formatting, which is less readable than f-strings.	Converting "%s: Adding %d..." to an f-string.


# Answers

