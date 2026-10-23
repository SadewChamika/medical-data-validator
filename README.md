# Medical Data Validator

A small Python script that validates a list of patient medical records. It checks the structure of the data and the format of every field, then reports exactly which records and fields are invalid.

## Features

- Confirms the input is a list or tuple of dictionaries
- Checks that each record has exactly the expected keys
- Validates every field against its own rule
- Prints a clear message for each problem, with the field, its value, and the record's position
- Returns `True` for valid data and `False` otherwise

## Record Format

Each record must be a dictionary with these keys:

| Key | Rule |
| --- | --- |
| `patient_id` | `p` followed by digits, case-insensitive (e.g. `P1001`) |
| `age` | Integer, 18 or older |
| `gender` | `male` or `female`, case-insensitive |
| `diagnosis` | String or `None` |
| `medications` | List of strings |
| `last_visit_id` | `v` followed by digits, case-insensitive (e.g. `V2301`) |

```python
{
    'patient_id': 'P1001',
    'age': 34,
    'gender': 'Female',
    'diagnosis': 'Hypertension',
    'medications': ['Lisinopril'],
    'last_visit_id': 'V2301',
}
```

## How It Works

- `find_invalid_records(...)` takes one record's fields as keyword arguments and returns a list of the keys that break the rules.
- `validate(data)` loops over the records, checks their structure, unpacks each one into `find_invalid_records` with `**`, and prints a message for every invalid field.

## Usage

Requires Python 3 and no external packages.

```bash
python medical-data-validator.py
```

The script validates the sample `medical_records` list at the bottom of the file. To check your own data, call `validate(your_data)`.

## Example Output

Valid data:

```
Valid format.
```

Invalid data:

```
Unexpected format 'patient_id: X1' at position 0.
Unexpected format 'age: 15' at position 0.
```

Structural problems:

```
Invalid format: expected a list or tuple.
Invalid format: expected a dictionary at position 2.
Invalid format: {...} at position 1 has missing and/or invalid keys.
```

