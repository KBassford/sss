# Shamir's Secret Sharing
Ali Mousa's sss library adapted for use in the generation of Split Keys compliant with Key Management Interoperability Protocol (KMIP).

The SplitKey structure is defined here: https://docs.oasis-open.org/kmip/kmip-spec/v2.0/csprd01/kmip-spec-v2.0-csprd01.html#_Toc6497445.

The X-intercept has now been changed to be sequential whole numbers, starting with 1, suitable for use with any application using standard split keys.

To fill in this structure, follow this procedure for each Split Key generated.
* Split Key Parts = Total number of shares generated (number used for "share" in GenerateShares).
* Key Part Identifier = X-intercept of key (X in the utils.Point structure).
* Split Key Threshold = Number of shares require to reconstitute the secret (number used for "threshold" in GenerateShares).
* Split Key Method = Enumerator, set to method 3, PSPF (XOR, GF16, PSPF, GF08).
* Prime Field Size = Prime used to generate shares (big.Int used for "prime" in GenerateShares).
* Key Block = Y-intercept of key (Y in the utils.Point structure).

## Documentation

### GenerateShares

`GenerateShares(threshold int, shares int, prime *big.Int) (*big.Int, []*utils.Point, error)`

This function creates a secret returned in the form of a big.Int, and a set of shares returned as an array of point structures.  In the event of an error, it is passed on, otherwise nil.

### RecoverSecret

`RecoverSecret(points []*utils.Point, modulus *big.Int) (*big.Int, error)`

This function recovers a secret from a set of points under `prime` modulus. The secret is returned as a big.Int and the error will be nil, otherwise the error will be filled in.

## To Do
* Tweak input/output, maybe even enter/return entire Split Key structures.
* May adapt this library to generate GF08 and GF16 as well.