# SuiteCRM API Documentation: Leads Module

---

### Introduction
This API allows users to create and update leads in SuiteCRM's Leads module. It supports CRUD operations (Create, Read, Update, Delete) for managing lead data within SuiteCRM.

### Base URL
`https://your_suitecrm_domain/api/v8`

### Authentication
This API requires authentication using OAuth 2.0. Obtain an access token by authenticating with SuiteCRM's OAuth server.

- **Authentication Endpoint:** `https://your_suitecrm_domain/api/access_token`
- **Required Scope:** `leads:write` (for write access to leads)

### Headers
- **Authorization:** `Bearer {access_token}`
- **Content-Type:** `application/json`

### Endpoints

#### Create a Lead
- **HTTP Method:** `POST`
- **Endpoint URL:** `/module/Leads`
- **Description:** Create a new lead in the Leads module.
- **Request Body:**
  ```json
  {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john@example.com",
    "phone": "123-456-7890",
    "status": "New",
    "source": "Website"
    // Additional attributes as needed
  }
  ```
  - `first_name`, `last_name`, `email`, `phone`: Mandatory fields for lead creation.
  - `status`: Status of the lead (e.g., New, Contacted, Converted).
  - `source`: Source of lead acquisition (e.g., Website, Referral).

#### Update a Lead
- **HTTP Method:** `PUT` or `PATCH`
- **Endpoint URL:** `/module/Leads/{lead_id}`
- **Description:** Update an existing lead in the Leads module.
- **Request Body:** (Similar to create, with fields to update)

#### Parameters
- `{lead_id}`: ID of the lead to be updated (UUID).

### Response
- **Success Response (200 OK):**
  ```json
  {
    "data": {
      "id": "abcdef123456",
      "message": "Lead updated successfully"
    }
  }
  ```
- **Error Responses:**
  - `400 Bad Request`: Invalid request format.
  - `401 Unauthorized`: Missing or invalid authentication token.
  - `404 Not Found`: Lead not found.

### Error Handling
- Detailed error messages and appropriate HTTP status codes are returned for various error scenarios.
- Refer to SuiteCRM's API documentation for a complete list of error codes and messages.

### Rate Limiting
- The API enforces rate limits to prevent abuse and maintain stability.
- Default rate limits: 100 requests per minute.

### Example Usage
#### Request:
```http
PUT /api/v8/module/Leads/abcdef123456 HTTP/1.1
Host: your_suitecrm_domain
Authorization: Bearer {access_token}
Content-Type: application/json

{
  "status": "Contacted",
  "phone": "987-654-3210"
}
```
#### Response:
```json
{
  "data": {
    "id": "abcdef123456",
    "message": "Lead updated successfully"
  }
}
```

---

This documentation provides comprehensive details about authentication, endpoints, request structure, response format, error handling, rate limiting, and example usage for SuiteCRM's Leads module API. Adjustments may be needed based on SuiteCRM's specific API capabilities and versions.
