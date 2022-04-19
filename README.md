

Step 1.
Checkout a version of sqlcipher, I know this isn't pure sqlite, but I want to see if I can
bring encryption along for the ride.

git clone https://github.com/sqlcipher/sqlcipher.git 4.5.1

coan
apt-file
static linking against openssl
https://stackoverflow.com/questions/26415485/finding-path-of-static-system-libraries-in-linux

Make sure everything builds and tests run.

I moved libcrypto.a to the /c/sqlite directory, it was a pain resolving conflicts.


```
./configure --enable-tempstore=yes CFLAGS="-DSQLITE_HAS_CODEC" LDFLAGS="-l:libcrypto.a"
make
make test
```

Start looking over the source and see what files I can remove to help clarify the structure.
A bit of an iterative process since I want to automate and document what I remove.

This process is a bit iterative. 

start using coan to remove preprocessor directives.
coan doesn't seem to like #line pragmas so search for everywhere they are emitted and removed the code emmitting them.


