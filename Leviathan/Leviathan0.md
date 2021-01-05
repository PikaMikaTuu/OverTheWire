Leviathan0

# Leviathan0 05/01/2021 07:18

# Login with ssh
`ssh leviathan0@leviathan.labs.overthewire.org -p 2223`
password: `leviathan0`

By default, ssh tries to connect to port ``22``.

# Enumeration
Running `ls -la` sshows a hidden folder `backup` and it has a file `bookmarks.html` owned by `leviathan1`.

Also note that we have `read` permission.

>./.backup:
total 140
drwxr-x--- 2 leviathan1 leviathan0   4096 Aug 26  2019 .
drwxr-xr-x 3 root       root         4096 Aug 26  2019 ..
-rw-r----- 1 leviathan1 leviathan0 133259 Aug 26  2019 bookmarks.html

# Let's search for keywords such `password`or `leviathan`

`grep -E 'password|leviathan' ./.backup/bookmarks.html`

>HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is rioGegei8m" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>

### Password for `leviathan1`: rioGegei8m