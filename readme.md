# ImpressPages (PHP 8 revival)

This is a community fork of [ImpressPages](https://github.com/impresspages/ImpressPages), whose last release (5.0.3) dates from 2017 and does not run on modern PHP. The `php8` branch brings it up to date while keeping the existing API, themes and plugins working.

**Requirements:** PHP 8.1 or newer (tested on PHP 8.5) and MySQL or MariaDB.

### What changed from 5.0.3

- Dependencies: Zend Framework i18n/service manager replaced by Laminas, PHPMailer 5.2 upgraded to 6.x, psr/log 1 to 3 supported.
- The Aura Router 2 dependency is replaced by a small built-in router with the same route syntax (`{param}`, optional `{/a,b}` segments, `where` tokens, GET/POST restriction, named URLs).
- The bundled less.php 1.7 is replaced by the maintained `wikimedia/less.php`; the bundled phpseclib is removed and download signatures are checked with PHP's own OpenSSL.
- PHP 8.x fixes: removed the reserved `String` class, declared dynamic properties, explicit nullable parameters, `(float)` casts, null-safe escaping helpers, `E_STRICT` removed, a crash in the translation loader and the DB exception class, and log messages trimmed to fit their column.
- The installer and admin no longer contact impresspages.org (the statistics service and tracking frames are gone; the server is offline).
- The start-pack `index.php` no longer swallows requests to `index.php` when using PHP's built-in web server.

The original README follows.

---

# ImpressPages core
This repository is used as a library for the main https://github.com/impresspages/ImpressPages respository. Here are stored the most fundamental features of ImpressPages. In long run, this repository should become into a self sustainable ImpressPages-framework without CMS.

## Installation

If you want to use the latest version from github, please follow these steps to get everything up and running.

1. Create a file called `composer.json` and put the following content in it:

```php
{
    "require": {
        "impresspages/impresspages": "5.0.*",
        "impresspages/plugin-google-analytics": "*"
    },
    "scripts": {
        "post-install-cmd": ["php vendor/impresspages/impresspages/bin/setup.php public"],
        "post-update-cmd": ["php vendor/impresspages/impresspages/bin/setup.php public"]
    },
    "autoload": {
        "psr-4": {"Plugin\\": "public/Plugin/"}
    }
}
```

2. Install all composer dependencies by running `composer install`

3. Start a webserver to serve the `public` directory. You can also use the built-in PHP webserver, switch into the public directory `cd public` and start the webserver using this command: `php -S localhost:8000 index.php`

4. Open your webserver and navigate to whatever address you are using, for example `http://localhost:8000`.

5. Follow the setup wizard.
