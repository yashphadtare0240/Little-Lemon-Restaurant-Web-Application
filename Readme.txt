LITTLE LEMON - META BACK-END CAPSTONE
===================================

START HERE
1. Install MySQL and create the database: CREATE DATABASE littlelemon CHARACTER SET utf8mb4;
2. Create and activate a Python virtual environment.
3. pip install -r requirements.txt
4. Set MYSQL_PASSWORD in your environment if the MySQL root user has a password.
5. python manage.py migrate
6. python manage.py createsuperuser
7. python manage.py runserver
8. Open http://127.0.0.1:8000/ and http://127.0.0.1:8000/book/

API PATHS TO TEST IN INSOMNIA (base URL http://127.0.0.1:8000)
GET     /restaurant/menu-items/                List menu items (public)
POST    /restaurant/menu-items/                Create menu item (Token auth)
GET     /restaurant/menu-items/1/              Retrieve menu item
PUT     /restaurant/menu-items/1/              Replace menu item (Token auth)
PATCH   /restaurant/menu-items/1/              Partially update menu item (Token auth)
DELETE  /restaurant/menu-items/1/              Delete menu item (Token auth)
GET     /restaurant/bookings/                  List bookings
GET     /restaurant/bookings/?date=2026-11-10 Filter bookings by date
POST    /restaurant/bookings/                  Create booking (public)
GET     /restaurant/bookings/1/                Retrieve booking
PUT     /restaurant/bookings/1/                Replace booking (Token auth)
PATCH   /restaurant/bookings/1/                Edit booking (Token auth)
DELETE  /restaurant/bookings/1/                Delete booking (Token auth)
GET     /bookings?date=2026-11-10             Legacy UI endpoint {"bookings": [...]}
POST    /bookings                             Legacy UI booking create
GET     /reservations?date=2026-11-10         Alias for booking list
POST    /restaurant/auth/users/               Register user
POST    /restaurant/auth/token/login/         Obtain auth token
POST    /restaurant/api-token-auth/           Obtain auth token (alternative)
POST    /restaurant/auth/token/logout/        Revoke token (authenticated)

For authenticated requests use header: Authorization: Token YOUR_TOKEN
Send Content-Type: application/json for JSON requests.

EXAMPLE REQUEST BODIES
Menu: {"title":"Greek Salad","price":"12.50","inventory":15}
Booking: {"first_name":"Asha","reservation_date":"2026-11-10","reservation_slot":12}
Registration: {"username":"reviewer","password":"SecurePass123!"}
Token login: {"username":"reviewer","password":"SecurePass123!"}
Reservation slots: integers 10 through 20 (24-hour time).
Each date + slot combination is unique; duplicates return validation errors.

UNIT TESTS
python manage.py test restaurant
Optional SQLite test-only fallback (no MySQL required):
Linux/macOS: USE_SQLITE=1 python manage.py test restaurant
PowerShell: $env:USE_SQLITE='1'; python manage.py test restaurant

GIT/GITHUB SUBMISSION
Create your own repository and commit/push the project, including this Readme.txt.
Example: git init && git add . && git commit -m "Little Lemon capstone"
Then add your GitHub remote and push the main branch. Submit YOUR repository URL to Coursera.
The ZIP itself does not constitute a Git commit or GitHub submission.

IMPORTANT: This sample is intended for local coursework demonstration.
Public anonymous booking creation and public booking names are coursework requirements,
not production-ready authorization/privacy controls. Add ownership checks and rate limits
before deploying publicly. Never commit actual MySQL passwords or production secrets.
