# Kinodev

- [What is about?](#what-is-about)
- [Architecture](#architecture)
- [Stack](#stack)

## What is about

KinoDev is a minimalistic MVP for streamlined cinema management and ticket sales. Built with a modern tech stack, it lets theater owners schedule screenings, configure halls and seat layouts, track real-time availability, and process online payments securely.

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

Backend: **.NET (C#)**, **ASP.NET Web API**

FrontEnd: **React**, **TypeScript**, **JavaScript** 

DB: **MySQL**, **MongoDB**, **Entity Framework Core**

Authentication: **ASP.NET Identity**

Message Broker: **Azure Service Bus**, **RabbitMQ**

Serverless: **Azure Functions**

Testing: **Unit Tests (xUnit)**

Containerization: **Docker**, **Traefik** reverse proxy

Version control: **Git**

Package Management: NuGet (private packages via **GitHub Packages**)

CI/CD: **GitHub Actions**, **Azure DevOps Pipelines**

Cloud: **Microsoft Azure**

Development Tools & IDEs: **Visual Studio**, **Visual Studio Code**

AI-Assisted Tools:: **Github Copilot**, **ChatGPT**

Code Hosting: **GitHub**

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
