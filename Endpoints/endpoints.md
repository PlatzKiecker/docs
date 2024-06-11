# Models

- [Models](#models)
  - [User Models](#user-models)
    - [User Data Model](#user-data-model)
  - [Restaurant Models](#restaurant-models)
    - [Restaurant Data Model](#restaurant-data-model)
    - [Zone Data Model](#zone-data-model)
    - [Table Data Model](#table-data-model)
    - [Vacation Data Model](#vacation-data-model)
    - [BookingPeriod Data Model](#bookingperiod-data-model)
  - [Booking Models](#booking-models)
    - [Booking Data Model](#booking-data-model)

## User Models

### User Data Model

Represents a user who manages a restaurant.

- **Fields**:
    - `email`: Email of the user (unique).
    - `password`: Password for user authentication.
    - `created`: Timestamp of when the user was created.
    - `is_admin`: Boolean indicating if the user is an admin.

- **Methods**:
    - `create_user(email, password, **kwargs)`: Creates a new user.
    - `create_superuser(email, password)`: Creates a new superuser.
    - `has_perm(perm, obj=None)`: Returns `True` if the user has the specified permission.
    - `has_module_perms(app_label)`: Returns `True` if the user has permissions for the specified app label.
    - `is_staff`: Returns `True` if the user is a staff member.

- **Example Usage**:
    
    ```python
    from user.models import User
    
    user = User.objects.create_user(email="example@example.com", password="securepassword")
    user.save()
    
    superuser = User.objects.create_superuser(email="admin@example.com", password="supersecurepassword")
    superuser.save()
    ```

---

## Restaurant Models

### Restaurant Data Model

Represents a restaurant managed by a user.

- **Fields**:
    - `name`: Name of the restaurant.
    - `user`: One-to-one relationship with `User`, representing the owner of the restaurant.

- **Example Usage**:
    
    ```python
    from restaurant.models import Restaurant
    from user.models import User
    
    user = User.objects.create_user(email="owner@example.com", password="securepassword")
    restaurant = Restaurant.objects.create(name="Example Restaurant", user=user)
    ```

### Zone Data Model

Represents a zone within a restaurant.

- **Fields**:
    - `name`: Name of the zone.
    - `bookable`: Boolean indicating if the zone can be booked.
    - `restaurant`: Foreign key relationship to `Restaurant`.

- **Methods**:
    - `save(*args, **kwargs)`: Custom save method to update tables' bookable status if the zone is not bookable.

- **Example Usage**:
    
    ```python
    from restaurant.models import Zone, Restaurant
    
    restaurant = Restaurant.objects.get(name="Example Restaurant")
    zone = Zone.objects.create(name="Main Hall", bookable=True, restaurant=restaurant)
    ```

### Table Data Model

Represents a table within a zone of a restaurant.

- **Fields**:
    - `name`: Name of the table.
    - `capacity`: Number of seats at the table.
    - `bookable`: Boolean indicating if the table can be booked.
    - `combinable`: Boolean indicating if the table can be combined with others.
    - `zone`: Foreign key relationship to `Zone`.

- **Example Usage**:
    
    ```python
    from restaurant.models import Table, Zone
    
    zone = Zone.objects.get(name="Main Hall")
    table = Table.objects.create(name="Table 1", capacity=4, bookable=True, combinable=False, zone=zone)
    ```

### Vacation Data Model

Represents a vacation period during which the restaurant is closed.

- **Fields**:
    - `start`: Start date and time of the vacation.
    - `end`: End date and time of the vacation.
    - `restaurant`: Foreign key relationship to `Restaurant`.

- **Example Usage**:
    
    ```python
    from restaurant.models import Vacation, Restaurant
    
    restaurant = Restaurant.objects.get(name="Example Restaurant")
    vacation = Vacation.objects.create(start="2024-06-01 00:00:00", end="2024-06-15 23:59:59", restaurant=restaurant)
    ```

### BookingPeriod Data Model

Represents the booking periods available for a restaurant.

- **Fields**:
    - `weekday`: Enum representing the day of the week.
    - `open`: Opening time for bookings.
    - `close`: Closing time for bookings.
    - `restaurant`: Foreign key relationship to `Restaurant`.

- **Example Usage**:
    
    ```python
    from restaurant.models import BookingPeriod, Restaurant
    
    restaurant = Restaurant.objects.get(name="Example Restaurant")
    booking_period = BookingPeriod.objects.create(weekday="MO", open="09:00:00", close="18:00:00", restaurant=restaurant)
    ```

---

## Booking Models

### Booking Data Model

Represents a booking made by a guest at a restaurant.

- **Fields**:
    - `guest_name`: Name of the guest.
    - `guest_phone`: Phone number of the guest.
    - `start`: Start date and time of the booking.
    - `end`: End date and time of the booking (optional).
    - `guest_count`: Number of guests.
    - `status`: Status of the booking (e.g., pending, confirmed, seated, cancelled, completed).
    - `notes`: Additional notes for the booking (optional).
    - `table`: Foreign key relationship to `Table`.
    - `restaurant`: Foreign key relationship to `Restaurant`.

- **Methods**:
    - `__str__()`: Returns a string representation of the booking.
    - `calculate_booking_endtime()`: Calculates and returns the end time of the booking based on the restaurant's default duration.

- **Example Usage**:
    
    ```python
    from booking.models import Booking
    from restaurant.models import Restaurant, Table
    
    restaurant = Restaurant.objects.get(name="Example Restaurant")
    table = Table.objects.get(zone__restaurant=restaurant, capacity=4)
    booking = Booking.objects.create(guest_name="John Doe", guest_phone="1234567890", start="2024-06-03 12:00:00", guest_count=2, table=table, restaurant=restaurant)
    booking.save()
    ```
