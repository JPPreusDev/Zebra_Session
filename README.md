# Zebra_Session

#### A drop-in replacement for PHP's default session handler which stores session data in a MySQL database, providing both better performance and better security and protection against session fixation and session hijacking.

----

[Packagist](https://packagist.org/) stats

[![Latest Stable Version](https://poser.pugx.org/stefangabos/zebra_session/v/stable)](https://packagist.org/packages/stefangabos/zebra_session) [![Total Downloads](https://poser.pugx.org/stefangabos/zebra_session/downloads)](https://packagist.org/packages/stefangabos/zebra_session) [![Monthly Downloads](https://poser.pugx.org/stefangabos/zebra_session/d/monthly)](https://packagist.org/packages/stefangabos/zebra_session) [![Daily Downloads](https://poser.pugx.org/stefangabos/zebra_session/d/daily)](https://packagist.org/packages/stefangabos/zebra_session) [![License](https://poser.pugx.org/stefangabos/zebra_session/license)](https://packagist.org/packages/stefangabos/zebra_session)

## Support the development of this library

This library is developed during my free time and a lot of time and effort has been put into it.

[![Donate](https://img.shields.io/badge/Be%20kind%20%7C%20Donate%20with%20-%20PayPal%20-brightgreen.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=AMF86638PS2S4)

Zebra_Session implements *session locking* - a way to ensure that data is correctly handled in a scenario with multiple concurrent AJAX requests.

It is also a solution for applications that are scaled across multiple web servers (using a load balancer or a round-robin DNS) and where the user's session data needs to be available. Storing sessions in a database makes them available to all of the servers!

The library supports "flashdata" - session variable which will only be available for the next server request, and which will be automatically deleted afterwards. Typically used for informational or status messages (for example: "data has been successfully updated").

Zebra_Session is was inspired by John Herren's code from the [Trick out your session handler](http://devzone.zend.com/413/trick-out-your-session-handler/) article and [Chris Shiflett](http://shiflett.org/articles/the-truth-about-sessions)'s articles about PHP sessions.

The code is heavily commented and generates no warnings/errors/notices when PHP's error reporting level is set to E_ALL.

## Features

- acts as a wrapper for PHP’s default session handling functions, but instead of storing session data in flat files it stores them in a MySQL database, providing better security and better performance

- it is a drop-in and seamingless replacement for PHP’s default session handler: PHP sessions will be used in the same way as prior to using the library; you don’t need to change any existing code!

- implements *row locks*, ensuring that data is correctly handled in scenarios with multiple concurrent AJAX requests

- because session data is stored in a database, the library represents a solution for applications that are scaled across multiple web servers (using a load balancer or a round-robin DNS)

- has comprehensive documentation

- the code is heavily commented and generates no warnings/errors/notices when PHP’s error reporting level is set to E_ALL

## Requirements

PHP 5.1.0+ with the **mysqli extension** activated, MySQL 4.1.22+

### Installation
Download the latest version, unpack it, and load it in your project

```php
require_once ('Zebra_Session.php');
```

### Installation with Composer
You can install Zebra_Session via [Composer](https://packagist.org/packages/stefangabos/zebra_session)
```
composer require stefangabos/zebra_session:dev-master
```

## How to use

Notice a directory called *install* containing a file named *session_data.sql*. This file contains the SQL code that will create a table that is used by the class to store session data. Import or execute the SQL code using your preferred MySQL manager (like phpMyAdmin or the fantastic Adminer) into a database of your choice.

*Note that this class assumes that there is an active connection to a MySQL database and it does not attempt to create one! If you really need the class to make a database connection, put the code in the "open" method of the class.*

```php
// first, connect to a database containing the sessions table
// like $link = mysqli_connect(host, username, password, database);

// include the Zebra_Session class
include 'path/to/Zebra_Session.php';

// instantiate the class
// this also calls session_start()
$session = new Zebra_Session($link, 'sEcUr1tY_c0dE');

// from now on, use sessions as you would normally
// this is why it is called a "drop-in replacement" :)
$_SESSION['foo'] = 'bar';

// data is in the database!
```

Visit the **[project's homepage](http://stefangabos.ro/php-libraries/zebra-session/)** for more information.
