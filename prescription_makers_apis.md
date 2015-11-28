# RxLabs API documentation 

RxLabs is a technology startup helping helthcare startups to streamline the execution.

# API List
API | Usage | Required
----|-------|--------- 
/api/v1/rx/sign | To sign a rx with RxLabs to get the rx_token and QR code | Required

# Security
A series of security protocols have been implemented to keep the communication secured.
* HTTPS endpoints
* Entire communications happens between whitelisted servers (IP Address & Domain names are registered with US)
* Infrastructure is regularly undergoes security audits by third party professionals.

# API Documentation

## To sign a prescription
### Endpoint
```xml
POST /api/v1/rx/sign
```
### Headers
```
MERCHANT_ID : {MERCHANT_ID_RECEIVED_FROM_RX_LABS}
```
### Body
```json
{
  "prescription_id" : "",
  "date" : "1988-12-04T00:00:00.000Z",
  "diagnosis" : "General fever",
  "patient" : {
    "email" : "akshay2@rxlabs.io",
    "phone_number" : "9970095388",
    /* For delivery purpose */
    "address" : "ABC 123",
    "labdmark" : "",
    "city" : "",
    "pin_code" : "411045"
  },
  "rx" : [
    {
      "name" : "Tablet 1",
      "type" : "tablet",
      "strength" : "",
      "frequency" : "once daily",
      "instructions" : "",
      "alergy_instructions" : ""
    },
    {
      "name" : "Tablet 2",
      "type" : "tablet", 
      "strength" : "",
      "frequency" : "1-1-1",
      "instructions" : "Before meal",
      "alergy_instructions" : ""
    }
  ]
}
```
### Responses
#### Success [200]
```json
{
  "success" : true,
  "api_version" : 1,
  "data" : {
    "rx_token" : "123k4kjh34kjhk2jg34kjgkjg234",
    "qr_code_image" : "https://api.rxlabs.io/rx/qrcode/123k4kjh34kjhk2jg34kjgkjg234",
    "rx_url" : "https://api.rxlabs.io/rx/123k4kjh34kjhk2jg34kjgkjg234"
  }
}
```
#### Failure [!= 200]
```json
{
  "success" : false,
  "api_version" : 1,
  "message" : "Something went wrong"
}
```
