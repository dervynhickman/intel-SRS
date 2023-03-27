Desription:

Web Databases are new in HTML5. Web Databases are hosted and persisted inside a user's browser. By allowing developers to create applications with rich query abilities it is envisioned that a new breed of web applications will emerge that have the ability to work online and off-line.

The example code in this article demonstrates how to create a very simple todo list manager. It is a very high level tour of some of the features available in HTML5.

Step 1. Opening the database #
The database needs to be opened before it can be accessed.
You need to define the name, version, description and the size of the database.Asynchronous and Transactional #
In the majority of cases where you are using Web Database support you will be using the Asynchronous API. The Asynchronous API is a non-blocking system and as such will not get data through return values, but rather will get data delivered to a defined callback function.

The Web Database support through HTML is transactional. It is no possible to execute SQL statements outside of a transaction. There are two types of transactions: read/write transactions (transaction()) and read only transactions (readTransaction()). Please note, read/write will lock the entire database.

Step 2. Creating a table #
You can only create a table by executing a CREATE TABLE SQL statemen inside a transaction.

We have defined a function that will create a table in the body onload event. If the table doesn't already exist, a table will be created.

The table is called todo and has 3 columns.

ID - a incrementing sequential ID column
todo - a text column that is the body of the item
added_on - the time that the todo item was created


Step 3. Adding data to a table #
We are building a todo list manager so it is pretty important that we are able to add todo items in to the database.

A transaction is created, inside the transaction an INSERT into the todo table is performed.

executeSql takes several parameters, the SQL to execute and the parameters values to bind the query.

Step 4. Selecting data from a table #
Now that the data is in the database, you need a function that gets the data back out. In Chrome, Webdatabase's use standard SQLite SELECT queries.

Note that all of these commands used in this sample are asynchronous and as such the data is not returned from the transaction or the executeSql call. The results are passed through to the success callback.

Step 4a. Rendering data from a table #
Once the data has been fetched from the table, the loadTodoItems method will be called.

The onSuccess callback takes two parameters. The first being the transaction of the query and the second being the result set. It is fairly simple to iterate across the data:The effect of this method call is that the todo list is rendered into a DOM Element called "todoItems".

Step 5. Deleting data from a table #Step 6. Hooking it all up #
When the page loads, open the database and create the table (if needed) and render any todo items that might already be in the database.A function that takes the data out of the DOM is needed so, call the html5rocks.webdb.addTodo method
