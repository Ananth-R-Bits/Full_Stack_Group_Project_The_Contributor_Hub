
# Logical Architecture  
## Full Stack E-Commerce Application

---

## 1. Introduction

This document describes the **Logical Architecture** of e-commerce application.  
The architecture is derived **directly from the implemented source code** of the project and reflects the actual structure of the frontend and backend components.

The system follows a **3-Tier Architecture**, consisting of:
1. Presentation Layer
2. Web API Layer
3. Database Layer

This design ensures separation between user interface, application logic, and data persistence while remaining simple and suitable for full-stack development.

---

## 2. Architectural Style

**Architecture Pattern Used:**  
**Three-Tier Client–Server Architecture**

- Frontend: Angular SPA
- Backend: ASP.NET Core Web API
- Database: SQL Server (via Entity Framework Core)

The backend combines application logic and data access in the controller layer, as observed in the implementation.

---

## 3. Layered Architecture Description
<img width="744" height="588" alt="LayeredArchitecture" src="https://github.com/user-attachments/assets/af899633-5105-42ad-ab06-7298a45e07dd" />

### 3.1 Presentation Layer (Frontend)

**Technology:**  
- Angular (TypeScript, HTML, CSS)

**Location in Codebase:**  

**Key Components:**
- LoginComponent
- RegisterComponent
- DashboardComponent (Product Listing + Search)
- ProductDetailComponent
- CartComponent
- OrdersComponent
- PaymentComponent (Dummy Payment)

**Responsibilities:**
- Rendering UI screens
- Handling user interactions
- Client-side validation
- Navigation and routing
- Invoking backend REST APIs using Angular services

**Interaction Pattern:**

Frontend components do not directly access the database.

---

### 3.2 Web API Layer (Backend)
<img width="859" height="378" alt="BackendStructure" src="https://github.com/user-attachments/assets/7d041556-8f99-4c98-b0d4-90cc529b6867" />

**Technology:**
- ASP.NET Core Web API
- Entity Framework Core

**Location in Codebase:**

**Controllers:**
- AuthController
- ProductsController
- CartController
- OrdersController

**Responsibilities:**
- Handling HTTP requests from frontend
- Performing business logic
- Managing authentication and authorization
- Processing orders and cart operations
- Interacting with the database using EF Core

**Important Architectural Note:**
There is **no separate repository or service layer**.  
Controllers directly use `AppDbContext` for database operations.

This makes the backend a **combined Application + Data Access layer**.

---

### 3.3 Data Access & Persistence Layer

**Technology:**
- SQL Server
- Entity Framework Core (ORM)

**Key Files:**

**Responsibilities:**
- Object–relational mapping
- Managing entity relationships
- CRUD operations
- Maintaining referential integrity

Entities are mapped using EF Core models.

---

## 4. Logical Layer Interaction

### Example: Order Placement Flow

1. User adds product to cart via Angular UI
2. CartComponent calls CartService
3. CartService sends HTTP request to CartController
4. CartController processes logic and updates database using AppDbContext
5. Order is created via OrdersController
6. Data is persisted in SQL Server
7. OrdersComponent fetches order history

---

## 5. Logical Architecture Diagram
<img width="308" height="633" alt="LA" src="https://github.com/user-attachments/assets/14c91107-a738-4f56-94f8-2f4d1dd6cdfd" />


---

## 6. Separation of Concerns

| Concern | Implementation |
|-------|----------------|
| UI Rendering | Angular Components |
| API Communication | Angular Services |
| Business Logic | Backend Controllers |
| Data Access | EF Core DbContext |
| Persistence | SQL Server |

Although backend logic and data access are combined, frontend and backend responsibilities are clearly separated.

---

## 7. Conclusion

The logical architecture of *The Contributor Hub* is a clean and functional **3-Tier full-stack architecture**.  

