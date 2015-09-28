---
title: eDNA API Reference

language_tabs:
  - json: JSON

toc_footers:
  - <a href='http://www.identitymindglobal.com/'>IdentityMind Global Home</a>
  - eDNA API Reference Beta v1.1.5

includes:	
  - PaymentTransaction
  - TransactionMonitoring
  - KYCmerchant
  - KYCconsumer
  - LoginAnnotation
  - reference

search: true

---

# eDNA 1.20 API

#### Transaction Evaluation

The IdentityMind Engine exports a REST based Web Service interface over HTTPS, using JSON to encode service request and response data.

A typical merchant / IdentityMind interaction to validate a transaction is shown below:

![](http://i.imgur.com/v9qj1DP.png)

#### Authentication

IdentityMind uses an SSL Server certificate for the client to authenticate the service.  The merchant is authenticated using HTTP basic authentication (over HTTPS) via a merchant name and password/license key that is supplied when the merchant registers for the service.

#### Testing in Different Environments

To test using different environments, replace `https://edna.identitymind.com` with the relevant URL. For example, to send a Payment Transaction to the Sandbox environment, use `https://sandbox.identitymind.com/im/transaction`, or to send a transaction to Staging, use `https://staging.identitymind.com/im/transaction`.

<link rel="icon" href="http://www.identitymindglobal.com/wp-content/uploads/2013/05/Favicon.png" type="image/png">