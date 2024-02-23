# PID Credential (Germany)

The German PID credential types inherit data fields from the [base
type](../PID-base/). Three credential types are defined depending on the source
of the PID information, resulting in the following hierarchy:

 - Base Type: `https://example.eudi.eu/credential/pid/1.0`
   - German Base Type: `https://example.bmi.bund.de/credential/pid/base/1.0`
     - PID based on ID Card: `https://example.bmi.bund.de/credential/pid/id-card/1.0`
     - PID based on Residence Permit: `https://example.bmi.bund.de/credential/pid/residence-permit/1.0`
     - PID based on EU Citizen eID card: `https://example.bmi.bund.de/credential/pid/eu-citizen-eid-card/1.0`
   - (... other national PID types)

Note: While this design option provides more granular credential types, it has a
privacy drawback: The source of the PID information is always revealed in the
credential type URI and would not be selectively disclosable. If the credential
is used, for example, for age verification, the Verifier learns not only the
age, but also that the person presenting the credential is not a German citizen.

This could be mitigated by using a single German PID credential type and
including the source of the PID information as a selectively disclosable data
field, as shown in [PID-de-option1](../PID-de-option1/).

## Example: PID based on ID Card

```yaml
{
    ## Base data (SD-JWT VC DM)
    "vct": "https://example.bmi.bund.de/credential/pid/id-card/1.0",
    "vct#integrity": "sha256-jo8433ot48utul8ura33",

    ## Base dataset

    "given_name": "Erika",
    "family_name": "Mustermann",
    "birthdate": "1963-08-12",

    ## Additional data

    "address": {
        "street_address": "Heidestraße 17",
        "locality": "Köln",
        "postal_code": "51147",
        "country": "DE"
    },

    "nationalities": [
        "DE"
    ],

    "birth_family_name": "Gabler",

    "place_of_birth": {
        "locality": "Berlin",
        "country": "DE"
    },

    "also_known_as": "Schwester Agnes"

    ## Derived claims
    "age_equal_or_over": {
        "12": true,
        "14": true,
        "16": true,
        "18": true,
        "21": true,
        "65": false
    },

    # key binding (SD-JWT VC DM)
    "cnf": {
        "jwk": {
            "kty": "EC",
            "crv": "P-256",
            "x": "52aDI_ur05n1f_p3jiYGUU82oKZr3m4LsAErM536crQ",
            "y": "ckhZ-KQ5aXNL91R8Eufg1aOf8Z5pZJnIvuCzNGfdnzo"
        }
    }
}
```

## Example: PID based on Residence Permit

```yaml
{
    ## Base data (SD-JWT VC DM)
    "vct": "https://example.bmi.bund.de/credential/pid/residence-permit/1.0",
    "vct#integrity": "sha256-jo8433ot48utul8ura33",

    ## Base dataset

    "given_name": "Erika",
    "family_name": "Mustermann",
    "birthdate": "1963-08-12",

    ## Additional data

    "nationalities": [
        "DE"
    ],

    "gender": "female",
    "birth_family_name": "Gabler",

    "place_of_birth": {
        "locality": "Berlin",
        "country": "DE"
    },

    "also_known_as": "Schwester Agnes"

    ## Derived claims
    "age_equal_or_over": {
        "12": true,
        "14": true,
        "16": true,
        "18": true,
        "21": true,
        "65": false
    },

    # key binding (SD-JWT VC DM)
    "cnf": {
        "jwk": {
            "kty": "EC",
            "crv": "P-256",
            "x": "52aDI_ur05n1f_p3jiYGUU82oKZr3m4LsAErM536crQ",
            "y": "ckhZ-KQ5aXNL91R8Eufg1aOf8Z5pZJnIvuCzNGfdnzo"
        }
    }
}
```

## Example: PID based on EU Citizen eID Card

```yaml
{
    ## Base data (SD-JWT VC DM)
    "vct": "https://example.bmi.bund.de/credential/pid/eu-citizen-eid-card/1.0",
    "vct#integrity": "sha256-jo8433ot48utul8ura33",

    ## Base dataset

    "given_name": "Erika",
    "family_name": "Mustermann",
    "birthdate": "1963-08-12",

    ## Additional data

    "address": {
        "street_address": "Heidestraße 17",
        "locality": "Köln",
        "postal_code": "51147",
        "country": "DE"
    },

    "nationalities": [
        "DE"
    ],

    "birth_family_name": "Gabler",

    "place_of_birth": {
        "locality": "Berlin",
        "country": "DE"
    },

    "also_known_as": "Schwester Agnes"

    ## Derived claims
    "age_equal_or_over": {
        "12": true,
        "14": true,
        "16": true,
        "18": true,
        "21": true,
        "65": false
    },

    # key binding (SD-JWT VC DM)
    "cnf": {
        "jwk": {
            "kty": "EC",
            "crv": "P-256",
            "x": "52aDI_ur05n1f_p3jiYGUU82oKZr3m4LsAErM536crQ",
            "y": "ckhZ-KQ5aXNL91R8Eufg1aOf8Z5pZJnIvuCzNGfdnzo"
        }
    }
}
```

