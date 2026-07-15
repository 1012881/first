## ADDED Requirements

### Requirement: User Registration
The system SHALL allow new users to register with a unique username and password.

#### Scenario: Successful registration
- **WHEN** a user submits a form with a unique username and password (min 6 characters)
- **THEN** the system creates a new user account with BCrypt-encrypted password
- **AND** returns a success message

#### Scenario: Duplicate username registration
- **WHEN** a user submits a registration form with an already-taken username
- **THEN** the system returns an error message indicating the username already exists

### Requirement: User Login
The system SHALL authenticate registered users and return a JWT token.

#### Scenario: Successful login
- **WHEN** a user submits correct username and password
- **THEN** the system returns a JWT token valid for 7 days
- **AND** includes user nickname in the response

#### Scenario: Invalid credentials
- **WHEN** a user submits incorrect username or password
- **THEN** the system returns a 401 error with message "用户名或密码错误"

### Requirement: JWT Authentication Guard
The system SHALL reject all API requests (except auth endpoints) that do not include a valid JWT token.

#### Scenario: Request without token
- **WHEN** a request is made to any protected endpoint without an Authorization header
- **THEN** the system returns a 401 error

#### Scenario: Request with expired token
- **WHEN** a request is made with an expired JWT token
- **THEN** the system returns a 401 error

#### Scenario: Request with valid token
- **WHEN** a request is made with a valid JWT token
- **THEN** the system extracts the user ID from the token
- **AND** allows the request to proceed
