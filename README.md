CakePHP-Stripe-Component-Full
=============================

Cakephp component for stripe payments - contains all the methods described in Stripe API. Cake version 2x. Was created with Stripe API version 1.15.0(latest at the moment).

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
if `logType` is set to `error` only errors will be saved, if `success` only successful requests, if you want to save both set it as `both`.

with this, be sure to create log file in `app/tmp/logs` directory with name `stripe.log`, and also add this in your bootstrap.php

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
Each function returns array - containing `status`, `message` and `data` keys


if response was successful, keys will be  

```
'status' => 'success',
'message' => 'Success',
'data' => the Stripe's response described in API docs, but as an associative array
```

if request failed, response will be

```
'status' => 'error',
'message' => the Stripe error message, if it was card error, boolen false otherwise
'data' => Stripe's error response
```

Function parameters are almost identical what is said in API docs, for example if it is necessary to create card, we need customer's id and the card data, either as array or as token (https://stripe.com/docs/api#create_card), so using `createCard($customerId = null, $card = null)` function, we should provide customer's id as first parameter `$customerId` and card data as second parameter `$card`.


List of functions


```
charge($data = null, $customerId = null)
retrieveCharge($chargeId = null)
updateCharge($chargeId = null, $data = array())
refundCharge($chargeId = null, $data = array())
captureCharge($chargeId = null, $data = array())
listCharges($data = array())
createCustomer($data)
retrieveCustomer($customerId = null)
updateCustomer($customerId = null, $fields = array())
deleteCustomer($customerId = null)
listCustomers($data = array())
createCard($customerId = null, $card = null)
retrieveCard($customerId = null, $cardId = null)
updateCard($customerId = null, $cardId = null, $data = array())
deleteCard($customerId = null, $cardId = null)
listCards($customerId = null, $data = array())
createSubscription($customerId = null, $subscription = null)
retrieveSubscription($customerId = null, $subscriptionId = null)
updateSubscription($customerId = null, $subscriptionId = null, $data = array())
cancelSubscription($customerId = null, $subscriptionId = null)
listSubscriptions($customerId = null, $data = array())
createPlan($data = array())
retrievePlan($planId = null)
updatePlan($planId = null, $data = array())
deletePlan($planId = null)
listPlans($data = array())
createCoupon($data = array())
retrieveCoupon($couponId = null)
deleteCoupon($couponId = null)
listCoupons($data = array())
deleteCustomerDiscount($customerId = null)
deleteSubscriptionDiscount($customerId = null, $subscriptionId = null)
retrieveInvoice($invoiceId = null)
retrieveInvoiceLine($invoiceId = null, $data = array())
createInvoice($customerId = null, $data = array())
payInvoice($invoiceId = null)
updateInvoice($invoiceId = null, $data = array())
listInvoices($customerId = null, $data = array())
retrieveUpcomingInvoice($customerId = null, $subscriptionId = null)
createInvoiceItem($customerId = null, $data = array())
retrieveInvoiceItem($invoiceItemId = null)
updateInvoiceItem($invoiceItemId = null, $data = array())
deleteInvoiceItem($invoiceItemId = null)
listInvoiceItems($data = array())
updateDispute($chargeId = null, $data = array())
closeDispute($chargeId = null)
createTransfer($recipientId = null, $data = array())
retrieveTransfer($transferId = null)
updateTransfer($transferId = null, $data = array())
cancelTransfer($transferId = null)
listTransfers($data = array())
createCardToken($card = null, $customerId = null)
createBankAccountToken($bankAccount = null)
retrieveToken($tokenId = null)
createRecipient($data)
retrieveRecipient($recipientId = null)
updateRecipient($recipientId = null, $fields = array())
deleteRecipient($recipientId = null)
listRecipients($data = array())
retrieveApplicationFee($applicationFeeId = null)
refundApplicationFee($applicationFeeId = null)
listApplicationFees($data = array())
retrieveAccount()
retrieveBalance()
retrieveBalanceTransaction($transactionId = null)
listBalanceHistory($data = array())
retrieveEvent($eventId = null)
listEvents($data = array())
```


## LICENSE
MIT









