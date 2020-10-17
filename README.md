![REST API Response Builder for Laravel](docs/img/logo.png)

# REST API Response Builder for Laravel #

[![Latest Stable Version](https://poser.pugx.org/marcin-orlowski/laravel-api-response-builder/v/stable)](https://packagist.org/packages/marcin-orlowski/laravel-api-response-builder)
[![Build Status](https://travis-ci.org/MarcinOrlowski/laravel-api-response-builder.svg?branch=master)](https://travis-ci.org/MarcinOrlowski/laravel-api-response-builder)
[![Code Quality](https://scrutinizer-ci.com/g/MarcinOrlowski/laravel-api-response-builder/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/MarcinOrlowski/laravel-api-response-builder/?branch=master)
[![Code Coverage](https://scrutinizer-ci.com/g/MarcinOrlowski/laravel-api-response-builder/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/MarcinOrlowski/laravel-api-response-builder/?branch=master)
[![Codacy Grade Badge](https://api.codacy.com/project/badge/Grade/44f427e872e2480597bde0242417a2a7)](https://www.codacy.com/app/MarcinOrlowski/laravel-api-response-builder)
[![Monthly Downloads](https://poser.pugx.org/marcin-orlowski/laravel-api-response-builder/d/monthly)](https://packagist.org/packages/marcin-orlowski/laravel-api-response-builder)
[![License](https://poser.pugx.org/marcin-orlowski/laravel-api-response-builder/license)](https://packagist.org/packages/marcin-orlowski/laravel-api-response-builder)

[![SensioLabs Insight](https://insight.sensiolabs.com/projects/5c5f4dc1-41d5-49f9-b4ba-6268aa3fea00/big.png)](https://insight.sensiolabs.com/projects/5c5f4dc1-41d5-49f9-b4ba-6268aa3fea00)

[![Unstable Version](https://poser.pugx.org/marcin-orlowski/laravel-api-response-builder/v/unstable)](https://packagist.org/packages/marcin-orlowski/laravel-api-response-builder)
[![Unstable Build Status](https://travis-ci.org/MarcinOrlowski/laravel-api-response-builder.svg?branch=dev)](https://travis-ci.org/MarcinOrlowski/laravel-api-response-builder)
[![Ustable Code Quality](https://scrutinizer-ci.com/g/MarcinOrlowski/laravel-api-response-builder/badges/quality-score.png?b=dev)](https://scrutinizer-ci.com/g/MarcinOrlowski/laravel-api-response-builder/?branch=dev)
[![Unstble Code Coverage](https://scrutinizer-ci.com/g/MarcinOrlowski/laravel-api-response-builder/badges/coverage.png?b=dev)](https://scrutinizer-ci.com/g/MarcinOrlowski/laravel-api-response-builder/?branch=dev)

## Table of contents ##

 * [Introduction](#introduction)
 * [Why should I use it?](#benefits)
 * [Usage examples](#usage-examples)
 * [Features](#features)
 * [Documentation](docs/docs.md)
 * [Requirements](docs/docs.md#requirements)
 * [Installation and Configuration](docs/docs.md#installation-and-configuration)
 * [License](#license)
 * [Changelog](CHANGES.md)

 **Upgrading from previous version? Check [compatibility docs](docs/compatibility.md) prior altering your `composer.json`!**

----

## Introduction ##

 `ResponseBuilder` is a [Laravel](https://laravel.com/) helper designed to build nice, normalized and easy to consume REST API
 JSON responses.

## Benefits ##

 `ResponseBuilder` is written for REST API developers by REST API developer and is based on my long-lasting experience on both
 "sides" as API dev and API consumer, of variety of REST APIs. It's lightweight, extensively tested, simple to use yet
 flexible and powerful, withon-the-fly data conversion, localization support, automatic error message building, support
 for chained APIs and (hopefully) exhaustive documentation. But that's not all! The JSON structure produced by `ResponseBuilder`
 is designed with **users of your API** in mind, to make dealing with your API a breeze. Simple JSON response, with well-defined
 and predictable structure, easy to consume without a hassle nor trickery.

 As a bonus, Android developers can use [ApiResponse](https://github.com/MarcinOrlowski/ApiResponse) library in their apps
 to handle `ResponseBuilder` responses.

 You are even covered in a case of emergency, as provided Exception Handler helper, ensures your API keeps talking JSON (and
 not HTML) to its clients even in case of unexpected and unhandled exception.

 Did I mention, you would also get free testing traits that automatically unit test your whole `ResponseBuilder` related code
 and configuration with just a few lines of code?

## Usage examples ##

 Operation successful? Conclude your controller method with:

```php
return RB::success();
```

 and your client will get nice JSON like

```json
{
  "success": true,
  "code": 0,
  "locale": "en",
  "message": "OK",
  "data": null
}
```

 Need to additionally return extra payload with the response? Pass it as
 argument to `success()`:

```php
$flight = App\Flight::where(...)->get();
return RB::success($flight); 
```

 and your client will get that data in `data` node of your response:

```json
{
  "success": true,
  "code": 0,
  "locale": "en",
  "message": "OK",
  "data": {
     "items": [
        {
          "airline": "lot",
          "flight_number": "lo123",
          ...
       },
       {
          "airline": "american",
          "flight_number": "am456",
          ...
       }
    ]
  }
}
```

 Something went wrong and you want to tell the clinet about that? Just do:

```php
return RB::error(250);
```

 The following JSON response will then be returned:

```json
{
   "success": false,
   "code": 250,
   "locale": "en",
   "message": "Your error message for code 250",
   "data": null
}
```

 Nice and easy! And yes, `message` can be easily customized! Also there're **much, much more** you can do with
 rich `ResponseBuilder` API. See [library documentation](docs/docs.md) for details and more examples!

----

## Features ##

 * Easy to use,
 * [Stable and production ready](https://travis-ci.org/MarcinOrlowski/laravel-api-response-builder),
 * On-the-fly data object conversion,
 * API chaining support,
 * Localization support,
 * Provides traits to help [unit test your API code](docs/testing.md),
 * Comes with [exception handler helper](docs/exceptions.md) to ensure your API stays consumable even in case of unexpected,
 * No additional dependencies.

----

## License ##

 * Written and copyrighted &copy;2016-2020 by Marcin Orlowski <mail (#) marcinorlowski (.) com>
 * ResponseBuilder is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)
