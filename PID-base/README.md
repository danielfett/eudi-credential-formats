# PID (Person Identification Data) Base Credential Example

The following notations are used to denote the original definitions of the data elements:

 - `(SD-JWT VC DM)` [SD-JWT VC DM](https://github.com/danielfett/sd-jwt-vc-dm)
 - `(OIDC)` [OpenID Connect Core 1.0](https://openid.net/specs/openid-connect-core-1_0.html)
 - `(eKYC)` [OpenID eKYC Identity Assurance](https://openid.net/specs/openid-connect-4-identity-assurance-1_0.html)

Not shown here: Claims regarding validity, issuer, status/revocation.

```yaml
{
    ## Base data (SD-JWT VC DM)
    "vct": "https://example.eudi.eu/credential/pid/1.0",      # mandatory, details to be defined
    "vct#integrity": "sha256-jo8433ot48utul8ura33",   # mandatory

    ## Base dataset that always needs to be present (OIDC)

    "given_name": "Jack",       # mandatory, may be an empty string
    "family_name": "Dougherty", # mandatory, may be an empty string

    # Note: Empty given_name or family_name is allowed if user has no such name.
    # Note: Either given_name or family_name must be non-empty.

    "birthdate": "1980-05-23",  # mandatory, may be partial date (e.g. "1980-05" or "1980")

    # to be discussed: cross-border identifier including its privacy implications

    ## Additional data

    "address": {                # optional (OIDC)
        "street_address": "123 Via Appia",
        "locality": "Rome",
        "region": "Lazio",
        "postal_code": "00100",
        "country": "IT"
    },

    "nationalities": [          # optional (eKYC)
        "DE",
        "IT"
    ],
    # Note: Semantics here is "nationalities known to the issuer",
    # which may be (1) incomplete or (2) not the view of the
    # country listed here.
    #
    # Note: If nationalities does not include the country of
    # residence, this implies that the person is a foreigner in the
    # country of residence.
    #
    # Note: The selective disclosure granularity for
    # nationalities needs to be defined.

    "gender": "male",           # optional (OIDC), todo: what are allowed values? → re-use existing definition

    "middle_name": "",          # optional (OIDC)

    "birth_given_name": "",     # optional (eKYC)
    "birth_family_name": "",    # optional (eKYC)
    "place_of_birth": {         # optional (eKYC)
        "locality": "Leipzig",
        "region": "Saxony",
        "country": "DD"
    },

    "title": "Dr.",             # optional (eKYC)
    "salutation": "Mr.",        # optional (eKYC)
    "also_known_as": "Jeff"     # optional (eKYC)

    ## Derived claims
    "age_equal_or_over": {      # can be expanded by member states, precise set to be defined
        "12": true,             # mandatory
        "14": true,             # mandatory
        "16": true,             # mandatory
        "18": true,             # mandatory
        "21": true,             # mandatory
        "65": false             # mandatory
    },
    # Note: Requests for the above must address individual elements
    # and release must be based on selective disclosure.

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