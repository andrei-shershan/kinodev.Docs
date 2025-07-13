# KinoDev

KinoDev is a minimalistic MVP for streamlined cinema management and ticket sales. Built with a modern tech stack, it lets theater owners schedule screenings, configure halls and seat layouts, track real-time availability, and process online payments securely.

__Follow this link to see the website: [KINODEV - minimalistic MVP](https://ui-hxh5eqemg5dmeddy.polandcentral-01.azurewebsites.net/)__

> [!NOTE]
> I used free or low-cost Azure services in the cloud, so **it runs a bit slowly**.

---

- [What is about?](#what-is-about)
- [Architecture](#architecture)
- [Stack](#stack)

## Architecture

This is a microservices architecture; it uses several APIs, databases, etc.

![kinodev drawio (2)](https://github.com/user-attachments/assets/491d567d-1763-456a-995e-e63bc5d487aa)

Main components:
- Frontend;
- Backend:
  - API gateway - main API hub;
  - Domain-service - responsible for working with DB;
  - Email-service - responsible for email-notifications / email sending;
  - Storage-service - responsible for adding resources (images, pdf) into storage, handling PDF service;
  - Payment-service - responsible for payment processing with Stripe and saving data in its separate DB;
  - PDF Functions - responsible for PDF generation with 3rd party;
  - Message broker - responsible for interservices communication;
  - Functions triggered by Service bus - responsible for proper business logic handling;
  - Identity - responsible for authorization;
  - Shared - NuGet package keeping DTOs, common logic, etc, to avoid code duplication between services
- Docker - for local development

> [!NOTE]
> Local and Live environments, in general, are the same, but they may use difference services / storages / containers for development and cost-saving reasons

> [!NOTE]
> I plan to simplify the architecture by reducing the number of web services (e.g. storage, email) and replacing them with Azure Functions

## Stack

Backend: **.NET (C#)**, **ASP.NET Web API**

FrontEnd: **React**, **TypeScript**, **JavaScript** 

DB: **MySQL**, **MongoDB**, **Entity Framework Core**

Authentication: **ASP.NET Identity**

Message Broker: **Azure Service Bus**, **RabbitMQ**

Serverless: **Azure Functions**

Testing: **Unit Tests (xUnit)**

Containerization: **Docker**, **Traefik** reverse proxy

Distributed Cache: **Redis**

Version control: **Git**

Package Management: **NuGet** (private packages via **GitHub Packages**)

CI/CD: **GitHub Actions**, **Azure DevOps Pipelines**

Cloud: **Microsoft Azure**

Development Tools & IDEs: **Visual Studio**, **Visual Studio Code**

Code Hosting: **GitHub**

AI-Assisted Tools*: **Github Copilot**, **ChatGPT**

_*AI was used mostly to assist, autocomplete, create boilerplates, vibe-coding took less than 30% of overall time. _

## Development

### Source code

All source code is available on GitHub:
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

Open Kinodev.Docker project, rename `.env.sample` to `.env`, replace all `{{ PROPER_KEY }}` values with proper keys / secrets.

Create an OpenSSL Configuration File `*.cnf`
Add the following DNS entries:

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

Generate the Certificate and Private Key, configure Traefik to Use Your Certificate, add `certs` folder to the root of the Docker project.

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

Navigate to `KinoDev.Docker` project, run `docker compose up --build -d`

<img width="977" height="507" alt="image" src="https://github.com/user-attachments/assets/aa713d12-9b78-43f7-a162-9590d7b698c2" />

Then all containers should be running in Docker

<img width="1875" height="945" alt="image" src="https://github.com/user-attachments/assets/b1b2e0ef-0e6a-49ec-9294-34ef8450e77d" />

And website is available on `ui.kinodev.localhost`

<img width="886" height="1024" alt="image" src="https://github.com/user-attachments/assets/94b427d8-5ab1-4c61-a259-eee41fa90765" />

### PR and branch policies

> [!NOTE]
> I know that for now commit history looks terrible :smile:> 
> In a real-life business project I would use proper commit messages, including ticket number and code changes description 

Direct commits to the `main` branch are disallowed by **branch policy**, all changes must be merged via **pull requests**.

Builds are run via **GitHub Actions** before pull request is merged.

<img width="908" height="166" alt="image" src="https://github.com/user-attachments/assets/5c89ce57-0b85-413a-9a12-ac27bb990f13" />

## Delivery

### Azure Portal

Azure Services are properly setup:

<img width="1733" height="829" alt="image" src="https://github.com/user-attachments/assets/3278dc43-ceda-4f20-b0c8-1c61ca85bb3f" />

### Azure Devops and CI / CD pipelines

Azure Devops setup to support Delivery / Deploy:

Environements:

<img width="1129" height="644" alt="image" src="https://github.com/user-attachments/assets/5a4ec617-f3fa-4145-97cf-ab299cca29b8" />

Service connection:
<img width="1006" height="953" alt="image" src="https://github.com/user-attachments/assets/4aefa90e-d0a6-4d1a-a93d-b6166fec40f3" />

Pipelines (use existing project pipelines from GitHub):
<img width="1909" height="817" alt="image" src="https://github.com/user-attachments/assets/5d6d80e1-a62c-4704-99bd-631faa38b5c2" />

Pipelines use Environment Variables:
<img width="1006" height="951" alt="image" src="https://github.com/user-attachments/assets/0fca6cfa-4950-42dd-aa74-736e8652f990" />

Environment requires Approvals to deploy:
<img width="1069" height="676" alt="image" src="https://github.com/user-attachments/assets/baefc933-397a-4089-bfda-7a51077c5859" />

When PR is merged, it requires Approval to deploy to Live stage:
<img width="1063" height="818" alt="image" src="https://github.com/user-attachments/assets/5ed0bb26-aca3-4e18-b7af-f0eb03c72043" />

When approved, then app is deployed:

<img width="1063" height="843" alt="image" src="https://github.com/user-attachments/assets/f1e2f25f-b2fc-4b66-b7bb-34c643bfb99d" />

## Monitoring

Application Insights Telemetry is available for services:

<img width="1692" height="802" alt="image" src="https://github.com/user-attachments/assets/f9d218d9-1d1b-4b9f-9a9c-3ebac876d3c1" />

<img width="1375" height="904" alt="image" src="https://github.com/user-attachments/assets/d2df6ea4-65ce-407d-8b96-b80a3ef23a90" />

<img width="1190" height="823" alt="image" src="https://github.com/user-attachments/assets/871667b5-47b1-47fe-af66-fe5172e8e844" />

## Use cases

### Admin Flow

#### Admin signin

> [!NOTE]
> I want to separate `customer-portal` and `admin-portal` projects and deploy them into separate apps

Navigate to `/signin` and enter Admin / Manager credentials.

<img width="1469" height="1006" alt="image" src="https://github.com/user-attachments/assets/5a7e25af-e3d0-4fcb-b9a8-04cb779215a5" />

After successful sign-in, the user is redirected to the `admin-portal`.

#### Admin creating a new movie showtime

Admin can add new cinema halls, movies and showtimews:

<img width="1096" height="1016" alt="image" src="https://github.com/user-attachments/assets/6dcb9ea2-82ae-48bc-8835-6b6d18e62c62" />

<img width="1069" height="1015" alt="image" src="https://github.com/user-attachments/assets/bcadcebd-608f-4e45-bc18-207c10417749" />

When show time added, it appears in `showing` section of Customer portal.

### Customer Flow

#### Purchase tickets

Customer selects a date and movie showtime:

<img width="1087" height="1024" alt="image" src="https://github.com/user-attachments/assets/a522e66b-5ebb-4c30-bb05-da6b4cfc86e4" />

<img width="1086" height="1033" alt="image" src="https://github.com/user-attachments/assets/66f45411-2f09-434a-8aa9-c39580f4a919" />

<img width="1024" height="1000" alt="image" src="https://github.com/user-attachments/assets/468efe85-f76e-4ed0-a074-c17fa7ddcd83" />

<img width="1096" height="1011" alt="image" src="https://github.com/user-attachments/assets/395b3495-de85-416c-9aec-b6239b913651" />

The customer receives a PDF of the ticket via email:
<img width="1406" height="826" alt="image" src="https://github.com/user-attachments/assets/4155bcb9-4820-4b1e-9e82-59bbe5e77cc4" />

#### Review tickets

Customer can download their tickets. They need to receive a verification code by email:
<img width="986" height="1014" alt="image" src="https://github.com/user-attachments/assets/2450c332-02d6-416f-86a8-92f6288d5787" />

If code is valid, then the customer sees their tickets:

<img width="1039" height="1017" alt="image" src="https://github.com/user-attachments/assets/c6105fca-fa5c-4069-af47-5f4b2c1baea4" />

## Afterwords

### What is good here?

- MVP is developed and deployed;
- It covers basic happy flow for admin and customer;
- In general, tech stack is good;
- New tools (AI) were used.

### What could be improved?

- General:
  - Code quality, it could be better;
  - Reduce amount of services;
  - Better error handling;
  - Increase test coverage, especially the UI with Jest
- Business logic:
  - Add more business logic to cover full management, including edit, delete, etc;
  - Add more details about movies - directors, actors, tags, ratings, etc.;
- Authenticaion and authorization:
  - Implement customer account;
  - Add authentication with Google, Facebook, etc;
- Payments:
  - Implement Stripe Webhook;
  - Add order cancellation and refund;
  - Add new payment provider with BLIK payments support;

### What's next?
Current development is temporarily suspended. I will resume it one day.
