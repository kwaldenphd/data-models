# Lab #5A: Introduction to Relational Database Systems and Data Models

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

## Acknowledgements

The author consulted the following resources when building this tutorial:
- [W3 Schools "Syntax"](https://www.w3schools.com/sql/default.asp)
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Tidy Data for Librarians"](https://librarycarpentry.org/lc-spreadsheets/)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "Open Refine"](https://librarycarpentry.org/lc-open-refine/)
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

# Understanding Relational Databases

## Why A Database

The data we've been using in this tutorial includes a table with information about baseball player birthplaces and birth dates. It also includes a second table with information about where baseball teams are located.

72- Open the `CSC_Datbase_Lab_Transactions.csv` file in a spreadsheet program.

<blockquote>Q12: What types of fields do you see in the Transactions table? What kinds of connections could you see across these three tables?</blockquote>

73- Let's say we wanted to see how many baseball players born in Puerto Rico played for teams located in the state of Iowa.

74- The `Player_Birthplaces` table includes information about where players were born. The `Team_Locations` table includes information about where teams are located. The `Transactions` table tells us which players played for which teams.

75- But the `Transactions` table on its own doesn't include the information about player birthplace and team location we need to answer the question of how many baseball players born in Puerto Rico played for teams located in the state of Iowa.

76- We could add that location information to the `Transactions` table, but we would end up with significant redundant and duplicate information.

77- Behold the magic of relational databases.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_29.png?raw=true" alt="Capture_2"  /></p>

Image from Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html).

As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "Relational databases consist of one or more tables of data. These tables have fields (columns) and records (rows). Every field has a data type. Every value in the same field of each record has the same type. These tables can be linked to each other when a field in one table can be matched to a field in another table."

78- Linking our three individual data tables in a relational database will enable us to answer the question about Puerto Rican players in Iowa without having to change the underlying data structure.

## What is an ERD?

79- An entity relationship diagram (sometimes called an ER Diagram or ERD) is a visual representation of tabular data structures that are linked as part of a database.

80- Building an ERD requires understanding the underlying structure of your data, as well as how you want to create links across individual tables.

81- ERDs have a specific vocabulary for describing database structure.

82- In 1997, computer scientist Peter Chen outlined a natural language framework for building ER diagrams.
<table>
 <tr>
  <th>English grammar structure</th>
  <th>ER structure</th>
 </tr>
 <tr>
  <td>Common noun</td>
  <td>Entity type</td>
 </tr>
 <tr>
  <td>Proper noun</td>
  <td>Entity</td>
 </tr>
 <tr>
  <td>Transitive verb</td>
  <td>Relationship type</td>
 </tr>
 <tr>
  <td>Intransitive verb</td>
  <td>Attribute type</td>
 </tr>
 <tr>
  <td>Adjective</td>
  <td>Attribute for entity</td>
 </tr>
 <tr>
  <td>Adverb</td>
  <td>Attribute for relationship</td>
 </tr>
</table>

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
  * For example each Grinnell student has a unique ID number.
- One-to-many relationships
  * A single Grinnell student registers for multiple courses.
- Many-to-many relationships
  * Multiple Grinnell students work with multiple faculty members, and multiple faculty members work with multiple students.

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

# SQL Query Syntax

As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "Structured Query Language, or SQL (sometimes pronounced 'sequel'), is a powerful language used to interrogate and manipulate relational databases. It is not a general programming language that you can use to write an entire program."

When working in a relational database, we an use SQL to write queries.

As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "a query is a question or request for data. For example, “How many journals does our library subscribe to?” When we query a database, we can ask the same question using a common language called Structured Query Language or SQL in what is called a statement. Some of the most useful queries - the ones we are introducing in this first section - are used to return results from a table that match specific criteria."

This section of the lab will introduce some basic elements of SQL syntax. 

## Selecting and Sorting
```SQL
SELECT [field]
FROM [table];
```

97- The `SELECT` query selects a specific field (column) from a specific table.

98- The semicolon `;` is required at the end of every SQL query.

99- Adding multiple columns after `SELECT` will return data from multiple columns.

```SQL
SELECT [field_1], [field_2], [field_3]
FROM [table];
```

<blockquote>Q20: How would you write an SQL query to select the list of player ids and birthplace countries from the Player_Birthplaces table? What data does this query return?</blockquote>

100- We might want to write a query to return all the unique values in a particular field.

101- For example, selecting the entire `country` field in the `Player_Birthplaces` table would return many duplicate values.

```SQL
SELECT DISTINCT [field]
FROM [table];
```

102- `SELECT DISTINCT` returns a list of unique values.

<blockquote>Q21: How would you write an SQL query to return the unique list of player birthplace countries from the Player_Birthplaces table? What data does this query return?</blockquote>

103- We might also want to sort the results returned by a query.

```SQL
SELECT *
FROM [table]
ORDER BY [field] ASC;
```

104- The `*` wildcard operator selects all the fields in a specific table.

105- `ORDER BY` specifies a field to use in sorting the query results.

106- `ASC` returns ascending results. `DESC` would return descending results.

<blockquote>Q22: How would you write an SQL query to return the unique list of team names from the Team_Locations table, sorted in reverse alphabetical order? What data does this query return?</blockquote>

```SQL
SELECT *
FROM [table]
ORDER BY [field_1] ASC, [field_2] DESC;
```

107- We can also sort on multiple fields.

108- In the query above, the `ORDER BY` statement sorts `[field_1]` first (ascending) and then sorts `[field_2]` (descending).

<blockquote>Q23: How would you write an SQL query to return the data from the Player_Birthplaces table, sorted in chronological order by birth year and reverse alphabetical order by country? What data does this query return?</blockquote>

## Filtering

109- Sometimes we may only want to return values that fall within a specific range or based on a particular set of conditions.

```SQL
SELECT *
FROM [Player_Birthplaces]
WHERE country='DO';
```

110- This query returns all columns from the `Player_Birthplaces` table where data in the `country` field is equal to `DO`.

111- The data returned by this query includes all the records for players born in the Dominican Republic.

112- We can also use operators to specify a range for the `WHERE` clause.

```SQL
SELECT *
FROM [Player_Birthplaces]
WHERE dob>1996;
```

113- This query returns all columns from `Player_Birthplaces` where data in the `dob` field is greater than `1996`.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_42.png?raw=true" alt="Capture_2"  /></p>

List of operators that can be used in a `WHERE` clause (from W3Schools [SQL Where Clause page](https://www.w3schools.com/sql/sql_where.asp)).

114- SQL query syntax requires single quotes around text values. Numeric fields do not need single quotes.

<blockquote>Q24: How would you write an SQL query to return the data from the Team_Locations table for teams located in states that start with the letter M? What data does this query return?</blockquote>

Learn more about operators at Beginner SQL's [Tutorial on SQL Comparison Keywords](https://beginner-sql-tutorial.com/sql-like-in-operators.htm).

## Aggregating and Calculating

We won't cover these functions in this lab, but SQL syntax includes functions that can group query results by particular fields and perform basic arithmetic functions on values in a database.

To learn more, visit Library Carpentry's [Aggregating & calculating values page](https://librarycarpentry.org/lc-sql/04-aggregating-calculating/index.html) and W3Schools' [SQL Tutorial](https://www.w3schools.com/sql/default.asp) pages for specific aggregating and calculating functions.

## Joins

115- The process of building a relational database in which you identify primary and foreign keys and build relationships across  tables does not change the underlying data structure.

116- We can accomplish this in SQL using `JOIN` functions.

117- According to W3Schools'[SQL Joins page](https://www.w3schools.com/sql/sql_join.asp), "A JOIN clause is used to combine rows from two or more tables, based on a related column between them."

```SQL
SELECT *
FROM [transactions]
JOIN [player_birthplaces]
ON transactions.player_ids = player_birthplaces.player_ids;
```

118- This query uses the `player_id` field to join the `Transactions` and `Player_Birthplaces` tables.

119- The query returns all columns in the joined query.

<blockquote>Q25: How would you write an SQL query that joins the Transactions and Team_Locations tables and returns all columns?  What data does this query return?</blockquote>

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_43.gif?raw=true" alt="Capture_2"  /></p>

120- There are four main types of `JOIN` functions.
- `(INNER) JOIN` returns matching records in both tables
- `LEFT (OUTER) JOIN` returns all records from the left table and only matching records from the right table
- `RIGHT (OUTER) JOIN` returns all records from the right table and only matching records from the left table
- `FULL (OUTER) JOIN` returns all matching records from both the left and right tables

Learn more about `JOIN` functions at W3Schools' [SQL Joins page](https://www.w3schools.com/sql/sql_join.asp).

<blockquote>Q26: Where would you start in writing an SQL query that answers our question about the number of players born in Puerto Rico playing for teams located in Iowa?</blockquote>

<blockquote>Q27: How would you describe the affordances of relational databases to someone who hasn't been through this lab?</blockquote>

<blockquote>Q28: What questions or thoughts do you have about building and interacting with relational databases?</blockquote>

# Optional: Relational Databases in Excel Using PivotTables

121- We can also work within Microsoft Excel to connect our three tables so we can utilize some of the features and functionality of a relational database from within Excel.

122- Open the Excel workbook you created earlier in this lab.

123- Load the `Transactions` file in a new sheet. 

124- Now you should have three sheets in the same Excel workbook.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_33.png?raw=true" alt="Capture_2"  /></p>

125- Under the `Data` menu area, select the `Relationships` option.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_34.png?raw=true" alt="Capture_2"  /></p>

126- In the `Manage Relationships` window, select `New`.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_35.png?raw=true" alt="Capture_2"  /></p>

127- Use the relational schema you built in Q19 to create relationships across the three tables.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_36.png?raw=true" alt="Capture_2"  /></p>

128- Once you've added relationships, close the `Manage Relationships` window.

129- Save your workbook.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_37.png?raw=true" alt="Capture_2"  /></p>

130- Select the `Manage Data Model` option under `Data`.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_38.png?raw=true" alt="Capture_2"  /></p>

131- You can select the `Diagram View` option to see the relational schema you have built in Excel.

132- Close the Power Pivot window.

133- Create a new blank sheet.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_39.png?raw=true" alt="Capture_2"  /></p>

134- Select `PivotTable` under `Insert`.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_40.png?raw=true" alt="Capture_2"  /></p>

135- In the `Create PivotTable` window, select the option to `Use this workbook's Data Model` and select the `Existing Worksheet` for the PivotTable location.

136- Click `OK`.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_41.png?raw=true" alt="Capture_2"  /></p>

137- You are now in the PivotTable interface where you can select data fields across tables using the relationships and data model.

<blockquote>From within the PivotTable, how could you select data fields to answer our question about the number of baseball players born in Puerto Rico who played for teams in Iowa? Describe your process and include a screenshot of the resulting PivotTable.</blockquote>

# Additional Resources

- [W3 Schools "Syntax"](https://www.w3schools.com/sql/default.asp)
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Tidy Data for Librarians"](https://librarycarpentry.org/lc-spreadsheets/)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "Open Refine"](https://librarycarpentry.org/lc-open-refine/)
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

Q20: How would you write an SQL query to select the list of player ids and birthplace countries from the Player_Birthplaces table? What data does this query return?

Q21: How would you write an SQL query to return the unique list of player birthplace countries from the Player_Birthplaces table? What data does this query return?
 
Q22: How would you write an SQL query to return the unique list of team names from the Team_Locations table, sorted in reverse alphabetical order? What data does this query return?
  
Q23: How would you write an SQL query to return the data from the Player_Birthplaces table, sorted in chronological order by birth year and reverse alphabetical order by country? What data does this query return?
   
Q24: How would you write an SQL query to return the data from the Team_Locations table for teams located in states that start with the letter M? What data does this query return?
   
Q25: How would you write an SQL query that joins the Transactions and Team_Locations tables and returns all columns? What data does this query return?
    
Q26: Where would you start in writing an SQL query that answers our question about the number of players born in Puerto Rico playing for teams located in Iowa?

Q27: How would you describe the affordances of relational databases to someone who hasn't been through this lab?

Q28: What questions or thoughts do you have about building and interacting with relational databases?

