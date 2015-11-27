# RxLabs API documentation 

RxLabs is a technology startup helping helthcare startups to streamline the execution.

## To register User with RxLabs system
This API helps merchant to register a user(patient) on the platform. `email`, `first_name`, `last_name`, `phone_number`,`age` and `sex` are the compulsory fields. This decides our machine learning engine to do some auto suggestions for your platform.

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
  "profile_pic_url" : "",
  "sex" : "Male",
  "age" : 24,
  "birth_date" : "1988-12-04T00:00:00.000Z",
  "phone_number" : "9970095388",
  "address_line_1": "ABC",
  "address_line_2" : "XYZ",
  "city" : "Pune",
  "state" : "Maharashtra",
  "country": "India",
  "pin_code" : "411045",
  "alergic_background" : [
    {
      "alergic_to" : "",
      "reason" : "",
      "dignosed_by" : ""
    },
    {
      "alergic_to" : "",
      "reason" : "",
      "dignosed_by" : ""
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
This API helps merchant to register a doctor on the platform. `email`, `first_name`, `last_name`, `phone_number`,`age`, `sex`, `degree`, `category` are the compulsory fields for doctors info. `clinic` information helps us to sign the `prescriptions` more securly.

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
  "doctor" : {
    "email" : "akshay@rxlabs.io",
    "first_name" : "Akshay",
    "last_name" : "Deo",
    "age" : 30,
    "sex" : "Male",
    "profile_pic_url" : "",
    "phone_number" : "9970095388",
    "address_line_1": "ABC",
    "address_line_2" : "XYZ",
    "city" : "Pune",
    "state" : "Maharashtra",
    "country": "India",
    "pin_code" : "411045",
    "degree" : "MBBS, MD General",
    "category" : "General Physician",
    "rating_percentage" : 10 
  },
  "clinic" : {
    "name" : "Great clinic",
    "phone_number" : "9970095388",
    "address_line_1": "ABC",
    "address_line_2" : "XYZ",
    "city" : "Pune",
    "state" : "Maharashtra",
    "country": "India",
    "pin_code" : "411045"
  }
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
    "email" : "akshay@rxlabs.io",
    "phone_number" : "9970095388"
  },
  "clinic" : {
    "name" : "Great Clinic",
    "phone_number" : "9988334455",
    "pin_code" : "411045",
  },
  "patient" : {
    "email" : "akshay2@rxlabs.io",
    "phone_number" : "9970095388"
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

## To retrieve a signed prescription
### Endpoint
```xml
GET /api/v1/rx/{rx_token}
```
### Headers
```
MERCHANT_ID : {MERCHANT_ID_RECEIVED_FROM_RX_LABS}
```
### Responses
#### Success [200]
```json
{
  "success" : true,
  "api_version" : 1,
  "data" : {
    "doctor" : {
      "email" : "akshay@rxlabs.io",
      "phone_number" : "9970095388"
    },
    "clinic" : {
      "name" : "Great Clinic",
      "phone_number" : "9988334455",
      "pin_code" : "411045",
    },
    "patient" : {
      "email" : "akshay2@rxlabs.io",
      "phone_number" : "9970095388"
    },
    "date" : "1988-12-04T00:00:00.000Z",
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
