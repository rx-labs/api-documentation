# RxLabs API documentation 

RxLabs is a technology startup helping helthcare startups to streamline the execution.

# API List
API | Usage
----|------
/api/v1/user/register | To register user for getting rx notification
[OPTIONAL] /api/v1/doctor/register | To register doctor for rx records
/api/v1/rx/sign | To sign a rx with RxLabs to get the rx_token and QR code
/api/v1/rx/validate/{rx_token} | To validate a rx_token with User info
/api/v1/rx/{rx_token} | To retreive the prescription for rx_token with User info
/api/v1/rx/{rx_token}/purchase | To record a transaction against rx_token

# Security
A series of security protocols have been implemented to keep the communication secured.
* HTTPS endpoints
* Entire communications happens between whitelisted servers (IP Address & Domain names are registered with US)
* Infrastructure is regularly undergoes security audits by third party professionals.

# API Documentation

## To register User with RxLabs system
This API helps merchant to register a user(patient) on the platform. `email`, `first_name`, `last_name`, `mobile`,`age` and `sex` are the compulsory fields. This decides our machine learning engine to do some auto suggestions for your platform.

### Endpoint
```xml
POST /api/v1/user/register
```
### Headers
```
MERCHANT_ID : {MERCHANT_ID_RECEIVED_FROM_RX_LABS}
```
### Body
```json
{
  "email" : "akshay@rxlabs.io",
  "first_name" : "Akshay",
  "last_name" : "Deo",
  "sex" : "Male",
  "birth_date" : "1988-12-04T00:00:00.000Z",
  "mobile" : "9970095218",
}
```
### Responses
#### Success [200]
```json
{
  "success" : true,
  "api_version" : 1,
  "message" : "User registered succsfully"
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

## To register Doctor with RxLabs system
This API helps merchant to register a doctor on the platform.

### Endpoint
```xml
POST /api/v1/doctor/register
```
### Headers
```
MERCHANT_ID : {MERCHANT_ID_RECEIVED_FROM_RX_LABS}
```
### Body
```json
{
  "email" : "akshay@rxlabs.io",
  "first_name" : "Akshay",
  "last_name" : "Deo",
  "mobile" : "997009523",
  "age" : 30,
  "sex" : "Male",
  "education" : [
    {
      "degress" : "BDS",
      "college" : "Rajiv Gandhi University Of Health Sciences, Karnataka",
      "graduation_year" : ""
    }
  ],
  "qualifications" : "BDS , MDS - Prosthodontics",
  "specialities" : "Prosthodontist , Dentist , Dental Surgeon",
  "experience_in_years" : "17",
  "rating_percentage" : 10 
}
```
### Responses
#### Success [200]
```json
{
  "success" : true,
  "api_version" : 1,
  "message" : "Doctor registered succsfully"
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
  "doctor" : {
    "doctor_id" : "1",
    "email" : "akshay@rxlabs.io",
    "phone_number" : "9970095388"
  },
  "clinic" : {
    "name" : "Great Clinic",
    "phone_number" : "9988334455"
  },
  "patient" : {
    "email" : "akshay2@rxlabs.io",
    "phone_number" : "9970095388"
  },
  "date" : "1988-12-04T00:00:00.000Z",
  "diagnosis" : "General fever",
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

## To validate a prescription
### Endpoint 
```xml
GET /api/v1/rx/validate/{rx_token}
```
### Headers
```
MERCHANT_ID : {MERCHANT_ID_RECEIVED_FROM_RX_LABS}
```
### Body
```json
{
  "email" : "akshay@rxlabs.io",
  "mobile" : "9988998899"
}
```
### Responses
#### Success [200]
```json
{
  "success" : true,
  "api_version" : 1,
  "message" : "Prescription is valid"
}
```
#### Failure [!= 200]
```json
{
  "success" : false,
  "api_version" : 1,
  "message" : "Prescription is not valid"
}
```

## To retrieve a signed prescription
### Endpoint
```xml
GET /api/v1/rx/{rx_token}
```
### Headers
```
MERCHANT_ID : {MERCHANT_ID_RECEIVED_FROM_RX_LABS}
```
### Body 
```json
{
  "user_id" : "",
  "email" : "akshay@rxlabs.io",
  "mobile" : "9988998899"
}
```
### Responses
#### Success [200]
```json
{
  "success" : true,
  "api_version" : 1,
  "data" : {
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
## To record a prescription purchase
### Endpoint
```xml
POST /api/v1/rx/{rx_token}/purchase
```
### Headers
```
MERCHANT_ID : {MERCHANT_ID_RECEIVED_FROM_RX_LABS}
```
### Body 
```json
{
  "user" : {
    "user_id" : "",
    "email" : "akshay@rxlabs.io",
    "mobile" : "9988998899"
  },
  "purchase_order" : {
    "timestamp" : "2015-12-04T00:00:00.000Z",
    "total_amount_in_paise" : 11000,
    "items" : [
      {
        "name" : "Tablet 1",
        "type" : "tablet",
        "quantity" : 3,
        "price_in_paise" : 1000
      }
    ]
  }
}
```
### Responses
#### Success [200]
```json
{
  "success" : true,
  "api_version" : 1,
  "message" : "Transaction is recorded"
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
