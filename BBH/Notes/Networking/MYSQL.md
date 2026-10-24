### enumeration

## nmap

[Mysql-Enum](https://nmap.org/nsedoc/scripts/mysql-enum.html)

## Perl

https://www.exploit-db.com/exploits/23081

msf

 auxiliary/admin/mysql/mysql_sql 



# Exploiting MySQL

Let's take a sanity check before moving on to try and exploit the database fully, and gain more sensitive information than just database names. We know:  

1. MySQL server credentials  

2. The version of MySQL running

3. The number of Databases, and their names.

**Key Terminology**

In order to understand the exploits we're going to use next- we need to understand a few key terms.

**Schema:**

In MySQL, physically, a _schema_ is synonymous with a _database_. You can substitute the keyword "SCHEMA" instead of DATABASE in MySQL SQL syntax, for example using CREATE SCHEMA instead of CREATE DATABASE. It's important to understand this relationship because some other database products draw a distinction. For example, in the Oracle Database product, a _schema_ represents only a part of a database: the tables and other objects owned by a single user.

**Hashes:**  

Hashes are, very simply, the product of a cryptographic algorithm to turn a variable length input into a fixed length output.

In MySQL hashes can be used in different ways, for instance to index data into a hash table. Each hash has a unique ID that serves as a pointer to the original data. This creates an index that is significantly smaller than the original data, allowing the values to be searched and accessed more efficiently

However, the data we're going to be extracting are password hashes which are simply a way of storing passwords not in plaintext format.

Lets get cracking.



msf

mysql_schemadump

scanner/mysql/mysql_hashdump





