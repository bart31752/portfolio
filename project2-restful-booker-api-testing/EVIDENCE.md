# Restful Booker API Testing - Evidence & Observations

This document should act as a non-exhaustive **VISUAL** reference in cases where postman may not be available to exemplify:  
- scripts used
- endpoints exhausted
- collection structure
- sample observations
- logic
 
**[View the Document on Google Drive]([https://drive.google.com/file/d/1XljRrPtq-v1lmuWZhM00IN7jbEfcdzFk/view?usp=drive_link])**

---

## 🧪 Test Collection Structure

The API testing was conducted using a Postman collection structured to validate the main CRUD operations (Create, Read, Update, Delete) for bookings, following a "Happy Path" scenario.

The collection included the following requests in sequence:
1.  **POST Auth** - Create a token
2.  **GET Booking IDs** - Retrieve a list of booking IDs
3.  **POST Create Booking** - Create a new booking
4.  **GET Booking** - Retrieve the created booking's details
5.  **PUT Update Booking** - Fully update the booking
6.  **PATCH Update Booking** - Partially update the booking
7.  **DELETE Booking** - Delete the booking


## 🔍 Key Observations & Findings

### 1. Authentication & Token Management
-   A `POST /auth` endpoint is used to generate a 15-character string token upon successful authentication with valid credentials (`admin`/`password123`).
-   **Observation:** The generated token was consistently 15 characters long. This was leveraged in tests to validate the token's format.
-   **Scripting:** The token was dynamically captured as a collection variable for reuse in subsequent requests (PUT, PATCH, DELETE) that require authentication via a `Cookie` header.

### 2. Data Integrity Risks
-   **Partial Updates (PATCH):** The API accepts `empty` or `null` values for any field during a PATCH request. This poses a potential data integrity risk, as it could allow invalid data to overwrite existing valid data.
-   **Input Validation:** The API does not appear to rigorously validate the format of input data in certain fields (e.g., `checkin` and `checkout` dates), which could lead to incorrect data being stored.

### 3. Security Consideration
-   **Observation:** The `POST /booking` (Create Booking) endpoint does not require any form of authentication. This is a potential security flaw, as it allows anyone to create bookings without verification.

### 4. Testing Scripts
-   Pre-request and Post-response scripts were effectively used to:
    -   Set collection variables (e.g., `baseUrl`, `token`, `bookingid`).
    -   Validate HTTP status codes.
    -   Verify response formats (JSON).
    -   Check data types and properties (e.g., ensuring `bookingid` is a number and not null).
    -   Log useful information for debugging (e.g., number of entries in a filtered search).
