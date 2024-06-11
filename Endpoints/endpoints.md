Sure, here's the adapted table of contents including the new endpoints:

# Endpoints
- [Endpoints](#endpoints)
  - [User Endpoints](#user-endpoints)
    - [Register](#register)
    - [Login](#login)
    - [Logout](#logout)
  - [Restaurant Endpoints](#restaurant-endpoints)
    - [Create new restaurant](#create-new-restaurant)
    - [Modify specific restaurant](#modify-specific-restaurant)
    - [Create new zone](#create-new-zone)
    - [List all zones](#list-all-zones)
    - [Modify specific zone](#modify-specific-zone)
    - [Create new table](#create-new-table)
    - [List all tables](#list-all-tables)
    - [Modify specific table](#modify-specific-table)
    - [Create new vacation period](#create-new-vacation-period)
    - [List all vacation periods](#list-all-vacation-periods)
    - [Modify specific vacation period](#modify-specific-vacation-period)
    - [Create new booking period](#create-new-booking-period)
    - [List booking periods](#list-booking-periods)
    - [Modify specific booking period](#modify-specific-booking-period)
  - [Booking Endpoints](#booking-endpoints)
    - [Create new booking](#create-new-booking)
    - [List all bookings](#list-all-bookings)
    - [Modify booking](#modify-booking)
    - [Available days](#available-days)
    - [Available time slots](#available-time-slots)

## User Endpoints

Placeholder Text

### Register

This endpoint allows for user registration by creating a new user in the system.

**HTTP Method:** POST

**Path:** /api/register

**Request Parameters:**

- None

**Request Body:**

- `username` (string, required): The username for the new user.
- `password` (string, required): The password for the new user.
- `email` (string, required): The email address for the new user.
- Other fields as defined in the `UserRegistrationSerializer`.

**Response:**

- **Status Code:** 201 Created
- **Content Type:** application/json

**Example Request:**

```http
POST /api/register
Host: example.com
Content-Type: application/json

{
  "username": "newuser",
  "password": "securepassword",
  "email": "user@example.com"
}
```

**Example Response:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "username": "newuser",
  "email": "user@example.com",
  "date_joined": "2023-06-05T12:34:56Z"
}
```

**Note:**

- Ensure that the request body includes all required fields as defined in the `UserRegistrationSerializer`.
- The endpoint will return a 400 Bad Request status code if any required fields are missing or invalid.

### Login

This endpoint allows for user login by authenticating the user and returning a token.

**HTTP Method:** POST

**Path:** /api/login

**Request Parameters:**

- None

**Request Body:**

- `username` (string, required): The username of the user.
- `password` (string, required): The password of the user.

**Response:**

- **Status Code:** 200 OK
- **Content Type:** application/json

**Example Request:**

```http
POST /api/login
Host: example.com
Content-Type: application/json

{
  "username": "existinguser",
  "password": "correctpassword"
}
```

**Example Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "token": "user-auth-token"
}
```

**Note:**

- Ensure that the request body includes both `username` and `password` fields.
- The endpoint will return a 400 Bad Request status code if any required fields are missing or invalid.
- Authentication is handled via `TokenAuthentication`, so the response will include an authentication token if the login is successful.

### Log Out

This endpoint allows for user logout by ending the user's session.

**HTTP Method:** GET

**Path:** /api/logout

**Request Parameters:**

- None

**Request Body:**

- None

**Response:**

- **Status Code:** 200 OK
- **Content Type:** application/json

**Example Request:**

```http
GET /api/logout
Host: example.com
Content-Type: application/json
```

**Example Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

**Note:**

- This endpoint requires that the user is authenticated before logging out.
- The endpoint will clear the user's session and log them out of the system.

---

## Restaurant Endpoints

Placeholder Text

### Create new restaurant

RestaurantCreateView

This endpoint allows for creating a new restaurant.

**HTTP Method:** POST

**Path:** /api/restaurants

**Request Parameters:**

- None

**Request Body:**

- `name` (string, required): The name of the restaurant.
- `address` (string, required): The address of the restaurant.
- `phone` (string, optional): The contact phone number of the restaurant.
- Other fields as defined in the `RestaurantSerializer`.

**Response:**

- **Status Code:** 201 Created
- **Content Type:** application/json

**Example Request:**

```http
POST /api/restaurants
Host: example.com
Content-Type: application/json

{
  "name": "New Restaurant",
  "address": "123 Main St",
  "phone": "555-1234"
}
```

**Example Response:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "name": "New Restaurant",
  "address": "123 Main St",
  "phone": "555-1234",
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Note:**

- Ensure that the request body includes all required fields as defined in the `RestaurantSerializer`.
- The endpoint will return a 400 Bad Request status code if any required fields are missing or invalid.

### Modify specific restaurant

RestaurantDetailView

This endpoint allows for retrieving, updating, or deleting a specific restaurant for the current user.

**HTTP Method:** GET, PUT, DELETE

**Path:** /api/restaurants/{id}

**Request Parameters:**

- `id` (integer, required): The ID of the restaurant to retrieve, update, or delete.

**Request Body:**

- `name` (string, optional): The name of the restaurant.
- `address` (string, optional): The address of the restaurant.
- `phone` (string, optional): The contact phone number of the restaurant.
- Other fields as defined in the `RestaurantSerializer`.

**Response:**

- **Status Code:** 
  - 200 OK (for GET and PUT)
  - 204 No Content (for DELETE)
- **Content Type:** application/json

**Example Request (GET):**

```http
GET /api/restaurants/1
Host: example.com
Content-Type: application/json
```

**Example Response (GET):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "Existing Restaurant",
  "address": "123 Main St",
  "phone": "555-1234",
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (PUT):**

```http
PUT /api/restaurants/1
Host: example.com
Content-Type: application/json

{
  "name": "Updated Restaurant",
  "address": "456 Elm St",
  "phone": "555-5678"
}
```

**Example Response (PUT):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "Updated Restaurant",
  "address": "456 Elm St",
  "phone": "555-5678",
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (DELETE):**

```http
DELETE /api/restaurants/1
Host: example.com
Content-Type: application/json
```

**Example Response (DELETE):**

```http
HTTP/1.1 204 No Content
```

**Note:**

- This endpoint filters restaurants based on the authenticated user.
- Ensure that the `id` provided in the path corresponds to a restaurant associated with the user.
- Authentication is required for this endpoint.
- The PUT request allows for updating any of the fields defined in the `RestaurantSerializer`.
- The DELETE request will remove the specified restaurant from the system.


### Create new zone

ZoneCreateView

This endpoint allows for creating a new zone within a restaurant.

**HTTP Method:** POST

**Path:** /api/zones

**Request Parameters:**

- None

**Request Body:**

- `name` (string, required): The name of the zone.
- `restaurant` (integer, required): The ID of the restaurant to which the zone belongs.
- Other fields as defined in the `ZoneSerializer`.

**Response:**

- **Status Code:** 201 Created
- **Content Type:** application/json

**Example Request:**

```http
POST /api/zones
Host: example.com
Content-Type: application/json

{
  "name": "Patio",
  "restaurant": 1
}
```

**Example Response:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "name": "Patio",
  "restaurant": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Note:**

- Ensure that the request body includes all required fields as defined in the `ZoneSerializer`.
- The endpoint will return a 400 Bad Request status code if any required fields are missing or invalid.

### List all zones

ZoneListView

This endpoint allows for listing all zones for the current user's restaurant.

**HTTP Method:** GET

**Path:** /api/zones

**Request Parameters:**

- None

**Request Body:**

- None

**Response:**

- **Status Code:** 200 OK
- **Content Type:** application/json

**Example Request:**

```http
GET /api/zones
Host: example.com
Content-Type: application/json
```

**Example Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "name": "Patio",
    "restaurant": 1,
    "created_at": "2023-06-05T12:34:56Z"
  },
  {
    "id": 2,
    "name": "Main Hall",
    "restaurant": 1,
    "created_at": "2023-06-06T12:34:56Z"
  }
]
```

**Note:**

- This endpoint filters zones based on the authenticated user's restaurant.
- Ensure that the user is authenticated, as the zones are filtered based on the authenticated user's restaurant.

### Modify specific zone

ZoneDetailView

This endpoint allows for retrieving, updating, or deleting a specific zone for the current user's restaurant.

**HTTP Method:** GET, PUT, DELETE

**Path:** /api/zones/{id}

**Request Parameters:**

- `id` (integer, required): The ID of the zone to retrieve, update, or delete.

**Request Body:**

- `name` (string, optional): The name of the zone.
- `restaurant` (integer, optional): The ID of the restaurant to which the zone belongs.
- Other fields as defined in the `ZoneSerializer`.

**Response:**

- **Status Code:** 
  - 200 OK (for GET and PUT)
  - 204 No Content (for DELETE)
- **Content Type:** application/json

**Example Request (GET):**

```http
GET /api/zones/1
Host: example.com
Content-Type: application/json
```

**Example Response (GET):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "Patio",
  "restaurant": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (PUT):**

```http
PUT /api/zones/1
Host: example.com
Content-Type: application/json

{
  "name": "Updated Patio",
  "restaurant": 1
}
```

**Example Response (PUT):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "Updated Patio",
  "restaurant": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (DELETE):**

```http
DELETE /api/zones/1
Host: example.com
Content-Type: application/json
```

**Example Response (DELETE):**

```http
HTTP/1.1 204 No Content
```

**Note:**

- This endpoint filters zones based on the authenticated user's restaurant.
- Ensure that the `id` provided in the path corresponds to a zone associated with the user's restaurant.
- Authentication is required for this endpoint.
- The PUT request allows for updating any of the fields defined in the `ZoneSerializer`.
- The DELETE request will remove the specified zone from the system.

### Create new table

TableCreateView

This endpoint allows for creating a new table within a zone.

**HTTP Method:** POST

**Path:** /api/tables

**Request Parameters:**

- None

**Request Body:**

- `number` (integer, required): The table number.
- `zone` (integer, required): The ID of the zone to which the table belongs.
- Other fields as defined in the `TableSerializer`.

**Response:**

- **Status Code:** 201 Created
- **Content Type:** application/json

**Example Request:**

```http
POST /api/tables
Host: example.com
Content-Type: application/json

{
  "number": 1,
  "zone": 1
}
```

**Example Response:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "number": 1,
  "zone": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Note:**

- Ensure that the request body includes all required fields as defined in the `TableSerializer`.
- The endpoint will return a 400 Bad Request status code if any required fields are missing or invalid.

### List all tables

TableListView

This endpoint allows for listing all tables for the current user's restaurant zones.

**HTTP Method:** GET

**Path:** /api/tables

**Request Parameters:**

- None

**Request Body:**

- None

**Response:**

- **Status Code:** 200 OK
- **Content Type:** application/json

**Example Request:**

```http
GET /api/tables
Host: example.com
Content-Type: application/json
```

**Example Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "number": 1,
    "zone": 1,
    "created_at": "2023-06-05T12:34:56Z"
  },
  {
    "id": 2,
    "number": 2,
    "zone": 1,
    "created_at": "2023-06-06T12:34:56Z"
  }
]
```

**Note:**

- This endpoint filters tables based on the authenticated user's restaurant zones.
- Ensure that the user is authenticated, as the tables are filtered based on the authenticated user's restaurant zones.

### Modify specific table

TableDetailView

This endpoint allows for retrieving, updating, or deleting a specific table for the current user's restaurant zones.

**HTTP Method:** GET, PUT, DELETE

**Path:** /api/tables/{id}

**Request Parameters:**

- `id` (integer, required): The ID of the table to retrieve, update, or delete.

**Request Body:**

- `number` (integer, optional): The table number.
- `zone` (integer, optional): The ID of the zone to which the table belongs.
- Other fields as defined in the `TableSerializer`.

**Response:**

- **Status Code:** 
  - 200 OK (for GET and PUT)
  - 204 No Content (for DELETE)
- **Content Type:** application/json

**Example Request (GET):**

```http
GET /api/tables/1
Host: example.com
Content-Type: application/json
```

**Example Response (GET):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "number": 1,
  "zone": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (PUT):**

```http
PUT /api/tables/1
Host: example.com
Content-Type: application/json

{
  "number": 2,
  "zone": 1
}
```

**Example Response (PUT):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "number": 2,
  "zone": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (DELETE):**

```http
DELETE /api/tables/1
Host: example.com
Content-Type: application/json
```

**Example Response (DELETE):**

```http
HTTP/1.1 204 No Content
```

**Note:**

- This endpoint filters tables based on the authenticated user's restaurant zones.
- Ensure that the `id` provided in the path corresponds to a table associated with the user's restaurant zones.
- Authentication is required for this endpoint.
- The PUT request allows for updating any of the fields defined in the `TableSerializer`.
- The DELETE request will remove the specified table from the system.

### Create new vacation period

VacationCreateView

This endpoint allows for creating a new vacation period for a restaurant.

**HTTP Method:** POST

**Path:** /api/vacations

**Request Parameters:**

- None

**Request Body:**

- `start_date` (date, required): The start date of the vacation period.
- `end_date` (date, required): The end date of the vacation period.
- `restaurant` (integer, required): The ID of the restaurant to which the vacation period belongs.
- Other fields as defined in the `VacationSerializer`.

**Response:**

- **Status Code:** 201 Created
- **Content Type:** application/json

**Example Request:**

```http
POST /api/vacations
Host: example.com
Content-Type: application/json

{
  "start_date": "2024-07-01",
  "end_date": "2024-07-15",
  "restaurant": 1
}
```

**Example Response:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "start_date": "2024-07-01",
  "end_date": "2024-07-15",
  "restaurant": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Note:**

- Ensure that the request body includes all required fields as defined in the `VacationSerializer`.
- The endpoint will return a 400 Bad Request status code if any required fields are missing or invalid.

### List all vacation periods

VacationListView

This endpoint allows for listing all vacation periods for the current user's restaurant.

**HTTP Method:** GET

**Path:** /api/vacations

**Request Parameters:**

- None

**Request Body:**

- None

**Response:**

- **Status Code:** 200 OK
- **Content Type:** application/json

**Example Request:**

```http
GET /api/vacations
Host: example.com
Content-Type: application/json
```

**Example Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "start_date": "2024-07-01",
    "end_date": "2024-07-15",
    "restaurant": 1,
    "created_at": "2023-06-05T12:34:56Z"
  },
  {
    "id": 2,
    "start_date": "2024-08-01",
    "end_date": "2024-08-10",
    "restaurant": 1,
    "created_at": "2023-06-06T12:34:56Z"
  }
]
```

**Note:**

- This endpoint filters vacation periods based on the authenticated user's restaurant.
- Ensure that the user is authenticated, as the vacation periods are filtered based on the authenticated user's restaurant.

### Modify specific vacation period

VacationDetailView

This endpoint allows for retrieving, updating, or deleting a specific vacation period for the current user's restaurant.

**HTTP Method:** GET, PUT, DELETE

**Path:** /api/vacations/{id}

**Request Parameters:**

- `id` (integer, required): The ID of the vacation period to retrieve, update, or delete.

**Request Body:**

- `start_date` (date, optional): The start date of the vacation period.
- `end_date` (date, optional): The end date of the vacation period.
- `restaurant` (integer, optional): The ID of the restaurant to which the vacation period belongs.
- Other fields as defined in the `VacationSerializer`.

**Response:**

- **Status Code:** 
  - 200 OK (for GET and PUT)
  - 204 No Content (for DELETE)
- **Content Type:** application/json

**Example Request (GET):**

```http
GET /api/vacations/1
Host: example.com
Content-Type: application/json
```

**Example Response (GET):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "start_date": "2024-07-01",
  "end_date": "2024-07-15",
  "restaurant": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (PUT):**

```http
PUT /api/vacations/1
Host: example.com
Content-Type: application/json

{
  "start_date": "2024-07-05",
  "end_date": "2024-07-20",
  "restaurant": 1
}
```

**Example Response (PUT):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "start_date": "2024-07-05",
  "end_date": "2024-07-20",
  "restaurant": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (DELETE):**

```http
DELETE /api/vacations/1
Host: example.com
Content-Type: application/json
```

**Example Response (DELETE):**

```http
HTTP/1.1 204 No Content
```

**Note:**

- This endpoint filters vacation periods based on the authenticated user's restaurant.
- Ensure that the `id` provided in the path corresponds to a vacation period associated with the user's restaurant.
- Authentication is required for this endpoint.
- The PUT request allows for updating any of the fields defined in the `VacationSerializer`.
- The DELETE request will remove the specified vacation period from the system.

### Create new booking period

BookingPeriodCreateView

This endpoint allows for creating a new booking period for a restaurant.

**HTTP Method:** POST

**Path:** /api/booking-periods

**Request Parameters:**

- None

**Request Body:**

- `start_time` (time, required): The start time of the booking period.
- `end_time` (time, required): The end time of the booking period.
- `restaurant` (integer, required): The ID of the restaurant to which the booking period belongs.
- Other fields as defined in the `BookingPeriodSerializer`.

**Response:**

- **Status Code:** 201 Created
- **Content Type:** application/json

**Example Request:**

```http
POST /api/booking-periods
Host: example.com
Content-Type: application/json

{
  "start_time": "18:00:00",
  "end_time": "22:00:00",
  "restaurant": 1
}
```

**Example Response:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "start_time": "18:00:00",
  "end_time": "22:00:00",
  "restaurant": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Note:**

- Ensure that the request body includes all required fields as defined in the `BookingPeriodSerializer`.
- The endpoint will return a 400 Bad Request status code if any required fields are missing or invalid.

### List booking period

BookingPeriodListView

This endpoint allows for listing all booking periods for the current user's restaurant.

**HTTP Method:** GET

**Path:** /api/booking-periods

**Request Parameters:**

- None

**Request Body:**

- None

**Response:**

- **Status Code:** 200 OK
- **Content Type:** application/json

**Example Request:**

```http
GET /api/booking-periods
Host: example.com
Content-Type: application/json
```

**Example Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "start_time": "18:00:00",
    "end_time": "22:00:00",
    "restaurant": 1,
    "created_at": "2023-06-05T12:34:56Z"
  },
  {
    "id": 2,
    "start_time": "11:00:00",
    "end_time": "14:00:00",
    "restaurant": 1,
    "created_at": "2023-06-06T12:34:56Z"
  }
]
```

**Note:**

- This endpoint filters booking periods based on the authenticated user's restaurant.
- Ensure that the user is authenticated, as the booking periods are filtered based on the authenticated user's restaurant.

### Modify specific booking period

BookingPeriodDetailView

This endpoint allows for retrieving, updating, or deleting a specific booking period for the current user's restaurant.

**HTTP Method:** GET, PUT, DELETE

**Path:** /api/booking-periods/{id}

**Request Parameters:**

- `id` (integer, required): The ID of the booking period to retrieve, update, or delete.

**Request Body:**

- `start_time` (time, optional): The start time of the booking period.
- `end_time` (time, optional): The end time of the booking period.
- `restaurant` (integer, optional): The ID of the restaurant to which the booking period belongs.
- Other fields as defined in the `BookingPeriodSerializer`.

**Response:**

- **Status Code:** 
  - 200 OK (for GET and PUT)
  - 204 No Content (for DELETE)
- **Content Type:** application/json

**Example Request (GET):**

```http
GET /api/booking-periods/1
Host: example.com
Content-Type: application/json
```

**Example Response (GET):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "start_time": "18:00:00",
  "end_time": "22:00:00",
  "restaurant": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (PUT):**

```http
PUT /api/booking-periods/1
Host: example.com
Content-Type: application/json

{
  "start_time": "19:00:00",
  "end_time": "23:00:00",
  "restaurant": 1
}
```

**Example Response (PUT):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "start_time": "19:00:00",
  "end_time": "23:00:00",
  "restaurant": 1,
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (DELETE):**

```http
DELETE /api/booking-periods/1
Host: example.com
Content-Type: application/json
```

**Example Response (DELETE):**

```http
HTTP/1.1 204 No Content
```

**Note:**

- This endpoint filters booking periods based on the authenticated user's restaurant.
- Ensure that the `id` provided in the path corresponds to a booking period associated with the user's restaurant.
- Authentication is required for this endpoint.
- The PUT request allows for updating any of the fields defined in the `BookingPeriodSerializer`.
- The DELETE request will remove the specified booking period from the system.

Certainly! Here’s the updated API documentation with the necessary details from the `BookingSerializer` and `BookingListSerializer` classes included:

---

## Booking Endpoints

### Create New Booking

This endpoint allows for creating a new booking.

**HTTP Method:** `POST`

**Path:** `/api/bookings`

**Request Parameters:**
> - None

**Request Body:**
> - `guest_name` (string, required): The name of the guest.
> - `guest_phone` (string, required): The phone number of the guest.
> - `start` (datetime, required): The start time of the booking.
> - `guest_count` (integer, required): The number of guests for the booking.
> - `notes` (string, optional): Any additional notes for the booking.
> - `table` (integer, optional): The ID of the table for the booking. If not provided, the system will assign an appropriate table based on availability and capacity.

**Response:**
> - Status Code: 201 Created
> - Content Type: application/json

**Example Request:**
```http
POST /api/bookings
Host: example.com
Content-Type: application/json

{
  "guest_name": "John Doe",
  "guest_phone": "123-456-7890",
  "start": "2024-06-12T18:00:00Z",
  "guest_count": 2,
  "notes": "Window seat if possible."
}
```

**Example Response:**
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "guest_name": "John Doe",
  "guest_phone": "123-456-7890",
  "start": "2024-06-12T18:00:00Z",
  "end": "2024-06-12T19:45:00Z",
  "guest_count": 2,
  "status": "Confirmed",
  "notes": "Window seat if possible.",
  "restaurant": 1,
  "table": 3
}
```

**Note:**
> - Ensure that the request body includes all required fields as defined in the `BookingSerializer`.
> - The endpoint will return a 400 Bad Request status code if any required fields are missing or invalid.
> - The `end` time for the booking is automatically calculated based on the restaurant’s default booking duration.

---

### List All Bookings

This endpoint allows for listing all bookings for the current user's restaurant.

**HTTP Method:** `GET`

**Path:** `/api/bookings`

**Request Parameters:**
> - None

**Request Body:**
> - None

**Response:**
> - Status Code: 200 OK
> - Content Type: application/json

**Example Request:**
```http
GET /api/bookings
Host: example.com
Content-Type: application/json
```

**Example Response:**
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "guest_name": "John Doe",
    "guest_phone": "123-456-7890",
    "start": "2024-06-12T18:00:00Z",
    "end": "2024-06-12T19:45:00Z",
    "guest_count": 2,
    "status": "Confirmed",
    "notes": "Window seat if possible.",
    "restaurant": 1,
    "table": 3
  },
  {
    "id": 2,
    "guest_name": "Jane Smith",
    "guest_phone": "987-654-3210",
    "start": "2024-06-13T19:00:00Z",
    "end": "2024-06-13T20:45:00Z",
    "guest_count": 4,
    "status": "Pending",
    "notes": "",
    "restaurant": 1,
    "table": 5
  }
]
```

**Note:**
> - This endpoint returns all bookings associated with the current user's restaurant.
> - The response will include all fields as defined in the `BookingListSerializer`.
> - Ensure that the user is authenticated, as the bookings are filtered based on the authenticated user's restaurant.

---

### Modify Booking

This endpoint allows for retrieving, updating, or deleting a specific booking for the current user's restaurant.

**HTTP Method:** `GET`, `PUT`, `DELETE`

**Path:** `/api/bookings/{id}`

**Request Parameters:**
> - `id` (integer, required): The ID of the booking to retrieve, update, or delete.

**Request Body:**
> - `guest_name` (string, optional): The name of the guest.
> - `guest_phone` (string, optional): The phone number of the guest.
> - `start` (datetime, optional): The start time of the booking.
> - `guest_count` (integer, optional): The number of guests for the booking.
> - `notes` (string, optional): Any additional notes for the booking.
> - `table` (integer, optional): The ID of the table for the booking.

**Response:**
> - Status Code: 200 OK (for GET and PUT), 204 No Content (for DELETE)
> - Content Type: application/json

**Example Request (GET):**
```http
GET /api/bookings/1
Host: example.com
Content-Type: application/json
```

**Example Response (GET):**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "guest_name": "John Doe",
  "guest_phone": "123-456-7890",
  "start": "2024-06-12T18:00:00Z",
  "end": "2024-06-12T19:45:00Z",
  "guest_count": 2,
  "status": "Confirmed",
  "notes": "Window seat if possible.",
  "restaurant": 1,
  "table": 3
}
```

**Example Request (PUT):**
```http
PUT /api/bookings/1
Host: example.com
Content-Type: application/json

{
  "guest_name": "John Doe",
  "guest_phone": "123-456-7890",
  "start": "2024-06-12T18:00:00Z",
  "guest_count": 3,
  "notes": "Change to three guests.",
  "table": 4
}
```

**Example Response (PUT):**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "guest_name": "John Doe",
  "guest_phone": "123-456-7890",
  "start": "2024-06-12T18:00:00Z",
  "end": "2024-06-12T19:45:00Z",
  "guest_count": 3,
  "status": "Confirmed",
  "notes": "Change to three guests.",
  "restaurant": 1,
  "table": 4
}
```

**Example Request (DELETE):**
```http
DELETE /api/bookings/1
Host: example.com
Content-Type: application/json
```

**Example Response (DELETE):**
```http
HTTP/1.1 204 No Content
```

**Note:**
> - This endpoint filters bookings based on the authenticated user's restaurant.
> - Ensure that the `id` provided in the path corresponds to a booking associated with the user's restaurant.
> - Authentication is required for this endpoint.
> - The `PUT` request allows for updating any of the fields defined in the `BookingSerializer`.
> - The `DELETE` request will remove the specified booking from the system.

---

### Available Days

Gets a list of available days for booking for the authenticated user's restaurant.

**HTTP Method:** `GET`

**Path:** `/available-days/`

**Request Parameters:**
> - `restaurant_id` (int, required): The ID of the restaurant.
> - `start_day` (date, required): The start date for checking availability (format: YYYY-MM-DD).
> - `guest_count` (int, required): The number of guests.

**Response:**
> - Status Code: 200 OK
> - Content Type: application/json

**Example Request:**
```http
GET /available-days/?restaurant_id=1&start_day=2024-06-12&guest_count=2
Host: example.com
Authorization: Token YOUR_AUTH_TOKEN
```

**Example Response:**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "available_days": [
    "2024-06-12",
    "2024-06-13",
    ...
  ]
}
```

**Note:**
> - This endpoint requires authentication.

---

### Available Time Slots

Gets a list of available time slots for booking for a specific day and guest count.

**HTTP Method:** `GET`

**Path:** `/available-time-slots/`

**Request Parameters:**
> - `restaurant_id` (int, required): The ID of the restaurant.
> - `day` (date, required): The date for checking available time slots (format: YYYY-MM-DD).
> - `guest_count` (int, required): The number of guests.

**Response:**
> - Status Code: 200 OK
> - Content Type: application/json

**Example Request:**
```http
GET /available-time-slots/?restaurant_id=1&day=2024-06-12&guest_count=2
Host: example.com
Authorization: Token YOUR_AUTH_TOKEN
```

**Example Response:**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "available_time_slots": [
    "18:00",
    "18:15",
    "18:30",
    "18:45",
    "19:00",
    ...
  ]
}
```

**Note:**
> - This endpoint requires authentication.
> - It checks the availability of time slots for a specific date and guest count.
> - The available time slots are filtered based on the restaurant’s booking periods and current reservations.

---
