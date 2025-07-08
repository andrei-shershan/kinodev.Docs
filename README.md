# Kinodev

- [What is about?](#what-is-about)
- [Architecture and stack](#architecture-and-stack)
  - [Architecture](#architecture)
  - [Stack](#stack)

## What is about

KinoDev is simple MVP project, representing Cinema management system.

> [!WARNING]
> This is MVP / Proof of concept only, it contais only limited happy path


## Architecture and stack

### Architecture

This is microservices architecture, uses several api, databases, etc.

![kinodev drawio (1)](https://github.com/user-attachments/assets/d3264515-08c7-4a2d-81aa-7adafb2051cc)


Main components:
- Frontend;
- Backend:
  - API gateway - main API hub;
  - Domain-service - responsible for working with DB;
  - Email-service - responsible for email-notifications / email sending;
  - Storage-service - responsible for adding resources (images, pdf) into storage, handling PDF service;
  - Payment-service - responsible for payment processing with Stripe and saving data in it's separate DB;
  - PDF Functions - responsible for PDF generation with 3rd party;
  - Message broker - responsible for interservices communication;
  - Functions triggered by Service bus - responsible for proper business logic handling;
  - Identity - responsible for authorization;
- Docker - for local development


### Stack


  
---
