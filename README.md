Webgriffe Magento2 PHPUnit
==========================

This module is a metapackage that will install the correct version of PHPUnit depending on the version of Magento 2 that is installed through Composer. This is useful for automated testing environments where an extension is automatically tested with several Magento versions and each one of these Magento versions needs a specific version of PHPUnit for the tests to work.
Specifically, at the time of writing this, Magento 2.0 and 2.1 require PHPUnit 4 (even though they seem to work fine with PHPUnit 5 as well), whereas Magento 2.2 requires PHPUnit 6.

Installation
------------

The typical usage of this package is as a dev requirement of a Magento 2 extension. In this case require this metapackage as follows:

```
composer require --dev webgriffe/magento2-phpunit
```

How this works
--------------

Each tag of this metapackage contains a composer.json that has a different version requirement for Magento and, depending on that version, a specific version of PHPUnit is required.
With each increasing tag number, the Magento version requirement increases. Composer will try to use the highest version of this metapackage, being limited by hte currently installed Magento 2 version. Once the highest usable tag has been determined, then the appropriate PHPUnit version is required by this package.
