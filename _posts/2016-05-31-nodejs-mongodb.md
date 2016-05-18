---
layout: post
title: "NodeJS & Databases: MongoDB"
comments: true
publish: false
---

Databases are an essential component of back-end architecture. NodeJS, which enables us to run JavaScript code on the server side, can connect to several of the major database server engines, including the relatively recent, but increasingly popular, MongoDB.

## Background

MySQL has been around since 1994 when it was first created by Michael Widenius and David Axmark. MySQL AB was sold to Sun Microsystems in 2008. Oracle then acquired Sun in 2010.

While Oracle so far still maintains a freely available version of MySQL, some newly developed features are only offered in the paid-for version. Just before Oracle took over, the original MySQL developers forked a copy of the MySQL code and set up MariaDB, a fully compatible database server which they say is guaranteed to stay free and open source, and which they continue to develop and enhance.


## Some RDBMS Terms

In relational database terminology, tables are sometimes referred to as relations, columns (or fields) as attributes and rows (or records) as tuples.

Each table typically maps to one discrete entity within the system, while each table row is identified uniquely by some sort of id field. Tables can be related via foreign keys, hence relational.

Relational database design is a specialisation within IT and often involves an analytical process referred to as normalisation.


## Installation & Set-up

For local installation, the MySQL database server can be downloded from the site linked below. Alternatively, on Windows one can install WampServer which comes bundled with MySQL. Similar bundled downloads exist in the Apple world, including MAMP and XAMPP.

For Cloud9 users, MySQL comes with the workspace, so there's nothing to download.

## MongoDB Shell Command Line

Cloud9 users can get at a MySQL command line prompt by opening a terminal window and typing in `mysql-ctl cli`.

If you have installed MySQL locally, from a command window at the installed mysql/bin folder, type in `mysqld` to start the database server. Do not close this window. Open another command window and, at the installed mysql/bin folder, type in `mysql` to get a MySQL prompt. Note that this may vary based on your local installation.



## Some example commands:

### To show/create/use databases:

`show databases;`

Cloud9:  `use c9;`

Local: `create database test;` then `use test;`

### To create a collection:
{% highlight sql %}
create table `category` (
`id` int auto_increment,
`name` char(10),
`description` varchar(45),
primary key (`id`)
) comment = 'expense category records' ;

-- note the back-ticks (as opposed to quotes)
-- very important in case we use reserved words
-- as field names or table names
{% endhighlight %}

### To insert documents:
{% highlight sql %}
insert into `category` set `name`='Groceries';

insert into `category` set `name`='Rent';

insert into `category` set `name`='Transport', `description`='trains, planes, buses';
    
insert into `category` (`name`) values ('whatever');
{% endhighlight %}

### To retrieve documents:
{% highlight sql %}
select * from `category`;

select * from `category` where `id`=1;

select `name` from `category`;
{% endhighlight %}


### To update documents:
{% highlight sql %}
update `category` set `description`='public transit' 
    where `id`=3;
    
update `category` c set `description` = c.name;
{% endhighlight %}

### To delete documents:
{% highlight sql %}
delete from `category` where `id` = 4;

-- note: will delete all records
delete from `category`;
{% endhighlight %}



## Running MongoDB commands from NodeJS back-end server

Next we shall be using these SQL commands from inside our NodeJS server. 

### Install the MongoDB NodeJS module

Unlike the `http` and `url` core modules we have used before, the `mysql` module that we will need to run these commands is not built-in. So we need to install it first. To do this, at the server code folder type in: `npm install mysql` 

Then, in our server.js code, we can then ask for this module by adding:  `var mysql = require('mysql');`

### Establish a connection

{% highlight javascript %}

...

var dbHost = process.env.IP || 'localhost',
    dbUser = process.env.C9_USER || 'root';

var connection = mysql.createConnection({
    host     : dbHost,
    user     : dbUser,
    password : '',
    database : 'c9'   // change if not on Cloud9
});

...

{% endhighlight %}


Note that the password and database name, and possibly even user, will be different if you're working off a local installation of MySQL i.e. on your computer, as opposed to on Cloud9.


### Code a route to get a list of categories

{% highlight javascript %}

...

var sql;
    
switch (route) {
    
    case '/categories':
        sql = 'select `id`,`name` from `category`';
        connection.query(sql, function(err, rows) {
            if (err) {
                console.error('categories sql error: ' + err.stack);
            } else {
                res.write(JSON.stringify(rows));
                res.end();
            }
        });
        break;

...

{% endhighlight %}



### Code a route to get a summary of expenses

{% highlight javascript %}

...

case '/summary':
    sql = 'select c.name, sum(e.amount) as `total` from `category` c left outer join `expense` e on c.id = e.categoryId group by c.id';
    connection.query(sql, function(err, rows) {
        if (err) {
            console.error('summary sql error: ' + err.stack);
        } else {
            res.write(JSON.stringify(rows));
            res.end();
        }
    });
    break;

...

{% endhighlight %}



### Code a route to insert an expense record

{% highlight javascript %}

...

case '/expense':
    var parms = url.parse(req.url,true).query,
        setFlds = {
            date: new Date(),
            amount: parms.amount,
            categoryId: parms.category
        };
            
        sql = 'insert into `expense` set ?';
            
        connection.query(sql, [setFlds], function(err, result) {
            if (err) {
                console.error('expense sql error: ' + err.stack);
            } else {
                res.write( JSON.stringify(result) );
                res.end();
            }
        });
            
        break;

...

{% endhighlight %}


### Test server.js

To try out these back-end server end-points, make sure to first start your database server, and then start your NodeJS server itself.

After we test these three end-points, we're done with our back-end changes, and we can next move on to coding the front-end of our little application.


## Coding the front-end

The requirements for this example front-end are exactly the same as the one we did for MySQL. In fact the same front-end code (HTML/CSS/JS) should run with little or no modification. This is an example of how the front-end part of an application is agnostic (does not know and does not need to know) about what technologies are being used in the back-end.

Here is a link to the full example code (back-end and front-end) on [GitHub](https://github.com/lcarbonaro/nodejs/tree/master/session27)

## References &amp; Resources

- [MongoDB Wikipedia entry](https://en.wikipedia.org/wiki/MongoDB)
- [MongoDB](https://docs.mongodb.com/manual/)
- [MongoDB for NodeJs (npm module docs](https://www.npmjs.com/package/mongodb)
- [MongoDB tutorial](http://www.tutorialspoint.com/mongodb/index.htm)
