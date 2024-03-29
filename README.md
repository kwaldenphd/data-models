# Introduction to Relational Database Systems

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>This tutorial was written by Katherine Walden and is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

The first part of this lab provides an overview of relational database data models. It covers core RDBMS syntax and provides a case-study based approach to demonstrate the utility of relational databases. It introduces students to the concept and components of an ERD, including entities, attributes, relationships, cardinality, and keys. It gives students hand-on experience building data models. It also covers relational schema.

By the end of this section, students will be able to:
- Understand the relational databases' core concepts and terminology
- Understand and articulate the utility of relational databases
- Describe the core components of an entity-relationship diagram 
- Construct ER and RS diagrams

The second part of this lab covers the basics of getting started with SQLite using DB Browser for SQLite. It provides an overview for SQLite and explains the core components of the DB Browser GUI interface. It uses a case-study approach to show how to build a relational database from CSV files in DB Browser, including setting keys and building table relationships.

By the end of this section, students will be able to:
- Understand the core components of SQL and the DB Browser for SQLite
- Have a working installation of DB Browser for SQLite on their personal computer
- Understand how to load structured data into DB Browser
- Understand how to set data types and key fields in DB Browser 
- Understand how to export from DB Browser

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=da5b8c14-e546-44fd-8f65-af36014781ce">Lecture/live coding playlist</a></td>
  </tr>
  </table>

## Acknowledgements

The author consulted the following resources when building this tutorial:
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "SQL"](https://librarycarpentry.org/lc-sql/)

Peer review and editing was provided by Spring 2021 graduate teaching assistant [Aidan Draper](https://github.com/adraper2).

# Table of Contents

- [Lecture & live coding](#lecture--live-coding)
- [Overview](#overview)
- [Lab notebook template](#lab-notebook-template)
- [Data](#data)
- [Tools](#tools)
- [Understanding Relational Databases](#understanding-relational-databases)
  * [From table to database](#from-table-to-database)
  * [Why do we need relational databases?](#why-do-we-need-relational-databases)
  * [What is a relational database?](#what-is-a-relational-database)
    * [Database Terminology](#database-terminology)
  * [What is an ERD?](#what-is-an-erd)
    * [Entities](#entities)
    * [Attributes](#attributes)
    * [Relationships](#relationships)
    * [Cardinality](#cardinality)
  * [Building an ERD](#building-an-erd)
    * [Where Are My Keys?](#where-are-my-keys)
    * [Relational Schema](#relational-schema)
  * [Additional Resources](#additional-data-model-resources)
- [Getting started with SQL](#getting-started-with-sql)
  * [What is SQLite](#what-is-sqlite)
  * [Installing DB Browser for SQLite](#installing-db-browser-for-sqlite)
  * [Getting Started with DB Browser for SQLite](#getting-started-with-db-browser-for-sqlite)
    * [Importing Tables from `.csv` Files](#importing-tables-from-csv-files)
    * [Setting Keys and Building Table Relationships](#setting-keys-and-building-table-relationships)
- [Additional Lab Notebook Questions](#additional-lab-notebook-questions)
- [Lab Notebook Questions](#lab-notebook-questions)

# Lecture & Live Coding

Throughout this lab, you will see a Panopto icon at the start of select sections.

This icon indicates there is lecture/live coding asynchronous content that accompanies this section of the lab. 

You can click the link in the figure caption to access these materials (ND users only).

Example:

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=4e53d598-3a0a-4ac9-9d9e-ae2f010196ca">Lecture/live coding playlist</a></td>
  </tr>
  </table>

# Overview

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=2c0a29bb-4b41-42ac-9862-ae2f00f68167">Overview</a></td>
  </tr>
  </table>

# Lab Notebook Template

[Link to lab notebook template (Google Doc)](https://docs.google.com/document/d/1hlcv_xovvtM9aSYEkyIlnmE71jnrqQ5b4WKazr4gYog/copy)
- Insert any needed ERDs or relational schema as images in the Google Doc.
  * [Tutorial for adding images/tables/drawings to a Google Doc](https://www.techrepublic.com/article/how-to-add-images-tables-and-drawings-to-a-google-doc-file/)

# Data

The following data files are used in this tutorial, with Google Drive links (ND users only) provided below:
- Google Sheets project with all needed files:
  * [`Combined_Workbook.xlsx`](https://docs.google.com/spreadsheets/d/1uan6i77n9mz62arr8wh-l2hICZ6JmYf2wWK_okDtiLw/edit?usp=sharing)
    * You can copy to your own Drive workspace and/or download as an Excel workbook (`.xlsx`)
    * NOTE: There is also a [`geography` table](https://drive.google.com/file/d/1y4VRl1Ye8_uMLxGmpAGlL-5eEU3qQ5PH/view?usp=sharing) included in the `Combined_Workbook` file. You can ignore it for the purposes of this lab.
- Individual CSV files:
  * [`Player_Birthplaces.csv`](https://drive.google.com/file/d/1qthm3HSN5FaEFusC1_Zk-0qL0A6LIEB-/view?usp=sharing)
  * [`Team_Locations.csv`](https://drive.google.com/file/d/1fttQhzoAwYOJC-mB17RATaqD4mfUTIV_/view?usp=sharing)
  * [`Combined_Transactions.csv`](https://drive.google.com/file/d/17Z9C7snAMjARTQYoRXufwaO2j9ssl0g8/view?usp=sharing)
    * You can download the CSV files to your computer and/or copy to Google Drive.

You can also download the four files in a compressed folder (`.zip`): [Google Drive link, ND users](https://drive.google.com/file/d/1KMJ35drSMj8shlw0zG1KIGqt9nXknyk3/view?usp=sharing)

# Tools

Part of what we'll be doing in this lab involves building a couple of specific types of diagrams: entity-relationship diagrams (ERDs) and relational schema (RS)

You're welcome to draw these by hand, but there are free online and downloadable tools you can use to generate these diagrams.

- Free generic drawing tools:
  - [Google Drawings](https://docs.google.com/drawings) *Google Drive tool*
  - [Microsoft Paint](https://www.microsoft.com/en-us/p/paint-3d/9nblggh5fv99) *Windows users*
  - [MacOS Paintbrush](https://paintbrush.sourceforge.io/) *Mac users*
- Free online database-specific tools:
  - [ERDPlus](https://erdplus.com/)
    * *Prof. Walden's go-to tool that lets you convert an ERD into a relational schema.*
  - [LucidChart](https://www.lucidchart.com/pages/?anonId=0.1c8414ae17e41a83751)
  - [Visual Paradigm Online](https://online.visual-paradigm.com/diagrams/solutions/free-erd-tool/)

# Understanding Relational Databases

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=c6042902-e729-4b39-a6f9-ae2f00f8b92e">Understanding Relational Databases</a></td>
  </tr>
  </table>

## From table to database

In *Inventing the Medium*, Janet Murray describes a table as "one of the basic building blocks of information design, an extension of the list through spatialization and the bases for database design." We've worked with tabular data (i.e. data organized in a table) previously when working with CSV files.

<p align="center"><a href="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_1.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_1.png?raw=true" /></a></p>

Image from Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html).

In tabular data structures, columns headers describe the data contained in corresponding columns, or fields. Each row contains as record with data in separate column cells, or fields. These building blocks of data structured as records with fields organized in a table are the foundation of a relational database. Let's unpack some of the terminology.

Term | Definition
--- | ---
**Data** | Any collection of symbolic units, often quantitative, collected or presented for the purpose of analysis. Data becomes most useful when structured by semantic segmentation into labeled units
**Record** | An entry in a database representing a single item, made up of discrete fields
**Fields** | In a database, a field is a segment of a record with a fixed length and data type that corresponds to a single semantic unit, like a name or address
**Table** | One of the basic building blocks of information design

## Why do we need relational databases?

Let's imagine we want to know how many professional baseball players that were born in Puerto Rico played for teams located in the state of Indiana during the 2016 season.

Our first step is to break down the different components of this research question, with an eye toward what data we would need to answer this question.
- We would need to have a list of people who played professional baseball during the 2016 season.
- We would need to know country birthplace information for everyone on that list.
- We would need to know what professional teams were located in Indiana during the 2016 season.
- We would need to know which players were on specific teams 

Our next step is to possible sources or resources that might provide this data. [Baseball Reference](https://www.baseball-reference.com/), "the complete source for current and historical baseball players, teams, scores and leaders," seems like a good place to start.

We could start by looking up the records for an individual player to see what information is available. Let's take a look at the [individual player page on Baseball Reference](https://www.baseball-reference.com/players/s/samarje01.shtml) for former Notre Dame baseball and football player Jeff Samardzija.

<p align="center"><a href="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_2.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_2.png?raw=true" /></a></p>

<p align="center"><a href="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_3.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_3.png?raw=true" /></a></p>

We can get some pieces of information from this page, like player birthplace and teams played for. But not all of that information is located in a table structure. And the table structure that is present doesn't lend itself to answering our specific research question.

We could also look at the individual team page for a team located in Indiana. Let's take a look at the [2019 season team page](https://www.baseball-reference.com/register/team.cgi?id=a87c825c) for the South Bend Cubs.

<p align="center"><a href="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_4.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_4.png?raw=true" /></a></p>

<p align="center"><a href="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_5.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_5.png?raw=true" /></a></p>

We can get some pieces of information from this page, like the team location and roster. But again, not all of that information is located in a table structure. And the table structure that is present doesn't lend itself to answering our specific research questions.

Since there are only 3 affiliated professional teams in Indiana, manually downloading the spreadsheets for these teams for a single season and wrangling the data into the structure needed to answer our specific research question wouldn't be overly time intensive. But let's say we might have other research questions down the line, or we might want to make our data available to other researchers. 

Only gathering data that responds to our specific research question might save time in the short term but foreclose possibilities long-term. Imagine the types of research questions we could ask and answer with data that covered multiple seasons, for teams in multiple locations.

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

Let's take a look at at Excel workbook that includes these three tables tables. Open the [`Combined_Workbook.xlsx`](https://docs.google.com/spreadsheets/d/1uan6i77n9mz62arr8wh-l2hICZ6JmYf2wWK_okDtiLw/edit?usp=sharing) file in a spreadsheet program (Google Sheets, Microsoft Excel, Apple Numbers).

This Excel workbook includes three tables:
- Player_Birthplaces
- Team_Locations
- Combined_Transactions
  * There's also a `geography` table, but we're going to ignore that for now. 

<blockquote>Q1: Spend some time exploring the tables. What kinds of information are included? How would you the fields in each table, using the language of string, double, and integer to describe the data types.</blockquote>

Type | Description | Example
--- | --- | ---
String | Used to store text or a string of non-integer characters | "This classroom is in Bond Hall" or "student"
Integer | Used to store positive or negative whole numbers | -25, 0, 25
Double | Used to store precise numerical values that include decimal points | 3.14159265359

You may need to consult the following resources as needed to understand this data:
- [ISO 3166 country code table (Wikipedia)](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Decoding_table)
- [United Nations geographic regions](https://unstats.un.org/unsd/methodology/m49/)
- [USPS list of state abbreviations](https://about.usps.com/who-we-are/postal-history/state-abbreviations.htm)
- [Wikipedia list of baseball team abbreviations](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_Baseball/Team_abbreviations)
- [Wikipedia glossary of baseball jargon](https://en.wiktionary.org/wiki/Appendix:Glossary_of_baseball)

So now that we have some structured data, let's return to our original research question. The `Player_Birthplaces` table includes information about where players were born. The `Team_Locations` table includes information about where teams are located. The `Transactions` table tells us which players played for which teams. But the `Transactions` table on its own doesn't include the information about player birthplace and team location we need to answer the question of how many baseball players born in Puerto Rico played for teams located in the state of Indiana. We could add that location information to the `Transactions` table, but we would end up with significant redundant and duplicate information.

Behold the magic of relational databases.

## What is a relational database?

<p align="center"><a href="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_1.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/data-models/blob/main/figures/Figure_1.png?raw=true" /></a></p>

Image from Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html).

As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "Relational databases consist of one or more tables of data. These tables have fields (columns) and records (rows). Every field has a data type. Every value in the same field of each record has the same type. These tables can be linked to each other when a field in one table can be matched to a field in another table."

Linking our three individual data tables in a relational database will enable us to answer the question about Puerto Rican players in Indiana without having to change the underlying data structure.

### Database Terminology

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=583db279-091c-43c7-a777-ae2f00fabc50">Database Terminology</a></td>
  </tr>
  </table>

A ***database*** is an information structure composed of identically structured records, which can be created, modified, and accessed individually…Each record of a database contains segments called fields. The set of all records sharing the same field structure is called a table. Databases structured as a single table are called flat file databases; those with multiple interlocking tables are relational databases.

Some terminology that goes along with relational database systems (sometimes called RDBMS, for relational database management system).
- An ***entity*** is any abstract item in a computer program that can be given a unique name. Entities often have attributes.
- An ***attribute*** is a quality of an abstract entity expressed as a generalized category (e.g., “color” as an attribute of flowers). Attributes have values that vary with particular instances of the abstract entity they describe (e.g., the color “red” of a particular flower). Such attribute/value pairs can take the form of fields in a database or metadata tags or variables attached to objects in computer programs.
- A **relationship** is the connection or association (most commonly) between two entities.

## What is an ERD?

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=583db279-091c-43c7-a777-ae2f00fabc50">ERDs</a></td>
  </tr>
  </table>

An entity relationship diagram (sometimes called an ER Diagram or ERD) is a visual representation of tabular data structures that are linked as part of a database. Building an ERD requires understanding the underlying structure of your data, as well as how you want to create links across individual tables. ERDs have a specific vocabulary for describing database structure. In 1997, computer scientist Peter Chen outlined a natural language framework for building ER diagrams.

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

<blockquote>Q2: What entities are in the Player_Birthplaces, Team_Locations, and Transactions tables? List the entitites by table and include some explanation of your thought process. If you're getting stuck, try describing the data included in each table using a sentence. Where are the nouns in each sentence?</blockquote>

Entities are represented as rectangles in an ER Diagram.

### Attributes

"A property or characteristic of an entity." ([The components and features of an ER diagram,](https://www.lucidchart.com/pages/er-diagrams#section_3) LucidChart)

<blockquote>Q3: What attributes are in the Player_Birthplaces, Team_Locations, and Transactions tables? What entities do these attributes describe? List the attributes by entity and table and include some explanation of your thought process. If you're getting stuck, go back to your list of entities from Q2. What non-entity information in each table might describe an entity?</blockquote>

Attributes are represented as ovals in an ER Diagram.

### Relationships

"How entities act upon each other or are associated with each other. Think of relationships as verbs. For example, the named student might register for a course. The two entities would be the student and the course, and the relationship depicted is the act of enrolling." ([The components and features of an ER diagram,](https://www.lucidchart.com/pages/er-diagrams#section_3) LucidChart)

<blockquote>Q4: What relationships do you see within and across entities in the Player_Birthplaces, Team_Locations, and Transactions tables? What entities do these relationships connect? Include some explanation of your thought process. If you're getting stuck, go back to your list of entities from Q2. How do these entities connect?</blockquote>

Relationships are represented as diamonds with lines that connect entity rectangles.

### Cardinality

"Defines the numerical attributes of the relationship between two entities or entity sets." ([The components and features of an ER diagram,](https://www.lucidchart.com/pages/er-diagrams#section_3) LucidChart)

Types of cardinality:

- One-to-one relationships
  * For example, each Notre Dame student has a unique ID number.
- One-to-many relationships
  * A single ND student registers for multiple courses.
- Many-to-many relationships
  * Multiple ND students work with multiple faculty members, and multiple faculty members work with multiple students.

The three main cardinal relationships:
- `one-to-one`
  * *one student associated with one mailing address*
- `one-to-many`
  * *one student registers for multiple courses, but all those courses have a single line back to that one student*
- `many-many`
  * *students as a group are associated with multiple faculty members, and faculty members in turn are associated with multiple students*

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_30.PNG?raw=true" alt="Capture_2"  /></p>

Cardinality is indicated through symbols added to the connecting lines of a relationship.

<blockquote>Q5: Include the cardinality for the relationships you identified in Q4. Include some explanation of your thought process.</blockquote>

Visit Lucidchart's [What is an Entity Relationship Diagram (ERD)?](https://www.lucidchart.com/pages/er-diagrams#top) to learn more about the history, components, and limits of ER Diagrams.

## Building an ERD

<blockquote>Q6: Build an ERD for the Player_Birthplaces, Team_Locations, and Transactions tables. Include your diagram as well as an explanation of your process.
<ul><li>Folks are welcome/encouraged to collaborate on this question. If so, include the names of your collaborators as part of your answer to this question.</li></ul></blockquote>

You can draw these by hand or use a drawing tool.

Free tools you can use to create ERDs:
- Free generic drawing tools:
  - [Google Drawings](https://docs.google.com/drawings) *Google Drive tool*
  - [Microsoft Paint](https://www.microsoft.com/en-us/p/paint-3d/9nblggh5fv99) *Windows users*
  - [MacOS Paintbrush](https://paintbrush.sourceforge.io/) *Mac users*
- Free online database-specific tools:
  - [ERDPlus](https://erdplus.com/)
    * *Prof. Walden's go-to tool that lets you convert an ERD into a relational schema.*
  - [LucidChart](https://www.lucidchart.com/pages/?anonId=0.1c8414ae17e41a83751)
  - [Visual Paradigm Online](https://online.visual-paradigm.com/diagrams/solutions/free-erd-tool/)

### Where Are My Keys?

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=5bad6da6-aa6b-4188-955b-ae2f00ff0583">Keys</a></td>
  </tr>
  </table>
  
By this point you may be wondering why our data tables have various `id` columns. The ERD we built in Q6 outlines the conceptual relationships across our data structures. To put that another way, ERDs are a conceptual model of a relational database structure.

But relationship database programs require matching data fields and unique identifiers to be able to manifest those conceptual relationships. These unique identifiers and matching fields are called `keys`.

- "The **primary key** is defined as a column (or set of columns) where each value is unique and identifies a single row of the table." ([Primary Key-Foreign Key Relationships,](https://docs.oracle.com/cd/E12100_01/books/admintool/admintool_DataModeling4.html) Oracle)

- "A **foreign key** is a column or a set of columns in one table that references the primary key columns in another table." ([Primary Key-Foreign Key Relationships,](https://docs.oracle.com/cd/E12100_01/books/admintool/admintool_DataModeling4.html) Oracle)

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_31.jpg?raw=true" alt="Capture_2"  /></p>

Image from [Foreign and Primary Key Differences (Visually Explained),](https://www.essentialsql.com/what-is-the-difference-between-a-primary-key-and-a-foreign-key/) EssentialSQL.

<blockquote>Q7: What fields in our tables are functioning as keys? Which ones are primary keys and which ones are foreign keys? Include some explanation of your thought process.</blockquote>

### Relational Schema

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=5bad6da6-aa6b-4188-955b-ae2f00ff0583">Relational Schema</a></td>
  </tr>
  </table>

ERDs are a conceptual model of the relationships in a database. An ERD may not directly map onto the structure of tables, fields, etc. in a relational database.

But, we might also want to represent our database structure based on tables, primary keys, and foreign keys. Relational schema (RS) model the logical, machine-readable relationship across tables and fields (linked by primary/foreign keys). Building a RS diagram involves listing fields by table, identifying relationships across tables, and which fields are serving as primary/foreign keys.

An image from StackExchange's [ER vs database schema diagrams page](https://dba.stackexchange.com/questions/119380/er-vs-database-schema-diagrams) that illustrates the difference:

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_c.png?raw=true" alt="Capture_2"  /></p>

Visit StackOverflow's [What is the different between ER Diagram and Database Schema?](https://stackoverflow.com/questions/17641134/what-is-different-between-er-diagram-and-database-schema) page to learn more.

<blockquote>Q8: Build a relational schema for a relational database that includes the Player_Birthplaces, Team_Locations, and Transactions tables. Include your diagram as well as an explanation of your process.
<ul><li>Folks are welcome/encouraged to collaborate on this question. If so, include the names of your collaborators as part of your answer to this question.</li></ul></blockquote>

## Additional Data Model Resources

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=28ed2cba-780a-4090-9b41-ae2f012ad599">Getting Started With ERDPlus</a></td>
  </tr>
  </table>

Free tools you can use to create ERDs and relational schema:
- Free generic drawing tools:
  - [Google Drawings](https://docs.google.com/drawings) *Google Drive tool*
  - [Microsoft Paint](https://www.microsoft.com/en-us/p/paint-3d/9nblggh5fv99) *Windows users*
  - [MacOS Paintbrush](https://paintbrush.sourceforge.io/) *Mac users*
- Free online database-specific tools:
  - [ERDPlus](https://erdplus.com/)
    * *Prof. Walden's go-to tool that lets you convert an ERD into a relational schema.*
  - [LucidChart](https://www.lucidchart.com/pages/?anonId=0.1c8414ae17e41a83751)
  - [Visual Paradigm Online](https://online.visual-paradigm.com/diagrams/solutions/free-erd-tool/)

To learn more about database design, ERDs, and relational schema:
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Lucid Chart "Database Design"](https://www.lucidchart.com/pages/database-diagram/database-design)
- [Lucid Chart "ER Diagrams"](https://www.lucidchart.com/pages/er-diagrams)

# Getting started with SQL

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=1c3a8553-0ceb-48cd-a658-ae2f012db592">SQLite</a></td>
  </tr>
  </table>

SQL stands for Structured Query Language. SQL "is a domain-specific language used in programming and designed for managing data held in a relational database management system (RDBMS)...It is particularly useful in handling structured data, i.e. data incorporating relations among entities and variables" ([Wikipedia, "SQL"](https://en.wikipedia.org/wiki/SQL)).

SQL was developed by IBM in the early 1970s. Relational Software, Inc. (now Oracle Corporation) released the first commercial implementations of SQL in the late 1970s. The American National Standards Institute (ANSI) and the International Organization for Standardization (ISO) adopted SQL as the official database query language in 1986. SQL is maintained by the ISO and is updated semi-regularly (typically every three years).
- [Link to official SQL documentation](https://standards.iso.org/ittf/PubliclyAvailableStandards/index.html)

For more on SQL history:
- Codd, Edgar F. (June 1970). "A Relational Model of Data for Large Shared Data Banks". *Communications of the ACM.* 13 (6): 377–87. https://doi.org/10.1145%2F362384.362685
- Chamberlin, Donald (2012). "Early History of SQL". *IEEE Annals of the History of Computing.* 34 (4): 78–82. https://doi.org/10.1109%2FMAHC.2012.61
- Chamberlin, Donald D; Boyce, Raymond F (1974). "SEQUEL: A Structured English Query Language." *Proceedings of the 1974 ACM SIGFIDET Workshop on Data Description, Access and Control. Association for Computing Machinery*: 249–64. https://doi.org/10.1145/800296.811515

## SQLite

We'll be using an implementation of SQL known as SQLite. "SQLite is a C-language library that implements a small, fast, self-contained, high-reliability, full-featured, SQL database engine. SQLite is the most used database engine in the world. SQLite is built into all mobile phones and most computers and comes bundled inside countless other applications that people use every day" ([SQLite, "What Is SQLite?"](https://www.sqlite.org/index.html)).

SQLite drives many commonly used programs and applications, including:
- Chrome, Firefox, and Safari web browsers
- Django
- Drupal
- Ruby on Rails
- Adobe Systems
- Evernote
- Skype
- iPhone text messages

Taking a quick look at SQLite's [Download](https://www.sqlite.org/download.html) and [Documentation](https://www.sqlite.org/docs.html) pages would suggest setting up a full implementation of STLite in your local computer environment is a tall order.
- *All hail the work of compilers*

So we're going to use a graphical-user interface (GUI) browser application that runs on top of SQLite. [Database Browser for SQLite (DB Browser)](https://sqlitebrowser.org/) is an open-source application that provides a graphical user interface for connecting to and interacting with a SQLite database. The DB Browser application bundles SQLite, so you won’t need to install SQLite separately.

## Installing DB Browser for SQLite

Navigate to https://sqlitebrowser.org/ in a web browser. Select the download version for your operating system:
- Windows: OOP Coders, ["Install DB Browser SQLite and create database"](https://youtu.be/CDen1TavGQ8) *YouTube* (2 September 2020)
- Mac: Cool IT Help, ["Sqlite Browser Installation on Mac OS"](https://youtu.be/SkXxnasbrFY) *YouTube* (3 October 2019)
- Google Chromebook: Follow the instructions for the Debian varation of Linux. 
  * See also: Dave McKay, ["How to Use DB Browser for SQLite on Linux"](https://www.howtogeek.com/704243/how-to-use-db-browser-for-sqlite-on-linux/), *How-To Geek* (16 September 2020)

Follow the installation instructions. Once the installation is complete, launch the program.

<blockquote>Q9: Describe your experience installing DB Browser for SQLite based on the provided instructions and available documentation. What challenges did you encounter, and how did you solve those problems?</blockquote>

## Getting started with DB Browser for SQLite

<p align="center"><a href="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_1.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_1.png?raw=true" /></a></p>

You should now be seeing the GUI (graphical user interface) window for the DB Browser application. We're going to create a relational database using the `.csv` files from the first part of this lab.

Click the "New Database" icon in the top-left hand menu bar, or select "New Database" under "Files." Save this database with a `.db` file extension in a dedicated location on your computer.

## Importing tables from `.csv` files

<p align="center"><a href="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_2.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_2.png?raw=true" /></a></p>

Add each of the `.csv` files by going to "Import table from CSV" under "Import" under "Files." Modify the table name if needed. 

<p align="center"><a href="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_3.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_3.png?raw=true" /></a></p>

When loading each table:
- Make sure the "Column names in first line" box is checked.
- Make sure comma is set as "Field separator," double quotation is set as "Quote character," and UTF-8 is set as "Encoding."
- Click "OK" to import the table from the `.csv` file.

<p align="center"><a href="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_5.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_5.png?raw=true" /></a></p>

Click on the "SQL Log" button on the bottom right-hand corner of the window to see the SQL commands used to import this data. These SQL commands are the programmatic expression of the steps we are taking using the graphical user interface.

Once we've done this for all of our `.csv` tables, our data should now be loaded into SQLite.

<p align="center"><a href="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_4.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_4.png?raw=true" /></a></p>

Click on the "Browse Data" tab to explore the data in each table (and make sure data imported correctly).

<blockquote>Q10: Describe yoru experience loading `.csv` files into DB Browser based on the provided instructions and available documentation. What challenges did you encounter, and how did you solve those problems?</blockquote>

## Setting Keys and Building Table Relationships

Now we need to set data types and identify our keys.
- Go back to [the first part of this lab](https://github.com/kwaldenphd/data-models#where-are-my-keys) if you're fuzzy on keys

Select the `Team_Locations` table and click on "Modify Table" icon. PC users can right-click on the selected table to see the "Modify Table" option.

<p align="center"><a href="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_6.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_6.png?raw=true" /></a></p>

For each table:
- Check the "Type" for each field and change as needed. 
- For fields that do not have null values, check `NN.` 
- For fields that have unique values, check `U`.
- We also want to make sure we check `PK` for this table's primary key field.

The bottom half of the "Edit table definition" window shows these steps in SQL syntax.
- Scroll down to the bottom of this embedded window if needed.

Click "OK" to apply these changes.

Go through the same process for the `Player_DoB` table.
- Check data types
- Mark not null values
- Mark unique values
- Set primary key

We'll go through a similar process for the `Combined_Transactions` table, but remember this table does not include a primary key--it has two foreign keys.
- *player_id or id_person*
- *team_id*

Before we can set the foreign keys, we have to change a foreign key constraint within the DB Browser application.

<p align="center"><a href="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_4.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_4.png?raw=true" /></a></p>

Select the "Edit Pragmas" tab.

<p align="center"><a href="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_7.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_7.png?raw=true" /></a></p>

Uncheck the box next to "Foreign Keys." Click "Save." Now we can modify the `Combined_Transactions` table and set our foreign key fields.

<p align="center"><a href="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_8.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_8.png?raw=true" /></a></p>

You may need to extend or widen the "Edit table definition" window to see the "Foreign Key" option.

<p align="center"><a href="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_9.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/sqlite-intro/blob/main/screenshots/Figure_9.png?raw=true" /></a></p>

Select the first foreign key field (`id_person`) and double click the blank space under "Foreign Key." You should see the option to specify a primary key reference table and field for the foreign key.

Go through the same process for the other foreign key field, `team_id`. Remember the bottom half of the "Edit table definition" window shows these steps in SQL syntax.
- Scroll down to the bottom of this embedded window if needed.

Huzzah! The ERD and relational schema we built in the first part of this lab exist in our newly-created database. Save all of these changes and close the program. We will use this newly-created database in an upcoming lab.

<blockquote>Q11: Describe your experience setting key fields and building table relationships to form a relational database in DB Browser, based on the provided instructions and available documentation. What challenges did you encounter, and how did you solve those problems?</blockquote>

## Additional SQL Resources

We'll spend more time with SQL in an upcoming lab, but if you want to explore:
- [Lab procedure](https://github.com/kwaldenphd/sql-queries-joins)
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "SQL"](https://librarycarpentry.org/lc-sql/)

# Additional Lab Notebook Questions

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=45b452c5-6e22-4fd7-9a81-ae2f0132f1b6">Lab Notebook Questions 12 & 13</a></td>
  </tr>
  </table>

There are two options for the additional lab notebook questions. Though you are welcome to do both, **<ins>you are only required to complete one</ins>.**

Free tools you can use to create ERDs and relational schema:
- Free generic drawing tools:
  - [Google Drawings](https://docs.google.com/drawings) *Google Drive tool*
  - [Microsoft Paint](https://www.microsoft.com/en-us/p/paint-3d/9nblggh5fv99) *Windows users*
  - [MacOS Paintbrush](https://paintbrush.sourceforge.io/) *Mac users*
- Free online database-specific tools:
  - [ERDPlus](https://erdplus.com/)
  - [LucidChart](https://www.lucidchart.com/pages/?anonId=0.1c8414ae17e41a83751)
  - [Visual Paradigm Online](https://online.visual-paradigm.com/diagrams/solutions/free-erd-tool/)

## Question 12

Take an existing dataset and reverse engineer a data model. Include narrative or text that documents your thought process as well as an ERD.

## Question 13

Describe a hypothetical situation in which you would be using/implementing a relational database. Build an ERD and RS for that implementation/use case. Include narrative or text that documents your thought process as well as ERD and RS diagrams.

# Lab Notebook Questions

[Link to lab notebook template (Google Doc)](https://docs.google.com/document/d/1hlcv_xovvtM9aSYEkyIlnmE71jnrqQ5b4WKazr4gYog/copy)
- Insert any needed ERDs or relational schema as images in the Google Doc.

Free tools you can use to create ERDs and relational schema:
- Free generic drawing tools:
  - [Google Drawings](https://docs.google.com/drawings) *Google Drive tool*
  - [Microsoft Paint](https://www.microsoft.com/en-us/p/paint-3d/9nblggh5fv99) *Windows users*
  - [MacOS Paintbrush](https://paintbrush.sourceforge.io/) *Mac users*
- Free online database-specific tools:
  - [ERDPlus](https://erdplus.com/)
    * *Prof. Walden's go-to tool that lets you convert an ERD into a relational schema.*
  - [LucidChart](https://www.lucidchart.com/pages/?anonId=0.1c8414ae17e41a83751)
  - [Visual Paradigm Online](https://online.visual-paradigm.com/diagrams/solutions/free-erd-tool/)

Q1: Spend some time exploring the tables. What kinds of information are included? How would you the fields in each table, using the language of string, double, and integer to describe the data types.

Q2: What entities are in the Player_Birthplaces, Team_Locations, and Transactions tables? List the entitites by table and include some explanation of your thought process. If you're getting stuck, try describing the data included in each table using a sentence. Where are the nouns in each sentence?

Q3: What attributes are in the Player_Birthplaces, Team_Locations, and Transactions tables? What entities do these attributes describe? List the attributes by entity and table and include some explanation of your thought process. If you're getting stuck, go back to your list of entities from Q2. What non-entity information in each table might describe an entity?

Q4: What relationships do you see within and across entities in the Player_Birthplaces, Team_Locations, and Transactions tables? What entities do these relationships connect? Include some explanation of your thought process. If you're getting stuck, go back to your list of entities from Q2. How do these entities connect?

Q5: Include the cardinality for the relationships you identified in Q4. Include some explanation of your thought process.

Q6: Build an ERD for the Player_Birthplaces, Team_Locations, and Transactions tables. Include your diagram as well as an explanation of your process
- *Folks are welcome/encouraged to collaborate on this question. If so, include the names of your collaborators as part of your answer to this question.*

Q7: What fields in our tables are functioning as keys? Which ones are primary keys and which ones are foreign keys? Include some explanation of your thought process.

Q8: Build a relational schema for a relational database that includes the Player_Birthplaces, Team_Locations, and Transactions tables. Include your diagram as well as an explanation of your process.
- *Folks are welcome/encouraged to collaborate on this question. If so, include the names of your collaborators as part of your answer to this question.*

Q9: Describe your experience installing DB Browser for SQLite based on the provided instructions and available documentation. What challenges did you encounter, and how did you solve those problems?

Q10: Describe your experience loading `.csv` files into DB Browser based on the provided instructions and available documentation. What challenges did you encounter, and how did you solve those problems?

Q11: Describe your experience setting key fields and building table relationships to form a relational database in DB Browser, based on the provided instructions and available documentation. What challenges did you encounter, and how did you solve those problems? 

**Q12 and Q13: Though you are welcome to do both, <ins>you are only required to complete one</ins>.**

Q12: Take an existing dataset and reverse engineer a data model. Include narrative or text that documents your thought process as well as an ERD.

Q13: Describe a hypothetical situation in which you would be using/implementing a relational database.
- Build an ERD and RS for that implementation/use case.
- Include narrative or text that documents your thought process as well as ERD and RS diagrams.
