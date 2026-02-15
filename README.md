# Stripe API Documentation

## Overview
The Stripe API allows developers to integrate secure payment processing into their applications.  
This guide covers how to create a PaymentIntent, which represents the lifecycle of a payment.

## Base URL
`https://api.stripe.com/v1/`


## Authentication
All requests require a Bearer token.  
Use your **secret key** (`sk_test_...` or `sk_live_...`) in the request header:

## Endpoints

### 1. Create a PaymentIntent
**Endpoint:**  
`POST /payment_intents`

**Parameters:**
| Name                  | Type    | Required | Description                                      |
|-----------------------|---------|----------|--------------------------------------------------|
| `amount`              | integer | Yes      | Amount to charge (in smallest currency unit, e.g., cents). |
| `currency`            | string  | Yes      | Currency code (e.g., `usd`, `inr`).              |
| `payment_method_types`| array   | Yes      | Allowed payment methods (e.g., `["card"]`).      |

**Request Example:**
```http
POST /v1/payment_intents
Authorization: Bearer sk_test_4eC39HqLyjWDarjtT1zdp7dc
Content-Type: application/x-www-form-urlencoded

amount=2000&currency=usd&payment_method_types[]=card

## Response Example

{
  "id": "pi_1FHEbSJyq12345",
  "object": "payment_intent",
  "amount": 2000,
  "currency": "usd",
  "status": "requires_payment_method",
  "client_secret": "pi_1FHEbSJyq12345_secret_67890"
}

## Retrieve a PaymentIntent

Endpoint:  
GET /payment_intents/{id}

Request Example
GET /v1/payment_intents/pi_1FHEbSJyq12345
Authorization: Bearer sk_test_4eC39HqLyjWDarjtT1zdp7dc

Response Example:
{
  "id": "pi_1FHEbSJyq12345",
  "amount": 2000,
  "currency": "usd",
  "status": "requires_payment_method"
}


Error Codes


Code	Meaning	Resolution
400	Bad Request	Invalid parameters. Check request format.
401	Unauthorized	Invalid or missing API key.
402	Request Failed	Payment declined. Retry with valid method.
500	Server Error	Stripe internal error. Retry request.

