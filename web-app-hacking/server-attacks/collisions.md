# Collisions

## Unicode Case Mapping Collisions

A collision occurs when two _different_ Unicode characters are uppercased or lowercased into the same character.

```
'ß'.toUpperCase() === 'ss'.toUpperCase() // true
'ß'.toUpperCase() === 'SS' // true
```

_Note: `'ß'.toLowerCase()` **does not** equal `ss`._

Click here for a [complete list of Unicode collisions](https://eng.getwisdom.io/awesome-unicode/#onetomanycasemappings).

You may sometimes be able to abuse this with "Forgot password" emails, for example. If it asks you for an email address, then instead of "sass@sass.com" you can put in "saß@sass.com" or "sass@saß.com". If the application converts it to lowercase and compares your input to "sass@sass.com", then the password reset link will be sent to your malicious email instead of "sass@sass.com".

Here's a vulnerable Node.js application's code, for example:

```
malicious_email = 'saß@sass.com';

// Converted to 'SASS@SASS.COM'
uppercased_email = malicious_email.toUpperCase();

// Will match a an existing user that's not controlled by the attacker ('SASS@SASS.COM')
user_id = get_user_from_database(uppercased_email);

if (user_id) {
  // Sends an email to 'saß@sass.com' for a password reset for the 'sass@sass.com' user.
  send_recovery_email(user_id, malicious_email);
}
```
