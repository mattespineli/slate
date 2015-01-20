# Feedback: Final Payment Transaction Result

## Arguments

The following URLs are used to notify IdentityMind of the acceptance or rejection of the transaction that was previously analyzed with the given transaction ID by the merchant's payment gateway or the merchant themselves. All arguments are optional. The transaction ID is part of the URL.

### Bank Authorization Feedback

[https://edna.identitymind.com/im/transaction/<transaction_ID>/bank-accepted](https://edna.identitymind.com/im/transaction/<transaction_ID>/bank-accepted)

[https://edna.identitymind.com/im/transaction/<transaction_ID>/bank-rejected](https://edna.identitymind.com/im/transaction/<transaction_ID>/bank-rejected)

### Merchant Final Resolution Feedback

[https://edna.identitymind.com/im/transaction/<transaction_ID>/accepted](https://edna.identitymind.com/im/transaction/<transaction_ID>/accepted)

[https://edna.identitymind.com/im/transaction/<transaction_ID>/rejected](https://edna.identitymind.com/im/transaction/<transaction_ID>/rejected)

[https://edna.identitymind.com/im/transaction/<transaction_ID>/rejected-ok](https://edna.identitymind.com/im/transaction/<transaction_ID>/rejected-ok) 

[https://edna.identitymind.com/im/transaction/<transaction_ID>/accepted-user-validated](https://edna.identitymind.com/im/transaction/<transaction_ID>/accepted-user-validated)

[https://edna.identitymind.com/im/transaction/<transaction_ID>/rejected-user-failed-validation](https://edna.identitymind.com/im/transaction/<transaction_ID>/rejected-user-failed-validation)

[https://edna.identitymind.com/im/transaction/<transaction_ID>/accepted-default](https://edna.identitymind.com/im/transaction/<transaction_ID>/accepted-default) 

[https://edna.identitymind.com/im/transaction/<transaction_ID>/rejected-default](https://edna.identitymind.com/im/transaction/<transaction_ID>/rejected-default)

**Note**: The transaction may be a payment transaction or an account transfer.

```code
EXAMPLE SERVICE REQUEST

{
  “auth_code”: “T1627H”,
  “auth_response_text”: “Decline”,
  “avs_result”: “Y”,
  “error_code”: “05”
}
```

> The response contains a JSON encoded message or error message:

```code
EXAMPLE SERVICE RESPONSE DATA

{
  “message”: “Feedback accepted for ACCEPT feedback on transaction 42”
}
```

	<table>		
		<tr>
			<th>Key</th>
			<th>Description</th>
			<th>Required</th>
		</tr>
		<tr>
			<td>auth_response</td>
			<td>Whether the gateway accepted or rejected the transaction</td>
			<td>No</td>
		</tr>
		<tr>
			<td>error_code</td>
			<td>The error code fields from the authorization request as expressed by the gateway</td>
			<td>No</td>
		</tr>
		<tr>
			<td>auth_response_text</td>
			<td>Auth comments from the gateway</td>
			<td>No</td>
		</tr>
		<tr>
			<td>reason</td>
			<td>Free-form descriptive text providing additional information about the feedback</td>
			<td>No</td>
		</tr>
		<tr>
			<td>avs_result</td>
			<td>The AVS response code from the gateway</td>
			<td>No</td>
		</tr>
		<tr>
			<td>cvv2_result</td>
			<td>The CVV2 response code from the gateway</td>
			<td>No</td>
		</tr>
		<tr>
			<td>gateway</td>
			<td>The name of the payment gateway used. This information is used to interpret the result/error codes. Currently, we support:
				<ul type="disc">
					<li>"MES" - Merchant e-Solutions</li>
					<li>"GC" - Google Checkout</li>
					<li>"PPP" - PayPal Pro</li>
					<li>"PFP" - Pay Flow Pro</li>
					<li>"CDP" - Centro de Pagos</li>
					<li>"commerce" - CommerceGate</li>
					<li>"DHD" - DHD Media</li>
					<li>"IDM" - IDMPay</li>
					<li>"SC" - Safe Charge</li>
					<li>"AUTH" - Auth.net</li>
					<li>"INTERAC" - Interac</li>
					<li>"generic" - See <i>Appendix C: Generic Gateway Codes</i></li>
				</ul>
			<b>Note</b>: While this field is required, backwards compatibility feedback will not be rejected if not present, but will instead be interpreted as MES gateway data. </td>
			<td>No</td>
		</tr>
		<tr>
			<td>auth_code</td>
			<td>Returned authorization code</td>
			<td>No</td>
		</tr>
		<tr>
			<td>bank_status</td>
			<td>The status of the transaction at the gateway/bank:
				<ul type="disc">
					<li>"a" - auth_only</li>
					<li>"c" - captured</li>
					<li>"d" - declined</li>
					<li>"v" - void</li>
					<li>"r" - refund</li>
					<li>"b" - chargeback</li>
					<li>"u" - unknown</li>
				</ul>
			Default is "u"</td>
			<td>No</td>
		</tr>
	</table>