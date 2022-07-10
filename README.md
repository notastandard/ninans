# NINANS - Ninans Is Not A Naming Standard

- [source code on GitHub](https://github.com/notastandard/ninans)

## Introduction
There are a number of public cloud providers who offer services in different geographic regions. Regions are always named differently across providers. Some people like to deploy things in multiple clouds. Some people like to encode information in the names of the resources they deploy in clouds. This may or may not be a good idea.

It may be useful to name stuff consistently, regardless of which cloud provider or region you use. That's NINANS.

## Principles
- Concise. Some systems require short hostnames (e.g. NetBIOS = 15 characters). Leave spare characters for local naming components.
- Compatible. Lower case letters and numbers only and start with a letter.
- Machine readable. Fixed length overall. Each name component is also fixed length.
- Predictable. Use existing standards (locations based on ISO standards).

## The not a standard

`${provider[2]}${service_qualifier[1]}${country[2]}${subdivision_or_compass_direction[3]}${numerical_qualifier[2]}`

(total 10 characters)

## Name components

### 1. Provider

| Code   | Provider              |
|--------|-----------------------|
| `aw`   | Amazon Web Services   |
| `az`   | Microsoft Azure       |
| `do`   | DigitalOcean          |
| `gc`   | Google Cloud Platform |

### 2. Service qualifier

| Code | Service qualifier                      |
|------|----------------------------------------|
| `b`  | AWS iso-b secret partition             |
| `e`  | Azure Early Updates Access Program     |
| `g`  | AWS GovCloud                           |
| `i`  | AWS iso secret partition               |
| `j`  | Azure Jio partner region               |
| `s`  | Standard region (no special qualifier) |

### 3. Country

Use the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) lowercased two character country code for the region.

### 4. Subdivision or compass direction

#### Subdivision (first preference)

- When the subdivision within a country of the provider region is known and documented, use the most specific but accurate available [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2) lowercased three character subdivision code for the location.
- Where multiple official codes for a single subdivision exist in different administrative languages, use the English code (e.g. Cardiff = `CRF`).
- Where subdivision codes are less than three characters in length, pad with `x` characters as a **suffix** to make three characters (e.g. California = `cax`, Seoul = `11x`).

#### Compass direction (second preference)

- A compass direction may be used instead of a country subdivison only when the country subdivision is unknown, but the compass direction is known. Use the accepted abbrevations for the [cardinal and ordinal compass directions](https://en.wikipedia.org/wiki/Cardinal_direction).
- Pad compass direction with `x` characters as a **prefix** to make three characters (e.g. north = `xxn`, southwest = `xsw`).

#### No subdivision or compass direction (third preference)

If no information about the subdivision or campass direction of a region is available, use three `x` characters.

### 5. Numerical qualifier

- The provider's own numerical qualifier for a region padded with a leading `0` if required (e.g. AWS us-east-1 = `01`).
- Where no numerical qualifier exists, use `00` (e.g. Azure westeurope = `00`).

## Special notes

1. **London**: The [ISO 3166-2:GB](https://en.wikipedia.org/wiki/ISO_3166-2:GB) standard, listing codes for subdivisions of the United Kingdom, has codes for the individual London boroughs and for the [City of London](https://en.wikipedia.org/wiki/City_of_London). It does not have a code for the [Greater London](https://en.wikipedia.org/wiki/Greater_London) area. Where a provider's region is listed simply as "London", use the code for the City of London (`LND`) for the NINANS subdivision component.

## Examples

| Provider              | Provider region name | Provider service qualifier   | Country           | Subdivision or compass direction | NINANS       |
|-----------------------|----------------------|------------------------------|-------------------|----------------------------------|--------------|
| Microsoft Azure       | centralus            | None                         | United States     | Iowa                             | `azsusiax00` |
| Microsoft Azure       | jioindiawest         | Azure Jio partner region     | India             | Gujarāt                          | `azjingjx00` |
| Microsoft Azure       | eastus2euap          | Early Updates Access Program | United States     | Virginia                         | `azeusvax02` |
| Microsoft Azure       | koreacentral         | None                         | Republic of Korea | Seoul                            | `azskr11x00` |
| Amazon Web Services   | eu-west-2            | None                         | United Kingdom    | London                           | `awsgblnd02` |
| Amazon Web Services   | us-gov-west-1        | AWS GovCloud                 | United States     | West United States               | `awgusxxw01` |
| DigitalOcean          | fra1                 | None                         | Germany           | Hesse                            | `dosdehex01` |
| Google Cloud Platform | asia-northeast1      | None                         | Japan             | Tokyo                            | `gcsjp13x01` |