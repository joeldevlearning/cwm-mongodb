# 1 - MongoDB Basics 

Let's take some baby steps with Mongo. We can work with our database interactively; inserting data is more fluid than in a traditional (relational) database.

### 1.1 Getting Started


- start mongod from /bin
- start robo3t (or mongo shell, if you like CLI-only). And remember in robo3t to click VIEW->LOGS, so you can see your history

### 1.2 Exploring


- first let's see what databases we have in here: `show dbs`
- ok so let's make one: `use library` 
- and let's see how many collections it has: `show collections`
- so let's add a collection:  `db.library.books.insertOne( {title: "My Two Faces"} )`

  - We can name a **database** that doesn't exist yet - and then instantly insert in to it
  - likewise we can create a **collection** just by naming and inserting something into it

- So now there's something in our database, but what? Let's ask: `db.library.books.find()`

- Let's try that with pretty printing: `db.library.books.find().forEach(printjson)`

- Notice the _id field. Mongodb inserts that for us and we can use it to refer to our documents (should all else fail!)

- Let's add more: 

  ```json
  db.library.books.insertMany( 
  [ 	{title: "Black Beauty"},
  	{title: "War and Peace"},
  	{title: "Buy Low, Sell High"},
  	{title: "My Life For The Horde"}
  ])
  ```

  ​

- Wow, how much is in there now? `db.library.books.count()`



##### HEY! Tired of typing that *db.this.that.what* stuff?

Try this: Assign your collection to a variable: `var books = db.library.books`

Now you can type something like `books.count()` 



### 1.3 Multiple Documents

- Hmm... we forgot something... right! the author. Let's add that now... but how? How do we grab a specific document? For example, "My Two Faces"? We need a way to find that *and* update it: 

  ```json
  books.updateOne({title: "My Two Faces"},
  {$set:     {author: "Superman"} })
  ```

  ​

  - We first identify our book document by its **exact** title

  - Then we use our first operator (!) `$set`, which is simply a command that takes parameters. `$set` takes a common-separated list of fields and values

  - Let's add something else random, like a timestamp. Mongodb (using BSON as it storage format) supports many more data types than JSON - like timestamps! 

    ```json
    books.updateOne({title: "My Two Faces"},
    {$set:     {timestamp: ISODate()} })
    ```

    ​


- Now what if we don't know the exact title? Can we just put part of it in there? `books.findOne( {title: "My"} )`

- Ok, how about `books.findOne( {title: "My*"} )`

- Yeah, so you need to use a regular expression for this type of search: 

  ```json
  books.find( {title: { $regex: /M/ } } )
  ```
  - Here we pass the $regex operator a simple regular expression, matching any title field that has a capital "M"

- Oh, but we might get more than one result. Can we narrow it down? Anyone? We could use an AND-like condition: 

  ```json
  books.find( {title: { $regex: /M/ }, author: { $regex: /S/ } } )
  ```

  Or...

  ```
  books.find( {title: { $regex: /my/i }})
  ```

  ​

NOTE: More regex goodness @ https://docs.mongodb.com/manual/reference/operator/query/regex/

### 1.4 Documents in Documents

- We have the option of putting objects inside objects. Let's put this object inside our recently created book documents: 

  ```json
  var meta = { 	
  	type: "fake book",
  	message: "for code meetup, not intended for the real library!"
  }
  ```

  Let's store this in **every** document in our books collection:

  ```json
  books.updateMany(
  { },
  {$set: {"meta": meta}}
  )
  ```

  Let's see the results! `books.find().forEach(printjson)`

  Oh... not quite what we wanted. Let's **obliterate** that meta field: 

  ```json
  books.updateMany(
  { },
  {$unset: {"meta": ""}}
  )
  ```

  Check that it's done: `books.find().forEach(printjson)`

  And now try again on adding our meta object:

  ```json
  books.updateMany(
  { },
  {$set: {meta}}
  )
  ```

  Check again: `books.find().forEach(printjson)`



### 1.5 Destroy all that you've built...

- Let's get drop Superman's book like a hot piece of Kryptonite. First, check that we know how to find it: 

  ```json
  books.find( {author: {$regex: /Super/} } ).forEach(printjson)
  ```

    And now, we pull out the big guns:

  ```json
  books.deleteOne( {author: {$regex: /Super/} } )
  ```

  Check the crater for any signs of life: 

  ```json
  books.find( {author: {$regex: /Super/} } )

  Fetched 0 record(s) in 1ms
  ```

  Satisfying, no? Let's do it again. How many books are left?

  ```
  books.count()
  ```

  And what is common to all the books? Well, they all have titles. They also all have that meta object. Let's use that against them!

  ```json
  books.find( { "meta": { $exists: true} } )
  ```

  Now that they are found, we go for the kill:

  ```json
  books.deleteMany( "meta": { $exists: true} )
  ```

  Crap! I always forget that extra set of brackets... quick, before they can react!

  ```json
  books.deleteMany( {"meta": { $exists: true} } )
  ```

  NOTE: There's also `db.inventory.remove( { } )`, easier but not as cool.

- We continue on! There are no more books, but still a collection:

  ```
  books.drop
  ```

  Woah. We just got this function definition? What is that? It's a javascript REPL feature - drop the parentheses on a function () and you get the function as data, not the function executed as code. Anyway, resuming...

  ```
  books.drop()
  ```

  Check to make sure its gone:

  ```
  show collections
  ```

  And now the empty database - a mere shell - also must be destroyed:

  ```
  db.dropDatabase()
  show dbs
  ```

  Quoth the raven: "Nevermore!"

