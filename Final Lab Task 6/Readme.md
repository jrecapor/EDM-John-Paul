# MongoDB Practice
Part 1. MongoDB Exercise in mongo shell
- create database
Connect to a running mongo instance, use a database named `mongo_practice`.
use mongo_practice
## Insert Documents
Insert the following documents into a `movies` collection.
```
title : Fight Club
writer : Chuck Palahniuk
year : 1999
actors : [
Brad Pitt
Edward Norton
]
```
```
- db.movies.insert({title:&quot;Fight Club&quot;, writer: &quot;Chuck Palahniuk&quot;, year: &quot;1999&quot;, actors:[&quot;Brad Pitt&quot;,
&quot;Edward Norton&quot;]})
```
```
title : Pulp Fiction
writer : Quentin Tarantino
year : 1994
actors : [
John Travolta
Uma Thurman
]
```
```
- db.movies.insert({title:&quot;Pulp Fiction&quot;, writer:&quot;Quentin Tarantino&quot;, year:&quot;2009&quot;, actors:[&quot;John
Travolta&quot;, &quot;Uma Thurman&quot;]})
```
```
title : Inglorious Basterds
writer : Quentin Tarantino
year : 2009
actors : [
Brad Pitt
Diane Kruger
Eli Roth
]
```
```
- db.movies.insert({title:&quot;Inglorious Basterds&quot;, writer:&quot;Quentin Tarantino&quot;, year:&quot;2009&quot;,
actors:[&quot;Brad Pitt&quot;, &quot;Diane Kruger&quot;, &quot;Eli Roth&quot;]})
```
```
title : The Hobbit: An Unexpected Journey
writer : J.R.R. Tolkein
year : 2012
franchise : The Hobbit
```
```
- db.movies.insert({title:&quot;The Hobbit: An unexpected Journey&quot;, writer:&quot;J.R.R. Tolkein&quot;,
year:&quot;2012&quot;,franchise:&quot;The Hobbit&quot;})
```
```
title : The Hobbit: The Desolation of Smaug
writer : J.R.R. Tolkein
year : 2013
franchise : The Hobbit
```
```
- db.movies.insert({title:&quot;The Hobbit: The Desolation of Smaug&quot;, writer:&quot;J.R.R Tolkien&quot;,
year:&quot;2013&quot;, franchise:&quot;The Hobbit&quot;})
```
```
title : The Hobbit: The Battle of the Five Armies
writer : J.R.R. Tolkein
year : 2012
franchise : The Hobbit
synopsis : Bilbo and Company are forced to engage in a war against an array of combatants
and keep the Lonely Mountain from falling into the hands of a rising darkness.
```
```
- db.movies.insert({title:&quot;The Hobbit: The Battle of the Five Armies&quot;, writer:&quot;J.R.R Tolkien&quot;,
year:&quot;2002&quot;, franchise:&quot;The Hobbit&quot;, synopsis:&quot;Bilbo and Company are forced to engage in a
war against an array of combatants and keep the Lonely Mountain from falling into the hands of
a rising darkness.&quot;})
```
```
title : Pee Wee Herman&#39;s Big Adventure
```
```
- db.movies.insert({title:&quot;Pee Wee Herman&#39;s Big Adventures&quot;})
```
```
title : Avatar
```
-  db.movies.insert({title:&quot;Avatar&quot;})

## Query / Find Documents
query the `movies` collection to
- get all documents
```
db.movies.find()
```
- get all documents with `writer` set to &quot;Quentin Tarantino&quot;
```
db.movies.find({writer:&quot;Quentin Tarantino&quot;})
```
- get all documents where `actors` include &quot;Brad Pitt&quot;
```
db.movies.find({actors:&quot;Brad Pitt&quot;})
```
- get all documents with `franchise` set to &quot;The Hobbit&quot;
```
db.movies.find({franchise:&quot;The Hobbit&quot;})
```
- get all movies released in the 90s
```
db.movies.find({year:{$gt:&quot;1990&quot;, $lt:&quot;2000&quot;}})
```
- get all movies released before the year 2000 or after 2010
```
db.movies.find({$or:[{year:{$gt:&quot;2010&quot;}},{year: {$lt:&quot;2000&quot;}}]})
```
## Update Documents
- add a synopsis to &quot;The Hobbit: An Unexpected Journey&quot; : &quot;A reluctant hobbit, Bilbo Baggins,
sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home
and the gold within it - from the dragon Smaug.&quot;
```
db.movies.update({_id:ObjectId(&quot;5c9f98e5e5c2dfe9b3729bfe&quot;)}, {$set:{synopsis:&quot;A reluctant
hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to
reclaim their mountain home - and the gold within it - from the dragon Smaug.&quot;}})
```
- add a synopsis to &quot;The Hobbit: The Desolation of Smaug&quot; : &quot;The dwarves, along with Bilbo
Baggins and Gandalf the Grey, continue their quest to reclaim Erebor, their homeland, from
Smaug. Bilbo Baggins is in possession of a mysterious and magical ring.&quot;
```
db.movies.update({_id:ObjectId(&quot;5c9fa42ae5c2dfe9b3729c03&quot;)}, {$set:{synopsis:&quot;The dwarves,
along with Bilbo Baggins and Gandalf the Grey, continue their quest to reclaim Erebor, their
homeland, from Smaug. Bilbo Baggins is in possession of a mysterious and magical ring.&quot;}})
```
- add an actor named &quot;Samuel L. Jackson&quot; to the movie &quot;Pulp Fiction&quot;
```

db.movies.update({_id:ObjectId(&quot;5c9f983ce5c2dfe9b3729bfc&quot;)}, {$push:{actors:&quot;Samuel L.
Jackson&quot;}})
```
## Text Search
- find all movies that have a synopsis that contains the word &quot;Bilbo&quot;
```
db.movies.find({synopsis:{$regex:&quot;Bilbo&quot;}})
```
- find all movies that have a synopsis that contains the word &quot;Gandalf&quot;
```
db.movies.find({synopsis:{$regex:&quot;Gandalf&quot;}})
```
- find all movies that have a synopsis that contains the word &quot;Bilbo&quot; and not the word &quot;Gandalf&quot;
```
db.movies.find({$and:[{synopsis:{$regex:&quot;Bilbo&quot;}}, {synopsis:{$not:/Gandalf/}}]})
```
- find all movies that have a synopsis that contains the word &quot;dwarves&quot; or &quot;hobbit&quot;
```
db.movies.find({$or:[{synopsis:{$regex:&quot;dwarves&quot;}}, {synopsis:{$regex:&quot;hobbit&quot;}}]})
```
- find all movies that have a synopsis that contains the word &quot;gold&quot; and &quot;dragon&quot;
```
db.movies.find({$and:[{synopsis:{$regex:&quot;gold&quot;}}, {synopsis:{$regex:&quot;dragon&quot;}}]})
```
## Delete Documents
- delete the movie &quot;Pee Wee Herman&#39;s Big Adventure&quot;
```
db.movies.remove({_id:ObjectId(&quot;5c9f992ae5c2dfe9b3729c00&quot;)})
```
- delete the movie &quot;Avatar&quot;
```
db.movies.remove({_id:ObjectId(&quot;5c9f9936e5c2dfe9b3729c01&quot;)})
```
# Here The Output of my Work
- Part 1. MongoDB Exercise in mongo shell
![usemongo](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/Usemongo.png)
- Insert the following documents into a `movies` collection.
![createmovies](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/movies.png)
- title : Fight Club

![insertmovie](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/chuck.png)
- title : Pulp Fiction

![insertmovie](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/tarantino.png)
- title : Inglorious Basterds

![insertmovie](Images/basterds.png)
- title : The Hobbit: An Unexpected Journey

![insertmovie](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/unjourney.png)
- title : The Hobbit: The Desolation of Smaug

![insertmovie](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/smaug.png)
- title : The Hobbit: The Battle of the Five Armies

![insert movie](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/thebattle.png)
- title : Pee Wee Herman&#39;s Big Adventure

![insertmovie](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/bigadventure.png)
- title : Avatar

![insertmovie](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/avatar.png)
## Query / Find Documents
- get all documents

![finddocuments](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/alldoc.png)
- get all documents with `writer` set to &quot;Quentin Tarantino&quot;

![finddocuments](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/writtertarantino.png)
 - get all documents where `actors` include &quot;Brad Pitt&quot;

![finddocuments](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/bradpitt.png)
 - get all documents with `franchise` set to &quot;The Hobbit&quot;

![finddocuments](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/thehobbit.png)
 - get all movies released in the 90s

![finddocuments](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/90's.png)
 - get all movies released before the year 2000 or after 2010

![finddocuments](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/2000.png)
## Update Documents
- add a synopsis to &quot;The Hobbit: An Unexpected Journey&quot; : &quot;A reluctant hobbit, Bilbo Baggins,
sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home
and the gold within it - from the dragon Smaug.&quot;

![updatedocuments](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/updateunexjourney.png)
- add a synopsis to &quot;The Hobbit: The Desolation of Smaug&quot; : &quot;The dwarves, along with Bilbo
Baggins and Gandalf the Grey, continue their quest to reclaim Erebor, their homeland, from
Smaug. Bilbo Baggins is in possession of a mysterious and magical ring.&quot;

![updatedocuments](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/updatesmaug.png)
- add an actor named &quot;Samuel L. Jackson&quot; to the movie &quot;Pulp Fiction&quot;

![updatedocuments](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/updatepulp.png)
## Text Search
- find all movies that have a synopsis that contains the word &quot;Bilbo&quot;

![search](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/findbilbo.png)
- find all movies that have a synopsis that contains the word &quot;Gandalf&quot;

![search](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/findgandalf.png)
- find all movies that have a synopsis that contains the word &quot;Bilbo&quot; and not the word &quot;Gandalf&quot;

![search](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/findbilbonotgandalf.png)
- find all movies that have a synopsis that contains the word &quot;dwarves&quot; or &quot;hobbit&quot;

![search](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/dwarves.png)
- find all movies that have a synopsis that contains the word &quot;gold&quot; and &quot;dragon&quot;

![search](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/dragon.png)
  ## Delete Documents
- delete the movie &quot;Pee Wee Herman&#39;s Big Adventure&quot;

![delete](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/deletebigadventure.png)
- delete the movie &quot;Avatar&quot;

![delete](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Lab%20Task%206/Images/deleteavatar.png)
