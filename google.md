# Google SAML SSO Configuration for SSD (Secure Software Delivery)

Authentication Type: Google SAML 2.0  
Deployment: Kubernetes  

---

## Table of Contents

1. Purpose  
2. Prerequisites  
3. Google SAML Application Setup  
4. Create Kubernetes Secret for SAML Metadata  
5. Update SSD Gate ConfigMap  
6. Update SSD Gate Deployment  
7. Restart SSD Gate Pod  
8. Configure Organisation & Role Mapping  
9. Restart Gate Service  
10. Validation  
11. Post-Login Access Management  
12. Common Issues & Troubleshooting  
13. Summary  

---

## 1. Purpose

This document provides a step-by-step technical guide to configure Google SAML Single Sign-On (SSO) for an SSD instance. It covers Google-side prerequisites, Kubernetes configuration, SSD Gate changes, and post-configuration validation.

---

## 2. Prerequisites

### 2.1 Google Workspace

- Google Workspace Admin access
- Permission to create Custom SAML applications
- Users must exist in Google Workspace
- Required Google Groups (example: `ssd-sandbox-admin`)

### 2.2 SSD Environment

- SSD deployed on Kubernetes
- Namespace where SSD is installed
- `kubectl` access with permission to:
  - Create secrets
  - Edit ConfigMaps
  - Update deployments
  - Restart pods

---

## 3. Google SAML Application Setup (High-Level)

> Please refer to the detailed Google SAML creation document for step-by-step screenshots.

1. Log in to Google Admin Console
2. Navigate to:  
   Apps → Web and mobile apps → Add app → Add custom SAML app
3. Configure the application using SSD SAML values:
   - ACS URL
   - Entity ID
4. Download the IdP Metadata XML file  
   Default filename: `GoogleIDPMetadata.xml`

This metadata file is required for SSD Gate configuration.

---

## 4. Create Kubernetes Secret for SAML Metadata

### 4.1 Rename Metadata File

```bash
mv GoogleIDPMetadata.xml metadata.xml
