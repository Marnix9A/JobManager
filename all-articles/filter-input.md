# Filter input

This section provides a quick overview of how filters can be specified in NAV/BC.

Please read [here](https://docs.microsoft.com/en-us/dynamics365/business-central/ui-enter-criteria-filters) for detailed information.

| Sample | Description |  |
| :-- | :-- | :-- |
| K1 | Filter _exactly_ **K1** | K1 |
| K\* | Filter all _starting with_ **K** | K1, K2, K18, KA2, KB6 _etc._ |
| \*2 | Filter all where _last part_ is _exactly_ **2** | J2, K2, KA2 _etc._ |
| K? | Filter all _starting with_ **K** _and_ next 1 character is _random_ | K1, K2 _etc._ |
| K?? | Filter all _starting with_ **K** _and_ next 2 characters is _random_ | K18, KA2, KB6 _etc._ |
| K1|K2 | Filter **K1** _or_ **K2** | K1, K2 |
| J\*|KA\* | Filter all _starting with_ **J** _or_ all _starting with_ **KA** | J1, J2, KA2 _etc._ |
| <>K1 | EXCLUDE _exactly_ **K1** | J1, J2, K2, K18, KA2, KB6 _etc._ |
| <>\*2 | EXCLUDE all where the last part is _exactly_ **2** | J1, K1, K18, KB6 _etc._ |
| <>K1&<>K18 | EXCLUDE **K1** _and_ also EXCLUDE **K18** | J1, J2, K2, KA2, KB6 _etc._ |
| <>J\*&<>KA\* | EXCLUDE all _starting with_ **J** _and_ EXCLUDE all _starting with_ **KA** | K1, K2, K18, KB6 _etc._ |
| KA2..KB6 | Filter all _from and including_ **KA2** _to and including_ **KB6** | J1, J2, K1, K18, KA2 _etc._ |

When using advanced filters using _\* | &_ the dropdown **CAN'T** be used for selecting values.
