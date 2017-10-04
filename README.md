Webgriffe Magento2 PHPUnit
==========================

This module is a metapackage that will install the correct version of PHPUnit depending on the version of Magento 2 that is installed through Composer. This is useful for automated testing environments where an extension is automatically tested with several Magento versions and each one of these Magento versions needs a specific version of PHPUnit for the tests to work.
Specifically, at the time of writing this, Magento 2.0 and 2.1 require PHPUnit 4 (even though they seem to work fine with PHPUnit 5 as well), whereas Magento 2.2 requires PHPUnit 6.

Installation
------------

The typical usage of this package is as a dev requirement of a Magento 2 extension. In this case do not require the PHPUnit package directly in your composer.json file. Instead require this metapackage as follows:

```
composer require --dev webgriffe/magento2-phpunit ^1.0
```

Notice the ^1.0 version constraint: this is important, as without this Composer would try to force the latest stable tag with a constraint such as ^1.1 and this may conflict with the Magento version you are using.
If you had the PHPUnit package installed previously, then it's normally necessary to remove the PHPUnit dependency prior to installing this metapackage:
 
```
composer remove phpunit/phpunit
```

How this works
--------------

Each tag of this metapackage contains a composer.json that has a different version requirement for Magento and, depending on that version, a specific version of PHPUnit is required.
With each increasing tag number, the Magento version requirement increases. Composer will try to use the highest version of this metapackage, being limited by the currently installed Magento 2 version. Once the highest usable tag has been determined, then the appropriate PHPUnit version is required by this package.

So, assume for example that your composer.json file requires Magento 2.1.x. When composer analyzes this metapackage, it will start with the latest tag (currently 1.1.1). This tag, however, requires Magento 2.2 or higher, and thus it is not suitable. Composer will then fallback to the next lower tag, 1.1.0, but this also needs Magento 2.2 or higher. Then Composer will try the 1.0.1 tag, and since this only requires Magento 2.0 or higher, Composer will choose this as the version to install. This tag, in turn, requires PHPUnit version 4.1.0 (the exact version required by Magento 2.0 and 2.1) or PHPUnit 5.4 or higher (but still within the 5.x major version). This is done because from what we could see, it seems like PHPUnit 5 works fine with Magento 2.0 and 2.1, and also because starting with version 5.4 there are some forward compatibility fixes that ease writing tests that work for both PHPUnit 5 and 6.
If you have problems with PHPUnit 5, then you can avoid this version being used by adding to your require-dev dependencies the following line:

```
"phpunit/phpunit": "^4.0 || ^6.0"
```

This will only allow PHPUnit 4.x and 6.x, thereby disallowing PHPUnit 5.x. Coupled with the version constraints in this metapackage, this will result in the installation of PHPUnit 4.1.0 for Magento 2.0.x and 2.1.x and PHPUnit 6.2.x for Magento 2.2.x
