## **Senior Backend Code Challenge – Halen Super App (Rideshare Microservice)**

### **Estimated Time: 2.5–3.5 Hours**

**Position:** Senior Backend Engineer (Node.js)  
**Focus:** Architecture, performance, scalability, clean code, and domain logic

---

### **Challenge Overview: Rideshare Service Microservice**

You're tasked with designing and building a **Rideshare Microservice** that powers ride booking, driver-rider coordination, and live tracking within the **Halen Super App**.

This challenge will evaluate your ability to:

* Architect a clean, scalable system

* Handle real-world ride lifecycle logic

* Secure and validate endpoints

* Handle geospatial and time-series data

* Communicate assumptions and decisions clearly

---

### **Core Functional Requirements**

#### **1\. Authentication \+ Role-Based Access**

* `POST /auth/register` — Register as a **rider** or **driver**

* `POST /auth/login` — Return a **JWT token**

* Secure all endpoints

* Add role-based access control:

  * Riders can **create rides**

  * Drivers can **accept and update rides**

---

#### **2\. Ride Lifecycle Management**

* `POST /rides` — Rider creates a new ride request  
   Fields: pickup address, dropoff address, ride type (e.g. “standard”, “premium”)

* `PATCH /rides/:id/accept` — Driver accepts the ride *(status becomes `accepted`)*

* `PATCH /rides/:id/start` — Driver starts the ride *(status becomes `in_progress`)*

* `PATCH /rides/:id/complete` — Driver completes ride *(status becomes `completed`)*

* `PATCH /rides/:id/cancel` — Rider or driver cancels *(status becomes `cancelled`)*

* `GET /rides/:id` — Retrieve ride info (including status, assigned driver, ETA, and last location)

Ride status flow:

requested → accepted → in\_progress → completed  
(requested → cancelled is allowed)

---

#### **3\. Live Location Tracking**

* `POST /rides/:id/locations` — Driver adds live location update  
   Fields: timestamp, latitude, longitude, optional accuracy

* `GET /rides/:id/locations` — Retrieve full location history for a ride

---

#### **4\. ETA Calculation**

* On `GET /rides/:id`, include:

  * **Remaining distance** (via Haversine formula)

  * **Average speed** over last 3 location updates

  * **Estimated time remaining** (simple logic: `distance / speed`)

---

### **Technical Constraints**

* **Use Node.js \+ Express** (NestJS acceptable)

* **Use JWT for authentication**

* **Use MongoDB** or **PostgreSQL**

* Apply **MVC or layered architecture**

* Add **validation** using Joi, Zod, or similar

* Handle errors and invalid states gracefully

---

### 

### **Advanced Considerations (Bonus for Senior-Level)**

Implement one or more of the following advanced features:

#### **🧩 Microservice Mindset**

* Add a simple `ride.events.log` array per ride OR simulate an event bus by logging events (e.g., `ride.accepted`, `ride.completed`)

* (Optional) Explain how this service would publish ride events in a real distributed system (Kafka, RabbitMQ, etc.)

#### **⚡ Real-Time with WebSockets**

* Broadcast location updates or ride status changes to a connected rider client via WebSocket (or Socket.IO)

#### **📦 Dockerization**

* Include a `Dockerfile` and `docker-compose.yml` for running locally

#### **✅ Testing**

* Add **unit tests** for auth and ride routes (e.g., using Jest, Mocha)

* Use mock data or stubs for driver/rider separation

#### **🚨 Rate Limiting**

* Add basic rate limiting per IP or user (e.g., `express-rate-limit`)

#### **📈 Performance Scaling Prompt**

In your README:

Briefly describe how you would scale this service to support **10,000 concurrent rides**, including location updates every 3 seconds.

---

### **📬 Deliverables**

* ✅ GitHub repo link

* ✅ Clear, concise **README** with:

  * Setup instructions (including `.env`)  
  * API route list with sample requests/responses  
  * Description of design decisions  
  * Notes on scalability or trade-offs

**(Optional: include Postman collection, seed script, or test runner)**

---

**Evaluation Rubric (Used by Top Companies)**

| Category | What We’re Looking For | Weight |
| :---- | :---- | :---- |
| Architecture | Scalable, modular, well-structured codebase | 🔥 High |
| Domain Modeling | Proper role handling, lifecycle states, event flow | 🔥 High |
| API Design | RESTful, consistent, properly documented | 🔥 High |
| Business Logic | ETA, geolocation handling, role restrictions | High |
| Code Quality | Clean, readable, maintainable, DRY | High |
| Security | Proper JWT auth, role-based access, protected endpoints | Medium |
| Testing | Coverage of critical paths | Medium |
| Documentation | Clarity and completeness of README/API docs | Medium |
| Bonus Features | WebSocket, Docker, microservice thinking, CI/CD | Bonus |

### **Closing Tip**

Treat this like you're coding one part of a larger production system. Keep it clean, write like a team will build on this, and document your thought process.
