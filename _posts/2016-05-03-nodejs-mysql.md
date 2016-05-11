---
layout: post
title: "NodeJS & Databases: MySQL"
comments: true
publish: true
---

Databases are an essential component of back-end architecture. NodeJS, which enables us to run JavaScript code on the server side, can connect to several of the major database server engines, including the very popular MySQL.

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

## MySQL Command Line

Cloud9 users can get at a MySQL command line prompt by opening a terminal window and typing in `mysql-ctl cli`.

If you have installed MySQL locally, from a command window at the installed mysql/bin folder, type in `mysqld` to start the database server. Do not close this window. Open another command window and, at the installed mysql/bin folder, type in `mysql` to get a MySQL prompt. Note that this may vary based on your local installation.

## Using phpmyadmin	

phpmyadmin is a browser-based interface and can be used instead of the MySQL command line.

Cloud9 users can access phpmyadmin by opening a terminal window and typing in `phpmyadmin-ctl install`. Then open the link displayed, in a separate browser tab.

If you have installed MySQL locally, depending on what you installed, you may have access to phpmyadmin, workbench, or other tools.


## Some example commands:

### To show/create/use databases:

`show databases;`

Cloud9:  `use c9;`

Local: `create database test;` then `use test;`

### To create a table:
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

### To insert records:
{% highlight sql %}
insert into `category` set `name`='Groceries';

insert into `category` set `name`='Rent';

insert into `category` set `name`='Transport', `description`='trains, planes, buses';
    
insert into `category` (`name`) values ('whatever');
{% endhighlight %}

### To retrieve records:
{% highlight sql %}
select * from `category`;

select * from `category` where `id`=1;

select `name` from `category`;
{% endhighlight %}


### To update records:
{% highlight sql %}
update `category` set `description`='public transit' 
    where `id`=3;
    
update `category` c set `description` = c.name;
{% endhighlight %}

### To delete records:
{% highlight sql %}
delete from `category` where `id` = 4;

-- note: will delete all records
delete from `category`;
{% endhighlight %}

### Some other useful commands:
{% highlight sql %}
show create table `category`;
{% endhighlight %}

{% highlight sql %}
-- note truncate vs. delete
truncate table `category`; 
{% endhighlight %}

### Foreign keys and selects across tables
{% highlight sql %}
-- let's create another table
create table `expense` (
`id` int auto_increment comment 'auto generated expense id',
`date` date,
`amount` decimal(6,2),
`details` varchar(50),
`categoryId` int comment 'foreign key to category table',
primary key (`id`)
) comment = 'expense records';
{% endhighlight %}

{% highlight sql %}
-- add some records to the expense table
insert into `expense` (`date`,`categoryId`,`amount`) 
    values('2016-05-01',2,1234);

-- can insert more than one record at a time
insert into `expense` (`date`,`categoryId`,`amount`)
    values ( curdate(),1,12.34 ), 
           ( curdate(),1,20 ), 
           ( curdate(),3,60 );

-- curdate() is built-in MySQL function
-- that returns the current date
{% endhighlight %}

{% highlight sql %}
select * from `expense`;
{% endhighlight %}

{% highlight sql %}
-- look-up category id. to show name
select e.*, c.name 
from `expense` e, `category` c 
where e.categoryId = c.id;
{% endhighlight %}

{% highlight sql %}
-- above can be done as inner join
select e.*, c.name 
from `expense` e
inner join `category` c on e.categoryId = c.id;
{% endhighlight %}

{% highlight sql %}
-- aggregation
select c.name, sum(e.amount) as `total`
from `category` c
left outer join `expense` e on c.id = e.categoryId
group by c.id;
{% endhighlight %}


## Running SQL commands from NodeJS back-end server

Next we shall be using these SQL commands from inside our NodeJS server. 

### Install the MySQL NodeJS module

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

The requirements for this front-end are very simple. 

  -  We will have a drop-down (select) listing all the categories. 
  
  -  We will have an input box to enter the expense amount, and a save button. 
  
  -  We will have a button to display an expense summary for each category.


Here is a link to the full example code (back-end and front-end) on [GitHub](https://github.com/lcarbonaro/nodejs/tree/master/session26)

## References &amp; Resources

- [MySQL](http://mysql.com/)
- [MariaDB](https://mariadb.org/)
- [MySQL npm module docs](https://www.npmjs.com/package/mysql)