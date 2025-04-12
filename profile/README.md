# FinTrack 🧾📊

**FinTrack** is a user-friendly personal financial tracker designed to help individuals **manually track and manage their investment portfolios** in one centralised location. It supports asset categories such as stocks, cryptocurrencies, and real estate, while providing **daily-updated market data** and historical analytics to help users make smarter financial decisions.

Whether you're a seasoned investor or just starting out, FinTrack offers a simple yet powerful way to stay on top of your financial journey.

---

## 🚀 Features

- Add, edit, and manage financial assets across multiple categories
- View daily-updated performance metrics
- Analyze portfolio value and asset distribution
- Batch ETL pipeline for fetching market data
- Modular architecture with scalable microservices

---

## 🛠 Tech Stack

| Layer        | Technology                             |
|--------------|-----------------------------------------|
| Frontend     | React, TypeScript                      |
| Backend      | Java, Spring Boot, REST API, PostgreSQL |
| ETL Pipeline | Python, External Financial APIs         |
| Messaging    | Kafka                                   |
| DevOps       | Jenkins, Docker, Quay                   |
| Planned      | Kubernetes, AWS deployment              |

---

## 📐 Architecture Overview

React (Frontend)
        ⇅
Java Spring Boot REST API
        ⇅
PostgreSQL
   ↑           ↑
Kafka       Python ETL Pipeline (Batch Daily Market Data)
             (Publishes to Kafka)

- User data flows from frontend to backend and is stored in PostgreSQL.
- Daily market data is pulled via the Python ETL pipeline and published to Kafka.
- Spring Boot backend consumes data from Kafka and updates relevant tables.

---

## 🛣 Roadmap / TODOs
- Cloud deployment (AWS: ECS, S3, RDS, CloudFront)
- CI/CD for all services with Jenkins + Quay
- User authentication and authorisation
- Enhanced portfolio analytics (risk, ROI, diversification index)
