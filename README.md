## Tech Stack

### Frontend

- **HTML5** - Semantic markup and structure
- **CSS3** - Advanced styling with Flexbox and Grid
- **Bootstrap 5** - Responsive design framework
- **JavaScript (ES6+)** - Interactive functionality and DOM manipulation
- **SVG Graphics** - Interactive Philippines map
- **Google Fonts** - Typography (Cardo & Source Sans Pro)

### Backend

- **Node.js** - JavaScript runtime environment
- **Express.js** - Web application framework
- **Express Session** - Session management
- **Express Validator** - Input validation and sanitization

### Database & Cloud Services

- **MySQL** - Local development database
- **PostgreSQL** - Production database management
- **Supabase** - Backend-as-a-Service for production database hosting

### Deployment & Hosting

- **Railway** - Backend hosting and deployment
- **Vercel** - Frontend hosting and CDN
- **GitHub** - Version control and CI/CD

### Security & Utilities

- **bcrypt** - Password hashing and security
- **CORS** - Cross-origin resource sharing
- **dotenv** - Environment variable management
- **Body Parser** - Request parsing middleware

## Prerequisites

### For Local Development

- **[Node.js](https://nodejs.org/)** (v14 or higher)
- **[MySQL](https://www.mysql.com/)** (v5.7 or higher) - **Required for local development**
- **[Git](https://git-scm.com/)** for version control
- A modern web browser (Chrome, Firefox, Safari, Edge)

### For Production Deployment

- **[GitHub](https://github.com/)** account
- **[Supabase](https://supabase.com/)** account - **PostgreSQL database for production**
- **[Railway](https://railway.app/)** account (Backend hosting)
- **[Vercel](https://vercel.com/)** account (Frontend hosting)



## Detailed Setup Guide

### Local Development Setup

### 1. **Clone the Repository**

```bash
git clone https://github.com/Ren-zee/exploremore.git
cd exploremore
```

### 2. **Install Dependencies**

```bash
npm install
```

**Dependencies included:**

- express
- express-session
- express-validator
- cors
- dotenv
- mysql2 (for local development)
- pg (PostgreSQL client for production)
- bcrypt
- body-parser

### 3. **Database Setup**

#### Local Development: MySQL

**Step 1: Install and Setup MySQL**

```sql
CREATE DATABASE exploremoreph;
USE exploremoreph;
-- Run the contents of models/database_schema.sql
```

**Step 2: Configure MySQL Connection**

The application uses MySQL for local development. Make sure MySQL is running on your machine.

#### Production Alternative: Supabase (PostgreSQL)

If you want to test with the production database locally:

1. Create a free account at [supabase.com](https://supabase.com)
2. Create a new project
3. Go to SQL Editor and run the contents of `models/supabase_schema.sql`
4. Get your connection string from Settings → Database

**Database includes:**

- `users` table - User authentication and management
- `feedback` table - User feedback and reviews
- Proper indexing for optimized performance
- Foreign key relationships for data integrity

### 4. **Environment Configuration**

Create a `.env` file in the root directory:

```env
# LOCAL DEVELOPMENT - MySQL Configuration
DB_HOST=localhost
DB_USER=your_mysql_username
DB_PASSWORD=your_mysql_password
DB_NAME=exploremoreph
DB_PORT=3306

# Alternative: PRODUCTION DATABASE - Supabase PostgreSQL (for testing)
# POSTGRES_URL=postgresql://postgres:[YOUR-PASSWORD]@db.[YOUR-PROJECT-REF].supabase.co:5432/postgres

# Session Configuration
SESSION_SECRET=your-session-secret-key

# Server Configuration
PORT=3001
NODE_ENV=development
```

**Important Notes:**

- **Local Development**: Use MySQL configuration (DB_HOST, DB_USER, etc.)
- **Production Testing**: Uncomment POSTGRES_URL if testing with Supabase locally

### 5. **Start the Application**

#### Development Mode

```bash
npm run dev
```

#### Production Mode

```bash
npm start
```

The server will start on `http://localhost:3001`

## Production Deployment Guide

### Prerequisites for Deployment

- GitHub repository with your code
- Supabase account
- Railway account
- Vercel account

### Step 1: Set up Supabase Database (Production PostgreSQL)

1. **Create Supabase Project**

   - Go to [supabase.com](https://supabase.com)
   - Create new project: `exploremore-ph`
   - Choose region closest to your users

2. **Set up Database Schema**

   - Go to SQL Editor in Supabase dashboard
   - Copy and run contents of `models/supabase_schema.sql` (PostgreSQL schema)

3. **Get Connection Details**
   - Go to Settings → Database
   - Copy connection string and individual parameters

**Note**: Production uses PostgreSQL via Supabase, different from local MySQL setup.

### Step 2: Deploy Backend to Railway

1. **Create Railway Project**

   - Go to [railway.app](https://railway.app)
   - Sign in with GitHub
   - Click "New Project" → "Deploy from GitHub repo"
   - Select your ExploreMore repository

2. **Configure Environment Variables**

   Add these variables in Railway dashboard:

   ```env
   # Production PostgreSQL via Supabase
   POSTGRES_HOST=your-supabase-host
   POSTGRES_USER=postgres
   POSTGRES_PASSWORD=your-supabase-password
   POSTGRES_DATABASE=postgres
   DB_PORT=5432
   SESSION_SECRET=your-very-secure-session-secret-key-here
   NODE_ENV=production
   FRONTEND_URL=https://your-app.vercel.app
   ```

   **Note**: Production environment uses PostgreSQL parameters, not MySQL.

3. **Deploy and Test**
   - Railway will automatically deploy
   - Test health endpoint: `https://your-app.railway.app/health`

### Step 3: Deploy Frontend to Vercel

1. **Update API URLs**

   In your frontend JavaScript files, update the API base URL:

   ```javascript
   const API_BASE_URL = "https://your-app.railway.app";
   ```

2. **Create Vercel Project**

   - Go to [vercel.com](https://vercel.com)
   - Import your GitHub repository
   - Configure:
     - Framework Preset: Other
     - Root Directory: `./`
     - Output Directory: `public`

3. **Deploy**
   - Click "Deploy"
   - Copy your Vercel URL

### Step 4: Update CORS Configuration

1. Update `FRONTEND_URL` in Railway with your Vercel URL
2. Railway will automatically redeploy

### Step 5: Test Production Deployment

Test these features:

- User registration and login
- Feedback submission
- All page navigation
- Admin features


## 📁 Project Structure

```
ExploreMore-PH/
├── 📁 config/
│   └── db.js                 # Database configuration
├── 📁 models/
│   ├── database_schema.sql   # MySQL schema for local development
│   └── supabase_schema.sql   # PostgreSQL schema for production
├── 📁 public/               # Frontend assets
│   ├── 📁 images/           # Image assets by region
│   │   ├── 📁 Luzon/        # Luzon tourist spot images
│   │   ├── 📁 Visayas/      # Visayas tourist spot images
│   │   └── 📁 Mindanao/     # Mindanao tourist spot images
│   ├── index.html           # Homepage with interactive map
│   ├── luzon.html           # Luzon tourist spots
│   ├── visayas.html         # Visayas tourist spots
│   ├── mindanao.html        # Mindanao tourist spots
│   ├── budget.html          # Budget planning page
│   ├── promos.html          # Promotions page
│   ├── aboutus.html         # About us page
│   ├── login.html           # Login page
│   ├── signup.html          # Registration page
│   ├── dashboard.html       # Admin dashboard
│   ├── dashboard-*.html     # Admin management pages
│   ├── auth.js              # Authentication logic
│   ├── budget.js            # Budget calculation
│   ├── dashboard.js         # Admin dashboard functionality
│   ├── feedback.js          # User feedback system
│   └── 📁 CSS files         # Styling for all pages
├── server.js                # Main server file
├── package.json             # Dependencies and scripts
├── .env                     # Environment variables (not in repo)
├── railway.json             # Railway deployment config
├── vercel.json              # Vercel deployment config
├── DeploymentGuide.md       # Detailed deployment instructions
├── ProductionDeployment.md  # Production checklist
└── README.md               # This file
```

## Additional Resources

- **[Supabase Documentation](https://supabase.com/docs)** - Database and backend services
- **[Railway Documentation](https://docs.railway.app)** - Backend hosting
- **[Vercel Documentation](https://vercel.com/docs)** - Frontend hosting
- **[Express.js Documentation](https://expressjs.com/)** - Web framework
- **[PostgreSQL Documentation](https://www.postgresql.org/docs/)** - Database

[![Node.js](https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express.js](https://img.shields.io/badge/Express.js-404D59?style=for-the-badge)](https://expressjs.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)](https://supabase.com/)
[![Railway](https://img.shields.io/badge/Railway-131415?style=for-the-badge&logo=railway&logoColor=white)](https://railway.app/)
[![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://vercel.com/)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white)](https://getbootstrap.com/)

## Database Architecture

**Important: This project uses different databases for different environments:**

- **Local Development**: MySQL database for ease of local setup
- **Production**: PostgreSQL (via Supabase) for scalable cloud hosting

Both database schemas are included in the `models/` directory with corresponding setup instructions.

---

**© 2025 ExploreMore PH. All rights reserved.**
