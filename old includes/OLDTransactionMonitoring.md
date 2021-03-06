# Transaction Monitoring

The evidence is the account transfer transaction data to be evaluated. It is supplied in the body of the HTTP-POST as JSON-encoded key value pairs. While all fields are not required, validation evaluation is more comprehensive when richer evidence is provided. 

#### Arguments

The following URLs are used for account transaction validation:

Validate an external transfer (deposit) into an account:  
`POST https://edna.identitymind.com/im/account/transferin`

Validate an internal transfer between accounts:  
`POST https://edna.identitymind.com/im/account/transfer`

Validate an external transfer (withdrawal) from an account:  
`POST https://edna.identitymind.com/im/account/transferout`

```code
EXAMPLE SERVICE REQUEST
```
```json
{ 
  "man" : "jdinh",
  "soc" : "facebook",
  "tea" : "james@gmail.com",
  "bc" : "Palo Alto",
  "bco" : "US",
  "bfn" : "James",
  "bln" : "Dinh",
  "bz" : "55555",
  "bs" : "CA",
  "bsn" : "123 anystreet",
  "dft" : "BC",
  "dfp" : "1872ABCD129E…",
  "ip" : "69.181.162.146",
  "tid" : "89",
  "pbc" : "792019bcc…",
  "ptoken"  : "356007XXXXXX000e",
  "dpbc" : "8ad0e8859…",
  "dptoken"  : "517074XXXXXX000e"
}
```
```code
EXAMPLE SERVICE RESPONSE DATA
```
```json
{ 
  "res" : "ACCEPT",
  "erd" : "Validated User",
  "tid" : "89",
  "rcd" : "1000,100,110,151,120",
  "frn" : "Fallthrough",
  "usc" : 43,
  "umrs":1372723453000,
  "ufs":1372101668000,
  "frd":"User is trusted and no fraud rules were triggered."
}

{
  "res" : "ERROR",
  "error_message" : "Bad data format:Failed to parse the date string provided in the data.  Please use ISO 8601 format."
}
```
> The response includes detailed result codes and the transaction unique identifier. The most important part of the response is whether the transaction is to be accepted, denied, or scheduled for manual review, which is dependent on the configured validation policy. The keys are fully defined in *Appendix A: Result Keys and Codes*.

	<br>
	<table>
		<tr>
			<th colspan=2>User Account</th>
		</tr>
		<tr>
			<th>Key</th>
			<th>Description</th>
		</tr>
		<tr>
			<td>man</td>
			<td>Free form unique identifier for the account at this merchant. Maximum length is 60 characters.<br><br><i>Optional</i></td>
		</tr>
		<tr>
			<td>tea</td>
			<td>Email address on record. An email address that the merchant is comfortable using to validate access to the account. Maximum length is 60 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>soc</td>
			<td>Indicates that the provided email address is associated with a social networking site, and is used for Oauth authentication. The following values are recommended:
				<ul type="disc">
					<li><code>facebook</code></li>
					<li><code>google</code></li>
					<li><code>twitter</code></li>
					<li><code>yahoo</code></li>
				</ul>
			Maximum length is 60 characters.
			<td>No</td>
		</tr>
		<tr>
			<td>ph</td>
			<td>Home phone on record. A landline phone number that the merchant is comfortable using to validate access to the account. Maximum length is 60 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>pm</td>
			<td>Mobile phone on record. A mobile phone number that the merchant is comfortable using to validate access to the account. Maximum length is 60 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>hiv</td>
			<td>The account is a high value account</td>
			<td>No</td>
		</tr>
		<tr>
			<td>clat</td>
			<td>The current latitude of the customer, specified in decimal degrees. Encoded as a string (e.g. <code>"clat":"37.4419"</code>)</td>
			<td>No</td>
		</tr>
		<tr>
			<td>clong</td>
			<td>The current longitude of the customer, specified in decimal degrees. Encoded as a string (e.g. <code>"clong":"-122.1419"</code>)</td>
			<td>No</td>
		</tr>


		<tr>
			<th colspan=3>Billing Address</th>
		</tr>
		<tr>
			<td>bfn</td>
			<td>First name associated with the payment/funding account. Maximum length is 30 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>bln</td>
			<td>Last name associated with the payment/funding account. Maximum length is 50 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>bsn</td>
			<td>Street address associated with the payment/funding account. Maximum length is 100 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>bc</td>
			<td>City associated with the payment/funding account. Data truncates to 30 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>bs</td>
			<td>State associated with the payment/funding account Maximum length is 30 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>bz</td>
			<td>Zip code associated with the payment/funding account. Maximum length is 20 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>bco</td>
			<td>Country associated with the payment/funding account. Maximum length is three characters.</td>
			<td>No</td>
		</tr>


		<tr>
			<th colspan=3>Device</th>
		</tr>
		<tr>
			<td>ip</td>
			<td>The IP address of the client as observed by the merchant.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dfp</td>
			<td>Device fingerprint blob. The interpretation of this blob is specified by the value of the <code>dft</code> attribute.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dft</td>
			<td>Device fingerprint type. Specifies the technology that was used to generate the blob.
				<ul type="disc">
					<li><code>BC</code> - BlueCava</li>
				</ul>
			Default is <code>BC</code></td>
			<td>No</td>
		</tr>
		<tr>
			<td>dts</td>
			<td>Third party service device token and scheme identifier. Contact IdentityMind for detailed format information.</td>
			<td>No</td>
		</tr>


		<tr>
			<th colspan=3>Payment</th>
		</tr>
		<tr>
			<td>pccn</td>
			<td>Credit/debit card unique identifier (hash) while obscuring actual number. IdentityMind will supply procedure to generate hash.
			<br><br>
			<b>Note</b>: The hash must be of the full card number, not a masked or tokenized representation. Maximum length is 128 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>pcct</td>
			<td>A masked or tokenized version of the credit card number. Maximum length is 64 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>phash</td>
			<td>Acount unique identifier (hash) while obscuring actual number. This is used when IdentityMind does not natively support the payment type.
			<br><br>
			<b>Note</b>: The hash must be of the full account number, not a masked or tokenized representation. Maximum length is 128 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>pbc</td>
			<td>Hash of the unique identifier for a Bitcoin wallet. Maximum length is 128 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>pach</td>
			<td>Hash of the unique identifier for an ACH account.
			<br><br>
			<b>Note</b>: The hash must be of the full card number, not a masked or tokenized representation. Maximum length is 128 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>ptoken</td>
			<td>A masked or tokenized version of the account token. This attribute is used in conjunction with <code>phash</code>, <code>pbc</code>, and <code>pach</code>. Maximum length is 64 characters.</td>
			<td>No</td>
		</tr>


		<tr>
			<th colspan=3>Transaction</th>
		</tr>
		<tr>
			<td>tti</td>
			<td>The date and time of the transaction as processed by the merchant. Expressed in UTC encoded as a UNIX timestamp.
				<ul type="disc">
					<li><code>"tti":1293887536</code></li>
					<li><code>"tti":"1293887536"</code></li>
				</ul>
			</td>
			<td>No</td>
		</tr>
		<tr>
			<td>tid</td>
			<td>Merchant unique identifier for the transaction. eDNA assigns an internal ID if none provided. The transaction ID must be encoded as a string (e.g. <code>"tid":"123455"</code>). Maximum length is 40 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>aflid</td>
			<td>The affiliate ID associated with this transaction. Encoded as a string. Maximum length is 100 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>aflsd</td>
			<td>The affiliate signup/creation date associated with this transaction. Either an ISO 8601 encoded string or UNIX timestamp.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>memo</td>
			<td>Free form text memo field</td>
			<td>No</td>
		</tr>


		<tr>
			<th colspan=3>Transfer Destination</th>
		</tr>
		<tr>
			<td>dman</td>
			<td>Free form unique identifier for the destination account at this merchant</td>
			<td>No</td>
		</tr>
		<tr>
			<td>demail</td>
			<td>Email address associated with the destination account</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dph</td>
			<td>Phone number associated with the destination account</td>
			<td>No</td>
		</tr>
		<tr>
			<td>amt</td>
			<td>If this transaction is a transfer, the amount being transferred.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>ccy</td>
			<td>If this transaction is a transfer, the currency of the <code>amt</code> field being transferred. Maximum length is three characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dpccn</td>
			<td>Unique identifier (hash) of the destination credit card while obscuring the actual number. IdentityMind will supply procedure to generate hash.
			<br><br>
			<b>Note</b>: The hash must be of the full card number, not a masked or tokenized representation.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dpcct</td>
			<td>A masked or tokenized version of the credit card number. IdentityMind will supply procedure to generate token.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dpppi</td>
			<td>Destination PayPal Payer ID</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dpppe</td>
			<td>Destination PayPal Payer email</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dpbc</td>
			<td>Hash of the unique identifier for the destination Bitcoin wallet ID</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dpach</td>
			<td>Hash of the unique identifier of the destination ACH account
			<br><br>
			<b>Note</b>: The hash must be of the full card number, not a masked or tokenized representation.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dphash</td>
			<td>Unique identifier (hash) of the destination payment instrument while obscuring actual number. This is used when IdentityMind does not natively support the payment type.
			<br><br>
			<b>Note</b>: The hash must be of the full account number, not a masked or tokenized representation.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>dptoken</td>
			<td>A masked or tokenized version of the destination payment instrument number. IdentityMind will supply procedure to generate token. This field is used in conjunction with <code>dpbc</code>, <code>dpach</code>, and <code>dptoken</code>.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>sfn</td>
			<td>The first name of the recipient. Maximum length is 30 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>sln</td>
			<td>THe last name of the recipient. Maximum length is 50 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>ssn</td>
			<td>The recipient street address (e.g. "123 Main St"). Maximum length is 100 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>sc</td>
			<td>The recipient city. Data truncates to 30 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>ss</td>
			<td>The recipient state. Maximum length is 30 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>sz</td>
			<td>The recipient zip code. Maximum length is 20 characters.</td>
			<td>No</td>
		</tr>
		<tr>
			<td>sco</td>
			<td>ISO 3166 country code of the recipient address of the transaction, encoded as a string. Default is <code>US</code>. Maximum length is three characters.</td>
			<td>No</td>
		</tr>
	</table>