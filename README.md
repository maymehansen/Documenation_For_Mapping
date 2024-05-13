# Documentation for m_question_2_maymehan

## m_question_2_maymehan
- Pathway: (IICS -> Data Integration -> Explore / All Projects -> Training -> maymehan -> m_question_2_maymehan)

## Overview
This mapping extracts data from the `person_training` table in the `training_postgres_public` source connection and transforms it according to client requirements. The transformed data is then loaded into a flat file target connection named "Flat File."

## Source Connection
- Connection: `training_postgres_public`
- Table: `person_training`

## Target Connection
- Connection: `Flat File`

## Transformation Steps
### Attribute Selection and Renaming
- `Preferred_First_Name`
- `Last_Name`
- `Gender`
- `Marital_Status`
- `Birth_Country`

### Creating `Older_Than_2000s_Flag` Field
- A new field is created to flag if individuals are born after January 1, 2000. 
- If an individual is born after January 1, 2000, the flag is set to 'Y'. Else, it is set to 'N'.

### Filtering Records
- Records with `Older_Than_2000s_Flag` marked as 'Y' are filtered out.

### Joining with Address Table
- After filtering, the `address_training` table is joined with the remaining records from `person_training`.
- Additional fields from the `address_training` table are returned:
  - `CITY`
  - `ADDRESS_TYPE`

## Design Decisions
- The source for this mapping is not a custom SQL query.

## Future Enhancements
- None at this time.

## Creator
Mayme Hansen
