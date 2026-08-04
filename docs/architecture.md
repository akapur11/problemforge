# Architecture Overview 
This document describes the high-level architecture of ProblemForge and how each component communicates. The architecture is designed to keep the frontend, backend, AI services, and data storage loosely coupled so the application can grow over time.

                User
                  │
                  ▼
     Next.js + React Frontend (UI)
                  │
          HTTPS Requests (REST API)
                  │
                  ▼
       FastAPI Backend API (Python)
                  │
      ┌───────────┼───────────┐
      ▼           ▼           ▼
      LLM API    PostgreSQL    External APIs
                (Later)     (Later)

# System Components
1. Frontend
   - Next.js
   - Responsibilities:
     - Homepage
     - Search form
     - Display project cards
     - Loading animations
     - Error messages

2. Backend
   - FastAPI
   - Responsibilities:
     - Receive requests
     - Validate user input
     - Call the AI
     - Format the response
     - Save projects
     - Handle errors

3. AI Layer
   - Initial:
    Backend
    
    ↓
    
    LLM API
    
    ↓
    
    Generated response

   - Later:
     Backend
      
      ↓
      
      Retrieve real-world information
      
      ↓
      
      LLM
      
      ↓
      
      Project ideas

4. Database
   - Saved projects
   - Categories
   - Users (later)
   - Generation history (later)

5. Data Flow
   User

    ↓
    
    Clicks Generate
    
    ↓
    
    Frontend sends POST request
    
    ↓
    
    Backend validates request
    
    ↓
    
    Backend creates AI prompt
    
    ↓
    
    LLM generates ideas
    
    ↓
    
    Backend formats JSON
    
    ↓
    
    Frontend displays cards

# Component Breakdown
1. Frontend
   - Home Page
   - Search Form
   - Results Page
   - Project Card
   - Navigation
   - Footer
     * Will become parts of React component
  
2. Backend
   - API Routes
   - AI Service
   - Database Service
   - Utility Functions

# Architecture Principles
- Keep frontend and backend independent
- Backend handles all AI communication
- Database access goes through the backend only
- Components should have a single responsibility
- Build features incrementally
- Optimize for readability over cleverness

# Future Architecture
  User
  
  ↓
  
  Frontend
  
  ↓
  
  Backend
  
  ↓
  
  Authentication
  
  ↓
  
  Database
  
  ↓
  
  Vector Database
  
  ↓
  
  AI
  
  ↓
  
  Analytics

# External APIs
- News APIs
- GitHub APIs
- Research paper APIs
- Trend analysis APIs

# AI Responsibilities
- Generate project ideas
- Explain why a problem matters
- Recommend technologies
- Estimate difficulty
- Suggest learning outcomes

## Design Decisions

### Why FastAPI?

Python has excellent support for AI tooling and integrates well with LLM APIs.

### Why Next.js?

Modern React framework with excellent performance and deployment support.

### Why PostgreSQL?

Reliable relational database that scales well and supports extensions like pgvector.

# Out of Scope (v1.0)
- Payments
- Premium subscriptions
- Mobile application
- Team collaboration
- Real-time notifications
- Admin dashboard
