# Test Plan: VWO Authentication

## 1. Role
Senior QA Automation Engineer / QA Lead with 15+ years of experience.

## 2. Purpose
Define an enterprise-grade, risk-based test plan for the VWO authentication surface at `https://app.vwo.com/#/login`, with coverage that is suitable for manual execution, automation handoff, and regression selection.

## 3. Context
The live login application exposes these authentication entry points:
- Email Address and Password
- Remember Me
- Forgot Password
- Google sign-in
- SSO sign-in
- Passkey sign-in
- Authentication-code, authenticator-code, and backup-code flows

VWO also documents session behavior including a default inactivity timeout and extended Remember Me session handling on the same browser/device.

## 4. Objectives
- Verify the login flow works for valid and invalid credentials.
- Validate authentication boundaries and session control.
- Confirm visible authentication methods behave correctly.
- Identify negative, security, and usability defects before release.
- Produce automation-ready coverage and a compact regression suite.

## 5. Scope
### In scope
- Login page load and rendering
- Email/password authentication
- Input validation and error handling
- Remember Me behavior
- Forgot Password behavior
- Google authentication flow
- SSO authentication flow
- Passkey authentication flow
- Auth-code, authenticator-code, and backup-code flows
- Logout, session expiry, and protected page access
- Cross-browser and responsive behavior for the login surface

### Out of scope
- Non-authentication application modules
- Provider-side defects outside VWO control
- Backend implementation details not exposed through the login journey

## 6. Assumptions and constraints
- Test accounts are available for valid, invalid, locked, and federated-auth scenarios.
- Google, SSO, and Passkey availability depends on account configuration and supported devices/browsers.
- Rate limiting and brute-force controls will be validated against documented security requirements, not guessed thresholds.

## 7. Test approach

### 7.1 Functional testing
Validate the happy path and input handling for the core login form.

Coverage:
- Login page loads successfully
- Email field accepts valid input
- Password field accepts valid input
- Password is masked
- Sign In succeeds with valid credentials
- Invalid credentials are rejected
- Empty fields are validated
- Invalid email formats are rejected
- Remember Me persists access as designed
- Forgot Password opens the reset flow correctly

### 7.2 Negative testing
Validate that the system fails safely for malformed and invalid inputs.

Coverage:
- Invalid email
- Invalid password
- Invalid email plus invalid password
- Empty email
- Empty password
- Both fields empty
- Malformed email
- Leading and trailing spaces
- Extremely long input
- Special characters
- Unauthorized account
- Authentication failure

### 7.3 Security testing
Validate authentication integrity and session protection.

Coverage:
- Authentication cannot be bypassed
- Protected pages cannot be accessed without authentication
- Password is not exposed
- Credentials are not exposed through URL
- Session is invalidated after logout
- Expired sessions cannot access protected resources
- Injection payloads are handled safely
- Authentication errors do not disclose sensitive information
- Brute-force and rate-limiting controls behave according to security requirements

### 7.4 UI and accessibility testing
Validate the visible login experience and interaction quality.

Coverage:
- Page layout
- Email field
- Password field
- Sign In button
- Remember Me
- Forgot Password
- Google, SSO, and Passkey entry points
- Error messages
- Focus behavior
- Keyboard navigation
- Responsive layout

### 7.5 Authentication integration testing
Validate external and device-based authentication flows end to end.

#### Google
Login -> Sign in with Google -> Google Authentication -> VWO

#### SSO
Login -> Sign in using SSO -> Email -> Identity Provider -> VWO

#### Passkey
Login -> Sign in with Passkey -> Device/Browser Authentication -> VWO

## 8. Prioritization model
### Critical
- Login success and failure handling
- Session validity and expiry
- Protected-page access control
- Credential leakage prevention

### High
- Remember Me
- Forgot Password
- Google authentication
- SSO authentication
- Passkey authentication

### Medium
- UI layout
- Error presentation
- Focus order
- Keyboard and responsive checks

## 9. Regression suite
Keep the always-run regression set small, stable, and automation-friendly:
- Valid login
- Invalid login
- Remember Me
- Logout and session invalidation
- Protected page access control
- Google sign-in
- SSO sign-in
- Passkey sign-in

## 10. Automation strategy
- Automate stable, repeatable, high-value scenarios first.
- Prioritize login, logout, session validation, and protected-resource checks.
- Automate federated flows only where provider access and environment stability are reliable.
- Keep brittle provider-dependent or device-dependent scenarios outside smoke automation.

## 11. Test data requirements
- Valid email/password account
- Invalid credentials
- Empty credential set
- Locked or unauthorized account
- Accounts enabled for Google, SSO, and Passkey
- Accounts enabled for code-based fallback flows
- Test browsers and devices that match supported configurations

## 12. Entry criteria
- Login application is reachable
- Required test accounts are provisioned
- External identity provider and passkey prerequisites are available
- Target browsers/devices are ready

## 13. Exit criteria
- Critical test cases pass
- High-priority negative and security cases pass
- No open blocker on login, session, or protected-access behavior
- Regression suite executed for the supported authentication paths

## 14. Risks
- Federated authentication availability may vary by environment.
- Session behavior may differ by browser/device and Remember Me state.
- Provider-side redirects can introduce instability in automation.

## 15. Deliverables
- Test plan
- Prioritized test cases
- Automation strategy
- Regression suite

## 16. Traceability
This plan maps directly to the documented VWO authentication surface and the observed login options in the live application.

## 17. Tone
Technical, precise, enterprise-grade, code-one.
