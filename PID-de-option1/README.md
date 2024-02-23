# PID Credential (Germany)

The German PID credential type inherits data fields from the [base
type](../PID-base/). A single German credential type is defined independent of
whether the data comes from an ID card, a residence permit, or an eID card for EU
citizens. A data field in the credential indicates the source of the PID.

Note: This is one of two design options, the other being
[PID-de-option2](../PID-de-option2/). See the notes there for a comparison of
the two options.

The data fields shown in the following example are available for the eID-based
German PIDs:

```yaml
{
    ## Base data (SD-JWT VC DM)
    "vct": "https://example.bmi.bund.de/credential/pid/1.0",  # metadata would define this as an extension of the base type https://example.eudi.eu/credential/pid/1.0
    "vct#integrity": "sha256-jo8433ot48utul8ura33",

    ## Base dataset that always needs to be present

    "given_name": "Erika",
    "family_name": "Mustermann",
    "birthdate": "1963-08-12",

    ## Additional data

    "source_document_type": "id_card",  # can also be "residence_permit" or "eu_citizen_eid_card"

    "address": {                        # available for ID card and eID card for EU citizens only
        "street_address": "Heidestraße 17",
        "locality": "Köln",
        "postal_code": "51147",
        "country": "DE"
    },

    "nationalities": [
        "DE"
    ],

    "gender": "female",                 # available for residence permit only
    "birth_family_name": "Gabler",

    "place_of_birth": {
        "locality": "Berlin",
        "country": "DE"
    },

    "also_known_as": " Schwester Agnes"

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
