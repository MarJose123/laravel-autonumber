# Laravel AutoNumber

A Fork from `alfa6661/laravel-autonumber`. Laravel package to create autonumber for Eloquent model

# Installation

You can install the package via composer:

```
composer require marjose123/laravel-autonumber
```

Publish the default configuration

```
php artisan vendor:publish --provider='Alfa6661\AutoNumber\AutoNumberServiceProvider'
```

Running migration

```
php artisan migrate
```

# Usage

Your Eloquent models should use the `Alfa6661\AutoNumber\AutoNumberTrait` trait

The trait contains an abstract method `getAutoNumberOptions()` that you must implement yourself.


```php
use Alfa6661\AutoNumber\AutoNumberTrait;
    
class Order extends Model
{
    use AutoNumberTrait;
    
    /**
     * Return the autonumber configuration array for this model.
     *
     * @return array
     */
    public function getAutoNumberOptions()
    {
        return [
            'order_number' => [
                'startingValue' => 11111, // optional if you want to start a different number than 1
                'format' => 'SO.?', // autonumber format. '?' will be replaced with the generated number.
                'length' => 5 // The number of digits in an autonumber
            ]
        ];
    }

}
```

You can also pass a `closure` for the format value.

```php
public function getAutoNumberOptions()
{
    return [
        'order_number' => [
            'startingValue' => 11111, // optional if you want to start a different number than 1
            'format' => function () {
                return 'SO/' . date('Ymd') . '/?'; // autonumber format. '?' will be replaced with the generated number.
            },
            'length' => 5 // The number of digits in the autonumber
        ]
    ];
}
```

## Saving Model

```php
$order = Order::create([
    'customer' => 'Mr. X',
]);
```

The order_number will be automatically generated based on the format given when saving the Order model.

```php
echo $order->order_number;

// SO/20170803/00001
```

## License

Laravel-autonumber is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).

## Contributing

Please report any issue you find in the issues page. Pull requests are more than welcome.
