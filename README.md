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
  - Shared - NuGet package keeping DTOs, common logic, etc, to avoid code duplicaiton between services
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

### Source code

All source code available on GitHub:
- [Docker](https://github.com/andrei-shershan/KinoDev.Docker)
- [UI](https://github.com/andrei-shershan/KinoDev.UI)
- [Identity](https://github.com/andrei-shershan/KinoDev.Identity)
- [ApiGateway](https://github.com/andrei-shershan/KinoDev.ApiGateway)
- [DomainService](https://github.com/andrei-shershan/KinoDev.DomainService)
- [PaymentService](https://github.com/andrei-shershan/KinoDev.Payment)
- [EmailService](https://github.com/andrei-shershan/KinoDev.EmailService)
- [StorageService](https://github.com/andrei-shershan/KinoDev.StorageService)
- [Functions](https://github.com/andrei-shershan/Kinodev.Functions)
- [Shared](https://github.com/andrei-shershan/KinoDev.Shared)

### Local running

Clone all repos above. 

Open Kinodev.Docker project, rename `.env.sample` to `.env`, replace all `{{ }}` values with propper keys / secrets.

Create an OpenSSL Configuration File `*.cnf`
Add next DNS:

```
DNS.1 = ui.kinodev.localhost
127.0.0.1 api-gateway.kinodev.localhost
127.0.0.1 domain-service.kinodev.localhost
127.0.0.1 ui.kinodev.localhost
127.0.0.1 identity.kinodev.localhost
127.0.0.1 payment-service.kinodev.localhost
127.0.0.1 email-service.kinodev.localhost
127.0.0.1 functions.kinodev.localhost
```

Generate the Certificate and Private Key, configure Traefik to Use Your Certificate, att `certs` folder into Docker project Root.

Adjust `C:\Windows\System32\drivers\etc\hosts`:

```
127.0.0.1 api-gateway.kinodev.localhost
127.0.0.1 domain-service.kinodev.localhost
127.0.0.1 ui.kinodev.localhost
127.0.0.1 identity.kinodev.localhost
127.0.0.1 images.kinodev.localhost
127.0.0.1 payment-service.kinodev.localhost
127.0.0.1 mongo-express.kinodev.localhost
127.0.0.1 servicebus.kinodev.localhost
127.0.0.1 sqledge.kinodev.localhost
127.0.0.1 rabbitmq.kinodev.localhost
127.0.0.1 rabbitmq-ui.kinodev.localhost
127.0.0.1 email-service.kinodev.localhost
127.0.0.1 gotenberg.kinodev.localhost
127.0.0.1 azurite-blob.kinodev.localhost
127.0.0.1 storage-service.kinodev.localhost
127.0.0.1 functions.kinodev.localhost
```

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
