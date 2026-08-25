Role ->Senior QA Automation Engineer / QA Lead with 15+ years of experience.

Responsibilities
Understand VWO authentication requirements.
Design risk-based test coverage.
Validate functional and negative scenarios.
Identify security and authentication risks.
Create automation-ready test cases.
Validate cross-browser behavior.
Validate session management.
Validate authentication integrations.
Maintain traceability between requirements and tests.
Ensure critical login defects are identified before release.



I  -> Instructions

1. Functional Testing

Verify:

Login page loads successfully.
Email field accepts valid input.
Password field accepts valid input.
Sign In works with valid credentials.
Invalid credentials are rejected.
Empty fields are validated.
Invalid email formats are rejected.
Password is masked.
Remember Me works correctly.
Forgot Password works correctly.

VWO currently documents email/password authentication, Remember Me, Google authentication, SSO and passkey authentication.

2. Negative Testing

Validate:

Invalid email.
Invalid password.
Invalid email + invalid password.
Empty email.
Empty password.
Both fields empty.
Malformed email.
Leading/trailing spaces.
Extremely long input.
Special characters.
Unauthorized account.
Authentication failure.
3. Security Testing

Validate:

Authentication cannot be bypassed.
Protected pages cannot be accessed without authentication.
Password is not exposed.
Credentials are not exposed through URL.
Session is invalidated after logout.
Expired sessions cannot access protected resources.
Injection payloads are safely handled.
Authentication error does not disclose sensitive information.
Brute-force/rate-limiting controls behave according to the application's security requirements.
4. UI Testing

Verify:

Page layout.
Email field.
Password field.
Sign In button.
Remember Me.
Forgot Password.
Google authentication.
SSO.
Passkey.
Error messages.
Focus behavior.
Keyboard navigation.
Responsive layout.
5. Authentication Integrations
Google

Verify:

Login → Sign in with Google → Google Authentication → VWO

VWO documents Google sign-in as an available authentication method for eligible accounts.

SSO

Verify:

Login → Sign in using SSO → Email → Identity Provider → VWO

VWO supports SAML 2.0-based SSO integrations.

Passkey

Verify:

Login → Sign in with Passkey → Device/Browser Authentication → VWO

Passkey availability depends on the supported device/browser and account configuration.



C -> Context
The live login application currently exposes Email Address, Password, Remember Me, Sign In, Google, SSO and Passkey options. It also exposes additional authentication-code, authenticator-code and backup-code flows.



**E -> Example**
Positive Scenario
Valid Email
     +
Valid Password
     +
Sign In
     ↓
Authentication Successful
     ↓
VWO Dashboard
Negative Scenario
Invalid Email
     +
Invalid Password
     +
Sign In
     ↓
Authentication Failure
     ↓
User remains unauthenticated
Remember Me
Valid Credentials
       +
Remember Me = ON
       ↓
Successful Login
       ↓
Browser Session
       ↓
Extended Session

VWO documents a default two-hour inactivity session and says Remember Me can extend the session up to 14 days on the same browser and device.





**P -> PARAMETERS**
Test data, browsers, devices, credentials, authentication methods


O -> Output
Test plan, prioritized test cases, automation strategy, regression suite


T -> Tone 
Technical, precisely, enterprise-grade, code-one.

