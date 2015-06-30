# onemonth-login

This is the project files for One Month Web Security's section on Brute force. This particular tools is used for username enumeration. We are taking a list of babynames, stripping out details so we only have the first name, then we are appending the email to the end. This gives us a list of users possible emails and we run a ruby script to confirm. This is not a general purpose tool but made to work with One Month's test security application. I did not write the code for either the test application or the ruby script.

## Generating the usernames
The following command can be used to download the baby files names (but are already included in this repo).

```bash
wget http://www.ssa.gov/oact/babynames/names.zip
```

This is a chained statement for taking the first 2000 male names and adding them to a new text document with proper formating

```bash
cat yob2013.txt | grep ",M," | head -n 2000 | cut -d , -f 1 | sort | uniq | awk '{print tolower($0)}' >> male2013.txt
```

And for females:

```bash
cat yob2013.txt | grep ",F," | head -n 2000 | cut -d , -f 1 | sort | uniq | awk '{print tolower($0)}' >> female2013.txt
```

To add the email to each of the names

```bash
cat male2013.txt | sed -e 's/$/@onemonthsimple.com/' >> onemonth2013.txt
```

and again for females:

```bash
cat female2013.txt | sed -e 's/$/@onemonthsimple.com/' >> onemonth2013.txt
```

## Running the attack
To run the attack with the generated userlist, run the following command

```bash
ruby onemonth-login.rb
```

This will attempt to enumerate any user names based on the error message recieved. This is a great example of why you should not tell a user if the username exists or not. Again, this is not a multipurpose tool but was written specifically for the one month application. Feel free to view or edit these files as necessary!

## Example Output

```bash
Found: chris@onemonthsimple.com
Found: jon@onemonthsimple.com
Found: lee@onemonthsimple.com
```
