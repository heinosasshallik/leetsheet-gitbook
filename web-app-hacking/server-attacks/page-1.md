# Command Injection

## Command Substitution

Command substitution can often prove to be a useful tool for exploiting command injection. For example, the following commands are equal to the `ping 127.0.0.1` command:

* `` ping `echo 127.0.0.1` ``&#x20;
* `ping $(echo 127.0.0.1)`&#x20;

The `sleep` command is often useful for discovery. Payload example: `$(sleep 5)`.

_Note: Command substitution only works when your injection is in double-quotes  (`echo "$INJECTION_HERE"`) or not in quotes at all (`echo $INJECTION_HERE`). If your injection is in single quotes (`echo '$INJECTION_HERE'`), then command substitutions are not done, and you will **need to break out of the single quotes first**._

## Automated Exploitation

You can use Commix for automated command injection testing:&#x20;

{% embed url="https://github.com/commixproject/commix" %}

## Bypassing Mitigations

### Escaping Functions

If there is a function that escapes arguments, such as PHP's `escapeshellarg`, then you can still have your input be some flag. This might lead to unexpected behaviour.

PHP's   `escapeshellcmd` is even looser. It allows you to specify any number of parameters, but only one command. So you can't chain commands, but depending on the program, you might be able to get the program to behave in interesting ways by submitting certain flags and parameters as input.

### Symbol Alternatives

There are often alternatives to common symbols:

* `$IFS` is a replacement for a SPACE character.
* `$SHELL` expands to the user’s preferred shell.&#x20;
* `$@` expands to positional arguments, if there are any.&#x20;
* You may be able to use newlines (`%0a` after URL encoding) instead of semicolons and tabs instead of spaces.

### Piping and Redirection

Look at the list of bash redirection and command operators for ideas to pipe and redirect output:&#x20;

{% embed url="http://unix.stackexchange.com/questions/159513/what-are-the-shells-control-and-redirection-operators" %}

### Edge Cases

If you know what command they're using inside a shell command execution function (such as `exec()`), make sure to experiment with edge cases on the command line. For example,`exec(ping blah 127.0.0.1)` is equal to `exec(ping 127.0.0.1)`.
