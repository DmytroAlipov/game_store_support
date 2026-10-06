## Customer Request Handler

<img width="1714" height="655" alt="Request_Handler" src="https://github.com/user-attachments/assets/2849f8aa-945b-49cf-95f6-6b2ba62f47e9" />

[`handle_customer_request.json`](./handle_customer_request.json) is a standalone
n8n workflow that turns a customer message into a short support summary, sends
the request to the support inbox, and records it in Google Sheets.

### Flow

1. Receives an HTTP `POST` request at the `customer-request` webhook.
2. Uses OpenAI to summarize the message and relevant customer
   details. The prompt instructs the model not to invent information.
3. Sends an email to the configured support address.
4. Appends a row to the `Customers` sheet.
5. Returns a JSON response containing `success` and the generated `summary`.

The email includes the summary, customer name and email, original message, and
serialized customer data. The sheet columns are `Name`, `Email`, `Message`,
`Summary`, `User Data`, and `Created At`.

### Setup

1. Import the JSON file into n8n.
2. Configure the OpenAI credential used by the AI node.
3. Configure the SMTP credential and change `support@example.com` to the
   support team's inbox.
4. Configure the Google Sheets credential, replace `REPLACE_GOOGLE_SHEET_ID`
   with the spreadsheet ID, and ensure it has a `Customers` tab with the
   columns listed above.
5. Save and test the workflow, then activate it to use its production webhook
   URL.

The exported workflow contains placeholder credential IDs. Select or create
the appropriate credentials in your n8n instance; do not rely on the IDs from
the export.

### Request

Send JSON with a `message` and optional customer `user` object. Both fields can
be nested under `body` (for example, when forwarded from another webhook) or
provided at the top level:

```json
{
  "message": "I need help with my order",
  "user": {
    "name": "Dima",
    "email": "dima@example.com",
    "orderId": "ORDER-1234567"
  }
}
```


Example request (replace the URL with the webhook URL shown by n8n):

```sh
curl -X POST "https://your-n8n-host/webhook/customer-request" \
  -H "Content-Type: application/json" \
  -d '{"message":"I need help with my order","user":{"name":"Alex","email":"alex@example.com"}}'
```

Successful runs return a response in this shape:

```json
{
  "success": true,
  "summary": "The customer is requesting help with an order."
}
```
