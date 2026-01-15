# Knowledge Repository - Frontend

A modern React-based knowledge management application built with Vite, featuring a rich text editor, article management, tagging system, and user authentication.

## ✨ Features

- **Rich Text Editor** - Powered by TipTap with support for:
  - Text formatting (bold, italic, underline, strikethrough)
  - Headings, lists, and blockquotes
  - Code blocks with syntax highlighting
  - Tables, images, and links
  - Text alignment and colors
- **Article Management** - Create, edit, view, and delete articles
- **Tagging System** - Organize articles with tags
- **Favorites** - Bookmark your favorite articles
- **Recently Viewed** - Track your reading history
- **User Profiles** - Personal profiles with article management
- **Dark/Light Theme** - Toggle between themes
- **Responsive Design** - Works on desktop and mobile

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| **Framework** | React 19 |
| **Build Tool** | Vite 7 |
| **Routing** | React Router DOM 7 |
| **HTTP Client** | Axios |
| **Rich Text Editor** | TipTap |
| **Testing** | Vitest + React Testing Library |
| **Linting** | ESLint |

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v18 or higher recommended)
- **npm** (v9 or higher) or **yarn**
- **Backend server** running on `http://localhost:3000` (see server README)

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone <repository-url>
cd knowledge_repo/client
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Configuration

The project uses environment files for configuration:

#### Development (`.env.development`)
```env
VITE_API_BASE=http://localhost:3000/api
```

#### Production (`.env.production`)
Create this file for production builds:
```env
VITE_API_BASE=https://your-production-api.com/api
```

> **Note:** All environment variables must be prefixed with `VITE_` to be exposed to the client-side code.

### 4. Start Development Server

```bash
npm run dev
```

The application will be available at `http://localhost:5173`

---

## 📜 Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server with hot reload |
| `npm run build` | Build for production |
| `npm run preview` | Preview production build locally |
| `npm run lint` | Run ESLint to check for code issues |
| `npm run test` | Run tests in watch mode |
| `npm run test:run` | Run tests once |
| `npm run test:coverage` | Run tests with coverage report |

---

## 📁 Project Structure

```
client/
├── public/               # Static assets
├── src/
│   ├── assets/           # Images and other assets
│   ├── components/       # Reusable components
│   │   ├── common/       # Common UI components (Loading, Toast, etc.)
│   │   ├── editor/       # Rich text editor components
│   │   └── layout/       # Layout components (Header, Footer)
│   ├── context/          # React Context providers
│   │   ├── AuthContext.jsx    # Authentication state
│   │   └── ThemeContext.jsx   # Theme (dark/light) state
│   ├── hooks/            # Custom React hooks
│   ├── pages/            # Page components
│   │   ├── ArticleDetail/    # Single article view
│   │   ├── ArticleEditor/    # Create/edit articles
│   │   ├── Articles/         # Article listing (home page)
│   │   ├── Favorites/        # Favorited articles
│   │   ├── Login/            # Authentication page
│   │   ├── Profile/          # User profile
│   │   ├── RecentlyViewed/   # Recently viewed articles
│   │   └── Tags/             # Tag management
│   ├── services/         # API service layer
│   │   └── api.js        # Axios-based API client
│   ├── styles/           # CSS stylesheets
│   │   ├── variables.css     # CSS custom properties
│   │   ├── base.css          # Base/reset styles
│   │   ├── layout.css        # Layout utilities
│   │   ├── components/       # Component-specific styles
│   │   ├── views/            # Page-specific styles
│   │   └── features/         # Feature-specific styles
│   ├── utils/            # Utility functions
│   ├── App.jsx           # Main application component
│   ├── main.jsx          # Application entry point
│   └── setupTests.js     # Test configuration
├── index.html            # HTML entry point
├── vite.config.js        # Vite configuration
├── eslint.config.js      # ESLint configuration
└── package.json          # Project dependencies
```

---

## 🔐 Authentication

The application uses JWT-based authentication. The `AuthContext` manages:

- User login/logout state
- Token storage (localStorage)
- Protected route handling

### Protected Routes

All routes except `/login` require authentication. Unauthenticated users are automatically redirected to the login page.

---

## 🎨 Theming

The application supports light and dark themes via `ThemeContext`. Theme preference is:

- Persisted in localStorage
- Applied via CSS custom properties (see `styles/variables.css`)
- Toggled via the header theme button

---

## 🧪 Testing

The project uses **Vitest** with **React Testing Library** for testing.

### Running Tests

```bash
# Run tests in watch mode
npm run test

# Run tests once
npm run test:run

# Run tests with coverage
npm run test:coverage
```

### Test File Naming

Test files should follow the pattern: `*.test.js` or `*.test.jsx`

---

## 🔗 API Integration

The frontend communicates with the backend via the API service layer (`src/services/api.js`).

### Base URL Configuration

The API base URL is configured via the `VITE_API_BASE` environment variable.

### API Endpoints Used

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/auth/login` | POST | User authentication |
| `/auth/me` | GET | Get current user |
| `/articles` | GET/POST | List/create articles |
| `/articles/:id` | GET/PUT/DELETE | Article CRUD |
| `/tags` | GET/POST | List/create tags |
| `/favorites` | GET/POST/DELETE | Manage favorites |
| `/recently-viewed` | GET/POST | Track viewed articles |
| `/users/profile` | GET/PUT | User profile management |

---

## 🏗️ Building for Production

```bash
# Create production build
npm run build

# Preview the build locally
npm run preview
```

The build output will be in the `dist/` directory, ready for deployment.

---

## 🐳 Docker Deployment

The project includes Docker configuration for production deployment using a multi-stage build.

### Files Overview

| File | Purpose |
|------|---------|
| `Dockerfile` | Multi-stage build that compiles the app and serves it with Nginx |
| `nginx.conf` | Nginx configuration with SPA routing, compression, and caching |
| `.dockerignore` | Excludes unnecessary files from the Docker build context |

### Building the Docker Image

```bash
docker build -t knowledge-repo-client .
```

### Running the Container

```bash
# Run on port 8080
docker run -d -p 8080:80 knowledge-repo-client

# Or run on a different port
docker run -d -p 3000:80 knowledge-repo-client
```

The application will be available at `http://localhost:8080` (or your chosen port).

### How It Works

The Dockerfile uses a **multi-stage build** for optimal image size:

1. **Stage 1 (Build):** Uses `node:20-alpine` to install dependencies and run `npm run build`
2. **Stage 2 (Production):** Uses `nginx:alpine` to serve the compiled static files

This approach results in a final image of ~25MB instead of ~1.2GB (if Node.js was included).

### Nginx Configuration

The `nginx.conf` file provides:

- **SPA Routing:** Redirects all routes to `index.html` for React Router compatibility
- **Gzip Compression:** Reduces file transfer size for faster loading
- **Static Asset Caching:** Caches JS, CSS, and images for 1 year
- **Security Headers:** Adds protection against common web vulnerabilities
- **Health Check Endpoint:** Provides a `/health` endpoint for container health monitoring

### Health Check

The Nginx configuration includes a `/health` endpoint for container health monitoring and load balancer probes.

```bash
# Test the health endpoint
curl http://localhost:8080/health
# Returns: healthy
```

This endpoint:
- Returns `200 OK` with body `healthy`
- Has access logging disabled to prevent log spam
- Can be used with Docker health checks or Kubernetes probes

**Docker Compose with health check:**
```yaml
services:
  frontend:
    build: .
    ports:
      - "8080:80"
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 5s
```

**Kubernetes liveness/readiness probe:**
```yaml
livenessProbe:
  httpGet:
    path: /health
    port: 80
  initialDelaySeconds: 5
  periodSeconds: 10
readinessProbe:
  httpGet:
    path: /health
    port: 80
  initialDelaySeconds: 5
  periodSeconds: 10
```

### Environment Variables

For production, you may need to configure the API base URL. Create a `.env.production` file before building:

```env
VITE_API_BASE=https://your-production-api.com/api
```

Then rebuild the Docker image to include the new configuration.

### Docker Compose (Optional)

If you have a backend server, you can use Docker Compose to run both services together. Create a `docker-compose.yml`:

```yaml
version: '3.8'
services:
  frontend:
    build: .
    ports:
      - "8080:80"
    depends_on:
      - backend
  
  backend:
    build: ../server
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=your_database_url
```

---

## 🐛 Troubleshooting

### Common Issues

#### "Network Error" or API connection issues
- Ensure the backend server is running on `http://localhost:3000`
- Check that `VITE_API_BASE` is correctly set in your `.env.development` file

#### Module not found errors
- Run `npm install` to ensure all dependencies are installed
- Delete `node_modules` and `package-lock.json`, then reinstall

#### Port 5173 already in use
- Stop any other Vite dev servers
- Or change the port in `vite.config.js`:
  ```js
  export default defineConfig({
    server: {
      port: 3001
    }
  })
  ```

---

## 📝 Development Notes

### Adding New Pages

1. Create a new folder in `src/pages/YourPage/`
2. Add `YourPage.jsx`, `YourPage.css`, and `YourPage.test.jsx`
3. Register the route in `App.jsx`

### Adding New Components

1. Create in `src/components/common/` (reusable) or `src/components/` (specific)
2. Follow existing patterns for consistency
3. Add corresponding test file

### CSS Organization

- Use `styles/variables.css` for theme tokens
- Component styles go in `styles/components/`
- Page-specific styles go in `styles/views/`

---

## 📄 License

This project is private and proprietary.
