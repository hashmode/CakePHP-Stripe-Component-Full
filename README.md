CakePHP-Stripe-Component-Full
=============================

Cakephp component for stripe payments - contains all the methods described in Stripe PHP API. Cake version 2x. Was created with Stripe API version 1.15.0(latest at the moment).

## Installation

1) Copy `StripeComponent.php` file to `app/Controller/Component` directory.

2) Download Stripe PHP library from https://stripe.com/docs/libraries and unpack it in Vendor folder, so the Stripe.php file will have the following path `app/Vendor/stripe/lib/Stripe.php`

3) Include in your controller, as `$components => array('Stripe')`, if you want save logs (by default disabled), use 

```
$components => array(
    'Stripe' => array(
      'logFile' => 'stripe',
      'logType' => 'error'
    )
);
```
if logType is set to `error` only errors will be saved, if `success` only successful requests, if you want to save both set it as `both`.

with this, be sure to create log file in `app/tmp/logs` direcoty with name `stripe.log`, and also add this in your bootstrap.php

```
CakeLog::config('stripe', array(
	'engine' => 'FileLog',
	'file' => 'stripe'
));

```

4) Set account settings from bootstrap 

```
Configure::write('Stripe.TestSecret', 'your test secret here');
Configure::write('Stripe.LiveSecret', 'your live secret here');
Configure::write('Stripe.mode', 'Test');
Configure::write('Stripe.currency', 'usd');
```



## Usage
Each function returns array - containing 'status', 'message' and 'data' keys
if response was successful, keys will be  'success', 'Success' and the stripe response(as described in API docs), but as an associative array respectively,
if request failed, keys will be 'error', the card error message if it was card_error, boolen false otherwise, and error data as an array respectively


## LICENSE
MIT









