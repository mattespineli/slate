# Transaction Monitoring

Evaluate a transfer between accounts, a withdrawal/transfer-out from an account, or funding/deposit/transfer-in to an account.

Validate an internal transfer between accounts:<br>
`POST https://edna.identitymind.com/im/account/transfer`

Validate an external transfer (deposit) into an account:<br>
`POST https://edna.identitymind.com/im/account/transferin`

Validate an external transfer (withdrawal) out of an account:<br>
`POST https://edna.identitymind.com/im/account/transferout`

<aside class="notice">Not all fields are required, but anti-fraud evaluation is more comprehensive when richer evidence is provided.</aside>

##### Arguments

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

<table>
		<tr>
			<th colspan=2>Account Transfer Data</th>
		</tr>
		<tr>
			<th>Parameter</th>
			<th>Description</th>
		</tr>
		<tr>
			<td>dman<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The destination account name</td>
		</tr>
		<tr>
			<td>demail<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The email address associated with the destination account</td>
		</tr>
		<tr>
			<td>dph<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The phone number associated with the destination account</td>
		</tr>
		<tr>
			<td>dpccn<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Destination credit card unique identifier (hash). IdentityMind will supply procedure to generate hash.<br><br>
			<b>Note</b>: The hash must be of the full card number, not a masked or tokenized representation.<br><br>Maximum length is 128 characters</td>
		</tr>
		<tr>
			<td>dpcct<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>A masked or tokenized version of the destination credit card number. IdentityMind will supply procedure to generate token.<br><br>Maximum length is 64 characters</td>
		</tr>
		<tr>
			<td>dpppi<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Destination PayPal Payer ID</td>
		</tr>
		<tr>
			<td>dpppe<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Destination PayPal Payer Email</td>
		</tr>
		<tr>
			<td>dphash<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Destination generic payment account unique identifier (hash). This is used when IdentityMind does not natively support the payment type.<br><br>
			If the payment instrument is Skrill, this will be a hash of the Skrill account email address.
			<br><br>			
			<b>Note</b>: The hash must be of the full account number, not a masked or tokenized representation<br><br>Maximum length is 128 characters</td>
		</tr>
		<tr>
			<td>dptoken<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>A masked or tokenized version of the destination account token
			<br><br>If the payment instrument is Skrill, the ptoken should follow the format <code>skrill:emailaddress</code>. For example, <code>skrill:johndoe@gmail.com</code>.			
			<br><br>Maximum length is 64 characters</td>
		</tr>
		<tr>
			<td>dpach<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Destination ACH account unique identifier (hash)<br><br>
			<b>Note</b>: The hash must be of the full account number, not a masked or tokenized representation<br><br>Maximum length is 128 characters</td>
		</tr>
		<tr>
			<td>dpbc<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Hash of the unique identifier for a destination Bitcoin wallet<br><br>Maximum length is 128 characters</td>
		</tr>
		<tr>
			<td>moto<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The MOTO/ECI (Electronic Commerce Indicator) indicator describes the type of eCommerce transaction that is taking place. 
				<ul type="disc">
					<li><code> </code> - (space) card present</li>
					<li><code>1</code> - MOTO: Single Transaction mail / telephone order</li>
					<li><code>2</code> - MOTO: Recurring Transaction</li>
					<li><code>3</code> - MOTO: Installment Payment</li>
					<li><code>4</code> - MOTO: Deferred Transaction</li>
					<li><code>5</code> - ECI: 3-D Secure Electronic Commerce Transaction</li>
					<li><code>6</code> - ECI: 3-D Secure Non-Authenticated Electronic Commerce Transaction</li>
					<li><code>7</code> - ECI: Channel Encrypted Transaction</li>
					<li><code>8</code> - ECI: Non-Secure Electronic Commerce Transaction</li>
				</ul>
				The default is <code>7</code> if the field is not supplied.		
			</td>
		</tr>
		<tr>
			<td>amt<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Transaction amount</td>
		</tr>
		<tr>
			<td>ccy<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>ISO 4217 currency code<br><br>Maximum length is 3 characters</td>
		</tr>
		<tr>
			<td>m<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Reflects the merchant's <code>merchantAPIname</code> that was assigned on account creation</td>
		</tr>
		<tr>
			<td>tid<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Transaction identifier. If not provided, an ID will be allocated<br><br>Maximum length is 40 characters</td>
		</tr>
		<tr>
			<td>man<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Account name for the user<br><br>Maximum length is 60 characters</td>
		</tr>
		<tr>
			<td>tea<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Email address for the user<br><br>Maximum length is 60 characters</td>
		</tr>
		<tr>
			<td>soc<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>OAuth service that authenticated the user. For example, <code>google</code> or <code>facebook</code></td>
		</tr>
		<tr>
			<td>ip<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Customer's IP address<br><br>Maximum length is 40 characters</td>
		</tr>
		<tr>
			<td>dfp<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Device fingerprint blob</td>
		</tr>
		<tr>
			<td>dft<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Device fingerprint type</td>
		</tr>
		<tr>
			<td>tti<br><font color=#446CB3>Object</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Transaction time in UTC. Encoded as a Unix timestamp or ISO 8601 string. Data containing milliseconds will not be accepted.</td>
		</tr>
		<tr>
			<td>bfn<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Billing (source) first name<br><br>Maximum length is 30 characters</td>
		</tr>
		<tr>
			<td>bln<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Billing (source) last name<br><br>Maximum length is 50 characters</td>
		</tr>
		<tr>
			<td>pccn<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Credit Card unique identifier (Hash). IdentityMind will supply procedure to generate hash.<br><br> 
			<b>Note</b>: The hash must be of the full card number, not a masked or tokenized representation.<br><br>Maximum length is 128 characters</td>
		</tr>
		<tr>
			<td>pcct<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>A masked or tokenized version of the credit card number. IdentityMind will supply procedure to generate token.<br><br>Maximum length is 64 characters</td>
		</tr>
		<tr>
			<td>pcty<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The card type. Possible values are:
				<ul type="disc">
					<li><code>CREDIT</code></li>
					<li><code>DEBIT</code></li>
					<li><code>PREPAID</code></li>
					<li><code>UNKNOWN</code></li>
				</ul>
		</tr>
		<tr>
			<td>phash<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Generic payment account unique identifier (Hash). This is used when IdentityMind does not natively support the payment type.<br><br>
			If the payment instrument is Skrill, this will be a hash of the Skrill account email address.
			<br><br>
			<b>Note</b>: The hash must be of the full account number, not a masked or tokenized representation.<br><br>Maximum length is 128 characters</td>
		</tr>
		<tr>
			<td>ptoken<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>A masked or tokenized version of the account token.
			<br><br>If the payment instrument is Skrill, the ptoken should follow the format <code>skrill:emailaddress</code>. For example, <code>skrill:johndoe@gmail.com</code>.			
			<br><br>Maximum length is 64 characters</td>
		</tr>
		<tr>
			<td>profile<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The policy profile to be used to evaluate this transaction. If no profile is specified, the DEFAULT profile is used. Prior to IDMRisk 1.19, this was encoded in the <code>smid</code> field.</td>
		</tr>
		<tr>
			<td>smna<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td><font color=#D91E18>Deprecated</font><br><br>The user-friendly name for the merchant for whom this transaction is being processed. Used for display purposes in the UI.</td>
		</tr>
		<tr>
			<td>smid<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td><font color=#D91E18>Deprecated</font><br><br>A unique identifier for the merchant for whom this transaction is being processed. Succeeded by the <code>profile</code> field in IDMRisk 1.19.</td>
		</tr>
		<tr>
			<td>bsn<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Billing (source) street. Includes house number, street name, and apartment number.<br><br>Maximum length is 100 characters</td>
		</tr>
		<tr>
			<td>bco<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Billing (source) country. ISO 3166-1 alpha-2 country code of the billing address of the transaction. Default is <code>US</code>.<br><br>Maximum length is 2 characters</td>
		</tr>
		<tr>
			<td>bz<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Billing (source) zip / postal code<br><br>Maximum length is 20 characters</td>
		</tr>
		<tr>
			<td>bc<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Billing (source) city<br><br>Data truncates to 30 characters</td>
		</tr>
		<tr>
			<td>bs<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Billing (source) state<br><br>Maximum length is 30 characters</td>
		</tr>
		<tr>
			<td>sfn<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Shipping (destination) first name<br><br>Maximum length is 30 characters</td>
		</tr>
		<tr>
			<td>sln<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Shipping (destination) last name<br><br>Maximum length is 50 characters</td>
		</tr>
		<tr>
			<td>ssn<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Shipping (destination) street. Includes house number, street name, and apartment number.<br><br>Maximum length is 100 characters</td>
		</tr>
		<tr>
			<td>sco<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Shipping (destination) country. ISO 3166-1 alpha-2 country code of the billing address of the transaction. Default is <code>US</code>.<br><br>Maximum length is 2 characters</td>
		</tr>
		<tr>
			<td>sz<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Shipping (destination) zip / postal code<br><br>Maximum length is 20 characters</td>
		</tr>
		<tr>
			<td>sc<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Shipping (destination) city<br><br>Data truncates to 30 characters</td>
		</tr>
		<tr>
			<td>ss<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Shipping (destination) state<br><br>Maximum length is 30 characters</td>
		</tr>
		<tr>
			<td>aflid<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Affiliate ID. The client specific identifier for the affiliate that generated this transaction.<br><br>Maximum length is 100 characters</td>
		</tr>
		<tr>
			<td>aflsd<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The signup/affiliate creation date of the affiliate associated with this transaction. Either an ISO 8601 encoded string or a Unix timestamp.</td>
		</tr>
		<tr>
			<td>blg<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Customer browser language. Values are defined in ISO 639-1.</td>
		</tr>
		<tr>
			<td>clat<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Customer latitude</td>
		</tr>
		<tr>
			<td>clong<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Customer longitude</td>
		</tr>
		<tr>
			<td>phn<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Customer primary phone number<br><br>Maximum length is 60 characters</td>
		</tr>
		<tr>
			<td>pm<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Customer mobile phone number<br><br>Maximum length is 60 characters</td>
		</tr>
		<tr>
			<td>pw<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Customer work phone number<br><br>Maximum length is 60 characters</td>
		</tr>
		<tr>
			<td>pach<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>ACH account unique identifier (hash)<br><br>
			<b>Note</b>: The hash must be of the full account number, not a masked or tokenized representation</td>
		</tr>
		<tr>
			<td>pbc<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Hash of the unique identifier for a Bitcoin wallet</td>
		</tr>
		<tr>
			<td>memo<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Free-form memo field for client use.<br><br>
			<code>memo</code> and <code>memo1</code>-<code>memo40</code> are available for use as custom fields. These custom fields are viewable, searchable, sortable, and can be labelled using the IdentityMind UI.<br><br>For example, you can send SKU through <code>memo1</code>, Quantity through <code>memo2</code>, and Region through <code>memo3</code>.
			</td>
		</tr>
	</table>

##### Response

```code
EXAMPLE SERVICE RESPONSE DATA
```
```json
    {
        "arpr": "DISABLED",
        "ednaScoreCard": {
            "ar": {
                "result": "DISABLED"
            },
            "er": {
                "reportedRule": {
                    "description": "Rule2360_RULE_DESC",
                    "details": "[Fired] ed:35(false) = false",
                    "name": "DUPTRANSACTION",
                    "resultCode": "MANUAL_REVIEW",
                    "ruleId": 2360,
                    "testResults": [
                        {
                            "details": "[Fired] ed:35(false) = false",
                            "fired": true,
                            "test": "ed:35"
                        }
                    ]
                }
            },
            "etr": [
                {
                    "details": "ed:34(true) = false",
                    "fired": false,
                    "test": "ed:34"
                },
                {
                    "details": "ed:32(true) = false",
                    "fired": false,
                    "test": "ed:32"
                },
                {
                    "details": "ed:36(true) = false",
                    "fired": false,
                    "test": "ed:36"
                },
                {
                    "details": "ed:1(true) = false",
                    "fired": false,
                    "test": "ed:1"
                },
                {
                    "details": "ed:2(true) = false",
                    "fired": false,
                    "test": "ed:2"
                },
                {
                    "details": "ed:56(true) = false",
                    "fired": false,
                    "test": "ed:56"
                },
                {
                    "details": "[Fired] ed:35(false) = false",
                    "fired": true,
                    "test": "ed:35"
                },
                {
                    "details": "USD",
                    "fired": false,
                    "test": "ed:42"
                },
                {
                    "details": "USD",
                    "fired": false,
                    "test": "ed:42"
                },
                {
                    "details": "ed:33(true) = false",
                    "fired": false,
                    "test": "ed:33"
                },
                {
                    "details": "ed:37(true) = false",
                    "fired": false,
                    "test": "ed:37"
                }
            ],
            "sc": [
               {
                    "details": "ed:37(true) = false",
                    "fired": false,
                    "test": "ed:37"
                }
            ]
        },
        "erd": "New card, neither device nor user account information supplied",
        "frd": "[Fired] ed:35(false) = false",
        "frn": "DUPTRANSACTION",
        "frp": "MANUAL_REVIEW",
        "rcd": "190,202,2360,131,536,150,121",
        "res": "MANUAL_REVIEW",
        "tid": "5200016",
        "upr": "UNKNOWN",
        "user": "UNKNOWN"
    }
```
> The response includes detailed result codes and the transaction unique identifier. The most important part of the response is whether the transaction is to be accepted, denied, or scheduled for manual review, which is dependent on the configured validation policy.

<table>
		<tr>
			<th colspan=2>Transaction Response Data</th>
		</tr>
		<tr>
			<th>Parameter</th>
			<th>Description</th>
		</tr>
		<tr>
			<td>user<br><font color=#446CB3>EDNAPolicyResult</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The current reputation of the user. Possible values are:
				<ul type="disc">
					<li><code>TRUSTED</code></li>
					<li><code>UNKNOWN</code></li>
					<li><code>SUSPICIOUS</code></li>
					<li><code>BAD</code></li>
				</ul></td>
		</tr>
		<tr>
			<td>erd<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>A description of the reason for the user's reputation</td>
		</tr>
		<tr>
			<td>upr<br><font color=#446CB3>EDNAPolicyResult</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The previous reputation of the user when they were last evaluated. Possible values are:
				<ul type="disc">
					<li><code>TRUSTED</code></li>
					<li><code>UNKNOWN</code></li>
					<li><code>SUSPICIOUS</code></li>
					<li><code>BAD</code></li>
				</ul></td>
		</tr>
		<tr>
			<td>res<br><font color=#446CB3>FraudPolicyResult</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Result of policy evaluation. Combines the result of fraud and automated review evaluations. Possible values are:
			<ul type="disc">
					<li><code>ACCEPT</code></li>
					<li><code>MANUAL_REVIEW</code></li>
					<li><code>DENY</code></li>
				</ul></td>
		</tr>
		<tr>
			<td>rcd<br><font color=#446CB3>string</font></td>
			<td>The set of result codes from the evaluation of the current transaction</td>
		</tr>
		<tr>
			<td>tid<br><font color=#446CB3>string</font></td>
			<td>The transaction ID</td>
		</tr>
		<tr>
			<td>frn<br><font color=#446CB3>string</font></td>
			<td>The name of the fraud rule that fired</td>
		</tr>
		<tr>
			<td>frp<br><font color=#446CB3>FraudPolicyResult</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Result of fraud evaluation. Possible values are:
			<ul type="disc">
					<li><code>ACCEPT</code></li>
					<li><code>MANUAL_REVIEW</code></li>
					<li><code>DENY</code></li>
				</ul></td>
		</tr>
		<tr>
			<td>frd<br><font color=#446CB3>string</font></td>
			<td>The description of the fraud rule that fired</td>
		</tr>
		<tr>
			<td>arpr<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Result of the automated review evaluation. Possible values are:
			<ul type="disc">
					<li><code>ERROR</code></li>
					<li><code>NO_POLICY</code></li>
					<li><code>DISABLED</code></li>
					<li><code>FILTERED</code></li>
					<li><code>PENDING</code></li>
					<li><code>FAIL</code></li>
					<li><code>INDETERMINATE</code></li>
					<li><code>SUCCESS</code></li>
				</ul></td>
		</tr>
				<tr>
			<td>arpd<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The description, if any, of the automated review rule that fired</td>
		</tr>
		<tr>
			<td>arpid<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The ID, if any, of the automated review rule that fired</td>
		</tr>
		<tr>
			<td>usc<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>User seen count</td>
		</tr>
		<tr>
			<td>ednaScoreCard<br><font color=#446CB3>ExternalizedTransactionScorecard</font></td>
			<td>The score card for the current transaction</td>
		</tr>
		<tr>
			<th colspan=2>Externalized Transaction Score Card</th>
		</tr>
		<tr>
			<td>ar<br><font color=#446CB3>AutomatedReviewEngineResult</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The result of the automated review policy for this transaction</td>
		</tr>
		<tr>
			<td>etr<br><font color=#446CB3>array[ConditionResult]</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The evaluated test results for this transaction</td>
		</tr>
		<tr>
			<td>sc<br><font color=#446CB3>array[ConditionResult]</font></td>
			<td>The test results for this transaction</td>
		</tr>
		<tr>
			<td>er<br><font color=#446CB3>ExternalizedEvaluationResult</font></td>
			<td>The result of the fraud policy evaluation for this transaction</td>
		</tr>
		<tr>
			<th colspan=2>Automated Review Engine Result</th>
		</tr>
		<tr>
			<td>result<br><font color=#446CB3>ReviewResult</font></td>
			<td>Result of rule. Possible values are:
				<ul type="disc">
					<li><code>ERROR</code></li>
					<li><code>NO_POLICY</code></li>
					<li><code>DISABLED</code></li>
					<li><code>FILTERED</code></li>
					<li><code>PENDING</code></li>
					<li><code>FAIL</code></li>
					<li><code>INDETERMINATE</code></li>
					<li><code>SUCCESS</code></li>
				</ul></td>
		</tr>
		<tr>
			<td>ruleId<br><font color=#446CB3>string</font></td>
			<td>The unique rule identifier</td>
		</tr>
		<tr>
			<td>ruleName<br><font color=#446CB3>string</font></td>
			<td>The rule name</td>
		</tr>
		<tr>
			<td>ruleDescription<br><font color=#446CB3>string</font></td>
			<td>The rule description</td>
		</tr>
		<tr>
			<th colspan=2>Externalized Evaluation Result</th>
		</tr>
		<tr>
			<td>firedRules<br><font color=#446CB3>List[ExternalizedRule]</font></td>
			<td>The complete set of rules that fired for this transaction</td>
		</tr>
		<tr>
			<td>reportedRule<br><font color=#446CB3>ExternalizedRule</font></td>
			<td>The rule that is being reported for this transaction. Other rules may have fired, see <code>firedRules</code></td>
		</tr>
		<tr>
			<th colspan=2>Externalized Rule</th>
		</tr>
		<tr>
			<td>name<br><font color=#446CB3>string</font></td>
			<td>The rule name</td>
		</tr>
		<tr>
			<td>description<br><font color=#446CB3>string</font></td>
			<td>Details of the evaluation of this rule for the current transaction</td>
		</tr>
		<tr>
			<td>details<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The rule description</td>
		</tr>
		<tr>
			<td>resultCode<br><font color=#446CB3>FraudPolicyResult</font></td>
			<td>Result of rule. Possible values are:
				<ul type="disc">
					<li><code>ACCEPT</code></li>
					<li><code>MANUAL_REVIEW</code></li>
					<li><code>DENY</code></li>
				</ul></td>
		</tr>
		<tr>
			<td>testResults<br><font color=#446CB3>array[ConditionResult]</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The results of the individual assertions of the rule</td>
		</tr>
		<tr>
			<td>ruleId<br><font color=#446CB3>integer</font></td>
			<td>The unique rule identifier</td>
		</tr>
		<tr>
			<th colspan=2>Condition Result</th>
		</tr>
		<tr>
			<td>fired<br><font color=#446CB3>boolean</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Whether the condition fired or not</td>
		</tr>
		<tr>
			<td>test<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>The ID of the security test or the key of the transaction data to which the condition applied</td>
		</tr>
		<tr>
			<td>waitingForData<br><font color=#446CB3>boolean</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Indicates that the result is waiting for an asynchronous response from the customer and/or third party service.</td>
		</tr>
		<tr>
			<td>details<br><font color=#446CB3>string</font><br><font color=#BDC3C7><i>optional</i></font></td>
			<td>Textual result of the condition</td>
		</tr>
	</table>