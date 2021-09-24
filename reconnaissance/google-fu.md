# Scour the Web

## Google Fu

### Subdomain Enumeration

&lt;Keyword&gt; &lt;site name&gt;

```text
site:*.wikimedia.org 
```

### File Extensions

Find php \(or any datatype\), txt and log files

```text
site:*.example.org ext:php | ext:txt | ext:log
```

## Old Files

Old files \(which haven't been deleted but are no longer in use\) may be in Google's archives. Refer to OWASP testing guide v4's "Google Hacking" for more info.

## Code Repositories

Look up the target on  github, gitlab, bitbucket etc

Gitrob can be used to query Github and search sensitive files from the command line itself for specific organisations.

Trufflehog is a tool that searches for secrets, you can use that on the repos.

## Cloud Storage

If you can find a company's cloud storage container \(like an Amazon S3 bucket\), then you might see interesting things there. They can be easy to misconfigure.

## Info Gathering Services

Shodan

Ichidan

data.com

## Hiring Platforms, Company page

Take a look at LinkedIn, and the company website's "Careers" page. You'll probably find:

*  technologies used by the company.
* employee names 

## Whois

Run a whois search to get a website owner's information:

* Name
* Email address

Search these in password dumps, correlate with admin accounts.

Ripe.net - whois  
Internet.ee - whois for estonian sites

## Virustotal

Surprisingly, you can get a bunch of information from virustotal:

* Subdomains
* Scanned files

Go to "Search" on [virustotal](https://www.virustotal.com) and search for the domain you care about.

