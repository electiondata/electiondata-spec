### Open Election Data Spec [DRAFT OF DRAFT]

#### Data Structure

```
Repo Name: UGA

.
+-- 2016
+-- 2015
|   +-- presidential
|   +-- legislative
|   +-- referendum
|   +-- subnational_legislative
|   +-- subnational_executive
+-- 2014
|   +-- presidential
| |   +-- 0
| |   +-- 1
|   | | +-- raw
|   | | +-- parsed
|   | | +-- processed
|   | | +-- context
|   | | +-- scripts
|   | | +-- README.md
|   +-- legislative
|   +-- referendum
|   +-- subnational_legislative
|   +-- subnational_executive
| +-- scripts
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
  - subnational_legislative
  - subnational_executive
- Election data for each category are indexed from 0 for each election chronically. For example, if Egypt's presidential election in 2013 was hold in three separate weeks, data for the first week will go under folder 0, data for second week goes to folder 1 and so on....
- Each indexed folder has four folders
  - raw: includes all data files in raw (original) format (e.g. pdf, Excel, html files)
  - parsed: includes raw data parsed to csv format
  - processed: includes normalized data in csv format using the election-data spec
  - context: includes any additional information/data/files about the election
  - scripts: includes the scripts used for parsing the raw data. The data in the parsed folder can be regenerated using the scripts in the script folder
  - README.md
- The repository root includes a script folder that has static-api generator scripts and linters for verifying the validity of processed csv files

**Note:** We will not cover US Elections

#### Process

For any new country, a contributor makes a copy of the election-seed repo that has the skeleton for the data structure and save it as a new repository using the country's alpha-3 code.

New data are then added as pull requests. An admin/contributor ensures that the pull request is correct and follows the requirements before merging it to the main branch.

Each repo includes tests that has to be passed on Travis before the PR can be merged.

The tests ensure that all parsed data follows the data spec set in this document

## Data Spec for the processed Data

### Required files:

- metadata.csv
- data.csv
- admin1.csv
- admin2.csv
- admin3.csv
- ....

The admin level csv files will match the total number of admin levels available in a particular election

### metadata.csv

**Fields:**

- id: a unique identified
- fieldname
- description

**Example:**

```
id, fieldname, description
1, id, The unique identifier
2, admin1, State
3, admin2, County
4, admin2, City
5, description, Candidates fullname (Lastname, Firstname)
6, votes, Number of the votes for the candidate
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
- votes

The admin fields can increment to as many as needed.

Each field must have a corresponding row in metadata.csv

Admin fields will reference ID numbers from the corresponding csv files. *[Note: while this approach saves space, I'm not entirely convinced that this has advantage over spelling out the name of the admin level in each row.]*

**Example:**

```
id, admin1, admin2, admin3, description, votes
1, 1, 3, 4, John Doe, 1234566
2, 1, 3, 4, John Adams, 55432
```

### admin1.csv

fields:

- id
- description

**Example:**

```
id, name
1, Virginia
2, North Carolina
```
