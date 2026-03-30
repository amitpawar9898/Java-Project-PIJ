# SIT Real-Time Stock Market Management System

**Team:** Amit Pawar (25070126501) | Gaurang Surte (25070126514) | Aditya Sharma (24070126016) | Aaron Frank (24070126503)  
**Guide:** Dr. Mayur Gaikwad | Symbiosis Institute of Technology, Pune

---

## Project Structure

```
SIT_StockMarket_Project/
├── pom.xml                              <- Maven dependencies
├── README.md                            <- This file
└── src/
    ├── main/
    │   ├── java/com/sit/stockmarket/
    │   │   ├── SitStockMarketApplication.java    <- Entry point
    │   │   ├── config/
    │   │   │   ├── SecurityConfig.java           <- Spring Security + JWT
    │   │   │   ├── WebSocketConfig.java          <- STOMP WebSocket
    │   │   │   └── DataInitializer.java          <- Seed data on startup
    │   │   ├── controller/
    │   │   │   ├── StockApiController.java       <- REST API endpoints
    │   │   │   └── PageController.java           <- Thymeleaf page routes
    │   │   ├── dto/
    │   │   │   ├── TradeRequest.java             <- Buy/Sell request DTO
    │   │   │   └── TradeResponse.java            <- Trade result DTO
    │   │   ├── exception/
    │   │   │   ├── StockNotFoundException.java
    │   │   │   ├── InsufficientBalanceException.java
    │   │   │   ├── InsufficientSharesException.java
    │   │   │   └── GlobalExceptionHandler.java
    │   │   ├── model/
    │   │   │   ├── base/
    │   │   │   │   └── FinancialInstrument.java  <- OOP: Inheritance base
    │   │   │   └── entity/
    │   │   │       ├── Stock.java                <- OOP: Inheritance + Encapsulation
    │   │   │       ├── User.java                 <- User entity
    │   │   │       ├── Trade.java                <- Trade entity
    │   │   │       ├── Portfolio.java            <- Portfolio entity
    │   │   │       ├── StockPrice.java           <- OHLCV historical data
    │   │   │       └── Prediction.java           <- LSTM prediction entity
    │   │   ├── repository/
    │   │   │   ├── StockRepository.java          <- JPA queries
    │   │   │   ├── UserRepository.java
    │   │   │   ├── TradeRepository.java
    │   │   │   ├── PortfolioRepository.java
    │   │   │   ├── PredictionRepository.java
    │   │   │   └── StockPriceRepository.java
    │   │   ├── service/
    │   │   │   ├── interfaces/
    │   │   │   │   ├── StockService.java         <- OOP: Abstraction
    │   │   │   │   └── PredictionService.java    <- OOP: Abstraction
    │   │   │   └── impl/
    │   │   │       ├── StockServiceImpl.java     <- NSE + simulation
    │   │   │       ├── UserServiceImpl.java      <- Auth + registration
    │   │   │       ├── TradeServiceImpl.java     <- Buy/Sell logic
    │   │   │       └── PortfolioServiceImpl.java <- P&L calculations
    │   │   ├── strategy/
    │   │   │   ├── SignalGenerator.java          <- OOP: Polymorphism interface
    │   │   │   ├── SimpleStrategy.java           <- Momentum strategy
    │   │   │   ├── RSIStrategy.java              <- RSI strategy
    │   │   │   └── MLStrategy.java              <- LSTM ML strategy
    │   │   └── websocket/
    │   │       └── StockWebSocketPublisher.java  <- Live price broadcast
    │   └── resources/
    │       ├── application.properties            <- All config
    │       ├── static/
    │       │   ├── css/style.css                 <- Dark theme styles
    │       │   └── js/app.js                     <- WebSocket + Trade JS
    │       └── templates/
    │           ├── login.html                    <- Auth pages
    │           ├── register.html
    │           ├── dashboard.html                <- Main trading view
    │           ├── portfolio.html                <- Holdings + P&L
    │           ├── trades.html                   <- Trade history
    │           └── fragments/
    │               ├── navbar.html               <- Shared navbar
    │               └── footer.html               <- Shared footer
    └── test/
        └── java/com/sit/stockmarket/
            └── SitStockMarketApplicationTests.java

```

---

## OOP Concepts (as per PDF requirement)

| Concept | Where |
|---------|-------|
| **Encapsulation** | `User.java`, `Stock.java` — private fields, getters/setters |
| **Inheritance** | `Stock.java` extends `FinancialInstrument.java` |
| **Abstraction** | `StockService.java`, `PredictionService.java` interfaces |
| **Polymorphism** | `SignalGenerator` interface → 3 different strategy implementations |
| **Composition** | `PortfolioServiceImpl` uses `PortfolioRepository` + `StockRepository` |

---

## REST API Endpoints

| Method | URL | Description |
|--------|-----|-------------|
| GET | `/api/stocks` | Get all 20 NSE stocks |
| GET | `/api/stocks/{symbol}` | Get single stock |
| GET | `/api/stocks/gainers` | Top 10 gainers |
| GET | `/api/stocks/losers` | Top 10 losers |
| POST | `/api/trade/buy` | Buy stock `{symbol, quantity}` |
| POST | `/api/trade/sell` | Sell stock `{symbol, quantity}` |
| GET | `/api/portfolio` | User portfolio + P&L |
| GET | `/api/trades` | Trade history |
| GET | `/api/search/{query}` | Search stocks |

---

## How to Run

### Option 1: H2 In-Memory (No setup needed — quick demo)
1. Open `application.properties`
2. Comment MySQL lines, uncomment H2 lines
3. Run: `mvn spring-boot:run`
4. Open: `http://localhost:8080`

### Option 2: MySQL (Full production)
1. Install MySQL, create database: `CREATE DATABASE sit_stockmarket;`
2. Update `application.properties` with your MySQL password
3. Run: `mvn spring-boot:run`
4. Open: `http://localhost:8080`

**Login:** `demo / demo123`  
**Admin:** `admin / admin123`

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Spring Boot 3.2, Java 17 |
| Security | Spring Security + BCrypt |
| Database | MySQL 8 / H2 |
| ORM | Spring Data JPA / Hibernate |
| Real-time | WebSocket + STOMP |
| Frontend | Thymeleaf + Vanilla JS |
| Cache | Spring Cache |
| Build | Maven |





// install 
Step 1 — Install Java 17

Go to: https://adoptium.net
Download JDK 17 (Temurin 17)
Install it — click Next → Next → Finish


Step 2 — Install Maven

Go to: https://maven.apache.org/download.cgi
Download apache-maven-3.9.x-bin.zip
Extract it to C:\maven
Add to Windows PATH:

Search "Environment Variables" in Windows
Click Environment Variables
Under System Variables → find Path → click Edit
Click New → type C:\maven\bin
Click OK → OK → OK


Restart VS Code completely


Step 3 — Verify installation
Open VS Code terminal and type:
java -version
mvn -version
Both should show version numbers.

Step 4 — Run the project
bashcd "D:\Stock Market Analysis\frontend\SIT_StockMarket_Project"
mvn spring-boot:run
```

---

## Step 5 — Open in browser
```
http://localhost:8080