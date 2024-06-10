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

# Modules

## User Module

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

## Restaurant Module

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

## Booking Module

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

## Module Name

Description of what the module does.

### Function/Class Name

Description of what the function/class does.

- Parameters/Attributes: Description of the parameters/attributes.
- Returns: Description of the return value (if applicable).
