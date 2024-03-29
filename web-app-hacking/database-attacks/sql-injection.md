---
description: SQLi / SQL Injection
---

# SQL Injection

## Manual Testing

How to test for SQL Injection manually.

### Verify the Existence of SQL Injection

Broadly, to verify the existence of SQL injection in a given field you can try to either:

1. Create an error
2. Use SQL operators and see if the data is changed according to SQL rules
3. Add a `sleep` statement to the SQL query

To **create an error**, you can:

* Add single and double quotes everywhere and see if it fails
* If there is an integer ID, then you can try a negative value, since negative IDs usually don't exist

Using **operators**, you can verify SQL like this:

* If there is an integer ID, then you can try to subtract from it.
  * `?id=11-1`, and see if the result is the same as `?id=10`
* If there is a string value, then that's trickier. You can try to concatenate to it, but it's easy to create an error accidentally.
  * `asd' + 'f` will work in MySQL, but not in PostgreSQL
  * `asd' || 'f` is the SQL standard, but it will **still create an error** in MySQL, because MySQL expects it in between a pair of parentheses. 

### Union-Based Exploitation

{% embed url="https://book.hacktricks.xyz/pentesting-web/sql-injection#exploiting-union-based" %}


You can query additional rows using `UNION SELECT`. Before you do that, you'll need to determine the amount of rows. You can use `ORDER BY` for that.
 

### General Tips

Here are some things to remember:

* For commenting stuff out, use `-- ` with a **space** at the end, because MySQL requires there to be a space.
* Don't forget to URLencode.
  * Browsers will omit extra spaces from the end of an URL, so your `-- ` will become just `--` and your exploit won't work for MySQL.


### Filter Evasion

Using **flexible MySQL syntax**:
https://websec.wordpress.com/2010/03/19/exploiting-hard-filtered-sql-injections/

Advanced ways to evade filters (using tricks like putting backslashes, using MySQL syntax, etc):
https://websec.files.wordpress.com/2010/11/sqli2.pdf

SQL smuggling for evading filters: 
If `INSERT` is blacklisted, then do `concat("INS", "ERT")`

Also **unicode smuggling**: 'Ā' may default to 'A' and thus evade detection.

## Automated Testing

Sqlmap GET example:

```
sqlmap -u "mysite.com/sql.php?param=1"
```

Sqlmap POST example:

```
sqlmap -u "mysite.com/sql.php" --method "POST" --data "POST_DATA_HERE" 
```

Sqlmap using a saved request:

```
sqlmap -r saved_http_request.txt
```

Useful flags:
* `--level`: Allows you to increase the sophistication level. Values `{1...5}`
* `--risk`: Allows you to increase the potential damage the script might do. Values `{1...5}`
* `--random-agent`: Random user agent
* `-v3`: Increase verbosity
* `--cookie`: set cookie
* `--proxy`: set a proxy

