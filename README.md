# Lab #5A: Introduction to Relational Database Systems and Data Models

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

## Acknowledgements

The author consulted the following resources when building this tutorial:
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "SQL"](https://librarycarpentry.org/lc-sql/)

# Table of Contents

- [Understanding Relational Databases](#understanding-relational-databases)
  * [Why A Database?](#why-a-database)
  * [What is an ERD?](#what-is-an-erd)
    * [Entities](#entities)
    * [Attributes](#attributes)
    * [Relationships](#relationships)
    * [Cardinality](#cardinality)
  * [Building an ERD](#building-an-erd)
    * [Where Are My Keys?](#where-are-my-keys)
    * [Relational Schema](#relational-schema)
- [Additional Resources](#additional-resources)
- [Lab Notebook Questions](#lab-notebook-questions)

# Data

Database_Lab_Data.xlsx

Database_Lab_Player_Birthplaces.csv

Database_Lab_Team_Locations.csv

Database_Lab_Transactions.csv

MAKE SURE THESE ARE CLEANED UP

# Understanding Relational Databases

## From table to database

In *Inventing the Medium*, Janet Murray describes a table as "one of the basic building blocks of information design, an extension of the list through spatialization and the bases for database design."

FIGURE 1

In tabular data structures, columns headers describe the data contained in corresponding columns, or fields. 

Each row contains as record with data in separate column cells, or fields.

Let's unpack some of the terminology.

Term | Definition
--- | ---
**Data** | Any collection of symbolic units, often quantitative, collected or presented for the purpose of analysis. Data become most useful when structured by semantic segmentation into labeled units
**Record** | An entry in a database representing a single item, made up of discrete fields
**Fields** | In a database, a field is a segment of a record with a fixed length and data type that corresponds to a single semantic unit, like a name or address
**Table** | One of the basic building blocks of information design

These building blocks of data structured as records with fields organized in a table are the foundation of a relational database.

We've worked with tabular data (i.e. data organized in a table) earlier in the semester when working with CSV files.

## Why do we need relational databases?

Let's imagine we want to know how many professional baseball players born in Puerto Rico played for teams located in the state of Iowa during the 2016 season.

Our first step is to break down the different components of this research question, with an eye toward what data we would need to answer this question.
- We would need to have a list of people who played professional baseball during the 2016 season.
- We would need to know country birthplace information for everyone on that list.
- We would need to know what professional teams were located in Indiana during the 2016 season.
- We would need to know which players were on specific teams 

Our next step is to possible sources or resources that might provide this data.

[Baseball Reference](https://www.baseball-reference.com/), "the complete source for current and historical baseball players, teams, scores and leaders," seems like a good place to start.

We could start by looking up the records for an individual player to see what information is available.

Let's take a look at the [individual player page on Baseball Reference](https://www.baseball-reference.com/players/s/samarje01.shtml) for former Notre Dame baseball and football player Jeff Samardzija.

FIGURE 2

FIGURE 3

We can get some pieces of information from this page, like player birthplace and teams played for.

But not all of that information is located in a table structure. 

And the table structure that is present doesn't lend itself to answering our specific research question.

We could also look at the individual team page for a team located in Indiana.

Let's take a look at the [2019 season team page](https://www.baseball-reference.com/register/team.cgi?id=a87c825c) for the South Bend Cubs.

FIGURE 4

FIGURE 5

We can get some pieces of information from this page, like the team location and roster.

But again, not all of that information is located in a table structure.

And the table structure that is present doesn't lend itself to answering our specific research questions.

Since there are only 3 affiliated professional teams in Indiana, manually downloading the spreadsheets for these teams for a single season and wrangling the data into the structure needed to answer our specific research question wouldn't be overly time intensive.

But let's say we might have other research questions down the line, or we might want to make our data available to other researchers. 

Only gathering data that responds to our specific research question might save time in the short term but foreclose possibilities long-term.

Imagine the types of research questions we could ask and answer with data that covered multiple seasons, for teams in multiple locations.

We could do some automated scraping and manual wrangling to end up with data structures that answer our specific research question but also would work to answer a variety of other research questions.

We could have a `Player_Birthplaces` table that includes information about where players were born.

id_person | dob | city | state | country | region | group | lat | long
--- | --- | --- | --- | --- | --- | --- | --- | ---
unique id for specific individual players | date of birth (year) | city of birth | state of birth | country of birth | birth country region | birth country geographical group | birth location latitude | birth location longitude
292345 | 1995 | | Baja California | MX | Central America | Latin America and the Caribbean | 30.033892 | -115.142511
223204 | 1995 | | Carabobo | VE | South America | Latin America and the Caribbean | 10.166667 | -68.083333
223511 | 1995 | | Carabobo | VE | South America | Latin America and the Caribbean | 10.166667 | -68.083333

We could have a `Team_Locations` table that includes information about team locations and affiliations.

team_id | season | affiliate_league | affiliate | league | team_name | classification | category | city | state | country
--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---
unique identifier for each team in specific season | season (year) | league for major league team affiliation | major league team affiliation | minor league name | team name | classification level (in hierarchical classification system) | team major or minor league status | team city | team state | team country
2016_Arizona_Diamondbacks | 2017 | NL | ARI | Arizona | Diamondbacks | Rk | MiLB | | AZ | US
2016_DominicanSummer_Diamondbacks1 | 2017 | NL | ARI | Dominican Summer | Diamondbacks 1 | FRk | MiLB | | | DO
2016_DominicanSummer_Diamondbacks2 | 2017 | NL | ARI | Dominican Summer | Diamondbacks 2 | FRk | MiLB | | | DO
2016_Northwest_Hillsboro | 2017 | NL | ARI | Northwest | Hillsboro | A- | MiLB | Hillsboro | OR | US

We could also have a `Combined_Transactions` that includes information about which players played on specific teams in a given season.

id_person | season | classification | category | league_name | team_name | team_id
--- | --- | --- | --- | --- | --- | ---
unique id for specific individual players | season (year) | classification level (in hierarchical classification system) | team major or minor league status | league name | team name | unique identifier for each team in specific season
484 | 2016 | MLB | MLB | American | NYY | 2016_American_NYY
484 | 2016 | MLB | MLB | American | NYY | 2016_American_NYY
625 | 2016 | MLB | MLB | American | BOS | 2016_American_BOS
706 | 2016 | MLB | MLB | American | HOU | 2016_American_HOU
706 | 2016 | MLB | MLB | American | HOU | 2016_American_HOU
837 | 2016 | MLB | MLB | National | PIT | 2016_National_PIT

Let's take a look at at Excel workbook that includes these three tables tables.

Open the `Database_Lab_Data.xlsx` file in a spreadsheet program.

This Excel workbook includes three tables:
- Player_Birthplaces
- Team_Locations
- Combined_Transactions

<blockquote>QX: Explore the tables. What fields do you see? How would you describe these fields, using the language of string, double, and integer to describe the data types.</blockquote>

Type | Description | Example
--- | --- | ---
String | Used to store text or a string of non-integer characters | "This classroom is in Bond Hall" or "student"
Integer | Used to store positive or negative whole numbers | -25, 0, 25
Double | Used to store precise numerical values that include decimal points | 3.14159265359

Consult the following resources as needed to understand this data:
- [ISO 3166 country code table (Wikipedia)](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Decoding_table)
- [United Nations geographic regions](https://unstats.un.org/unsd/methodology/m49/)
- [USPS list of state abbreviations](https://about.usps.com/who-we-are/postal-history/state-abbreviations.htm)
- [Wikipedia list of baseball team abbreviations](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_Baseball/Team_abbreviations)
- [Wikipedia glossary of baseball jargon](https://en.wiktionary.org/wiki/Appendix:Glossary_of_baseball)


73- So now that we have some structured data, let's return to our original research question.

74- The `Player_Birthplaces` table includes information about where players were born. The `Team_Locations` table includes information about where teams are located. The `Transactions` table tells us which players played for which teams.

75- But the `Transactions` table on its own doesn't include the information about player birthplace and team location we need to answer the question of how many baseball players born in Puerto Rico played for teams located in the state of Indiana.

76- We could add that location information to the `Transactions` table, but we would end up with significant redundant and duplicate information.

77- Behold the magic of relational databases.

## What is a relational database?

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_29.png?raw=true" alt="Capture_2"  /></p>

Image from Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html).

As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "Relational databases consist of one or more tables of data. These tables have fields (columns) and records (rows). Every field has a data type. Every value in the same field of each record has the same type. These tables can be linked to each other when a field in one table can be matched to a field in another table."

78- Linking our three individual data tables in a relational database will enable us to answer the question about Puerto Rican players in Indiana without having to change the underlying data structure.

### Database Terminology

A ***database*** is an information structure composed of identically structured records, which can be created, modified, and accessed individually…Each record of a database contains segments called fields. The set of all records sharing the same field structure is called a table. Databases structured as a single table are called flat file databases; those with multiple interlocking tables are relational databases.

Some terminology that goes along with relational database systems (sometimes called RDBMS, for relational database management system).

An ***entity*** is any abstract item in a computer program that can be given a unique name. Entities often have attributes.

An ***attribute*** is a quality of an abstract entity expressed as a generalized category (e.g., “color” as an attribute of flowers). Attributes have values that vary with particular instances of the abstract entity they describe (e.g., the color “red” of a particular flower). Such attribute/value pairs can take the form of fields in a database or metadata tags or variables attached to objects in computer programs.

## What is an ERD?

79- An entity relationship diagram (sometimes called an ER Diagram or ERD) is a visual representation of tabular data structures that are linked as part of a database.

80- Building an ERD requires understanding the underlying structure of your data, as well as how you want to create links across individual tables.

81- ERDs have a specific vocabulary for describing database structure.

82- In 1997, computer scientist Peter Chen outlined a natural language framework for building ER diagrams.

English Grammar Structure | ERD Structure
--- | ---
Common noun | Entity type
Proper noun | Entity
Transitive verb | Relationship type
Intransitive verb | Attribute type
Adjective | Attribute for entity
Adverb | Attribute for relationship

<blockquote>Peter Pin-Shan Chen, "English, Chinese and ER Diagrams," Data & Knowledge Engineering 23 (1997), 5-16. https://doi.org/10.1016/S0169-023X(97)00017-7</blockquote>

### Entities

"A definable thing—-such as a person, object, concept or event-—that can have data stored about it. Think of entities as nouns. Examples: a customer, student, car or product." ([The components and features of an ER diagram,](https://www.lucidchart.com/pages/er-diagrams#section_3) LucidChart)

<blockquote>Q13: What entities are in the Player_Birthplaces, Team_Locations, and Transactions tables? List the entitites by table and include some explanation of your thought process. If you're getting stuck, try describing the data included in each table using a sentence. Where are the nouns in each sentence?</blockquote>

83- Entities are represented as rectangles in an ER Diagram.

### Attributes

"A property or characteristic of an entity." ([The components and features of an ER diagram,](https://www.lucidchart.com/pages/er-diagrams#section_3) LucidChart)

<blockquote>Q14: What attributes are in the Player_Birthplaces, Team_Locations, and Transactions tables? What entities do these attributes describe? List the attributes by entity and table and include some explanation of your thought process. If you're getting stuck, go back to your list of entities from Q13. What non-entity information in each table might describe an entity?</blockquote>

84- Attributes are represented as ovals in an ER Diagram.

### Relationships

"How entities act upon each other or are associated with each other. Think of relationships as verbs. For example, the named student might register for a course. The two entities would be the student and the course, and the relationship depicted is the act of enrolling." ([The components and features of an ER diagram,](https://www.lucidchart.com/pages/er-diagrams#section_3) LucidChart)

<blockquote>Q15: What relationships do you see within and across entities in the Player_Birthplaces, Team_Locations, and Transactions tables? What entities do these relationships connect? Include some explanation of your thought process. If you're getting stuck, go back to your list of entities from Q13. How do these entities connect?</blockquote>

85- Relationships are represented as diamonds with lines that connect entity rectangles.

### Cardinality

"Defines the numerical attributes of the relationship between two entities or entity sets." ([The components and features of an ER diagram,](https://www.lucidchart.com/pages/er-diagrams#section_3) LucidChart)

86- Types of cardinality:

- One-to-one relationships
  * For example each Notre Dame student has a unique ID number.
- One-to-many relationships
  * A single ND student registers for multiple courses.
- Many-to-many relationships
  * Multiple ND students work with multiple faculty members, and multiple faculty members work with multiple students.

87- The three main cardinal relationships are one-to-one, one-to-many, and many-many. A one-to-one example would be one student associated with one mailing address. A one-to-many example (or many-to-one, depending on the relationship direction): One student registers for multiple courses, but all those courses have a single line back to that one student. Many-to-many example: Students as a group are associated with multiple faculty members, and faculty members in turn are associated with multiple students.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_30.PNG?raw=true" alt="Capture_2"  /></p>

88- Cardinality is indicated through symbols added to the connecting lines of a relationship.

<blockquote>Q16: Include the cardinality for the relationships you identified in Q15. Include some explanation of your thought process.</blockquote>

Visit Lucidchart's [What is an Entity Relationship Diagram (ERD)?](https://www.lucidchart.com/pages/er-diagrams#top) to learn more about the history, components, and limits of ER Diagrams.

## Building an ERD

<blockquote>Q17: Work with a colleague to build an ERD for the Player_Birthplaces, Team_Locations, and Transactions tables. Include your diagram as well as an explanation of your process.</blockquote>

89- You can draw these by hand, use a drawing tool, or use a free online ERD tool like [ERDPlus](https://erdplus.com/) or [LucidChart](https://www.lucidchart.com).

## Where Are My Keys?

90- By this point you may be wondering why our data tables have various `id` columns. 

91- The ERD we built in Q17 outlines the conceptual relationships across our data structures.

92- But relationship database programs require matching data fields and unique identifiers to be able to manifest those conceptual relationships.

93- These unique identifiers and matching fields are called keys.

"The primary key is defined as a column (or set of columns) where each value is unique and identifies a single row of the table." ([Primary Key-Foreign Key Relationships,](https://docs.oracle.com/cd/E12100_01/books/admintool/admintool_DataModeling4.html) Oracle)

"A foreign key is a column or a set of columns in one table that references the primary key columns in another table." ([Primary Key-Foreign Key Relationships,](https://docs.oracle.com/cd/E12100_01/books/admintool/admintool_DataModeling4.html) Oracle)

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_31.jpg?raw=true" alt="Capture_2"  /></p>

Image from [Foreign and Primary Key Differences (Visually Explained),](https://www.essentialsql.com/what-is-the-difference-between-a-primary-key-and-a-foreign-key/) EssentialSQL.

<blockquote>Q18: What fields in our tables are functioning as keys? Which ones are primary keys and which ones are foreign keys? Include some explanation of your thought process.</blockquote>

## Relational Schema

94- ER Diagrams represent the conceptual relationships in a relational database structure.

95- But, we might also want to represent our database structure based on tables, primary keys, and foreign keys.

96- An image from StackExchange's [ER vs database schema diagrams page](https://dba.stackexchange.com/questions/119380/er-vs-database-schema-diagrams) that illustrates the difference:

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_c.png?raw=true" alt="Capture_2"  /></p>

<blockquote>Q19: Work with a colleague to build a relational schema for a relational database that includes the Player_Birthplaces, Team_Locations, and Transactions tables. Include your diagram as well as an explanation of your process.</blockquote>

Visit StackOverflow's [What is the different between ER Diagram and Database Schema?](https://stackoverflow.com/questions/17641134/what-is-different-between-er-diagram-and-database-schema) page to learn more.

# Project prompts

Take an existing dataset and reverse engineer a data model

Describe a hypothetical situation in which you would be using/implementing a relational database

Build an ERD and RS for that implementation/use case


# Additional Resources
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "SQL"](https://librarycarpentry.org/lc-sql/)
- [Lucid Chart "Database Design"](https://www.lucidchart.com/pages/database-diagram/database-design)
- [Lucid Chart "ER Diagrams"](https://www.lucidchart.com/pages/er-diagrams)

# Lab Notebook Questions

Q1: What questions do you have about these principles? Which ones are unclear are confusing?
   
Q2: What fields are represented in these datasets? Describe the data fields in your own words. Use the language of string, double, and integer to describe the data fields.
    
Q3: Provide 3 distinct examples from the sample datasets that do not conform to tidy data principles. Include the example as well as an explanation.

Q4: Discuss with a colleague what issues you are seeing in these datasetes. What commonalities or patterns are you seeing?

Q5: How would you address these pattern errors so the data conforms to tidy data principles? Describe what steps you would take to address at least 3 pattern errors. For each error, include the following elements: an example of the error, an explanation of your method to address the error, and the same example as tidy data.
    
Q6: Compare your experience working in OpenRefine to other experiences you have had in a text editor or spreadsheet program. In what ways do you understand, perceive, or relate to the data differently through working in OpenRefine? Describe your experience cleaning this data in OpenRefine.

Q7: Describe a past experience working with a spreadsheet program. What were you trying to do? How did it go? What was your overall feeling about working with data in a spreadsheet program?

Q8: Compare your experience working in Excel to your experience working in OpenRefine. In what ways do you understand, perceive, or relate to the data differently through working in Excel? Describe your experience cleaning this data in Excel.

Q9: For the baseball datasets we have been working with in this lab, what do you think may have contributed to or caused the pattern errors we needed to address? How could these pattern errors be addressed in the data entry process?

Q10: Describe how you would go about building a survey form or template for the `CSC_Database_Lab_PlayerBirthplaces.csv` file. You DO NOT need to actually create or submit a survey form. Describe what types of questions and pre-defined question or field options could you use to more effectively generate the data in this file.

Q11: Describe how you would go about using data validation to build a template for the `CSC_Database_Lab_PlayerBirthplaces.csv` file. You DO NOT need to actually create or submit a template. Describe what data validation options and pre-defined field options could you use to more effectively generate the data in this file.

Q12: What types of fields do you see in the Transactions table? What kinds of connections could you see across these three tables?

Q13: What entities are in the Player_Birthplaces, Team_Locations, and Transactions tables? List the entitites by table and include some explanation of your thought process. If you're getting stuck, try describing the data included in each table using a sentence. Where are the nouns in each sentence?

Q14: What attributes are in the Player_Birthplaces, Team_Locations, and Transactions tables? What entities do these attributes describe? List the attributes by entity and table and include some explanation of your thought process. If you're getting stuck, go back to your list of entities from Q13. What non-entity information in each table might describe an entity?

Q15: What relationships do you see within and across entities in the Player_Birthplaces, Team_Locations, and Transactions tables? What entities do these relationships connect? Include some explanation of your thought process. If you're getting stuck, go back to your list of entities from Q13. How do these entities connect?

Q16: Include the cardinality for the relationships you identified in Q15. Include some explanation of your thought process.

Q17: Work with a colleague to build an ERD for the Player_Birthplaces, Team_Locations, and Transactions tables. Include your diagram as well as an explanation of your process.

Q18: What fields in our tables are functioning as keys? Which ones are primary keys and which ones are foreign keys? Include some explanation of your thought process.

Q19: Work with a colleague to build a relational schema for a relational database that includes the Player_Birthplaces, Team_Locations, and Transactions tables. Include your diagram as well as an explanation of your process.
