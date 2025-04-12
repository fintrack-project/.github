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

[ React (Frontend) ] <---> [ Java Spring Boot REST API ] <---> [ PostgreSQL ] ↑ | [ Kafka Message Broker ] ↑ [ Python ETL Pipeline (batch daily market data) ]


- User data flows from frontend to backend and is stored in PostgreSQL.
- Daily market data is pulled via the Python ETL pipeline and published to Kafka.
- Spring Boot backend consumes data from Kafka and updates relevant tables.

---

## 🧰 Getting Started

### Prerequisites

- Node.js + npm
- Java 17+
- Python 3.10+
- PostgreSQL
- Docker
- Kafka (locally or via container)
- Jenkins (optional for CI/CD)

### Setup

```bash
# 1. Clone the repo
git clone https://github.com/your-username/fintrack.git
cd fintrack

# 2. Set up environment variables
cp .env.example .env
# Fill out .env for backend, frontend, and Python ETL

# 3. Build and run backend
cd backend
./gradlew build
docker build -t fintrack-backend .
docker run -p 8080:8080 fintrack-backend

# 4. Run frontend
cd ../frontend
npm install
npm run dev

# 5. Start Kafka and run ETL pipeline (Python)
cd ../etl
pip install -r requirements.txt
python main.py
