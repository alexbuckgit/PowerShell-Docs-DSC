---
description: Reference for the 'base64' DSC configuration document function
ms.date:     05/09/2024
ms.topic:    reference
title:       base64
---

# base64

## Synopsis

Returns the base64 representation of an input string.

## Syntax

```Syntax
base64(<inputString>)
```

## Description

The `base64()` function returns the [base64][01] representation of an input string. Passing data
encoded as base64 can reduce errors in passing data, especially when different tools require
different escape characters.

## Examples

### Example 1 - Convert a string to base64

The configuration converts a basic string value with the `base64()` function.

```yaml
# base64.example.1.dsc.config.yaml
$schema: https://raw.githubusercontent.com/PowerShell/DSC/main/schemas/2024/04/config/document.json
resources:
  - name: Echo 'abc' in base64
    type: Test/Echo
    properties:
      output: "[base64('abc')]"
```

```bash
dsc --input-file base64.example.1.dsc.config.yaml config get
```

```yaml
results:
- name: Echo 'abc' in base64
  type: Test/Echo
  result:
    actualState:
      output: YWJj
messages: []
hadErrors: false
```

### Example 2 - Convert a concatenated string to base64

The configuration uses the [concat()][02] function inside the `base64()` function to combine the
strings `a`, `b`, and `c` into `abc` before returning the base64 representation.

```yaml
# base64.example.2.dsc.config.yaml
$schema: https://raw.githubusercontent.com/PowerShell/DSC/main/schemas/2024/04/config/document.json
resources:
  - name: Echo concatenated 'a', 'b', 'c' in base64
    type: Test/Echo
    properties:
      output: "[base64(concat('a', 'b', 'c'))]"
```

```bash
dsc --input-file base64.example.2.dsc.config.yaml config get
```

```yaml
results:
- name: Echo concatenated 'a', 'b', 'c' in base64
  type: Test/Echo
  result:
    actualState:
      output: YWJj
messages: []
hadErrors: false
```

## Parameters

### inputString

The `base64()` function expects a single string as input. The function converts the value into a
base64 representation. If the value isn't a string, DSC raises an error when validating the
configuration document.

```yaml
Type:         string
Required:     true
MinimumCount: 1
MaximumCount: 1
```

## Output

The `base64()` function returns the base64 representation of the **inputString** value.

```yaml
Type: string
```

<!-- Link reference definitions -->
[01]: https://en.wikipedia.org/wiki/Base64
[02]: concat.md
