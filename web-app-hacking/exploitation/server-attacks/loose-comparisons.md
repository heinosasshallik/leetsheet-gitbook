# Loose Comparisons

## MySQL

{% embed url="https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html" %}

MySQL's `=` operator does loose comparisons by default. These comparisons all evaluate to true:

* `SELECT '0' = 0;`
* `SELECT '0.0' = 0;`
* `SELECT '0      ' = '0';`

_Note: Postgresql doesn't do loose comparisons by default._

## PHP

{% embed url="https://owasp.org/www-pdf-archive/PHPMagicTricks-TypeJuggling.pdf" %}

PHP has loose comparisons ("==") and strict comparisons ("==="). Loose comparisons have some weird conversion rules which can be used to trick the application into doing what you want.

_Note: Python and JS also have loose comparisons._

Use cases:

* CSRF token bypass
* Authentication bypass
* Subverting application logic in general

**JSON is really useful** for exploiting this because if the application takes JSON input, you can specify the type of the variable you're sending. In other words, you can also send ints and booleans, not just strings.&#x20;

### Compare string to integer

Most strings are equal to the integer 0.

* `TRUE: "0000" == int(0)`&#x20;
* `TRUE: "1abc" == int(1)`&#x20;
* `TRUE: "0abc" == int(0)`&#x20;
* `TRUE: "abc" == int(0) // !!`

### Compare string to string

PHP does strange conversions between strings if they look like numbers.

* `TRUE: "0e12345" == "0e54321"`
* `TRUE: "0e12345" <= "1"`&#x20;
* `TRUE: "0e12345" == "0"`&#x20;
* `TRUE: "0xF" == "15"`

### Array comparison

Let's say you want to bypass the following if-condition:

```
if (strcmp($_POST['password'], 'thePassword') == 0) {
 // do authenticated things
}
```

If you submit an array as `$_POST['password']` like this: `password[]=` , then the `strcmp` operation will error out. The result will be NULL.

Thanks to type juggling, `NULL == 0` is true, and you bypass the check and do authenticated things.

