## Language System

The new Language System uses two framework-wide functions for string translation, the first one being **__()**, which is designed to be used in the App folder and the second being **__d()**, designed to be used on Language Domains; those Language Domains are the Modules, the Templates or the System.

**IMPORTANT:** When a specified domain matches both a Module and Template name, the Module will take precedence. In other words, there should not be a Module and a Template with the same name, for the Language System to work properly.

The usage of both translation functions is very simple, they contain the string to be translated and optional parameters. For example 

```php
// Get a translation for App Domain (default)
$translated = __('Hello, {0}', $username);

// Get a translation for Users Module Domain
$translated = __d('users', 'Welcome back, {0}!', $username);

// Get a translation for System Domain
$translated = __d('system', 'File not found: {0}', $filename);
```

Please note that the Domains are specified in **snake_case** transformation and that the translation string's parameters are using the ICU notation, which is used also by the PHP's INTL extension.

There is also a utility script that has been introduced, called **scripts/makelangs.php**, and it should be used to update the Framework's Language files, after introducing new translation strings in your application.

The Language files used by this new Language System are called **messages.php** and will be found in the usual locations, i.e. **app/Language/En/messages.php** or **app/Modules/Users/Language/En/messages.php**