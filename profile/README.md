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

## 📦 Repository Overview
This project follows a polyrepo architecture to modularize different components of the Personal Financial Tracker system. Below are the descriptions of each repository:

[financial-tracker-frontend](https://github.com/fintrack-project/financial-tracker-frontend)
A React + TypeScript frontend that allows users to view, add, and manage their financial assets through a responsive dashboard. This interface connects to the backend API for real-time asset tracking, historical data visualization, and portfolio insights.

[financial-tracker-backend](https://github.com/fintrack-project/financial-tracker-backend)
A Java Spring Boot application that provides RESTful APIs to handle user assets, portfolio data, and integrate with ETL pipelines. It manages business logic, coordinates with the PostgreSQL database, and communicates with Kafka for async data processing.

[financial-tracker-db](https://github.com/fintrack-project/financial-tracker-db)
Contains PostgreSQL schema definitions, DDL scripts, and database migration files to support backend operations. This repo ensures the database stays version-controlled and can be reliably set up across environments.

[financial-tracker-etl](https://github.com/fintrack-project/financial-tracker-etl)
A Python-based ETL service that fetches daily market data from external APIs, processes it, and sends structured data through Kafka for backend ingestion. Supports tracking of stocks, crypto, and other assets.

[financial-tracker-infra](https://github.com/fintrack-project/financial-tracker-infra)
Infrastructure-as-code (IaC) and CI/CD configurations using Jenkins, Docker, and Kubernetes (planned). This repo also contains deployment scripts and containerization logic to manage services across development and production environments.

---

## 📐 Architecture Overview

![FinTrack Architecture](/profile/asset/FinTrack_Architecture.png)

- User data flows from frontend to backend and is stored in PostgreSQL.
- Daily market data is pulled via the Python ETL pipeline and published to Kafka.
- Spring Boot backend consumes data from Kafka and updates relevant tables.

---

## 🛣 Roadmap / TODOs
- Cloud deployment (AWS: ECS, S3, RDS, CloudFront)
- CI/CD for all services with Jenkins + Quay
- User authentication and authorisation
- Enhanced portfolio analytics (risk, ROI, diversification index)
