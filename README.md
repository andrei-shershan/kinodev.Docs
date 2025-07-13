# KinoDev

KinoDev is a minimalistic MVP for streamlined cinema management and ticket sales. Built with a modern tech stack, it lets theater owners schedule screenings, configure halls and seat layouts, track real-time availability, and process online payments securely.

__Follow this link to see the website: [KINODEV - minimalistic MVP](https://ui-hxh5eqemg5dmeddy.polandcentral-01.azurewebsites.net/)__

> [!NOTE]
> Free or Low cost Azure services were used for deployment, so it works **'a little bit'** slow

> [!NOTE]
> Current project state is delivered MVP, it contains only minimal happy flow path.
> Further development temporary postponed.

---

- [What is about?](#what-is-about)
- [Architecture](#architecture)
- [Stack](#stack)


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

Distributed Cache: **Redis**

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

Navigate to `KinoDev.Docker` prokect, run `docker compose up --build -d`

<img width="977" height="507" alt="image" src="https://github.com/user-attachments/assets/aa713d12-9b78-43f7-a162-9590d7b698c2" />

Then all containers should run in Docker
<img width="1875" height="945" alt="image" src="https://github.com/user-attachments/assets/b1b2e0ef-0e6a-49ec-9294-34ef8450e77d" />

And website is available on `ui.kinodev.localhost`

<img width="886" height="1024" alt="image" src="https://github.com/user-attachments/assets/94b427d8-5ab1-4c61-a259-eee41fa90765" />


### PR and branch policies

> [!NOTE]
> I know that for now commit history looks terrible :smile:
> 
> In real life business project I would use proper commit messages, incuding ticket number and code changes description 

Direct commits to the `main` branch are disallowed by **branch policy**, all changes must be merged via **pull requests**.

Builds are run via **GitHub Actions** before pull request is merged.

<img width="908" height="166" alt="image" src="https://github.com/user-attachments/assets/5c89ce57-0b85-413a-9a12-ac27bb990f13" />

## Delivery

### Azure Portal

Azure Services are properly setup.

<img width="1733" height="829" alt="image" src="https://github.com/user-attachments/assets/3278dc43-ceda-4f20-b0c8-1c61ca85bb3f" />

> [!NOTE]
> I used Free / Minimal Cost services only

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

- MPV is developed and deployed;
- It covers basic happy flow for admin and customer;

### What could be improved?

- Code quality, it could be better;
- Adjust architecture, reduce unnecessary services;
- Be careful with timezones;
- Add more business logic to cover full managment, including edit, delete, etc;
- Add more details about movies - directors, actors, tags, ratings, etc.;
- Implement customer account;
- Add authentication with Google, Facebook, etc;
- Implement Stripe Webhook;
- Add new payment provider with BLIK payments support;
- Propper error handling;
- Increase test coverage, esprecially UI with jest.

### What's next?
Current development is temporarily suspend. I will continue one day...
