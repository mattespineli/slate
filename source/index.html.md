---
title: eDNA API Reference

language_tabs:
  - json: JSON

toc_footers:
  - <a href='http://www.identitymindglobal.com/'>IdentityMind Global Home</a>
  - eDNA API Reference Beta v1.1.9

includes:	
  - PaymentTransaction
  - TransactionMonitoring
  - KYCmerchant
  - KYCconsumer
  - LoginAnnotation
  - reference

search: true

---

# eDNA 1.21 API

#### Transaction Evaluation

The IdentityMind Engine exports a REST based Web Service interface over HTTPS, using JSON to encode service request and response data.

A typical merchant / IdentityMind interaction to validate a transaction is shown below:

![](http://i.imgur.com/v9qj1DP.png)

#### Authentication

IdentityMind uses an SSL Server certificate for the client to authenticate the service.  The merchant is authenticated using HTTP basic authentication (over HTTPS) via a merchant name and password/license key that is supplied when the merchant registers for the service.

#### Testing in Different Environments

To test using different environments, replace `https://edna.identitymind.com` with the relevant URL. For example, to send a Payment Transaction to the Sandbox environment, use `https://sandbox.identitymind.com/im/transaction`, or to send a transaction to Staging, use `https://staging.identitymind.com/im/transaction`.

Do <b>not</b> send real data to the Sandbox environment. Likewise, test data should <b>not</b> be sent to the Production environment. The Staging environment can be used for both real and test data. The Staging environment should not be treated as a production system as data sent to Staging is deleted every week.

<aside class="warning">Clear text credit card numbers should <b>never</b> be sent to IdentityMind. Instead, IdentityMind uses a cryptographically secure hash to have a unique representation of each credit card. IdentityMind provides the required utilities to generate these hashes. See <a href="#payment-instrument-hashing">Payment Instrument Hashing</a> for more details.</aside>

<link rel="icon" href="http://www.identitymindglobal.com/wp-content/uploads/2013/05/Favicon.png" type="image/png">