# Querying Data

We're diving into a real dataset! Let's go! We'll grab some real data and then get to work on querying it.

Our chosen dataset comes from New York City: Baby names!

#### 1) Learn about and explore the dataset here: 

https://data.cityofnewyork.us/Health/Most-Popular-Baby-Names-by-Sex-and-Mother-s-Ethnic/25th-nujf

There are about 22,000 records here, so not big, but interesting enough. Notice the columns and what values they hold.

#### 2) Download the CSV version of the data:

It's easiest to import the CSV version into mongodb.

We can do this using mongoimport, with the following parameters:

`mongoimport --db baby --collection names --type csv --file babies.csv --headerline`

#### 3) Brainstorm

Have any ideas for querying this data? Think a minute.

#### 4) Query Ideas

Consider the following suggestions:

- (a-1) Find your name!

- (a-2) Find a name close to yours, e.g. ALICE wants to find names that have "AL" in them

- (a-3) Find how many people share your name AND your ethnicity AND your gender

  ​

- (b-1) Sort the names by rank for one ethnic group or one year or one gender

- (b-2) Find the top name for all groups or all years or all genders

- (b-3) Find the least popular name for a year or ethnic group (or both!)

  ​

- (c) Count how many unique names there are

- (d) Count the same name across ethnicities (e.g. how many IRIS babies)?

- (e) Find the ethnic group with the fewest reported births



### Need help?

Try the docs: https://docs.mongodb.com/manual/tutorial/query-documents/