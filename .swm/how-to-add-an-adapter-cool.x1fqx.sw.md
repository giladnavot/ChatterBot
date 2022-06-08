---
id: x1fqx
name: How to Add an Adapter cool
file_version: 1.0.2
app_version: 0.8.8-1
file_blobs:
  chatterbot/logic/mathematical_evaluation.py: ed6269afd440d361296e9b448fc69aa7c271e979
  chatterbot/logic/__init__.py: e43167beea80696abc4e044a4d2218229b01f507
  examples/memory_sql_example.py: 08855863b6b58145bd69329564855f5f4cfec68a
  examples/terminal_example.py: 73bd605410f2fbe5c1a4ab10a564dcaf5c3a3d10
  chatterbot/adapters.py: 4819b96d7a58c1f3b91a55a9d53e99b0fd1189e1
  chatterbot/logic/logic_adapter.py: bab251cf6481ae9323814015066b2c157298a8ae
  chatterbot/logic/best_match.py: fa6e98999fa39ba645ecee67a69dac2f5baacbe3
  chatterbot/logic/unit_conversion.py: 3cddc5134518a34a1467ba009de3ef94a830822c
  chatterbot/logic/time_adapter.py: 26a84c49997f6fd2bb36c12e7c08e8c1ce5dd2f9
---

This document covers how to create a new Adapter.

An Adapter is {Explain what a Adapter is and its role in the system}

Some examples of `Adapter`[<sup id="2g77vl">↓</sup>](#f-2g77vl)s are `BestMatch`[<sup id="Z7HW4R">↓</sup>](#f-Z7HW4R), `MathematicalEvaluation`[<sup id="Z1DntY4">↓</sup>](#f-Z1DntY4), `TimeLogicAdapter`[<sup id="8SAsH">↓</sup>](#f-8SAsH), and `UnitConversion`[<sup id="1av4A5">↓</sup>](#f-1av4A5).
Note: some of these examples inherit indirectly from `Adapter`[<sup id="2g77vl">↓</sup>](#f-2g77vl).

<br/>

> **NOTE: Inherit from `LogicAdapter`[<sup id="1GFrC0">↓</sup>](#f-1GFrC0)**
>
> Most `Adapter`[<sup id="2g77vl">↓</sup>](#f-2g77vl)s inherit directly from `LogicAdapter`[<sup id="1GFrC0">↓</sup>](#f-1GFrC0) and almost none inherit directly from `Adapter`[<sup id="2g77vl">↓</sup>](#f-2g77vl).
> In this document we demonstrate inheriting from `LogicAdapter`[<sup id="1GFrC0">↓</sup>](#f-1GFrC0).

<br/>

## TL;DR - How to Add a `LogicAdapter`[<sup id="1GFrC0">↓</sup>](#f-1GFrC0)

1. Create a new class inheriting from `LogicAdapter`[<sup id="1GFrC0">↓</sup>](#f-1GFrC0)&nbsp;
   - Place the file under [[sym:./chatterbot/logic({"type":"path","text":"chatterbot/logic","path":"chatterbot/logic"})]],
     e.g. `MathematicalEvaluation`[<sup id="Z1DntY4">↓</sup>](#f-Z1DntY4) is defined in [[sym:./chatterbot/logic/mathematical_evaluation.py({"type":"path","text":"chatterbot/logic/mathematical_evaluation.py","path":"chatterbot/logic/mathematical_evaluation.py"})]].
2. Implement `__init__`[<sup id="IHnxD">↓</sup>](#f-IHnxD), `process`[<sup id="Z10GhmT">↓</sup>](#f-Z10GhmT), and `can_process`[<sup id="Z1rwi7X">↓</sup>](#f-Z1rwi7X).
3. Update [[sym:./chatterbot/logic/__init__.py({"type":"path","text":"chatterbot/logic/__init__.py","path":"chatterbot/logic/__init__.py"})]].
3. Update [[sym:./examples/memory_sql_example.py({"type":"path","text":"examples/memory_sql_example.py","path":"examples/memory_sql_example.py"})]].
3. Update [[sym:./examples/terminal_example.py({"type":"path","text":"examples/terminal_example.py","path":"examples/terminal_example.py"})]].
4. **Profit** 💰

<br/>

## Example Walkthrough - `MathematicalEvaluation`[<sup id="Z1DntY4">↓</sup>](#f-Z1DntY4)
We'll follow the implementation of `MathematicalEvaluation`[<sup id="Z1DntY4">↓</sup>](#f-Z1DntY4) for this example.

A `MathematicalEvaluation`[<sup id="Z1DntY4">↓</sup>](#f-Z1DntY4) is {Explain what MathematicalEvaluation is and how it works with the Adapter interface}

<br/>

## Steps to Adding a new `LogicAdapter`[<sup id="1GFrC0">↓</sup>](#f-1GFrC0)

<br/>

### 1\. Inherit from `LogicAdapter`[<sup id="1GFrC0">↓</sup>](#f-1GFrC0).
All `LogicAdapter`[<sup id="1GFrC0">↓</sup>](#f-1GFrC0)s are defined in files under [[sym:./chatterbot/logic({"type":"path","text":"chatterbot/logic","path":"chatterbot/logic"})]].

<br/>

We first need to define our class in the relevant file, and inherit from `LogicAdapter`[<sup id="1GFrC0">↓</sup>](#f-1GFrC0):
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 chatterbot/logic/mathematical_evaluation.py
```python
⬜ 3      from chatterbot import languages
⬜ 4      
⬜ 5      
🟩 6      class MathematicalEvaluation(LogicAdapter):
⬜ 7          """
⬜ 8          The MathematicalEvaluation logic adapter parses input to determine
⬜ 9          whether the user is asking a question that requires math to be done.
```

<br/>

### 2\. Implement `__init__`[<sup id="IHnxD">↓</sup>](#f-IHnxD), `process`[<sup id="Z10GhmT">↓</sup>](#f-Z10GhmT), and `can_process`[<sup id="Z1rwi7X">↓</sup>](#f-Z1rwi7X)

<br/>

Implement `__init__`[<sup id="IHnxD">↓</sup>](#f-IHnxD).

<br/>

This is how we implemented it for `MathematicalEvaluation`[<sup id="Z1DntY4">↓</sup>](#f-Z1DntY4) {Explain what's happening in this implementation}
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 chatterbot/logic/mathematical_evaluation.py
```python
⬜ 19               The language is set to ``chatterbot.languages.ENG`` for English by default.
⬜ 20         """
⬜ 21     
🟩 22         def __init__(self, chatbot, **kwargs):
🟩 23             super().__init__(chatbot, **kwargs)
🟩 24     
🟩 25             self.language = kwargs.get('language', languages.ENG)
🟩 26             self.cache = {}
⬜ 27     
⬜ 28         def can_process(self, statement):
⬜ 29             """
```

<br/>

The goal of `process`[<sup id="Z10GhmT">↓</sup>](#f-Z10GhmT) is to {Explain process's role}.

<br/>

This is how we implemented it for `MathematicalEvaluation`[<sup id="Z1DntY4">↓</sup>](#f-Z1DntY4) {Explain what's happening in this implementation}
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 chatterbot/logic/mathematical_evaluation.py
```python
⬜ 34             self.cache[statement.text] = response
⬜ 35             return response.confidence == 1
⬜ 36     
🟩 37         def process(self, statement, additional_response_selection_parameters=None):
🟩 38             """
🟩 39             Takes a statement string.
🟩 40             Returns the equation from the statement with the mathematical terms solved.
🟩 41             """
🟩 42             from mathparse import mathparse
🟩 43     
🟩 44             input_text = statement.text
🟩 45     
🟩 46             # Use the result cached by the process method if it exists
🟩 47             if input_text in self.cache:
🟩 48                 cached_result = self.cache[input_text]
🟩 49                 self.cache = {}
🟩 50                 return cached_result
🟩 51     
🟩 52             # Getting the mathematical terms within the input statement
🟩 53             expression = mathparse.extract_expression(input_text, language=self.language.ISO_639.upper())
🟩 54     
🟩 55             response = Statement(text=expression)
🟩 56     
🟩 57             try:
🟩 58                 response.text = '{} = {}'.format(
🟩 59                     response.text,
🟩 60                     mathparse.parse(expression, language=self.language.ISO_639.upper())
🟩 61                 )
🟩 62     
🟩 63                 # The confidence is 1 if the expression could be evaluated
🟩 64                 response.confidence = 1
🟩 65             except mathparse.PostfixTokenEvaluationException:
🟩 66                 response.confidence = 0
🟩 67     
🟩 68             return response
⬜ 69     
```

<br/>

The goal of `can_process`[<sup id="Z1rwi7X">↓</sup>](#f-Z1rwi7X) is to {Explain can_process's role}.

<br/>

This is how we implemented it for `MathematicalEvaluation`[<sup id="Z1DntY4">↓</sup>](#f-Z1DntY4) {Explain what's happening in this implementation}
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 chatterbot/logic/mathematical_evaluation.py
```python
⬜ 25             self.language = kwargs.get('language', languages.ENG)
⬜ 26             self.cache = {}
⬜ 27     
🟩 28         def can_process(self, statement):
🟩 29             """
🟩 30             Determines whether it is appropriate for this
🟩 31             adapter to respond to the user input.
🟩 32             """
🟩 33             response = self.process(statement)
🟩 34             self.cache[statement.text] = response
🟩 35             return response.confidence == 1
⬜ 36     
⬜ 37         def process(self, statement, additional_response_selection_parameters=None):
⬜ 38             """
```

<br/>

## Update additional files with the new class
Every time we add a new `LogicAdapter`[<sup id="1GFrC0">↓</sup>](#f-1GFrC0), we reference it in a few locations.
We will still look at `MathematicalEvaluation`[<sup id="Z1DntY4">↓</sup>](#f-Z1DntY4) as our example.

<br/>

3\. Don't forget to add the new class to [[sym:./chatterbot/logic/__init__.py({"type":"path","text":"chatterbot/logic/__init__.py","path":"chatterbot/logic/__init__.py"})]], for instance:
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 chatterbot/logic/__init__.py
```python
⬜ 8      __all__ = (
⬜ 9          'LogicAdapter',
⬜ 10         'BestMatch',
🟩 11         'MathematicalEvaluation',
⬜ 12         'SpecificResponseAdapter',
⬜ 13         'TimeLogicAdapter',
⬜ 14         'UnitConversion',
```

<br/>

4\. Add the new class to [[sym:./examples/memory_sql_example.py({"type":"path","text":"examples/memory_sql_example.py","path":"examples/memory_sql_example.py"})]], like so:
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 examples/memory_sql_example.py
```python
⬜ 10         storage_adapter='chatterbot.storage.SQLStorageAdapter',
⬜ 11         database_uri=None,
⬜ 12         logic_adapters=[
🟩 13             'chatterbot.logic.MathematicalEvaluation',
⬜ 14             'chatterbot.logic.TimeLogicAdapter',
⬜ 15             'chatterbot.logic.BestMatch'
⬜ 16         ]
```

<br/>

5\. Update [[sym:./examples/terminal_example.py({"type":"path","text":"examples/terminal_example.py","path":"examples/terminal_example.py"})]], for example:
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 examples/terminal_example.py
```python
⬜ 10         'Terminal',
⬜ 11         storage_adapter='chatterbot.storage.SQLStorageAdapter',
⬜ 12         logic_adapters=[
🟩 13             'chatterbot.logic.MathematicalEvaluation',
⬜ 14             'chatterbot.logic.TimeLogicAdapter',
⬜ 15             'chatterbot.logic.BestMatch'
⬜ 16         ],
```

<br/>

<!-- THIS IS AN AUTOGENERATED SECTION. DO NOT EDIT THIS SECTION DIRECTLY -->
### Swimm Note

<span id="f-IHnxD">__init__</span>[^](#IHnxD) - "chatterbot/logic/mathematical_evaluation.py" L22
```python
    def __init__(self, chatbot, **kwargs):
```

<span id="f-2g77vl">Adapter</span>[^](#2g77vl) - "chatterbot/adapters.py" L1
```python
class Adapter(object):
```

<span id="f-Z7HW4R">BestMatch</span>[^](#Z7HW4R) - "chatterbot/logic/best_match.py" L5
```python
class BestMatch(LogicAdapter):
```

<span id="f-Z1rwi7X">can_process</span>[^](#Z1rwi7X) - "chatterbot/logic/mathematical_evaluation.py" L28
```python
    def can_process(self, statement):
```

<span id="f-1GFrC0">LogicAdapter</span>[^](#1GFrC0) - "chatterbot/logic/logic_adapter.py" L7
```python
class LogicAdapter(Adapter):
```

<span id="f-Z1DntY4">MathematicalEvaluation</span>[^](#Z1DntY4) - "chatterbot/logic/mathematical_evaluation.py" L6
```python
class MathematicalEvaluation(LogicAdapter):
```

<span id="f-Z10GhmT">process</span>[^](#Z10GhmT) - "chatterbot/logic/mathematical_evaluation.py" L37
```python
    def process(self, statement, additional_response_selection_parameters=None):
```

<span id="f-8SAsH">TimeLogicAdapter</span>[^](#8SAsH) - "chatterbot/logic/time_adapter.py" L7
```python
class TimeLogicAdapter(LogicAdapter):
```

<span id="f-1av4A5">UnitConversion</span>[^](#1av4A5) - "chatterbot/logic/unit_conversion.py" L10
```python
class UnitConversion(LogicAdapter):
```

<br/>

This file was generated by Swimm. [Click here to view it in the app](https://swimm-web-app.web.app/repos/Z2l0aHViJTNBJTNBQ2hhdHRlckJvdCUzQSUzQWdpbGFkbmF2b3Q=/docs/x1fqx).