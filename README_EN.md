# 🏛️ National Assembly Issue - A Better Korea Through Citizens' Voices

[한국어](./README.md)

## 📌 Service Introduction

National Assembly Issue is a civic engagement platform that helps citizens easily understand complex legislation, express their support or opposition, and ask questions through an AI chatbot. It provides real-time summaries of National Assembly proceedings and bill information to promote democratic participation.


## ✨ Key Features

### 📜 Bill Viewing and Voting
- Browse and view detailed information on proposed bills
- Participate in approval/opposition voting on bills
- Real-time voting rate and participant count
- Filter bills by category (Transportation, Housing, Economy, Welfare, Environment, Education, etc.)
- Sort by latest or vote count

### 🔥 Popular Bill Recommendations
- Highlight HOT bills with high voting rates
- Real-time popular bill marquee slider
- Priority display for high citizen engagement issues

### 🏛️ National Assembly Meeting Summaries
- AI-analyzed National Assembly meeting summaries
- Real-time updates on today's Assembly activities
- Overview of key discussions and agendas

### 🤖 AI Chatbot Assistant
- **Bill Chatbot**: Real-time Q&A about legislation
- **Meeting Chatbot**: Detailed explanations of Assembly proceedings
- **Streaming Response**: SSE (Server-Sent Events) based real-time conversational interface

### 🔍 Integrated Search
- Search by bill title and content
- Real-time search result updates


## 🛠️ Tech Stack

### Backend
- **Framework**: Spring Boot 3.5.6
- **Language**: Java 21
- **Database**: MySQL
- **ORM**: Spring Data JPA
- **Reactive**: Spring WebFlux (async streaming)
- **External APIs**: 
  - National Assembly Open API (bills, meeting records)
  - Upstage AI API (LLM chatbot, document analysis)
- **PDF Processing**: Apache PDFBox 3.0.3
- **HTML Parsing**: Jsoup 1.17.2

### Frontend
- **Framework**: React 19.1.1
- **Language**: TypeScript 5.8.3
- **Build Tool**: Vite 7.1.7
- **Routing**: React Router DOM 7.9.2
- **State Management**: React Query 5.90.2
- **Styling**: Tailwind CSS 4.1.13
- **HTTP Client**: Axios 1.12.2
- **Icons**: Lucide React 0.544.0

### Development Tools
- **Linter**: ESLint 9.36.0
- **Type Checking**: TypeScript ESLint 8.44.0
- **CSS Processing**: PostCSS 8.5.6, Autoprefixer 10.4.21


## 🏗️ System Architecture

```
┌─────────────┐     ┌──────────────────────────────────────────────┐
│   Frontend  │────▶│                  Backend                      │
│   (React)   │◀────│              (Spring Boot)                    │
└─────────────┘     │                                                │
                    │  ┌────────────────────────────────────────┐   │
                    │  │              Controllers                │   │
                    │  │  • BillController (/api/bills)         │   │
                    │  │  • MeetingController (/api/meetings)   │   │
                    │  │  • ChatBotController (/api/chatbot)    │   │
                    │  └────────────────────────────────────────┘   │
                    │                     │                          │
                    │  ┌────────────────────────────────────────┐   │
                    │  │              Services                   │   │
                    │  │  • BillService, VoteService            │   │
                    │  │  • MeetingService, MeetingSummaryService│   │
                    │  │  • ChatBotService, UpstageApiService   │   │
                    │  │  • DocumentParserService, PdfService   │   │
                    │  └────────────────────────────────────────┘   │
                    │                     │                          │
                    │  ┌──────────┐  ┌─────────────────────────┐   │
                    │  │  MySQL   │  │    External APIs         │   │
                    │  │ Database │  │  • National Assembly API │   │
                    │  └──────────┘  │  • Upstage AI API        │   │
                    │                └─────────────────────────┘   │
                    └──────────────────────────────────────────────┘
```


## 📁 Project Structure

### Backend
```
backend/
├── src/main/java/com/donzo/naitssu/
│   ├── domain/
│   │   ├── bill/                    # Bill domain
│   │   │   ├── controller/          # REST API controllers
│   │   │   ├── service/             # Business logic
│   │   │   │   ├── BillService.java
│   │   │   │   ├── AssemblyApiService.java  # National Assembly API integration
│   │   │   │   └── UpstageService.java      # AI summarization
│   │   │   ├── repository/          # JPA Repository
│   │   │   ├── entity/              # JPA Entity
│   │   │   └── dto/                 # Request/Response DTOs
│   │   ├── meeting/                 # Meeting domain
│   │   │   ├── controller/
│   │   │   ├── service/
│   │   │   │   ├── MeetingService.java
│   │   │   │   ├── MeetingApiService.java
│   │   │   │   ├── MeetingSummaryService.java
│   │   │   │   ├── DocumentParserService.java
│   │   │   │   └── PdfProcessingService.java
│   │   │   ├── scheduler/           # Auto-update scheduler
│   │   │   ├── repository/
│   │   │   ├── entity/
│   │   │   └── dto/
│   │   ├── chatbot/                 # AI Chatbot domain
│   │   │   ├── controller/
│   │   │   ├── service/
│   │   │   │   ├── ChatBotService.java
│   │   │   │   └── UpstageApiService.java  # SSE streaming
│   │   │   └── dto/
│   │   ├── vote/                    # Vote domain
│   │   │   ├── entity/
│   │   │   └── repository/
│   │   └── assembly/                # Assembly session domain
│   │       └── entity/
│   └── global/
│       ├── config/                  # Configuration
│       │   ├── CorsConfig.java
│       │   └── WebClientConfig.java
│       └── entity/
│           └── BaseEntity.java      # Common entity
└── build.gradle
```

### Frontend
```
frontend/
├── src/
│   ├── apis/              
│   │   ├── client/        # API client configuration
│   │   ├── hooks/         # React Query custom hooks
│   │   ├── services/      # API service functions
│   │   └── types/         # API type definitions
│   ├── components/        
│   │   ├── Header.tsx
│   │   ├── BillCard.tsx
│   │   ├── chatbot.tsx
│   │   ├── MeetingChatbot.tsx
│   │   └── Pagination.tsx
│   ├── pages/             
│   │   ├── Home/          # Home page
│   │   ├── BillPage/      # Bill list page
│   │   ├── BillDetailPage/# Bill detail page
│   │   └── ConferencePage/# Assembly meeting page
│   ├── routes/           
│   ├── styles/            
│   ├── utils/             
│   └── lib/               
├── public/                
└── package.json
```


## 🔌 API Specification

### Bill API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/bills` | Get all bills |
| GET | `/api/bills/{id}` | Get bill details |
| GET | `/api/bills/page` | Paginated query (tag, sort filters) |
| GET | `/api/bills/search` | Keyword search |
| POST | `/api/bills/sync` | Sync with National Assembly API |
| POST | `/api/bills/{id}/vote` | Vote (approve/oppose) |

### Meeting API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/meetings` | Get meetings (cursor-based pagination) |
| GET | `/api/meetings/latest` | Get latest meeting |

### ChatBot API
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/chatbot/chat/stream` | SSE streaming chat |
| POST | `/api/chatbot/session` | Create session |
| GET | `/api/chatbot/health` | Health check |


## 🎨 Main Pages

### 1. Home (`/`)
- Bill highlights
- Today's Assembly meeting summary
- Real-time popular bill summary

### 2. Bill List (`/bills`)
- Complete bill listing
- Category filtering
- Search and sort features

### 3. Bill Detail (`/bills/:id`)
- Detailed bill information
- Status and voting results
- AI chatbot Q&A about the bill

### 4. Assembly Meetings (`/conferences`)
- Meeting record list
- AI summary information
- Chatbot Q&A about meeting content


## 🚀 Getting Started

### Backend
```bash
cd backend
./gradlew bootRun
```

### Frontend
```bash
cd frontend
npm install
npm run dev
```


## 📄 License

This project is licensed under the MIT License.
