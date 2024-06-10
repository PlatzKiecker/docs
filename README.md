# PlatzKiecker

PlatzKiecker is a project that aims to implement a table management system for restaurants.

## Table of Contents

- [Project Structure](#project-structure)
- [Installation and Usage](#installation-and-usage)
- [Modules](#modules)
  - [User Module](#user-module)
    - [User Data Model](#user-data-model)
  - [Restaurant Module](#restaurant-module)
    - [Restaurant Data Model](#restaurant-data-model)
    - [Zone Data Model](#zone-data-model)
    - [Table Data Model](#table-data-model)
    - [Vacation Data Model](#vacation-data-model)
    - [BookingPeriod Data Model](#bookingperiod-data-model)
  - [Booking Module](#booking-module)
    - [Booking Data Model](#booking-data-model)
  - [Script/Module Name](#scriptmodule-name)
    - [Function/Class Name](#functionclass-name)
- [Endpoints](#endpoints)
  - [User Endpoints](#unser-endpoints)
    - [Register](#register)
    - [Login](#login)
    - [Logout](#logout)
  - [Restaurant Endpoints](#restaurant-endpoints)
    - [Create new restaurant](#create-new-restaurant)
    - [Modify specific restaurant](#modify-specific-restaurant)
    - [Create new zone](#create-new-zone)
    - [List all zones](#list-all-zones)
    - [Modify specific zone ](#modify-specific-zone)
    - [Create new table](#create-new-table)
    - [List all tables ](#list-all-tables)
    - [Modify specific table](#modify-specific-table)
    - [Create new vacation period](#create-new-vacation-period)
    - [List all vacation periods](#list-all-vacation-periods)
    - [Modify specific vacation period](#modify-specific-vacation-period)
    - [Create new booking period](#create-new-booking-period)
    - [List booking period](#list-booking-period)
    - [Modify specific booking period](#modify-specific-booking-period)
  - [Booking endpoints](#booking-endpoints)
    - [Create new booking](#create-new-bookings)
    - [List all bookings](#list-all-bookings)
    - [Modify bookings](#modify-bookings)
    
  
- [Contributing](#contributing)
- [License](#license)

## Project Structure

Each component has its own directory in the root directory. By that we ensure Modularity and independance between used components.

## Installation and Usage

For Setting up the project, please refer to the [project directory](https://github.com/PlatzKiecker/platzkiecker?tab=readme-ov-file#installation)

## Modules

### User Module

Module for managing users who can administer restaurants.

- Usage:
1. Import this module: `from user.models import User`.
2. This module sets up the `User` model for managing users of the application.
3. This module reads user data for authentication and association with a restaurant.

**Note:**

> Each user can manage only one restaurant.
> 
- Example Usage/Config:
    
    ```python
    from user.models import User
    
    user = User(email="example@example.com", password="securepassword")
    user.save()
    
    ```
    
- **User Data Model**

Represents a user who manages a restaurant.

- **Fields**:
    - `email`: Email of the user (unique).
    - `password`: Password for user authentication.

---

### Restaurant Module

Module for managing restaurant-related data, including zones, tables, vacations, and booking periods.

- Usage:
1. Import this module: `from restaurant.models import Restaurant, Zone, Table, Vacation, BookingPeriod`.
2. This module sets up the `Restaurant`, `Zone`, `Table`, `Vacation`, and `BookingPeriod` models for managing restaurant data.
3. This module reads restaurant data to manage zones, tables, vacations, and booking periods.

**Note:**

> Each restaurant is managed by a single user.
> 
- Example Usage/Config:
    
    ```python
    from restaurant.models import Restaurant, Zone, Table, Vacation, BookingPeriod
    from user.models import User
    
    user = User.objects.create(email="owner@example.com", password="securepassword")
    restaurant = Restaurant.objects.create(name="Example Restaurant", user=user)
    zone = Zone.objects.create(name="Main Hall", bookable=True, restaurant=restaurant)
    table = Table.objects.create(capacity=4, bookable=True, combinable=False, zone=zone)
    vacation = Vacation.objects.create(start="2024-06-01 00:00:00", end="2024-06-15 23:59:59", restaurant=restaurant)
    booking_period = BookingPeriod.objects.create(weekday="MO", open="09:00:00", close="18:00:00", default_duration="01:00:00", restaurant=restaurant)
    
    ```
    
- **Restaurant Data Model**

Represents a restaurant managed by a user.

- **Fields**:
    - `name`: Name of the restaurant.
    - `user`: One-to-one relationship with `User`, representing the owner of the restaurant.
- **Zone Data Model**

Represents a zone within a restaurant.

- **Fields**:
    - `name`: Name of the zone.
    - `bookable`: Boolean indicating if the zone can be booked.
    - `restaurant`: Foreign key relationship to `Restaurant`.
- **Table Data Model**

Represents a table within a zone of a restaurant.

- **Fields**:
    - `capacity`: Number of seats at the table.
    - `bookable`: Boolean indicating if the table can be booked.
    - `combinable`: Boolean indicating if the table can be combined with others.
    - `zone`: Foreign key relationship to `Zone`.
- **Vacation Data Model**

Represents

a vacation period during which the restaurant is closed.

- **Fields**:
    - `start`: Start date and time of the vacation.
    - `end`: End date and time of the vacation.
    - `restaurant`: Foreign key relationship to `Restaurant`.
- **BookingPeriod Data Model**

Represents the booking periods available for a restaurant.

- **Fields**:
    - `weekday`: Enum representing the day of the week.
    - `open`: Opening time for bookings.
    - `close`: Closing time for bookings.
    - `default_duration`: Default duration for bookings.
    - `restaurant`: Foreign key relationship to `Restaurant`.

---

### Booking Module

Module for managing bookings for restaurants.

- Usage:
1. Import this module: `from booking.models import Booking`.
2. This module sets up the `Booking` model for managing reservations.
3. This module reads booking data to manage reservations for restaurants.

**Note:**

> Each booking is associated with a specific restaurant and table.
> 
- Example Usage/Config:
    
    ```python
    from booking.models import Booking
    from restaurant.models import Restaurant, Table
    
    restaurant = Restaurant.objects.get(name="Example Restaurant")
    table = Table.objects.get(zone__restaurant=restaurant, capacity=4)
    booking = Booking.objects.create(guest_name="John Doe", guest_phone="1234567890", start="2024-06-03 12:00:00", guest_count=2, table=table, restaurant=restaurant)
    
    ```
    
- **Booking Data Model**

Represents a booking made by a guest at a restaurant.

- **Fields**:
    - `guest_name`: Name of the guest.
    - `guest_phone`: Phone number of the guest.
    - `start`: Start date and time of the booking.
    - `guest_count`: Number of guests.
    - `status`: Status of the booking (e.g., pending, confirmed, seated, cancelled, completed).
    - `notes`: Additional notes for the booking.
    - `table`: Foreign key relationship to `Table`.
    - `restaurant`: Foreign key relationship to `Restaurant`.

### Module Name

Description of what the module does.

#### Function/Class Name

Description of what the function/class does.

- Parameters/Attributes: Description of the parameters/attributes.
- Returns: Description of the return value (if applicable).

## Endpoints

PLaceholder Text

### User Endpoints

Placeholder Text

#### Register

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

#### Login

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

#### Log Out

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

### Restaurant Endpoints

Placeholder Text

#### Create new restaurant

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

#### Modify specific restaurant

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


#### Create new zone

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

#### List all zones

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

#### Modify specific zone

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

#### Create new table

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

#### List all tables

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

#### Modify specific table

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

#### Create new vacation period

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

#### List all vacation periods

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

#### Modify specific vacation period

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

#### Create new booking period

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

#### List booking period

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

#### Modify specific booking period

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

### Booking Endpoints

Placeholder text

#### Create new booking

BookingCreateView

This endpoint allows for creating a new booking.

HTTP Method: POST

Path: /api/bookings

Request Parameters:

None
Request Body:

field1 (type, required): Description of the field.
field2 (type, optional): Description of the field.
Other fields as defined in the BookingSerializer.
Response:

Status Code: 201 Created
Content Type: application/json
Example Request:

http
Code kopieren
POST /api/bookings
Host: example.com
Content-Type: application/json

{
  "field1": "value1",
  "field2": "value2"
}
Example Response:

http
Code kopieren
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "field1": "value1",
  "field2": "value2",
  "created_at": "2023-06-05T12:34:56Z"
}
Note:

Ensure that the request body includes all required fields as defined in the BookingSerializer.
The endpoint will return a 400 Bad Request status code if any required fields are missing or invalid.

#### List all Bookings


BookingListView


This endpoint allows for listing all bookings for the current user's restaurant.

**HTTP Method:** GET

**Path:** /api/bookings

**Request Parameters:**

- None

**Request Body:**

- None

**Response:**

- **Status Code:** 200 OK
- **Content Type:** application/json

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
    "field1": "value1",
    "field2": "value2",
    "created_at": "2023-06-05T12:34:56Z"
  },
  {
    "id": 2,
    "field1": "value3",
    "field2": "value4",
    "created_at": "2023-06-06T12:34:56Z"
  }
]
```

**Note:**

- This endpoint returns all bookings associated with the current user's restaurant.
- The response will include all fields as defined in the `BookingSerializer`.
- Ensure that the user is authenticated, as the bookings are filtered based on the authenticated user's restaurant.

#### Modify bookings

BookingDetailView


This endpoint allows for retrieving, updating, or deleting a specific booking for the current user's restaurant.

**HTTP Method:** GET, PUT, DELETE

**Path:** /api/bookings/{id}

**Request Parameters:**

- `id` (integer, required): The ID of the booking to retrieve, update, or delete.

**Request Body:**

- `field1` (type, optional): Description of the field.
- `field2` (type, optional): Description of the field.
- Other fields as defined in the `BookingSerializer`.

**Response:**

- **Status Code:** 
  - 200 OK (for GET and PUT)
  - 204 No Content (for DELETE)
- **Content Type:** application/json

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
  "field1": "value1",
  "field2": "value2",
  "created_at": "2023-06-05T12:34:56Z"
}
```

**Example Request (PUT):**

```http
PUT /api/bookings/1
Host: example.com
Content-Type: application/json

{
  "field1": "new_value1",
  "field2": "new_value2"
}
```

**Example Response (PUT):**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "field1": "new_value1",
  "field2": "new_value2",
  "created_at": "2023-06-05T12:34:56Z"
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

- This endpoint filters bookings based on the authenticated user's restaurant.
- Ensure that the `id` provided in the path corresponds to a booking associated with the user's restaurant.
- Authentication is required for this endpoint.
- The PUT request allows for updating any of the fields defined in the `BookingSerializer`.
- The DELETE request will remove the specified booking from the system.

## Contributing

If you plan on contributing to this project, feel free to contact us.

## License

This repository is licensed under the [MIT License](LICENSE).
