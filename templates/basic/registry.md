# Registry Pattern

This pattern avoids hardcoding logic like ifelse by storing the behaviour in a central registry e.g. dictionary.

Rather than calling functions directly, you register then and later call them dynamically.

## Example

```python
# Function relying on checks
def check_function(data: annot, param2: str) -> None:

    # Check 1
    if param2 == 'string1':
        function1(data)
    # Check 2
    if param2 == 'string2':
        function2(data)
    # Check 3
    if param3 == 'string3':
        function3(data)
```

This function relies on hardcoded checks that are not scalable if more values for `param2` are added, and then checks are required.

A registry of functions and related strings can be defined **after** function definition to produce a scalable method of applying behaviours.

```python
# Define registry as a dictionary of string keys tied to function values
registry = {
    'string1': function1,
    'string2': function2,
    'string3': function3,
}
```

This allows the original function to be rewritten using the registry.

```python
def check_function(data: annot, param2: str) -> None:
    # Get function registered to param2 string
    data_function = registry.get(param2)
    # Apply function to data
    data_function(data)
```

If a new relevant function is defined, it can easily be added to the registry, with no change required in `check_function()`.
