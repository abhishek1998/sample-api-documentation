# SuiteCRM API Documentation: Leads Module

## Introduction
This API allows users to create and update leads in SuiteCRM's Leads module. It supports CRUD operations (Create, Read, Update, Delete) for managing lead data within SuiteCRM.

## Base URL
`https://your_suitecrm_domain/api/v8`

## Authentication
This API requires authentication using OAuth 2.0. Obtain an access token by authenticating with SuiteCRM's OAuth server.

- **Authentication Endpoint:** `https://your_suitecrm_domain/api/access_token`
- **Required Scope:** `leads:write` (for write access to leads)

## Headers
- **Authorization:** `Bearer {access_token}`
- **Content-Type:** `application/json`

## Create a Lead

### Endpoint
- **HTTP Method:** `POST`
- **Endpoint URL:** `/module/Leads`

### Example Request
```http
POST https://your_suitecrm_domain/api/v8/module/Leads
Authorization: Bearer {access_token}
Content-Type: application/json

{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "phone": "123-456-7890",
  "status": "New",
  "source": "Website"
}
```
### Attributes

| Attribute   | Type    | Description                                      |
|-------------|---------|--------------------------------------------------|
| `first_name`  | string  | First name of the lead (required).               |
| `last_name`   | string  | Last name of the lead (required).                |
| `email`       | string  | Email address of the lead (required).            |
| `phone`       | string  | Phone number of the lead (required).             |
| `status`      | string  | Status of the lead (e.g., New, Contacted).      |
| `source`      | string  | Source of lead acquisition (e.g., Website).      |

### Example Response
```json
{
  "data": {
    "id": "abcdef123456",
    "message": "Lead created successfully"
  }
}
```

## Update a Lead

### Endpoint
- **HTTP Method:** `PUT`
- **Endpoint URL:** `/module/Leads/{lead_id}`

### Parameters
- `{lead_id}`: ID of the lead to be updated (UUID).

### Attributes (in Request Body)
- Same attributes as in the create request.

### Example Request
```http
PUT https://your_suitecrm_domain/api/v8/module/Leads/abcdef123456
Authorization: Bearer {access_token}
Content-Type: application/json

{
  "status": "Contacted",
  "phone": "987-654-3210"
}
```

### Example Response
```json
{
  "data": {
    "id": "abcdef123456",
    "message": "Lead updated successfully"
  }
}
```

## **Error Responses:**
Though in most cases you'll receive an `HTTP 200` response with a plain text ok indicating that your message was posted successfully, it's best to prepare for scenarios where attempts to publish a message will fail.

  - `400 Bad Request`: Invalid request format.
  - `401 Unauthorized`: Missing or invalid authentication token.
  - `403 Forbidden`: The API key doesn't have permission to perform the request.
  - `404 Not Found`: Lead not found.

## Rate Limiting
- The API enforces rate limits to prevent abuse and maintain stability.
- Default rate limits: 100 requests per minute.
