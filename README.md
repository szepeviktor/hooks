# PoP Hooks

[![Build Status][ico-travis]][link-travis]
[![Quality Score][ico-code-quality]][link-code-quality]
[![Software License][ico-license]](LICENSE.md)

<!--
[![Latest Version on Packagist][ico-version]][link-packagist]
[![Coverage Status][ico-scrutinizer]][link-scrutinizer]
[![Total Downloads][ico-downloads]][link-downloads]
-->

Contracts to implement hooks for PoP. The concept of a “hook” is the same [as in WordPress](https://developer.wordpress.org/plugins/hooks/): an “action” allows executing extra functionality, and a “filter” allows to modify a value.

## Install

Via Composer

``` bash
composer require getpop/hooks
```

## Usage

Initialize the component:

``` php
\PoP\Root\ComponentLoader::initializeComponents([
    \PoP\Hooks\Component::class,
]);
```

Use it:

```php
use PoP\Hooks\Facades\HooksAPIFacade;

// Get an instance of the service
$hooksapi = HooksAPI::getInstance();

// Add a hook for an Action
$hooksapi->addAction($actionName, $functionName, $priority, $argNum);

// Add a hook for a Filter
$hooksapi->addFilter($filterName, $functionName, $priority, $argNum);

// Execute an Action
$hooksapi->doAction($actionName, $param1, $param2, ...);

// Execute a Filter
$filterValue = $hooksapi->applyFilters($filterName, $filterValue, $param1, $param2, ...);

// Remove an Action
$hooksapi->removeAction($actionName, $functionName, $priority, $argNum);

// Remove a Filter
$hooksapi->removeFilter($filterName, $functionName, $priority, $argNum);
```

## Architecture Design and Implementation

### Hooks

PoP uses hooks (as pioneered by [WordPress](https://codex.wordpress.org/Plugin_API)) everywhere, through both functions `doAction` and `applyFilters` as defined through interface `HooksAPI`, allowing any piece of code to be overridable by any 3rd party, or be injected extra functionality. For WordPress, the implementation of the interface is trivial. Other systems can rely on packages to implement this functionality (eg: [this one](https://github.com/tormjens/eventy) or [this one](https://github.com/voku/php-hooks)).

## PHP versions

Requirements:

- PHP 7.4+ for development
- PHP 7.1+ for production

### Supported PHP features

Same as the [Supported PHP features for `getpop/root`](https://github.com/getpop/root/#supported-php-features)

### Downgrading code to PHP 7.1

Via [Rector](https://github.com/rectorphp/rector) (dry-run mode):

```bash
composer downgrade-code
```

## Standards

[PSR-1](https://www.php-fig.org/psr/psr-1), [PSR-4](https://www.php-fig.org/psr/psr-4) and [PSR-12](https://www.php-fig.org/psr/psr-12).

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Testing

``` bash
composer test
```

## Static Analysis

Execute [phpstan](https://github.com/phpstan/phpstan) with level 8:

``` bash
composer analyse
```

To run checks for level 0 (or any level from 0 to 8):

``` bash
./vendor/bin/phpstan analyse -l 0 src tests
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) and [CODE_OF_CONDUCT](CODE_OF_CONDUCT.md) for details.

## Security

If you discover any security related issues, please email leo@getpop.org instead of using the issue tracker.

## Credits

- [Leonardo Losoviz][link-author]
- [All Contributors][link-contributors]

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

[ico-version]: https://img.shields.io/packagist/v/getpop/hooks.svg?style=flat-square
[ico-license]: https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square
[ico-travis]: https://img.shields.io/travis/getpop/hooks/master.svg?style=flat-square
[ico-scrutinizer]: https://img.shields.io/scrutinizer/coverage/g/getpop/hooks.svg?style=flat-square
[ico-code-quality]: https://img.shields.io/scrutinizer/g/getpop/hooks.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/getpop/hooks.svg?style=flat-square

[link-packagist]: https://packagist.org/packages/getpop/hooks
[link-travis]: https://travis-ci.org/getpop/hooks
[link-scrutinizer]: https://scrutinizer-ci.com/g/getpop/hooks/code-structure
[link-code-quality]: https://scrutinizer-ci.com/g/getpop/hooks
[link-downloads]: https://packagist.org/packages/getpop/hooks
[link-author]: https://github.com/leoloso
[link-contributors]: ../../contributors
