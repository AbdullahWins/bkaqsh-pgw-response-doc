# bKash Formal Sandbox Testing Results

Project: EasyTruck Integration

Tested By: Netro Systems Engineering Team

Date: January 26, 2026

## API Request/Response Documentation

---

### 1. Grant Token API

**API Title:** Grant Token API

**API URL:** `https://tokenized.sandbox.bka.sh/v1.2.0-beta/tokenized/checkout/token/grant`

**Request Headers:**
```json
{
  "username": "sandboxTokenized...",
  "password": "sandboxTokenized...",
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "app_key": "0vWQuCRGiUX7...",
  "app_secret": "jcUNPBgbcq..."
}
```

**API Response:**
```json
{
  "statusCode": "0000",
  "statusMessage": "Successful",
  "id_token": "eyJraWQiOiJvTVJzNU9Z...",
  "token_type": "Bearer",
  "expires_in": 3600,
  "refresh_token": "eyJjdHkiOiJKV1QiLCJl..."
}
```

---

### 2. Create Payment API

**API Title:** Create Payment (Tokenized Checkout)

**API URL:** `https://tokenized.sandbox.bka.sh/v2/tokenized-checkout/payment/create`

**Request Headers:**
```json
{
  "Authorization": "Bearer eyJraWQiOiJvTVJzNU9Z...",
  "x-app-key": "0vWQuCRGiUX7...",
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "mode": "0011",
  "payerReference": "01929918378",
  "callbackURL": "http://localhost:5000/api/v1/bkash/callback",
  "amount": "600.00",
  "currency": "BDT",
  "intent": "sale",
  "merchantInvoiceNumber": "696f6aaa770c18c96e6e53cd",
  "subMerchantName": "EasyTruck"
}
```

**API Response:**
```json
{
  "paymentId": "TR0011PXUbxbT1769405202127",
  "bkashURL": "https://sandbox.payment.bkash.com/?paymentId=TR0011PXUbxbT1769405202127&hash=7T6iG1r!BtaYY62NMD67CBRyzfBSC1X6mBKDoe4LK9n3K9_CR1o-c5rpF.Pl_sgtE7I)agEIrWR_cphPdx2Qb9!yveLLCQ5LHkX51769405202127&mode=0011&apiVersion=v2/",
  "callbackURL": "http://localhost:5000/api/v1/bkash/callback",
  "successCallbackURL": "http://localhost:5000/api/v1/bkash/callback?paymentID=TR0011PXUbxbT1769405202127&status=success&signature=jkRWIzcMdM",
  "failureCallbackURL": "http://localhost:5000/api/v1/bkash/callback?paymentID=TR0011PXUbxbT1769405202127&status=failure&signature=jkRWIzcMdM",
  "cancelledCallbackURL": "http://localhost:5000/api/v1/bkash/callback?paymentID=TR0011PXUbxbT1769405202127&status=cancel&signature=jkRWIzcMdM",
  "amount": "600.00",
  "intent": "sale",
  "currency": "BDT",
  "paymentCreateTime": "2026-01-26T11:26:42:127 GMT+0600",
  "transactionStatus": "Initiated",
  "merchantInvoiceNumber": "696f6aaa770c18c96e6e53cd",
  "signature": "jkRWIzcMdM"
}
```

---

### 3. Execute Payment API

**API Title:** Execute Payment (Tokenized Checkout)

**API URL:** `https://tokenized.sandbox.bka.sh/v2/tokenized-checkout/payment/execute`

**Request Headers:**
```json
{
  "Authorization": "Bearer eyJraWQiOiJvTVJzNU9Z...",
  "x-app-key": "0vWQuCRGiUX7...",
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "paymentId": "TR0011PXUbxbT1769405202127"
}
```

**API Response:**
```json
{
  "paymentId": "TR0011PXUbxbT1769405202127",
  "trxId": "DAQ20OC4BG",
  "transactionStatus": "Completed",
  "amount": "600.00",
  "currency": "BDT",
  "intent": "sale",
  "paymentExecuteTime": "2026-01-26T11:30:00:137 GMT+0600",
  "merchantInvoiceNumber": "696f6aaa770c18c96e6e53cd",
  "subMerchantName": "EasyTruck",
  "payerType": "Customer",
  "payerReference": "01929918378",
  "payerAccount": "01929918378",
  "maxRefundableAmount": "600.00"
}
```

---

### 4. Query Payment Status API (Mandatory)

**API Title:** Query Payment Status

**API URL:** `https://tokenized.sandbox.bka.sh/v2/tokenized-checkout/payment/status`

**Request Headers:**
```json
{
  "Authorization": "Bearer eyJraWQiOiJvTVJzNU9Z...",
  "x-app-key": "0vWQuCRGiUX7...",
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "paymentId": "TR0011PXUbxbT1769405202127"
}
```

**API Response:**
```json
{
  "paymentId": "TR0011PXUbxbT1769405202127",
  "trxId": "DAQ20OC4BG",
  "transactionStatus": "Completed",
  "amount": "600.00",
  "currency": "BDT",
  "intent": "sale",
  "paymentExecuteTime": "2026-01-26T11:30:00:137 GMT+0600",
  "merchantInvoiceNumber": "696f6aaa770c18c96e6e53cd",
  "payerReference": "01929918378",
  "subMerchantName": "EasyTruck",
  "payerType": "Customer",
  "payerAccount": "01929918378",
  "maxRefundableAmount": "600.00"
}
```

**Note:** This API returns the same response structure as Execute Payment and can be used as a fallback to verify payment status.

---

## Error Code Implementation Testing

### Test Scenario A: Duplicate Transaction Error

**First Transaction (Successful):**
- Invoice Number: `696f6aaa770c18c96e6e53cd`
- Payment ID: `TR0011PXUbxbT1769405202127`
- Timestamp: `2026-01-26T11:26:42:127 GMT+0600`
- trxID: `DAQ20OC4BG`
- Amount: `600.00 BDT`
- Status: Completed
- Screenshot: <img width="720" height="395" alt="bkash-payment-successful_720" src="https://github.com/user-attachments/assets/0852b4b3-48c6-46c9-88a3-3a0dfd39f04b" />


**Second Transaction (Duplicate - Within time window):**
- Invoice Number: `696f6a4f770c18c96e6e535e`
- Payment ID: `TR0011ocLssVR1769406693730`
- Timestamp: `2026-01-26T11:51:33:730 GMT+0600`
- Amount: `600.00 BDT` (Same as first transaction)
- **Error Code:** `2029`
- **Internal Code:** `ETC70052`
- **Error Message:** `"Duplicate for All Transactions"`
- Screenshot: <img width="720" height="395" alt="bkash-payment-failed_720" src="https://github.com/user-attachments/assets/e48dd2d1-59e7-474d-8759-e23eddae7b1a" />

**Note:** The duplicate transaction error was successfully triggered by attempting a second payment with the same amount (600.00 BDT) from the same payer (01929918378) within the detection window.

---

### Test Scenario B: Payment Cancelled

**Transaction Details:**
- Invoice Number: `696f6a0e770c18c96e6e5324`
- Payment ID: `TR0011cSysfA71769406840699`
- Timestamp: `2026-01-26T11:54:00:699 GMT+0600`
- User Action: Clicked "Close" button on bKash payment page
- Redirect URL: `http://localhost:5000/api/v1/bkash/callback?paymentID=...&status=cancel&signature=...`
- Message Displayed: "Payment Cancelled"
- Callback Log: `Payment cancelled: TR0011cSysfA71769406840699`
- Screenshot: <img width="719" height="395" alt="bkash-payment-cancel_720" src="https://github.com/user-attachments/assets/ba32cd74-feb7-437e-beaf-e3d64b19188d" />

---

### Test Scenario C: Invalid OTP (3 Failed Attempts)

**Transaction Details:**
- Invoice Number: `696f6a0e770c18c96e6e5324`
- Payment ID: `TR0011cSysfA71769406840699`
- Timestamp: `2026-01-26T11:54:00:699 GMT+0600`
- User Action: Entered wrong OTP 3 times
- Error Code: `2031`
- Error Message: `"Invalid OTP. Transaction failed"`
- Redirect URL: `http://localhost:5000/api/v1/bkash/callback?paymentID=...&status=failure&signature=...`
- Message Displayed: "Payment Failed"
- Callback Log: `Payment failed: TR0011cSysfA71769406840699`
- Screenshot: <img width="720" height="395" alt="bkash-payment-failed_720" src="https://github.com/user-attachments/assets/a99e258b-487c-4659-a353-c3f5987082af" />


## Company Contact Information
For technical inquiries regarding these test results or the integration middleware, please contact the development partner:

Company Name: Netro Systems

Website: www.netrosystems.com

Support Email: support@netrosystems.com

Address: Level 6, Hi-Tech Park, Rajshahi, Bangladesh

Confidentiality Notice: This report contains sandbox credentials and internal invoice mapping intended for review by the bKash Onboarding Team and Netro Systems internal stakeholders only.
