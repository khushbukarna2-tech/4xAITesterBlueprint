# Test Cases: VWO Authentication

## Reference
- PRD/source: VWO authentication requirements
- Scope: `https://app.vwo.com/#/login`

## Test data
- Valid user with email/password access
- Invalid credentials
- Unauthorized/locked user
- User with Google auth enabled
- User with SSO enabled
- User with Passkey enabled
- User with code-based fallback enabled

## Priority model
- P0: login, session, protected-access, security bypass
- P1: core auth flows, federated auth, Remember Me, Forgot Password
- P2: UI, accessibility, responsive behavior

---

## Functional test cases

### TC-F01 - Login page loads successfully
- **Priority:** P0
- **Type:** Functional
- **Automation:** Yes
- **Preconditions:** User is not authenticated
- **Steps:**
  1. Open the VWO login page.
  2. Observe the page render.
- **Expected:**
  - Login page loads without error.
  - Email, Password, Sign In, Remember Me, Forgot Password, Google, SSO, and Passkey are visible.

### TC-F02 - Sign in with valid email and password
- **Priority:** P0
- **Type:** Functional
- **Automation:** Yes
- **Preconditions:** Valid user exists
- **Steps:**
  1. Enter a valid email.
  2. Enter a valid password.
  3. Click Sign In.
- **Expected:**
  - Authentication succeeds.
  - User is redirected to the dashboard or authenticated landing page.

### TC-F03 - Reject invalid credentials
- **Priority:** P0
- **Type:** Functional / Negative
- **Automation:** Yes
- **Preconditions:** User is not authenticated
- **Steps:**
  1. Enter an invalid email/password combination.
  2. Click Sign In.
- **Expected:**
  - Login fails.
  - User remains unauthenticated.
  - A non-sensitive error message is shown.

### TC-F04 - Validate empty email field
- **Priority:** P0
- **Type:** Validation
- **Automation:** Yes
- **Preconditions:** User is not authenticated
- **Steps:**
  1. Leave Email empty.
  2. Enter any password.
  3. Click Sign In.
- **Expected:**
  - Email validation is shown.
  - Login is blocked.

### TC-F05 - Validate empty password field
- **Priority:** P0
- **Type:** Validation
- **Automation:** Yes
- **Preconditions:** User is not authenticated
- **Steps:**
  1. Enter any email.
  2. Leave Password empty.
  3. Click Sign In.
- **Expected:**
  - Password validation is shown.
  - Login is blocked.

### TC-F06 - Reject malformed email format
- **Priority:** P0
- **Type:** Validation
- **Automation:** Yes
- **Preconditions:** User is not authenticated
- **Steps:**
  1. Enter malformed email values such as `user@`, `user.com`, or `user@@test.com`.
  2. Enter a password.
  3. Click Sign In.
- **Expected:**
  - Email format is rejected.
  - Login is blocked.

### TC-F07 - Remember Me keeps session as designed
- **Priority:** P1
- **Type:** Functional
- **Automation:** Partial
- **Preconditions:** Valid user exists
- **Steps:**
  1. Select Remember Me.
  2. Sign in with valid credentials.
  3. Close and reopen the browser session as applicable.
- **Expected:**
  - Session persists according to product rules.
  - User remains signed in for the supported duration on the same device/browser.

### TC-F08 - Forgot Password opens reset flow
- **Priority:** P1
- **Type:** Functional
- **Automation:** Yes
- **Preconditions:** User is on login page
- **Steps:**
  1. Click Forgot Password.
- **Expected:**
  - Password reset flow opens successfully.

---

## Negative test cases

### TC-N01 - Reject invalid email and invalid password together
- **Priority:** P0
- **Type:** Negative
- **Automation:** Yes
- **Preconditions:** User is not authenticated
- **Steps:**
  1. Enter invalid email.
  2. Enter invalid password.
  3. Click Sign In.
- **Expected:**
  - Authentication fails safely.
  - No account is created or exposed.

### TC-N02 - Handle leading and trailing spaces
- **Priority:** P1
- **Type:** Negative
- **Automation:** Yes
- **Preconditions:** User is not authenticated
- **Steps:**
  1. Enter email/password with leading and trailing spaces.
  2. Click Sign In.
- **Expected:**
  - Inputs are trimmed or rejected per design.
  - Authentication outcome is correct and consistent.

### TC-N03 - Handle extremely long input
- **Priority:** P1
- **Type:** Negative
- **Automation:** Yes
- **Preconditions:** User is not authenticated
- **Steps:**
  1. Enter an extremely long email or password value.
  2. Click Sign In.
- **Expected:**
  - UI remains stable.
  - Input is constrained or rejected safely.

### TC-N04 - Handle special characters safely
- **Priority:** P1
- **Type:** Negative / Security
- **Automation:** Yes
- **Preconditions:** User is not authenticated
- **Steps:**
  1. Enter special characters in email/password fields.
  2. Click Sign In.
- **Expected:**
  - No unexpected behavior occurs.
  - Authentication fails safely if credentials are invalid.

### TC-N05 - Unauthorized account cannot sign in
- **Priority:** P0
- **Type:** Negative
- **Automation:** Yes
- **Preconditions:** Unauthorized or locked user exists
- **Steps:**
  1. Enter the unauthorized account credentials.
  2. Click Sign In.
- **Expected:**
  - Access is denied.
  - Error message does not reveal sensitive details.

---

## Security test cases

### TC-S01 - Protected page cannot be accessed without authentication
- **Priority:** P0
- **Type:** Security
- **Automation:** Yes
- **Preconditions:** User is logged out
- **Steps:**
  1. Directly open a protected VWO page URL.
- **Expected:**
  - User is redirected to login or blocked.

### TC-S02 - Logout invalidates the session
- **Priority:** P0
- **Type:** Security
- **Automation:** Yes
- **Preconditions:** User is signed in
- **Steps:**
  1. Click Logout.
  2. Use browser back navigation or refresh protected page.
- **Expected:**
  - Session is invalidated.
  - Protected resources are no longer accessible.

### TC-S03 - Expired session cannot access protected resources
- **Priority:** P0
- **Type:** Security
- **Automation:** Partial
- **Preconditions:** Session timeout can be simulated
- **Steps:**
  1. Sign in.
  2. Let the session expire or simulate inactivity timeout.
  3. Attempt to access a protected page.
- **Expected:**
  - Session is treated as expired.
  - Access is denied.

### TC-S04 - Credentials are not exposed in URL
- **Priority:** P0
- **Type:** Security
- **Automation:** Yes
- **Preconditions:** User is on login page
- **Steps:**
  1. Sign in with valid or invalid credentials.
  2. Inspect browser URL.
- **Expected:**
  - Credentials are not present in the URL.

### TC-S05 - Authentication errors do not disclose sensitive information
- **Priority:** P0
- **Type:** Security
- **Automation:** Yes
- **Preconditions:** Invalid credentials available
- **Steps:**
  1. Attempt login with invalid credentials.
  2. Review the error message.
- **Expected:**
  - Error message is generic.
  - No stack trace, account state, or security detail is revealed.

### TC-S06 - Injection payloads are handled safely
- **Priority:** P0
- **Type:** Security
- **Automation:** Partial
- **Preconditions:** User is on login page
- **Steps:**
  1. Enter basic injection payloads in the input fields.
  2. Submit the form.
- **Expected:**
  - Payload is treated as text.
  - No script execution or unsafe behavior occurs.

### TC-S07 - Brute-force/rate limiting behavior is enforced
- **Priority:** P0
- **Type:** Security
- **Automation:** Partial
- **Preconditions:** Security testing window is approved
- **Steps:**
  1. Repeat invalid sign-in attempts as allowed by security rules.
  2. Observe system response.
- **Expected:**
  - Rate limiting or lockout behaves according to requirements.
  - No bypass is possible.

---

## UI and accessibility test cases

### TC-U01 - Login page layout renders correctly
- **Priority:** P2
- **Type:** UI
- **Automation:** Partial
- **Preconditions:** User is on login page
- **Steps:**
  1. Review the page layout.
- **Expected:**
  - All key controls are visible and aligned.

### TC-U02 - Error messages are visible and readable
- **Priority:** P2
- **Type:** UI
- **Automation:** Yes
- **Preconditions:** Trigger validation or authentication error
- **Steps:**
  1. Submit invalid data.
  2. Observe the error area.
- **Expected:**
  - Error message is visible, readable, and near the relevant control.

### TC-U03 - Focus behavior and keyboard navigation work
- **Priority:** P2
- **Type:** Accessibility
- **Automation:** Partial
- **Preconditions:** User is on login page
- **Steps:**
  1. Navigate using Tab and Shift+Tab.
  2. Activate controls using keyboard only.
- **Expected:**
  - Logical focus order exists.
  - Controls are keyboard accessible.

### TC-U04 - Responsive layout remains usable
- **Priority:** P2
- **Type:** UI
- **Automation:** Partial
- **Preconditions:** Browser viewport can be resized
- **Steps:**
  1. View the page on desktop and mobile-sized viewports.
- **Expected:**
  - Login form remains usable and intact.

---

## Authentication integration test cases

### TC-I01 - Google sign-in works end to end
- **Priority:** P1
- **Type:** Integration
- **Automation:** Partial
- **Preconditions:** Google auth is enabled for the account
- **Steps:**
  1. Click Google.
  2. Complete Google authentication.
  3. Return to VWO.
- **Expected:**
  - User is authenticated in VWO successfully.

### TC-I02 - SSO sign-in works end to end
- **Priority:** P1
- **Type:** Integration
- **Automation:** Partial
- **Preconditions:** SSO is enabled for the account
- **Steps:**
  1. Click SSO.
  2. Enter email if prompted.
  3. Complete identity provider authentication.
  4. Return to VWO.
- **Expected:**
  - User is authenticated in VWO successfully.

### TC-I03 - Passkey sign-in works end to end
- **Priority:** P1
- **Type:** Integration
- **Automation:** Partial
- **Preconditions:** Passkey is enabled on a supported device/browser
- **Steps:**
  1. Click Passkey.
  2. Complete device/browser authentication.
  3. Return to VWO.
- **Expected:**
  - User is authenticated in VWO successfully.

### TC-I04 - Code-based fallback flow works
- **Priority:** P1
- **Type:** Integration / Functional
- **Automation:** Partial
- **Preconditions:** Account supports authentication-code, authenticator-code, or backup-code flow
- **Steps:**
  1. Start the fallback authentication flow.
  2. Enter a valid code.
  3. Complete sign-in.
- **Expected:**
  - User is authenticated successfully.

---

## Regression subset
- TC-F02
- TC-F03
- TC-F07
- TC-S01
- TC-S02
- TC-I01
- TC-I02
- TC-I03

## Notes
- Automation priority should start with P0 and stable P1 flows.
- Federated and device-bound flows should be automated only where the environment is stable.
