# Overview

| Developed by | Guardrails AI |
| --- | --- |
| Date of development | Feb 15, 2024 |
| Validator type | Format |
| Blog |  |
| License | Apache 2 |
| Input/Output | Output |

# Description

This validator checks to see if a given numerical output is within an expected range.

# Installation

```bash
$ guardrails hub install hub://guardrails/valid-range
```

# Usage Examples

## Validating string output via Python

In this example, we’ll use this validator to check for the age of the pet lying within some expected ranges.

```python
# Import Guard and Validator
from guardrails.hub import ValidRange
from guardrails import Guard

# Initialize Validator
val = ValidRange(
		min=0,
		max=10,
		on_fail="fix"
)

# Setup Guard
guard = Guard.from_string(
    validators=[val, ...],
)

guard.parse("5")  # Validator passes
guard.parse("10.5")  # Validator fails
```

## Validating JSON output via Python

In this example, we’ll use the validator to check that a field of a JSON output is within an expected range.

```python
# Import Guard and Validator
from pydantic import BaseModel
from guardrails.hub import ValidRange
from guardrails import Guard

# Initialize Validator
val = ValidRange(
		min=0,
		max=10,
		on_fail="fix"
)

# Create Pydantic BaseModel
class PetInfo(BaseModel):
		pet_name: str
		pet_age: str = Field(validators=[val])

# Create a Guard to check for valid Pydantic output
guard = Guard.from_pydantic(output_class=PetInfo)

# Run LLM output generating JSON through guard
guard.parse("""
{
		"pet_name": "Caesar",
		"pet_age": "5"
}
""")
```

## Validating string output via RAIL

tbd

## Validating JSON output via RAIL

tbd

# API Reference

`__init__`

- `min`: The inclusive minimum value of the range.
- `max`: The inclusive maximum value of the range.
- `on_fail`: The policy to enact when a validator fails.
