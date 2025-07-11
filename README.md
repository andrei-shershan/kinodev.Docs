# Kinodev

- [What is about?](#what-is-about)
- [Architecture and stack](#architecture-and-stack)
  - [Architecture](#architecture)
  - [Stack](#stack)

## What is about

KinoDev is simple MVP project, representing Cinema management system.

> [!IMPORTANT]
> Current project state is delivered MVP, it contains only minimal happy flow path.
> Further development temporary postponed.

## Architecture

This is microservices architecture, uses several api, databases, etc.

![kinodev drawio (2)](https://github.com/user-attachments/assets/491d567d-1763-456a-995e-e63bc5d487aa)

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

> [!NOTE]
> Local and Live environment architectually the same, but they may use difference services / storages / containers for development and cost-saving reasons

> [!NOTE]
> I plan to simplify arcitecture by reducing amound of web-services (storage-service, email-service) and replace them with Azure Functions

## Stack

Backend: .net, etc
UI: React, typescipt, etc.
DB: MySQL, MongoDB, etc
etc.

Github Copilot

## Development

### Local running

Local run process with Docker

### Source code

Github source

### PR and branch policies

Github PR and branch policies, build actions

## Delivery

### Azure Devops

Azure devops environment

### Azure Portal

Azure Portal details

### CI / CD pipelines

Pipelines and applies process

## Monitoring

Monitoring with App insights

## Use cases

### Admin Flow

#### Admin signin

#### Admin review pages

#### Admin creation new moview showtime process

### User Flow

#### Purchase tickets

#### Review tickets

## Afterwords

### What is good here?

### What could be improved?

### What's next?
---
