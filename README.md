# Welcome to Learning with Astra #

If you have attended recently our workshops here, we ask you to create your own Github repo showing off your learning journey with Astra. You could use this repo here as a start: fork it and update it with your own examples.

## Explain your use case ##

Pick an example application that you could see on Astra and describe the entities and queries for it. 

Include diagrams, screenshots etc to make it more interesting and better convey your ideas.

A result application for running races



## Create your own tables on Astra ##

Example tables that we used in the workshop:

```
CREATE TABLE IF NOT EXISTS comments_by_user (
    userid uuid,
    commentid timeuuid,
    videoid uuid,
    comment text,
    PRIMARY KEY ((userid), commentid)
) WITH CLUSTERING ORDER BY (commentid DESC);

CREATE TABLE IF NOT EXISTS comments_by_video (
    videoid   uuid,
    commentid timeuuid,
    userid    uuid,
    comment   text,
    PRIMARY KEY ((videoid), commentid)
) WITH CLUSTERING ORDER BY (commentid DESC);
```

Show us your own tables - for the data model of your choice.

CREATE TABLE IF NOT EXISTS running_race_by_runner (
    runnerid uuid,
    running_race_id uuid,
    running_race_name text,
    running_race_date date,
    running_race_distance int,
    placement int,
    hours tinyint,
    minutes tinyint,
    seconds tinyint,
    PRIMARY KEY ((runnerid), running_race_id)
);

CREATE TABLE IF NOT EXISTS comments_by_running_race (
    running_race_id uuid,
    commentid timeuuid,
    userid uuid,
    comment text,
    PRIMARY KEY ((running_race_id), commentid)
) WITH CLUSTERING ORDER BY (commentid DESC);
    

## Insert some data ##

Here some example data that we used in the workshop:

```
INSERT INTO comments_by_user (userid, commentid, videoid, comment)
VALUES (11111111-1111-1111-1111-111111111111, NOW(), 12345678-1234-1111-1111-111111111111, 'I keep watching this video');

INSERT INTO comments_by_user (userid, commentid, videoid, comment)
VALUES (11111111-1111-1111-1111-111111111111, NOW(), 12345678-1234-1111-1111-111111111111, 'Soo many comments for the same video');
```

Show off your own data inserts, into your own tables:

INSERT INTO running_race_by_runner (runnerid, running_race_id, running_race_name, running_race_date,
    running_race_distance, placement, hours, minutes, seconds)
VALUES (11111111-1111-1111-1111-111111111111, 12345678-1234-1111-1111-111111111111, 'Stockholm Marathon', '2018-06-01',
    42195, 500, 3, 15, 11);
    
INSERT INTO running_race_by_runner (runnerid, running_race_id, running_race_name, running_race_date,
    running_race_distance, placement, hours, minutes, seconds)
VALUES (11111111-1111-1111-1111-111111111111, 12345678-1234-1234-1111-111111111111, 'Prague Halfmarathon', '2018-04-08',
    21097, 200, 1, 28, 30);
    
INSERT INTO comments_by_running_race (running_race_id, commentid, userid, comment)
VALUES (12345678-1234-1111-1111-111111111111, 11111111-1111-1111-1111-111111111111, 11111111-1111-1111-1111-111111111111, 'A bit warm and humid');

INSERT INTO comments_by_running_race (running_race_id, commentid, userid, comment)
VALUES (12345678-1234-1234-1111-111111111111, NOW(), 11111111-1111-1111-1111-111111111111, 'Cold at the start, but sunny');

Now show the output, for example:

SELECT *
FROM running_race_by_runner;

SELECT *
FROM comments_by_running_race;

Include some screenshots!
![Test Image 1](https://github.com/PeterJohansson309/learning-with-Astra/blob/master/SELECTSATSCASSANDRA.JPG)

## Experiment with CRUD and show the outputs: ##

Examples from the workshop:

```
UPDATE comments_by_video 
SET comment = 'This is fun!' 
WHERE videoid = 12345678-1234-1111-1111-111111111111 AND commentid = 494a3f00-e966-11ea-84bf-83e48ffdc8ac;

SELECT * FROM comments_by_video;
```

```
DELETE FROM comments_by_video 
WHERE videoid = 12345678-1234-1111-1111-111111111111 AND commentid = 494a3f00-e966-11ea-84bf-83e48ffdc8ac;

SELECT * FROM comments_by_video;
```

Show us something similar with your own tables.

UPDATE running_race_by_runner
SET hours = 1
WHERE runnerid = 11111111-1111-1111-1111-111111111111 AND running_race_id = 12345678-1234-1111-1111-111111111111;

UPDATE comments_by_running_race
SET comment = 'Yes world record!!!'
WHERE running_race_id = 11111111-1111-1111-1111-111111111111 AND commentid = 11111111-1111-1111-1111-111111111111;

SELECT * FROM running_race_by_runner;
SELECT * FROM comments_by_running_race;

![Test Image 2](https://github.com/PeterJohansson309/learning-with-Astra/blob/master/SELECTSATSCASSANDRA2.JPG)

Try something different:

Check out the CQL reference and try commands that we did not use in the workshop:

https://docs.datastax.com/en/cql-oss/3.3/cql/cql_reference/cqlReferenceTOC.html

Let us know what you find:
LIGTHWEIGHT TRANSACTIONS

INSERT INTO running_race_by_runner (runnerid, running_race_id, running_race_name, running_race_date,
    running_race_distance, placement, hours, minutes, seconds)
VALUES (11111111-1111-1111-1111-111111111111, 12345678-1234-1234-1234-111111111111, 'Kistaloppet', '2018-09-15',
    10000, 50, 0, 39, 40) IF NOT EXISTS;
    
UPDATE running_race_by_runner
SET placement = 62
WHERE runnerid = 11111111-1111-1111-1111-111111111111 and running_race_id = 12345678-1234-1234-1234-111111111111
IF placement = 50;

SELECT * FROM running_race_by_runner;

![Test Image 3](https://github.com/PeterJohansson309/learning-with-Astra/blob/master/SELECTSATSCASSANDRA3.JPG)

Or connect, read and write to your Astra database via other methods.

Tell us how you do it, we would love to know. 

Just used CQL Console

The starry sky is the limit: Build your own app with Astra and show it off for a chance to have it included with our Sample Galleries



