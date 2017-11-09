## Prep For MongoDB/NoSQL meetup

**November 9th, Tysons-Pimmet Library off Route 7 @ 6:30pm**

Meetup Link: https://www.meetup.com/Code-With-Me/events/244366281/



### Introduction

Hi everyone, welcome to our meetup event for mongodb! We invite you to bring your own machine to the meetup. 

To make your night fun and productive, I recommend you complete the following steps on your machine *before* the meetup night. Don't worry - it's easy and a great way to get into the topic! 



### 1) Install mongodb 

Please refer to the mongodb documentation for installation steps:

https://docs.mongodb.com/manual/administration/install-community/

We will use the "community edition" version 3.4 (32 vs. 64bit and SSL vs no-SSL do not concern us). I will demo things on Windows 8.1 with the "cmdr" command line console (http://cmder.net/), but feel free to use your OS and shell of choice!



### 2) Successfully startup mongod (server)

The mongodb installation instructions for your OS also tell you how to start mongod:

https://docs.mongodb.com/manual/administration/install-community/

Start mongod (the server daemon) once, from the command line, just to make sure it works. (Notice that you need a data directory, else mongod complains).



### 3) Start mongo (javascript shell) and run some test commands

The mongo shell is introduced in the official documentation:

https://docs.mongodb.com/manual/mongo/

Start the shell (called "mongo") from the command line and run some commands:

`use myFirstDB`

`db.myCollection.insertOne( { whoIsAwesome: "Me"} )`

`db.myCollection.find()`

Feel free to experiment and play with more commands.  



## Extras:

- Want a nice GUI program to view and mess with mongoDB? Try Robo 3T (formerly robomongo) https://robomongo.org/
- Want some sample data to play with? Try importing the restaurants collection, as described in the official docs: https://docs.mongodb.com/getting-started/shell/import-data/



### Help! I'm stuck!

No worries. Message Joel on meetup.com: https://www.meetup.com/Code-With-Me/members/230760511/
