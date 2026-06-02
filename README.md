# OWASP Juice Shop API Security Testing – BOLA Vulnerability Assessment

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

GET /rest/basket/1
GET /rest/basket/2
GET /rest/basket/3
GET /rest/basket/4
GET /rest/basket/5
GET /rest/basket/6

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

---

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

## Remediation

The application should verify ownership of every basket before granting access.

Recommended controls:

* Enforce server-side authorization checks
* Validate resource ownership on every request
* Implement role-based access controls where appropriate
* Reject requests for resources not owned by the authenticated user

---

## Conclusion

The assessment successfully identified a Broken Object Level Authorization vulnerability within the OWASP Juice Shop API. The vulnerability allows authenticated users to access and manipulate resources belonging to other users through predictable object identifiers.

This project demonstrates practical API security testing techniques and highlights the importance of enforcing authorization controls on all object references.

