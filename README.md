# Unified Project Planning

A modern web application built with Next.js 14+ that provides a unified dashboard for accessing multiple project planning tools and applications.

## 🚀 Features

- **🔐 Azure AD Authentication** - Secure login with Microsoft Azure Active Directory
- **📊 Unified Dashboard** - Single interface to access all project planning tools
- **🚀 Application Launchpad** - Quick access to Omnichannel Planning, LFID Geo Graph Targeting, and Attention+
- **👤 Profile Management** - User profile and account settings management
- **🔒 Password Management** - Secure password change and reset functionality
- **📱 Large Screen Optimized** - Designed for desktop and laptop screens

## 🛠️ Tech Stack

- **Framework**: Next.js 14+ (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS + shadcn/ui
- **Authentication**: NextAuth.js + Azure AD
- **State Management**: React Context (Phase 1), Redux Toolkit (Future)
- **Forms**: React Hook Form + Zod validation
- **Icons**: Lucide React
- **HTTP Client**: Axios

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

| Software | Version | Purpose | Download |
|----------|---------|---------|----------|
| Node.js | 18.x+ | Runtime environment | [Download](https://nodejs.org/) |
| npm | 9.x+ | Package manager | Included with Node.js |
| Git | 2.x+ | Version control | [Download](https://git-scm.com/) |
| VS Code | Latest | IDE (recommended) | [Download](https://code.visualstudio.com/) |

### Verify Installation

```bash
node --version    # Should show v18.x or higher
npm --version     # Should show 9.x or higher
git --version     # Should show 2.x or higher
```


## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/localfactor/unified-platform-frontend-user.git
cd unified-platform-frontend-user
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Setup

```bash
# Copy environment template
cp .env.example .env.local

# Edit .env.local with your actual values
```

### 4. Configure Environment Variables

Update `.env.local` with your actual values:

```env
# NextAuth.js Configuration
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-secret-key-here

# Azure AD Configuration
AZURE_AD_CLIENT_ID=your-azure-client-id
AZURE_AD_CLIENT_SECRET=your-azure-client-secret
AZURE_AD_TENANT_ID=your-azure-tenant-id

# API Configuration
API_BASE_URL=http://localhost:8000
API_TIMEOUT=10000

# Application Configuration
APP_NAME=Unified Project Planning
APP_VERSION=1.0.0
```

### 5. Azure AD Setup

1. **Create Azure AD App Registration**:
   - Go to [Azure Portal](https://portal.azure.com/)
   - Navigate to "Azure Active Directory" → "App registrations"
   - Click "New registration"
   - Set redirect URI: `http://localhost:3000/api/auth/callback/azure-ad`

2. **Configure Authentication**:
   - Add platform: "Web"
   - Redirect URI: `http://localhost:3000/api/auth/callback/azure-ad`
   - Logout URL: `http://localhost:3000/login`

3. **Get Credentials**:
   - Copy "Application (client) ID" → `AZURE_AD_CLIENT_ID`
   - Copy "Directory (tenant) ID" → `AZURE_AD_TENANT_ID`
   - Create client secret → `AZURE_AD_CLIENT_SECRET`

### 6. Run the Application

```bash
# Start development server
npm run dev

# Open http://localhost:3000 in your browser
```

## 📁 Project Structure

### 🏗️ Co-located Components Architecture

This project follows the **co-located components structure** where components are placed close to where they're used, rather than in a global components folder. This approach provides several benefits:

- **🎯 Better Organization**: Components are grouped with their related pages/features
- **🔍 Easier Navigation**: Find components quickly by looking in the same directory as the page
- **📦 Reduced Coupling**: Components are naturally scoped to their specific use cases
- **🚀 Better Performance**: Easier to implement code splitting and lazy loading
- **🧹 Cleaner Imports**: Shorter, more intuitive import paths

### 📂 Structure Breakdown

- **`app/(auth)/_components/`** - Authentication-specific components (LoginForm, ForgotPasswordForm, etc.)
- **`app/(dashboard)/_components/`** - Dashboard-specific components (Sidebar, AppCard, etc.)
- **`app/(dashboard)/profile/_components/`** - Profile-specific components (ProfileForm, PasswordChangeForm, etc.)
- **`components/`** - Only truly shared components (LoadingSpinner, ErrorBoundary, etc.)
- **`components/ui/`** - shadcn/ui components (Button, Input, Card, etc.)

```
src/
├── app/                          # Next.js App Router
│   ├── (auth)/                   # Authentication routes
│   │   ├── _components/          # Auth-specific components
│   │   │   ├── LoginForm.tsx    # Login form component
│   │   │   ├── ForgotPasswordForm.tsx
│   │   │   ├── ResetPasswordForm.tsx
│   │   │   └── MicrosoftLoginButton.tsx
│   │   ├── login/               # Login page
│   │   │   └── page.tsx
│   │   ├── forgot-password/     # Forgot password page
│   │   │   └── page.tsx
│   │   └── reset-password/      # Password reset page
│   │       └── page.tsx
│   ├── (dashboard)/             # Dashboard routes
│   │   ├── _components/          # Dashboard-specific components
│   │   │   ├── Sidebar.tsx      # Dashboard sidebar
│   │   │   ├── UserProfile.tsx  # User profile dropdown
│   │   │   ├── AppCard.tsx      # Application card
│   │   │   ├── AccessRequestModal.tsx
│   │   │   └── FeatureCard.tsx   # Dashboard feature cards
│   │   ├── dashboard/           # Main dashboard
│   │   │   └── page.tsx
│   │   ├── apps/                # Applications page
│   │   │   └── page.tsx
│   │   └── profile/             # User profile
│   │       ├── _components/     # Profile-specific components
│   │       │   ├── ProfileForm.tsx
│   │       │   ├── PasswordChangeForm.tsx
│   │       │   ├── ProfilePicture.tsx
│   │       │   └── AccountTabs.tsx
│   │       └── page.tsx
│   ├── api/                     # API routes
│   │   └── auth/                # NextAuth.js API
│   ├── globals.css              # Global styles
│   └── layout.tsx               # Root layout
├── components/                   # Shared/Common components only
│   ├── ui/                      # shadcn/ui components
│   ├── common/                  # Truly shared components
│   │   ├── LoadingSpinner.tsx   # Loading states
│   │   ├── ErrorBoundary.tsx    # Error handling
│   │   ├── ConfirmDialog.tsx    # Confirmation dialogs
│   │   └── Toast.tsx            # Toast notifications
│   └── layout/                  # Global layout components
│       ├── Header.tsx           # Global header
│       └── Footer.tsx           # Global footer
├── lib/                         # Utility libraries
│   ├── auth.ts                  # NextAuth configuration
│   └── utils.ts                 # Utility functions
├── types/                       # TypeScript type definitions
├── contexts/                    # React Context providers
├── hooks/                       # Custom React hooks
├── utils/                       # Utility functions
├── constants/                   # Application constants
└── middleware.ts                # Next.js middleware
```

## 🎨 Available Scripts

```bash
# Development
npm run dev              # Start development server
npm run build            # Build for production
npm start                # Start production server

# Code Quality
npm run lint             # Run ESLint
npm run lint:fix         # Fix ESLint issues
npm run format           # Format code with Prettier
npm run format:check     # Check code formatting
npm run type-check       # Run TypeScript type checking

# Testing
npm run test             # Run tests
npm run test:watch       # Run tests in watch mode
npm run test:coverage    # Run tests with coverage

# Component Management
npx shadcn-ui@latest add [component-name]  # Add new shadcn/ui component
```

## 🔧 Development Workflow

### 1. Feature Development

```bash
# Create feature branch
git checkout -b feature/your-feature-name

# Make changes and commit
git add .
git commit -m "feat: add your feature"

# Push to remote
git push origin feature/your-feature-name
```

### 2. Code Quality

```bash
# Before committing, run:
npm run lint:fix          # Fix linting issues
npm run format            # Format code
npm run type-check        # Check types
npm run test              # Run tests
```

### 3. Pull Request

1. Create pull request from feature branch to `main`
2. Ensure all checks pass
3. Request code review
4. Merge after approval

## 🧪 Testing

### Running Tests

```bash
# Run all tests
npm run test

# Run tests in watch mode
npm run test:watch

# Run tests with coverage
npm run test:coverage
```

### Test Structure

```
src/
├── __tests__/                 # Test files
│   ├── components/            # Component tests
│   ├── pages/                 # Page tests
│   ├── utils/                 # Utility tests
│   └── setup.ts               # Test setup
```

## 🚀 Deployment

### Production Build

```bash
# Build for production
npm run build

# Start production server
npm start
```

### Environment Variables (Production)

```env
NEXTAUTH_URL=https://your-domain.com
NEXTAUTH_SECRET=your-production-secret
AZURE_AD_CLIENT_ID=your-production-client-id
AZURE_AD_CLIENT_SECRET=your-production-client-secret
AZURE_AD_TENANT_ID=your-production-tenant-id
API_BASE_URL=https://your-api-domain.com
```


## 🐛 Troubleshooting

### Common Issues

#### 1. Authentication Issues
```bash
# Check environment variables
cat .env.local

# Verify Azure AD configuration
# Ensure redirect URIs match exactly
```

#### 2. Build Issues
```bash
# Clear Next.js cache
rm -rf .next

# Reinstall dependencies
rm -rf node_modules package-lock.json
npm install
```

#### 3. TypeScript Issues
```bash
# Run type checking
npm run type-check

# Check for missing types
npm install @types/[package-name]
```

#### 4. Port Already in Use
```bash
# Kill process on port 3000
lsof -ti:3000 | xargs kill -9

# Or use different port
npm run dev -- -p 3001
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Built with ❤️ using Next.js, TypeScript, and Tailwind CSS**
