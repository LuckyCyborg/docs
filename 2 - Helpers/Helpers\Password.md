The password file uses a password library from [https://github.com/ircmaxell/password_compat](https://github.com/ircmaxell/password_compat)

The  library is intended to provide forward compatibility with the [password_*](http://php.net/password) functions being worked on for PHP 5.5

This library requires PHP >= 5.3.7 OR a version that has the $2y fix backported into it (such as RedHat provides). Note that Debian's 5.3.3 version is **NOT** supported.

To create a hash of a password, call the password_hash method and provide the password to be hashed, once done save the $hash.

```php
$hash = Password::password_hash($password, PASSWORD_BCRYPT);
```

When logging in a user their hash must be retrieved from the database and compared against the provided password to make sure they match, for this a method called password_verify is used, it has 2 parameters the first is the user provided password the second is the hash from the database.

```php
    if(Password::password_verify($_POST['password'],$data[0]->password)){
     //passed
    } else {
     //failed
    }
```

From time to time you may update your hashing parameters (algorithm, cost, etc). So a function to determine if rehashing is necessary is available:

```php
if(Password::password_verify($password, $hash)) {
   if(Password::password_needs_rehash($hash, $algorithm, $options)) {
    $hash = Password::password_hash($password, $algorithm, $options); /* Store new hash in db */
   }
}
```
