# Hardware and Software Requirements

This section outlines the hardware and software requirements essential for the operation of **AIMS (Automated Intervention and Mastery System)**, which functions as the Learning Management and Grading module within the school's integrated **Enterprise Resource Planning (ERP)** system. The system is designed to support the student and faculty population of **Hinigaran National High School** (~6,500 users).

## 1. Hardware Requirements

To ensure stability during peak concurrency on locally-provisioned hardware, the following hardware standards are established. The minimum specifications are based on the actual equipment available at Hinigaran High School.

### 1.1 Server-Side Requirements (On-Premise)
The system is deployed as a monolithic PERN stack on a single local server. The "Minimum" specification reflects the laptop hardware provided by the school for this deployment.

| Components | Minimum Specification (Local Server) | Recommended Specification (Scale Target) |
| :--- | :--- | :--- |
| **Server CPU** | **AMD Ryzen 5** (3000 Series+) or **Intel Core i5** (10th Gen+) | **AMD Ryzen 7** (5000 Series+) or **Intel Core i7** (12th Gen+) |
| **Server RAM** | **8 GB DDR4** | 16 GB to 32 GB DDR4/DDR5 |
| **Server Storage** | **500 GB HDD/SSD** | 1 TB NVMe SSD (RAID 1 Configuration) |
| **Network (ISP)** | 25 Mbps Symmetric (Fiber) | 100 Mbps to 1 Gbps Symmetric Fiber |
| **UPS / Power** | 650VA Uninterruptible Power Supply | 1500VA UPS with Surge Protection |

**Server Rationale & "Panel-Ready" Performance Strategy:**
*   **Memory Management (8GB):** Since 8GB is shared, the system utilizes **Node.js Memory Limits** (`--max-old-space-size=2048`) to ensure the OS and PostgreSQL always have enough headroom to function without swapping to the slow disk.
*   **HDD Optimization (Mechanical Drive Defense):** Recognizing that the beneficiary may provide a mechanical HDD, the system implements **Disk I/O Mitigation**:
    1.  **PostgreSQL Tuning:** The database is configured with optimized `effective_io_concurrency` set to 0 (for HDD) and increased `checkpoint_completion_target` to smooth out write spikes.
    2.  **Aggressive Indexing:** All high-traffic tables (Students, Grades, Schedules) are strictly indexed via Prisma to ensure the HDD read-head minimizes physical movement during queries.
    3.  **Log Throttling:** Non-critical system logging is minimized to reduce constant write operations that can slow down mechanical drives.
*   **CPU Concurrency:** The Ryzen 5 or Core i5 (6+ cores) is leveraged through **PM2 Clustering**, allowing the system to process logic-heavy tasks in parallel, reducing the overall wait time for users during disk-bound operations.

### 1.2 Client-Side Requirements (User Roles)
The system is browser-based, ensuring compatibility across the diverse devices used by the Hinigaran High School community.

| User Role | Device Type | Minimum Specifications |
| :--- | :--- | :--- |
| **System Admin / IT** | Laptop/Desktop | **Intel Core i5** (10th Gen) or **AMD Ryzen 5** (3000 Series), 8GB RAM |
| **Registrar / Staff** | Laptop/Desktop | **Intel Core i3** (10th Gen) or **AMD Ryzen 3** (3000 Series), 8GB RAM |
| **Teachers** | Laptop/Tablet | **Intel Core i3** (8th Gen) or **AMD Ryzen 3** (2000 Series), 8GB RAM |
| **Students** | Smartphone/PC | Android 10+ / iOS 15+, 4GB RAM (Browser: Chrome/Edge) |

---

## 2. Software Requirements

The ERP utilizes the **PERN Stack** (PostgreSQL, Express, React, Node.js) to provide a responsive, unified experience across all modules.

### Table 2: Software Environment

| Category | Requirement |
| :--- | :--- |
| **Operating System** | Ubuntu Server 22.04 LTS (Lightweight Headless Version) |
| **Database** | PostgreSQL 16.x (Relational data integrity) |
| **ORM** | Prisma v6.x (Type-safe database abstraction) |
| **Runtime** | Node.js 20.x LTS |
| **Web Server** | Nginx (Reverse Proxy & Static File Hosting) |
| **Process Manager** | PM2 with Clustering Mode |
| **Public Exposure** | Cloudflare Tunnel (Secure tunneling without port forwarding) |

### 2.1 Optimization & Deployment Strategy
*   **Monolithic Synergy:** By stitching AIMS with EnrollPro and ATLAS into a monolithic deployment, we eliminate network latency between services, which is critical when running on local school hardware.
*   **Static Offloading:** Nginx serves the React frontend as static files. This prevents the Node.js backend from reading files from the HDD for every user request, saving disk bandwidth for the database.
*   **Cloudflare Tunnel:** Ensures the internal server is accessible to students at home without exposing the school's local IP or requiring port forwarding on the provided hardware.
