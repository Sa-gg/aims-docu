# Hardware and Software Requirements

	This section outlines the hardware and software requirements essential for the effective operation of AIMS: Automated Intervention and Mastery System, functioning as a core module within the school's integrated Enterprise Resource Planning (ERP) platform.

Hardware Requirements
	To ensure the reliable performance of AIMS: Automated Intervention and Mastery System for a school population of approximately 6,500 users, the baseline hardware configurations and technical standards are detailed below:

Table 1
Hardware Components and Specification
| Component | Minimum Specification | Recommended Specification | Justification |
| :--- | :--- | :--- | :--- |
| Server CPU | AMD Ryzen 5 (3000 Series+) or Intel Core i5 (10th Gen+) | AMD Ryzen 7 (5000 Series+) or Intel Core i7 (12th Gen+) | Handles concurrent AI quiz generation, grading computations, and simultaneous request processing for up to 6,500 users of Hinigaran National High School. |
| Server RAM | 8 GB DDR4 | 16 GB to 32 GB DDR4/DDR5 | Holds active session data, mastery analytics, and PostgreSQL working sets during peak concurrent access. |
| Server Storage | 256 GB HDD / SSD | 1 TB NVMe SSD (RAID 1 Configuration) | Stores the PostgreSQL database, uploaded learning resources, AI-generated content, and system backups. |
| Network (ISP) | 25 Mbps stable Symmetric connection | 100 Mbps to 1 Gbps Symmetric Fiber | Required for stable access by teachers and students via Cloudflare Tunnel from off-campus locations. |
| Teacher Client | Intel Core i3 (8th Gen) or AMD Ryzen 3, 8 GB RAM | Intel Core i5 (11th Gen) or AMD Ryzen 5, 12 GB RAM | Supports the interactive grading interface, quiz editor, and real-time class management features. |
| Student (Mobile / PC) | Android 10.0+ / iOS 15.0+, 4 GB RAM | Android 13.0+ / iOS 17.0+, 6 GB RAM | Ensures compatibility with the responsive student portal and modern browser rendering standards. |

Software Requirements
	To successfully implement the AIMS module within the institution's integrated Enterprise Resource Planning (ERP) system, the dedicated on-premises server must be equipped with a specific suite of software components. The foundational requirement is a stable Linux distribution, specifically Ubuntu Server LTS 22.04 or higher, which provides the hosting environment for all unified backend services. For database management, PostgreSQL version 16 or higher must be installed to handle the localized storage of academic records, enrollment data, and mastery analytics via the Prisma ORM. Additionally, the Node.js v20 LTS runtime environment is required on the server to execute the core backend logic and asynchronous intervention tasks.

	For efficient resource management and system stability, Docker and Docker Compose v2.x are utilized to containerize the monolithic services, providing strict memory capping and process isolation critical for the provided 8 GB RAM hardware. Nginx (version 1.24+) is necessary to serve as a high-performance reverse proxy and to handle the delivery of static frontend assets, thereby offloading processing requirements from the application server. The system also implements JWT and bcrypt protocols for secure authentication and credential hashing, ensuring controlled role-based access for Hinigaran National High School personnel. To support continuous delivery and rapid bug resolution, Git is used for version control and a CI/CD pipeline is integrated to automate testing and deployment, ensuring that any code fix or update can be pushed to the live server seamlessly without manual intervention. Additionally, AnyDesk is installed on the server to enable the development team to provide remote troubleshooting and maintenance support without requiring physical presence at the school site. On the client side, including teachers and students, no specialized software installation is required beyond a modern web browser capable of rendering the responsive portals through the secure Cloudflare Tunnel connection.

Table 2
Software Components and Requirements
| Category | Requirement |
| :--- | :--- |
| Operating System | Ubuntu Server 22.04 LTS (Headless) |
| Database | PostgreSQL 16.x with Prisma ORM |
| Runtime | Node.js 20.x LTS |
| Containerization | Docker Engine and Docker Compose v2.x |
| Web Server / Reverse Proxy | Nginx 1.24+ (Static File Hosting and Reverse Proxy) |
| Process Manager | PM2 (Internal Container Clustering) |
| Public Exposure | Cloudflare Tunnel (Secure tunneling without port forwarding) |
| Authentication | JSON Web Tokens (JWT) and bcrypt credential hashing |
| Version Control | Git (source code management and change tracking) |
| CI/CD Pipeline | GitHub Actions (automated testing and deployment on push) |
| Remote Support | AnyDesk (remote desktop access for off-site troubleshooting) |
| Client Requirement | Modern web browser (Google Chrome, Microsoft Edge, or Mozilla Firefox) |
