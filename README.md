# OWASP Juice Shop API Security Testing – BOLA Vulnerability Assessment

> Practical API security assessment demonstrating identification and validation of a Broken Object Level Authorization (BOLA) vulnerability in OWASP Juice Shop.

## Executive Summary

A security assessment was performed against the OWASP Juice Shop API to evaluate authorization controls on basket-related endpoints. Testing identified a Broken Object Level Authorization (BOLA) vulnerability that allowed authenticated users to access and modify basket resources belonging to other users by manipulating object identifiers within API requests.

The vulnerability was successfully validated through unauthorized basket access, basket enumeration, item insertion, and item deletion activities. Due to the potential for unauthorized access and modification of user-owned resources, the finding was classified as High severity according to OWASP API Security Top 10 guidance.

## Overview

This project demonstrates the discovery and validation of a Broken Object Level Authorization (BOLA) vulnerability in the OWASP Juice Shop application.

The assessment was conducted in a controlled lab environment using Burp Suite Community Edition and Kali Linux. The objective was to evaluate whether authenticated users could access or manipulate resources belonging to other users by modifying object identifiers within API requests.

---

## Objectives

* Intercept and analyze API traffic
* Identify object references used by the application
* Test authorization controls
* Verify whether access control checks are properly enforced
* Document security findings and impact

---

## Lab Environment

### Operating System

* Kali Linux 2024

### Tools Used

* Burp Suite Community Edition
* Firefox Browser
* OWASP Juice Shop

### Target Application

* OWASP Juice Shop

---

## Methodology

### 1. Authentication

A valid user account was created and authenticated within the application.

### 2. Traffic Interception

Application traffic was intercepted using Burp Suite Proxy and analyzed within Repeater.

### 3. API Enumeration

Multiple API endpoints were identified, including basket-related endpoints.

Example:

GET /rest/basket/1

### 4. Authorization Testing

Basket identifiers were modified manually to determine whether authorization checks were enforced.

Examples tested:

```http
GET /rest/basket/1
GET /rest/basket/2
GET /rest/basket/3
GET /rest/basket/4
GET /rest/basket/5
GET /rest/basket/6
```

### 5. Impact Validation

The assessment verified that an authenticated user could:

* Access baskets belonging to other users
* View basket contents
* Add items to another user's basket
* Delete items from another user's basket

---

## Findings

### Vulnerability

Broken Object Level Authorization (BOLA)

### Classification

OWASP API Security Top 10:

API1:2023 Broken Object Level Authorization

CWE:

CWE-639 Authorization Bypass Through User-Controlled Key

### Severity

High

### CVSS v3.1 (Estimated)

7.5 High

## Finding Summary

| Vulnerability | Severity | Status |
|--------------|----------|--------|
| Broken Object Level Authorization (BOLA) | High | Confirmed |

Authenticated users were able to access and modify resources belonging to other users by manipulating object identifiers within API requests.

## Evidence

The following behaviors were observed:

| Test                            | Result  |
| ------------------------------- | ------- |
| Access Basket 1                 | Success |
| Access Basket 2                 | Success |
| Access Basket 3                 | Success |
| Access Basket 4                 | Success |
| Access Basket 5                 | Success |
| Access Basket 6                 | Success |
| Add Item to Another Basket      | Success |
| Delete Item from Another Basket | Success |

---

## Security Impact

An attacker could:

* Access other users' shopping carts
* Modify basket contents
* Delete products from another user's basket
* Interfere with purchases
* Enumerate user resources

This demonstrates insufficient authorization validation on object references supplied by the client.

---

## Screenshots

### 1. User Authentication Verification

![User Authentication](screenshots/01-user-authentication.png)

---

### 2. Legitimate Basket Access

![Legitimate Basket Access](screenshots/02-legitimate-basket-access.png)

---

### 3. Unauthorized Basket Access

![Unauthorized Basket Access](screenshots/03-unauthorized-basket-access.png)

---

### 4. Basket Enumeration

![Basket Enumeration](screenshots/04-basket-id-enumeration.png)

---

### 5. Unauthorized Basket Modification

![Basket Modification](screenshots/05-unauthorized-basket-modification.png)

---

### 6. Unauthorized Basket Item Deletion

![Basket Item Deletion](screenshots/06-unauthorized-basket-item-deletion.png)

## Remediation

The application should verify ownership of every basket before granting access.

Recommended controls:

* Enforce server-side authorization checks
* Validate resource ownership on every request
* Implement role-based access controls where appropriate
* Reject requests for resources not owned by the authenticated user

---

## Skills Demonstrated

- API Security Testing
- Burp Suite Community Edition
- OWASP API Top 10
- Broken Object Level Authorization (BOLA)
- HTTP Request Manipulation
- Authorization Testing
- Vulnerability Validation
- Security Documentation
- Kali Linux

 ## References

- OWASP API Security Top 10 2023
- CWE-639 Authorization Bypass Through User-Controlled Key
- OWASP Juice Shop Project

 ## Disclaimer

This project was conducted in a controlled lab environment for educational and ethical security testing purposes only. No unauthorized testing was performed against real-world systems.

## Conclusion

The assessment successfully identified a Broken Object Level Authorization vulnerability within the OWASP Juice Shop API. The vulnerability allows authenticated users to access and manipulate resources belonging to other users through predictable object identifiers.

This project demonstrates practical API security testing techniques and highlights the importance of enforcing authorization controls on all object references.

