# Hardware and Software Requirements

	This section outlines the hardware and software requirements essential for the effective operation of AIMS: Automated Intervention and Mastery System, functioning as a core module within the school's integrated Enterprise Resource Planning (ERP) platform.

Hardware Requirements
	To ensure the reliable performance of AIMS: Automated Intervention and Mastery System for a school population of approximately 6,500 users, the baseline hardware configurations and technical standards are detailed below:

Table 1
Hardware Components and Specification
| Components | Minimum Specification | Recommended Specification |
| :--- | :--- | :--- |
| Server CPU | AMD Ryzen 5 (3000 Series+) or Intel Core i5 (10th Gen+) | AMD Ryzen 7 (5000 Series+) or Intel Core i7 (12th Gen+) |
| Server RAM | 8 GB DDR4 | 16 GB to 32 GB DDR4/DDR5 |
| Server Storage | 500 GB HDD / SSD | 1 TB NVMe SSD (RAID 1 Configuration) |
| Network (ISP) | 25 Mbps stable Symmetric connection | 100 Mbps to 1 Gbps Symmetric Fiber |
| Admin / Registrar Client | Intel Core i3 (10th Gen) or AMD Ryzen 3, 8 GB RAM | Intel Core i5 (12th Gen) or AMD Ryzen 5, 16 GB RAM |
| Teacher / Staff Client | Intel Core i3 (8th Gen) or AMD Ryzen 3, 8 GB RAM | Intel Core i5 (11th Gen) or AMD Ryzen 5, 12 GB RAM |
| Learner / Guardian (Mobile) | Android 10.0+ / iOS 15.0+, 4 GB RAM | Android 13.0+ / iOS 17.0+, 6 GB RAM |

Software Requirements
	The software environment for AIMS utilizes a modern full-stack PERN architecture (PostgreSQL, Express, React, Node.js) featuring PostgreSQL for relational data integrity and an Ubuntu-based Linux server for enhanced stability and security. To maximize efficiency on the school's local hardware, the system is deployed using Docker Compose for containerization, which allows for strict resource capping and process isolation. The application is designed to be entirely browser-based, ensuring that administrators, registrars, teachers, and learners can access the system using an up-to-date web browser such as Google Chrome, Microsoft Edge, or Mozilla Firefox without the need for additional local software installations. 

	To accommodate the high user volume of 6,500 individuals on locally-provisioned hardware, the system is optimized through PM2 clustering and Nginx reverse proxying to offload static file serving and maximize concurrent request handling. While development was conducted on Windows 11, the system is deployed via Cloudflare Tunnel to provide a secure and responsive experience across various platforms and mobile devices. This setup makes the system more secure, accessible, and efficient, maintaining full compatibility with modern operating systems while ensuring data remains protected within the school's private local environment.
