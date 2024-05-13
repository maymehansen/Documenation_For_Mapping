# Documentation for IICS Training Question 2

## m_question_2_maymehan
- Pathway: (IICS -> Data Integration -> Explore / All Projects -> Training -> maymehan -> m_question_2_maymehan)

## Overview/Links
  - [Link to Informatica](http://go.byu.edu/infadev)

This mapping extracts data from the `person_training` table in the `training_postgres_public` source connection and transforms it according to client requirements. The transformed data is then loaded into a flat file target connection named "Flat File."

## Business Logic
Target Connection
- `Flat File`

Creating `Older_Than_2000s_Flag` Field
- A new field created to flag if individuals are born after January 1, 2000. 
- If an individual is born after January 1, 2000, the flag is set to 'Y'. Else, it is set to 'N'.

Filtering Records
- Records with `Older_Than_2000s_Flag` marked as 'Y' are filtered out.
  
## Permissions

Database Username
- training_postgres_public

## Mapping (Sources and Targets)

TRAINING_POSTGRES_PUBLIC.PERSON_TRAINING

     *This table gives us information about the person including the following attributes: Preferred_First_Name, Last_Name, Gender, Marital_Status and     Birth_Country.

TRAINING_POSTGRES_PUBLIC.ADDRESS_TRAINING
     *This table gives us information about the person including the following attributes: CITY and ADDRESS_TYPE.

## Design Decisions
- The source is not a custom SQL query as per client request.
## Past/Frequent Issues
- N/A
## Future Enhancements
- None at this time.
## Creators and Editors of the process
Mayme Hansen
