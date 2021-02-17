# SQL
## 1️⃣ How to comment in SQL
`-- hi there this is a comment in sql`

## 2️⃣ Selection / Sort / Search
**Note**: The table will need to be wrapped around quotations. The `(\n)` means that there needs to be a line break 

- `select * from "Games"` - this statement will return the table
- `select count(*) from "Games"` - using the built in ‘count’, this statement will return how many rows the table has. The `count(*)` is known as an aggregate function. 
- `select id, title from "Games"` - the statements above are selecting all information but we are specifying the columns that we want from the table. We are looking for `id` and `title`
- `select id, title from "Games" (\n) limit 10` - this statement will only return 10 items from the table. 
- `select id, title from "Games" (\n) order by title (\n) limit 10` - this statement will return data that is alphabetized by title and a limit of 10. SQL is a bit tricky where you need to alphabetize first then limit the data. You cannot swap the order by and limit. 
- `select * from "Games" (\n) where genre = 'Action'` - this statement is searching where the string exactly matches in the table. 
- `select * from "Games" (\n) where ilike '%Action%'` - using this sort of search is where we are searching where the data ‘includes’ Action, and we are using `ilike` which is case insensitive whereas `like` is case sensitive, the `%` acts as wildcards. 
- `select * from "Games" (\n) where genre ilike '%action%' (\n) or genre ilike '%rpg%'` - this will filter data based on whether the genre includes either action or rpg, you can replace `or`with `and` to make a different statement 

### Filtering
The example being used is from our twinmo app. 
```
SELECT * FROM "Transactions"
WHERE 
	("senderID" = 205 
	AND type = "request"
	AND status = true)
OR 
	("recipientID" = 205 
	AND type = "request"
	AND status = false)
OR 
	("recipientID" = 205
	AND type = "payment"
ORDER BY "createdAt" desc
```

### Joining
```
SELECT * FROM 
"Transactions" t JOIN "Users" u ON 
t."senderID" = u.id
WHERE u.id = 205
```
This will join the “Transactions” and “Users” table, any resulting rows from the query, we will be able to see all the columns that are from both tables. The ON specifies 

```
SELECT * FROM 
"Transactions" t JOIN "Users" u ON 
(t."senderID" = u.id OR t."recipientID" = u.id)
WHERE u.id = 205
```

### Dates
```
SELECT * FROM "Data"
WHERE "timeStamp" > "2021-02-14 10:37:00+00"
ORDER BY "timeStamp" desc
```
This will select all data from Data where the timeStamp is greater than the specific time that is listed and we are going to order it timeStamp in descending order.

## 3️⃣ Alter / Update
- `ALTER TABLE users ADD score smallint`
`ALTER TABLE` command from SQL `users` the name of the table, note that is case insensitive and if your table name contains uppercase letters you will need to wrap it with quotations `ADD` command from SQL `score` the name of the new column you wish to create `smallint` the datatype of the new column, there are a lot of datatypes. 

- `UPDATE users SET score = 50 WHERE name = 'Tony'` - this reads as “update the users table where the name is ‘Tony’ and update score to 50”

## 👎🏼 Cons of SQL
You cannot use variables in SQL. For example, if you want to grab the user id from the sessions you can easily pass that data in Sequelize and you cannot do that in SQL. Sequelize is like a translation error between SQL and JS. 