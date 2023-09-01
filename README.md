## JSON schemas for validating CACAO Security Playbooks

This repository contains non-normative JSON schemas for validating CACAO Security Playbooks. The JSON schemas provided are intended to follow the CACAO specification and its versions as developed and specified by the [OASIS CACAO Technical Committee](https://www.oasis-open.org/committees/cacao).

The working version of the CACAO Specification is available at: [CACAO Specification](https://docs.google.com/document/d/144kgoCnZbxc0CXms3EeACf4Sz84lmEt88JoVr4FnmSc/)

In particular, JSON validation schemas for a specific version of CACAO  are provided in different branches of this repository or can be accessed by pivoting from the table below.


| CACAO Specification Version | URL for JSON schemas |Reference|
| :--- | :--- |:--- |
| **Version 2.0 Committee Specification Draft 03**| [https://github.com/cyentific-rni/cacao-json-schemas/tree/cacao-v2.0-csd03](https://github.com/cyentific-rni/cacao-json-schemas/tree/cacao-v2.0-csd03) |CACAO Security Playbooks Version 2.0. Edited by Bret Jordan and Allan Thomson. 15 August 2023. OASIS Committee Specification Draft 03. https://docs.oasis-open.org/cacao/security-playbooks/v2.0/csd03/security-playbooks-v2.0-csd03.html. Latest version: https://docs.oasis-open.org/cacao/security-playbooks/v2.0/security-playbooks-v2.0.html. |
| **Version 2.0 Committee Specification Draft 01**| [https://github.com/cyentific-rni/cacao-json-schemas/tree/cacao-v2.0-csd01](https://github.com/cyentific-rni/cacao-json-schemas/tree/cacao-v2.0-csd01) |CACAO Security Playbooks Version 2.0. Edited by Bret Jordan and Allan Thomson. 21 February 2023. OASIS Committee Specification Draft 01. https://docs.oasis-open.org/cacao/security-playbooks/v2.0/csd01/security-playbooks-v2.0-csd01.html. Latest version: https://docs.oasis-open.org/cacao/security-playbooks/v2.0/security-playbooks-v2.0.html. |
| **Version 1.0 Committee Specification 02**| [https://github.com/cyentific-rni/cacao-json-schemas/tree/cacao-v1.0-cs02](https://github.com/cyentific-rni/cacao-json-schemas/tree/cacao-v1.0-cs02) |CACAO Security Playbooks Version 1.0. Edited by Bret Jordan and Allan Thomson. 23 June 2021. OASIS Committee Specification 02. https://docs.oasis-open.org/cacao/security-playbooks/v1.0/cs02/security-playbooks-v1.0-cs02.html. Latest stage: https://docs.oasis-open.org/cacao/security-playbooks/v1.0/security-playbooks-v1.0.html. |

We are also maintaining a working version in `working` branch.

## Validation Example with Python

The code below validates a CACAO playbook with CACAO JSON schemas from this repo utilizing a python package called "jsonschema". For further details please head to the [official documentation](https://python-jsonschema.readthedocs.io/en/stable/). (The example run on python version 3.11.)

```python
from jsonschema import validate, ValidationError, SchemaError
import requests
import json

# Reads CACAO JSON schemas from this repo (branch: cacao-v2.0-csd03).
url = "https://raw.githubusercontent.com/cyentific-rni/cacao-json-schemas/cacao-v2.0-csd03/schemas/playbook.json"
cacao_schema = requests.get(url).json()


# Read CACAO JSON from a local file
with open('./cacao_playbook.json') as file:
      cacao_json = json.load(file)

# Validate CACAO JSON with JSON schemas and look for errors.
try:
    validate(instance=cacao_json, schema=cacao_schema)
 
# Hits when the JSON schema itself contains error.
except SchemaError as schemaError:
    print("There is an error with the schema")
    print(schemaError)

# Hits when the CACAO JSON is not compliant with JSON schemas. 
# The error are appearing in chronological order one by one. 
except ValidationError as validationError:
    print(validationError)
```

For other packages and languages for validating JSON schemas, please head to the official documentation of [json-schema.org -> implementations -> validators](https://json-schema.org/implementations.html#validators).
