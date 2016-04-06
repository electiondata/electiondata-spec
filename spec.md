### Open Election Data Spec [DRAFT]

#### Data Structure

```
Repo Name: UGA

.
+-- 2016
+-- 2015
|   +-- presidential
|   +-- legislative
|   +-- referendum
+-- 2014
|   +-- presidential
| |   +-- 2016-election-round1
| |   +-- 2016-election-round2
|   | | +-- raw
|   | | +-- parsed
|   | | +-- scripts
|   | | +-- README.md
|   | | +-- results_metadata.yml
|   | | +-- results.csv
|   | | +-- voter_registration_metadata.yml
|   | | +-- voter_registration.csv
|   +-- legislative
|   +-- referendum
|   +-- subnational_legislative
|   +-- subnational_executive
+-- scripts
+-- README.md
+-- .travis.yml


```

- Data for each country is stored in a Github repository
- Country repos are named using [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) This example uses UGA (Uganda)
- In each repository, election data are stored in folders representing the year the data is from
- Each year includes folders for specific category of elections. The categories are
  - presidential
  - legislative
  - referendum
- We only cover national elections. Subnational elections are not covered at this point.
- Any election that doesn't fall under the mentioned three categories are not covered.
- Election data for each category are stored in folders named after the particular election. For example a first round of a presidential election in 2016 is stored in a folder called `2016-election-round1`. There is no specific rule on how to name the folder. The ONLY rule is to use `-` instead of space.
- Each named folder has three folders and several files. The folders are:
  - raw: includes all relevant files in the raw (original) format (e.g. pdf, Excel, html files)
  - parsed: includes the raw data parsed to csv format
  - scripts: includes the scripts used for parsing the raw data. The data in the parsed folder can be regenerated using the scripts in the script folder. The must be at least two script files:
    - parsed.sh | `generates the parsed data from the raw folder`
    - processed.sh | `generates the processed data from the parsed folder`
- The folder also includes csv files that have processed data. Here are the examples:
  - results_metadata.yml
  - results.csv
  - voter_registration_metadata.yml
  - voter_registration.csv
- The repository root includes a script folder that has static-api generator scripts and linters for verifying the validity of processed csv files

-**Note:** We will not cover US Elections

#### Process

For any new country, a contributor makes a copy of the election-seed repo that has the skeleton for the data structure and save it as a new repository using the country's alpha-3 code.

New data are then added as pull requests. An admin/contributor ensures that the pull request is correct and follows the requirements before merging it to the main branch.

Each repo includes tests that has to be passed on Travis before the PR can be merged.

The tests ensure that all parsed data follows the data spec set in this document.

## Data Spec for the processed Data

### Required files:

- results_metadata.yml
- results.csv
- ....

### results_metadata.yml

**Fields:**

- id: a unique identified
- fieldname
- description

**Example:**

```yml
- id: a unique identified
- admin1: State
- admin2: Country
- description: Name of the candidate on the ballot
- count: Number of votes
```

### data.csv

**Fields:**

- id
- admin1
- admin2
- admin3
- admin4
- admin5
- ....
- ....
- description
- count

The admin fields can increment to as many as needed.

Each field must have a corresponding row in metadata.yml

**Example:**

```
id, admin1, admin2, admin3, description, count
1, Virginia, Fairfax, Arlington, John Doe, 1234566
2, Maryland, Montogmery Country, Silver Spring, John Adams, 55432
```
