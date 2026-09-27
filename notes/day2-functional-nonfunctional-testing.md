# QA Notes — Functional & Non-Functional Testing Concepts

## Object Properties Testing
Object properties refer to the attributes of UI elements on the front end — dropdowns, enable/disable buttons, radio buttons (e.g. male/female selection), etc. Every UI element has properties that need to be verified.

Example: after entering an email/username, the cursor should automatically move to the password field, ready for input. This is called **object property testing** and is part of functional testing under system testing.

## Database Testing
SQL is important here, but database testing requires a different skill set than pure functional testing. As a functional tester, the main focus is **DML (Data Manipulation Language)** operations — Insert, Update, Delete performed via the front end.

**Process:**
1. Perform an operation (insert/update/delete) on the front end (e.g. an employee module)
2. Check the database at the backend to confirm the data was stored/updated/deleted correctly

Since we don't know the front-end internals, this is **black box testing**; since we check via SQL queries at the backend, that part is **white box testing**. Combining both makes this **grey box testing**.

## Error Handling
Part of functional testing — focuses on verifying error messages on the UI. Messages should be clear, understandable, and easy to read by the client/user.

## Calculations and Manipulation Testing
Especially important in financial and banking applications. The goal is to verify that calculations work correctly, using positive, negative, valid, and invalid test data.

## Links — Existence and Execution Testing
Applies mainly to web-based applications (not mobile/desktop).
- **Link existence**: verifying the link exists as per the requirement document
- **Link execution**: verifying clicking the link navigates to the correct/desired page

**Types of links:**
1. **Internal link** — navigates to another section within the same page
2. **External link** — navigates to a different page
3. **Broken link** — performs no action; doesn't navigate anywhere (often placeholders for future functionality)

*Note: In GUI testing, we also check link color and whether it changes color after being clicked.*

## Cookies and Session Testing
Applies to web-based applications.
- **Cookies** are client-side — created and saved by the browser based on info the user provides. This explains why ads/info persist even after closing a window without logging out. Testing checks whether cookies are being created/saved correctly.
- **Sessions** are server-side — e.g., in banking applications, if no action is performed for a few minutes, the session times out and the user must log in again. This is a security mechanism (session timeout).

---

# Non-Functional Testing

Focused on **customer expectations**, not just requirements. Requires a different environment and skill set compared to functional testing — especially performance and security testing.

## Performance Testing
Measures how quickly an application responds. Mainly relevant for web applications (less relevant for desktop, where speed isn't usually an issue).

Three types:
1. **Load Testing** — gradually increasing the number of users/load on the application
2. **Stress Testing** — suddenly increasing/decreasing load to check if/where the application breaks
3. **Volume Testing** — checking how much data the application can handle (e.g., large uploads, high record counts)

## Security Testing
Involves two key concepts:
- **Authentication** — verifying user identity (e.g., correct login credentials)
- **Authorization** — verifying restricted access (e.g., HR department shouldn't access financial data)

## Recovery Testing
Testing the ability to go from an abnormal to a normal state — e.g., recovering deleted data (Gmail's Trash folder, or Drafts) is a recovery testing example.

## Compatibility Testing
Checks whether the software works correctly across different devices/versions.
- **Forward compatibility** — newer versions should work as expected
- **Backward compatibility** — older versions should still run correctly on current devices

**Hardware/Configuration Testing** falls under this — ensuring the application works across different hardware/OS (Windows, Linux, etc.)

## Installation Testing
Verifies the installation and uninstallation process:
- Is the installation screen clear and simple?
- Does uninstallation work properly, cleanly removing all files?
- Note: leftover files from incomplete uninstalls can cause issues on reinstallation

---

## Interview Note
**Q: If you find extra/unnecessary functionality during testing that isn't in the requirements, is it a bug?**
**A: Yes.** Any functionality should match what's defined in the FRS (Functional Requirements Specification) document. Extra features not in the requirements count as bugs — this also relates to **garbage testing** (removing unnecessary/unrequested features), which falls under security and garbage testing practices.
