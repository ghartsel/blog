---
title: "Indirectly Speaking"
subtitle: A CSS library for creating beautiful Tufte-inspired HTML documents.
description: "If the description field is not empty, its contents will show in the home page instead of the first 140 characters of the post."
date: "2014-03-29"
toc: false
weight: 160
meta: false
math: false
hideDate: true
hideReadTime: true
---

In C, the programming term for calling a function indirectly through a table of function pointers is often referred to as a "dispatch table" or "jump table."

A dispatch table is essentially an array or a structure containing function pointers, where each pointer corresponds to a specific function. By indexing into this table, you can indirectly call the desired function. This technique is commonly used in scenarios like implementing state machines, virtual function tables (in object-oriented programming emulation).

The computer science terminology for calling a function indirectly, without specifying the implementation detail of a "function table," is **"dynamic dispatch"** or **"late binding."**

Key Concepts:

- **Dynamic Dispatch**: This refers to the process of determining which function to call at runtime, rather than at compile time. It allows the program to decide which function to invoke based on conditions or inputs that are only known during execution.

- **Late Binding**: This is a broader term that describes resolving function calls or method implementations at runtime, rather than at compile time. It is often used in object-oriented programming to implement polymorphism, where the specific method to call is determined by the actual type of the object at runtime.

In the context of your question, the paradigm of indirectly calling a function (without specifying how it is implemented) aligns with **dynamic dispatch** or **late binding**. These terms emphasize the runtime decision-making aspect rather than the specific mechanism (like a function table).

The concept you're describing is closely related to the term "indirection" in computer science. Specifically, the paradigm of calling a function indirectly can be referred to as "function indirection" or simply "indirection."

- Indirection refers to the general concept of accessing something (e.g., a value, function, or resource) indirectly, typically through a pointer, reference, or intermediate mechanism.

- In the context of function calls, function indirection means invoking a function not by its name directly, but through an intermediate reference, such as a function pointer, a table, or another abstraction.

The computer science terminology that describes this paradigm is "function indirection" or more specifically "indirect function calls." This refers to the concept of accessing and invoking functions through an intermediary reference (the pointer) rather than calling them directly by name.

The term "level of indirection" is also commonly used when discussing this pattern, referring to the extra step of reference resolution that occurs before the function is actually called.

In academic computer science literature, you might also encounter terms like "dynamic dispatch" or "indirect invocation" to describe this mechanism of runtime function selection and execution.

# Array of Dictionaries

How do I define an array of dictionaries in python? In Python, you can define an array (or more accurately, a list) of dictionaries like this:

```python
array_of_dicts = [
    {"key1": "value1", "key2": "value2"},
    {"keyA": "valueA", "keyB": "valueB"},
    {"keyX": "valueX", "keyY": "valueY"}
]
```

Here’s a breakdown:

- Each dictionary is enclosed in curly braces {}.
- Dictionaries contain key-value pairs separated by colons.
- The list is enclosed in square brackets [], with dictionaries separated by commas.

## Accessing Array Elements

You can access individual dictionaries or their values:

```python
# Access the first dictionary
first_dict = array_of_dicts[0]
print(first_dict)  # Output: {'key1': 'value1', 'key2': 'value2'}

# Access a value within the first dictionary
value = array_of_dicts[0]["key1"]
print(value)  # Output: 'value1'
```

## Adding to the Array

You can add a new dictionary to the list using the append method:

```python
array_of_dicts.append({"keyNew": "valueNew"})
print(array_of_dicts)
```

This structure is useful for handling collections of related data.

How do you access a dictionary element? In Python, you can access elements of a dictionary using its keys. There are a few common ways to do this:

- Using Square Brackets. This is the most straightforward way:

```python
my_dict = {"key1": "value1", "key2": "value2"}
value = my_dict["key1"]
print(value)  # Output: "value1"
```

If the key does not exist, this will raise a KeyError.

- Using the get() Method. This method is safer because it allows you to specify a default value if the key does not exist:

```python
my_dict = {"key1": "value1", "key2": "value2"}
value = my_dict.get("key1")  # Output: "value1"
value = my_dict.get("key3", "default_value")  # Output: "default_value"
```

If no default is provided, get() returns None.

- Using a Loop. If you need to iterate through all key-value pairs:

```python
my_dict = {"key1": "value1", "key2": "value2"}
for key, value in my_dict.items():
    print(f"{key}: {value}")
# Output:
# key1: value1
# key2: value2
```

- Checking for Existence Before Accessing. You can check if a key exists in the dictionary using the in keyword:

```python
my_dict = {"key1": "value1", "key2": "value2"}
if "key1" in my_dict:
    print(my_dict["key1"])  # Output: "value1"
```

# Implementing a State Machine using Indirect Reference

How can the following python code that implements a state machine be improved, and could you share the Python code for the state machine?

```python
# state machine functions

def f00(x): # initial state
    global nextState
    print('state=0, event = 0, param = {}'.format(x))

def f01(x):
    global nextState
    print('state=0, event = 1, param = {}'.format(x))

def f10(x):
    global nextState
    print('state=1, event = 0, param = {}'.format(x))

def f11(x): # terminal state
    global nextState
    print('state=1, event = 1, param = {}'.format(x))

fsm = [
    [{"function": f00, "nextState": 0}, {"function": f01, "nextState": 1}],
    [{"function": f10, "nextState": 1}, {"function": f11, "nextState": 0}]
 ]

# state machine executor
nextState = 0
def handleEvent(event, param):
    global fsm
    global nextState
    fsm[nextState][event]["function"](param)
    nextState = fsm[nextState][event]["nextState"]

# state-machine driven application
event = 0
param = 0
while param < 4:
    handleEvent(event, param)
    event = event ^ 1
    param = param + 1
```

This implementation is functional but has room for improvement in terms of readability, maintainability, and avoiding the use of global variables. Here's a breakdown of potential improvements.

- Eliminate Global Variables. Global variables like nextState and fsm can make the code harder to debug and test. Pass nextState as part of a StateMachine object or a function argument instead.

- Encapsulate the State Machine in a Class. Using a class can organize the code better and allow the state machine to maintain its internal state.

- Use Descriptive Names. Rename variables and functions to improve readability (e.g., fsm → state_transitions, handleEvent → process_event).

- Improve Transition Table Representation. The state-transition table could use named tuples, enums, or a dictionary to make the code more intuitive and maintainable.


## Refactored Code

Here's a refactored version:

```python
from typing import Callable, Any

class StateMachine:
    def __init__(self):
        self.state = 0
        self.state_transitions = [
            [{"function": self.f00, "next_state": 0}, {"function": self.f01, "next_state": 1}],
            [{"function": self.f10, "next_state": 1}, {"function": self.f11, "next_state": 0}]
        ]
    
    def f00(self, x: Any):
        print(f"state=0, event=0, param={x}")

    def f01(self, x: Any):
        print(f"state=0, event=1, param={x}")

    def f10(self, x: Any):
        print(f"state=1, event=0, param={x}")

    def f11(self, x: Any):
        print(f"state=1, event=1, param={x}")

    def process_event(self, event: int, param: Any):
        transition = self.state_transitions[self.state][event]
        transition["function"](param)
        self.state = transition["next_state"]

# State-machine driven application
if __name__ == "__main__":
    sm = StateMachine()
    event, param = 0, 0

    while param < 4:
        sm.process_event(event, param)
        event ^= 1  # Toggle between 0 and 1
        param += 1
```

Improvements explained:

- Encapsulation: The StateMachine class encapsulates all state machine-related logic.
- State Isolation: The state is now an instance variable, avoiding the use of global variables.
- Readability: The state-transition logic and state function definitions are more structured.
- Scalability: It's easier to extend with new states and events.

Can you rewrite the code defining events as literals instead of integers? Certainly. Defining events as literals improves code readability and makes it easier to understand the purpose of each event. Here's the refactored code using event literals:

## Refactored Code with Event Literals

```python
from typing import Callable, Any

class StateMachine:
    EVENT_ZERO = "event_zero"
    EVENT_ONE = "event_one"

    def __init__(self):
        self.state = 0
        self.state_transitions = {
            0: {
                self.EVENT_ZERO: {"function": self.f00, "next_state": 0},
                self.EVENT_ONE: {"function": self.f01, "next_state": 1},
            },
            1: {
                self.EVENT_ZERO: {"function": self.f10, "next_state": 1},
                self.EVENT_ONE: {"function": self.f11, "next_state": 0},
            },
        }

    def f00(self, x: Any):
        print(f"state=0, event=event_zero, param={x}")

    def f01(self, x: Any):
        print(f"state=0, event=event_one, param={x}")

    def f10(self, x: Any):
        print(f"state=1, event=event_zero, param={x}")

    def f11(self, x: Any):
        print(f"state=1, event=event_one, param={x}")

    def process_event(self, event: str, param: Any):
        if event not in self.state_transitions[self.state]:
            raise ValueError(f"Invalid event '{event}' for state {self.state}")
        transition = self.state_transitions[self.state][event]
        transition["function"](param)
        self.state = transition["next_state"]

# State-machine driven application
if __name__ == "__main__":
    sm = StateMachine()
    event = StateMachine.EVENT_ZERO
    param = 0

    while param < 4:
        sm.process_event(event, param)
        # Toggle event between EVENT_ZERO and EVENT_ONE
        event = StateMachine.EVENT_ONE if event == StateMachine.EVENT_ZERO else StateMachine.EVENT_ZERO
        param += 1
```

Key Changes

- Event Literals:

   - Defined events as class-level constants (EVENT_ZERO and EVENT_ONE).
   - Replaced integer event identifiers with these literals.

- Transition Table:
   - Converted the state-transition table to use event literals as keys, making the mapping clear.

- Error Handling:
   - Added a check in process_event to raise a ValueError if an invalid event is provided for the current state.

- Improved Readability:
   - Events now explicitly describe their purpose, avoiding confusion caused by numeric identifiers.

This approach ensures better readability and reduces the likelihood of bugs caused by using incorrect event identifiers.

Can you rewrite the code also defining states as literals instead of integers? Certainly. Defining states as literals improves readability and makes the state machine easier to maintain. Here's the refactored code with both states and events defined as literals:

## Refactored Code with State and Event Literals

```python
from typing import Any

class StateMachine:
    # State literals
    STATE_ZERO = "state_zero"
    STATE_ONE = "state_one"

    # Event literals
    EVENT_ZERO = "event_zero"
    EVENT_ONE = "event_one"

    def __init__(self):
        self.state = self.STATE_ZERO
        self.state_transitions = {
            self.STATE_ZERO: {
                self.EVENT_ZERO: {"function": self.f00, "next_state": self.STATE_ZERO},
                self.EVENT_ONE: {"function": self.f01, "next_state": self.STATE_ONE},
            },
            self.STATE_ONE: {
                self.EVENT_ZERO: {"function": self.f10, "next_state": self.STATE_ONE},
                self.EVENT_ONE: {"function": self.f11, "next_state": self.STATE_ZERO},
            },
        }

    # State-specific functions
    def f00(self, x: Any):
        print(f"state=state_zero, event=event_zero, param={x}")

    def f01(self, x: Any):
        print(f"state=state_zero, event=event_one, param={x}")

    def f10(self, x: Any):
        print(f"state=state_one, event=event_zero, param={x}")

    def f11(self, x: Any):
        print(f"state=state_one, event=event_one, param={x}")

    # State machine processor
    def process_event(self, event: str, param: Any):
        if event not in self.state_transitions[self.state]:
            raise ValueError(f"Invalid event '{event}' for state '{self.state}'")
        transition = self.state_transitions[self.state][event]
        transition["function"](param)
        self.state = transition["next_state"]

# State-machine driven application
if __name__ == "__main__":
    sm = StateMachine()
    event = StateMachine.EVENT_ZERO
    param = 0

    while param < 4:
        sm.process_event(event, param)
        # Toggle event between EVENT_ZERO and EVENT_ONE
        event = StateMachine.EVENT_ONE if event == StateMachine.EVENT_ZERO else StateMachine.EVENT_ZERO
        param += 1
```

Key Changes:

- State Literals:
   - States are defined as class-level constants (STATE_ZERO and STATE_ONE).
   - State identifiers in the transition table now use these literals.

- Event Literals:
   - Events continue to be represented as literals (EVENT_ZERO and EVENT_ONE).

- Improved Readability:
   - Transition logic explicitly uses named states and events, making it self-explanatory.

- Error Handling:
   - An error is raised if an invalid event is attempted for the current state.

- Ease of Extension:
   - Adding new states or events is straightforward, as the literals provide clear documentation within the code.

This version of the code is more maintainable, intuitive, and robust.
