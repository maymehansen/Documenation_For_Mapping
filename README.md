# Documentation for Mapping_1

## Canvas IICS
Canvas/Canvas Integrations
  - Pathway: (IICS -> Data Integration -> Explore / All Projects -> Canvas -> Canvas Integrations)

## Overview/Links
  - [Link to Informatica](http://go.byu.edu/infadev)

- [Admin Log In to BETA Canvas](https://byu.beta.instructure.com/login/canvas)

Job Scheduler Job Set Name/Names
  - Canvas_Daily
  - Canvas_Hourly

Link to CI
  - (currently do not have one)

Link to Integration KB*
  - Currently KB0032308, we need to make a new one that is specifically for Canvas?

Contact Info of Service Manager/Customers of Integration
  - Bradley Ross / Teaching, Learning, Research Portfolio.

## Business Logic
Original Customer requirements
  - Used by ~10% of BYU students and professors, alongside Learning Suite, it's used to administer courses that are better fit for this platform over Learning Suite. Having each professor maintain Canvas manually is a nightmare, so this is the process we put into place.

Reason why the integration was created in the first place
  - Created while updating from legacy systems, but very important because it is actively used throughout the school year. These processes keep a lot of programs running, including important graduate classes that professors like to have more control over.

Business purpose for creating the integration
  - Canvas offers flexibility for teachers and is a very familiar place for students working on courses. More in our control than Learning Suite, and important to have in case Learning Suite ever failed or we decided to transition, we would already have this an option.

What data is it using and where is it going
  - Data comes from different oracle tables, Canvas itself, and Oracle Param Files and goes straight back to Canvas (Web Services API).


## Permissions
GRO groups you should be a part of to work on the integration
  - IICS_Academics_Dev gro group
  - Also, helpful to be added as an admin to the BYU Canvas Beta to see if processes are working (talk with Quin Swallow to get this permission)

Location and name of LastPass Share folder for passwords (store this in Lastpass, Database User password, API client credentials, and API client secret there) -Could move to AWS Parameter Store? *
  - Shared - Canvas Integrations (we do not a have a gro group tied to it yet)

Database Username
  - iics_canvas_integrations

Link to DSAs related to the integration
  - DSR-20221013
  - DSA-20221013

## Mapping (Sources and Targets)
Database.Schema.Table - Used in query

CESPRD.IICS_CANVAS_INTEGRATIONS.CURRENT_YEAR_TERM

     *This is used to give us the current year term.  It helps us push class enrollments up to Canvas for the current term.

CESPRD.IICS_CANVAS_INTEGRATIONS.NEXT_YEAR_TERM

     *This is used to give us the next year term.  It helps us push class enrollments up to Canvas for the next year term from the current one.

CESPRD.IICS_CANVAS_INTEGRATIONS.FUTURE_YEAR_TERM

     *This is used to give us the future year term.  It helps us push class enrollments up to Canvas for the third year term from the current one.

CESPRD.COMMON.CONTROL_DATES semester
      
      *This is used to give us the start and end dates of current and upcoming semesters

CESPRD.CANVAS_LMS.ENROLLMENT_DIM

      *This is used to... (see m_canvas_delete_athlete_observers)

CESPRD.CANVAS_LMS.PSEUDONYM_DIM

      *This is used to... (see m_canvas_delete_athlete_observers)

CESPRD.GRO.PERSON_GROUP

      *This is used to... (see m_canvas_delete_athlete_observers)

CESPRD.CANVAS_LMS.ENROLLMENT_TERM_DIM

    *This is used to find the dept. name and then assign into in Canvas.

CESPRD.ACADUNIT.SUBJECT_AREA

    *See mt_Canvas_Sub_Accounts_Sync. This is used to find the dept. name and then assign into in Canvas.

CESPRD.ACADUNIT.ACADEMIC_UNIT

    *See mt_Canvas_Sub_Accounts_Sync. This is being used to compare against a couple different tables and with canvas.

CESPRD.IICS_CANVAS_INTEGRATIONS.CLASS_SECTION

      *This is used to find the dept. name and then assign into in Canvas. It can also be used to compare with other ones.

CESPRD.IICS_CANVAS_INTEGRATIONS.CANVAS_SECTIONS

     *see mt_canvas_section_delete. Use to pull the canvas sections and to see when they have last been updated, cleaning up the data.

CESPRD.IICS_CANVAS_INTEGRATIONS.IDENTIFIER

      *This is used when the NET ID has been updated.

CESPRD.IICS_CANVAS_INTEGRATIONS.CLASS_ATTRIBUTE (very often shortened in queries to "ca")

      *This is the canvas table of information about the different classes.

CESPRD.STDREG.STD_CLASSES

    *This is used to check students classes that they have registered for.

CESPRD.PRO.PERSON

    *This is the table that contains all of the info for different BYU students.

CESPRD.CANVAS.SECTION_NUMBER

    *not entirely sure what this one is doing.

CESPRD.IICS_CANVAS_INTEGRATIONS.PERSON_GROUP

    *This is the table that groups different students into groups fro queries. Such as students, observers, etc.

CESPRD.IICS_CANVAS_INTEGRATIONS.STD_FLAG_HOLDS

    *This is the table that contains all of the info for different BYU students.


Why is it needed?
-  API.swaggerFileName (Github Informatica-config-files -> Swagger -> Dev -> Canvas -> Find file you are working in)

Link to API documentation
  - [Link to API documentation from Canvas](https://canvas.instructure.com/doc/api/users.html#method.users.create)
  - To influence how IICS interacts with the API, follow the swagger path above ^
## Design Decisions
  - Lots of design changes have been made regarding the BYU change to @byu.edu emails
## Past/Frequent Issues
  - [Canvas has interesting properties with stickiness, here is an article where you can learn more about it.](https://community.canvaslms.com/t5/SIS-User-Articles/Canvas-Sticky-Fields-UI-Override/ta-p/255108)
  - Operations using email can often not properly function, regarding the May 10th BYU change to only @byu.edu emails. Be sure to check that they BYU_internal_email tables are functioning properly. We have used a Lookup for the BYU email, and then hardcoded 'net.id' concat with '@byu.edu'.
## Future Enhancement Ideas/Vendor Future Fixes?
  - Optimizing some processes may be possible, but otherwise things are working so far.
## Creators and Editors of the process
  - Spencer Boyer
  - Sam McKnight
  - Logan Brewer
  - Abe Lamoreaux

\* means that some decisions are coming soon that could change how we do this.
