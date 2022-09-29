# Web Fuzzing

## Ffuf

{% embed url="https://allabouttesting.org/top-25-example-usage-of-ffuf-web-fuzzer/" %}

Using ffuf to fuzz a POST payload with two wordlists at once:

```
ffuf -w ./dirs.txt:DIR -w filenames.txt:FILENAME \
     -u http://backend/api/v1/admin/file \
     -H 'Content-Type: application/json' \
     -X POST \
     -d '{"file":"/var/www/DIR/FILENAME.py"}'
```
