# L1 - Cloudflare bindings for Laravel

![CI](https://github.com/renoki-co/l1/workflows/CI/badge.svg?branch=master)
[![codecov](https://codecov.io/gh/renoki-co/l1/branch/master/graph/badge.svg)](https://codecov.io/gh/renoki-co/l1/branch/master)
[![StyleCI](https://github.styleci.io/repos/:styleci_code/shield?branch=master)](https://github.styleci.io/repos/:styleci_code)
[![Latest Stable Version](https://poser.pugx.org/renoki-co/l1/v/stable)](https://packagist.org/packages/renoki-co/l1)
[![Total Downloads](https://poser.pugx.org/renoki-co/l1/downloads)](https://packagist.org/packages/renoki-co/l1)
[![Monthly Downloads](https://poser.pugx.org/renoki-co/l1/d/monthly)](https://packagist.org/packages/renoki-co/l1)
[![License](https://poser.pugx.org/renoki-co/l1/license)](https://packagist.org/packages/renoki-co/l1)

Extend your PHP/Laravel application with Cloudflare bindings.

This package offers support for:

- [x] [Cloudflare D1](https://developers.cloudflare.com/d1)
- [ ] [Cloudflare KV](https://developers.cloudflare.com/kv/)
- [ ] [Cloudflare Queues](https://developers.cloudflare.com/queues)

## 🚀 Installation

You can install the package via Composer:

```bash
composer require renoki-co/l1
```

## 🙌 Usage

### D1 with raw PDO

Though D1 is not a relational database, it can be used as a PDO driver via our connector.

```php
use RenokiCo\L1\D1\D1Pdo;
use RenokiCo\L1\D1\D1PdoStatement;
use RenokiCo\L1\CloudflareD1Connector;

$pdo = new D1Pdo(
    dsn: 'sqlite::memory:',
    connector: new CloudflareD1Connector(
        database: 'your_database_id',
        token: 'your_api_token',
        accountId: 'your_cf_account_id',
    ),
);
```

### D1 with Laravel

In your `config/database.php` file, add a new connection:

```php
'connections' => [
    'd1' => [
        'driver' => 'd1',
        'prefix' => '',
        'database' => env('CLOUDFLARE_D1_DATABASE_ID', ''),
        'api' => 'https://api.cloudflare.com/client/v4',
        'auth' => [
            'token' => env('CLOUDFLARE_TOKEN', ''),
            'account_id' => env('CLOUDFLARE_ACCOUNT_ID', ''),
        ],
    ],
]
```

Then in your `.env` file, set up your Cloudflare credentials:

```
CLOUDFLARE_TOKEN=
CLOUDFLARE_ACCOUNT_ID=
CLOUDFLARE_D1_DATABASE_ID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

The `d1` driver will proxy the PDO queries to the Cloudflare D1 API to run queries.

## 🐛 Testing

``` bash
vendor/bin/phpunit
```

## 🤝 Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## 🔒  Security

If you discover any security related issues, please email <alex@renoki.org> instead of using the issue tracker.

## 🎉 Credits

- [Alex Renoki](https://github.com/rennokki)
- [All Contributors](../../contributors)