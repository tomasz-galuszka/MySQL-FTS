
##### Create new database
`CREATE DATABASE android;`

##### use database
`USE android;`

##### crate new table
`CREATE TABLE post_history(
Id int not null PRIMARY KEY,
PostHistoryTypeId int,
PostId int,
RevisionGUID VARCHAR(100),
CreationDate VARCHAR(50),
UserId int,
Text text
);`

##### load data
`LOAD XML LOCAL INFILE '/home/tomasz/Downloads/PostHistory.xml' INTO TABLE post_history;`

##### add fts index
`ALTER TABLE post_history ADD FULLTEXT(body);`

##### select using LIK
`SELECT PostId, CreationDate, SUBSTR(text, 1, 100) FROM post_history WHERE text LIKE '%xperia%' OR text LIKE '%vodafone%' ORDER BY PostId LIMIT 10;`

##### select using FTS
`SELECT PostId, CreationDate, SUBSTR(text, 1, 100) FROM post_history WHERE MATCH(text) AGAINST('"vodafone"' '"xperia"' in BOOLEAN MODE) ORDER BY PostId LIMIT 10;`
`
