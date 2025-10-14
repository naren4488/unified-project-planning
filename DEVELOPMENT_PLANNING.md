# 🚀 Unified Platform Frontend - Development Planning

## 📁 Project Structure

```
src/
├── app/                          # Next.js App Router
│   ├── (auth)/                   # Auth route group
│   │   ├── login/               # Username/password login
│   │   ├── ms-login/            # Microsoft OAuth login
│   │   └── forgot-password/     # Password recovery
│   ├── (dashboard)/             # Protected dashboard routes
│   │   ├── page.tsx             # Home page (/)
│   │   ├── apps/                # Launchpad page (/apps)
│   │   ├── notifications/       # Notifications page (/notifications)
│   │   └── profile/             # Profile page (/profile)
│   ├── globals.css              # Global styles
│   ├── layout.tsx               # Root layout
│   └── middleware.ts            # Route protection
├── components/                   # Reusable UI components
│   ├── ui/                      # shadcn/ui components
│   ├── auth/                    # Authentication components
│   ├── dashboard/               # Dashboard-specific components
│   ├── forms/                   # Form components
│   └── layout/                  # Layout components
├── lib/                         # Utility functions and configs
│   ├── auth.ts                  # NextAuth.js configuration
│   ├── api.ts                   # External API client
│   ├── utils.ts                 # Utility functions
│   └── validations.ts           # Form validation schemas
├── hooks/                       # Custom React hooks
├── store/                       # State management
│   ├── contexts/                # React Context providers
│   └── slices/                  # Redux slices (future)
├── types/                       # TypeScript type definitions
└── constants/                   # Application constants
```

## 🛣️ Route Structure

### Authentication Routes

| Route | Component | Purpose | Protection |
|-------|-----------|---------|------------|
| `/auth/login` | `LoginPage` | Username/password login | Public |
| `/auth/login/ms` | `MicrosoftLoginPage` | Microsoft OAuth login | Public |
| `/auth/forgot-password` | `ForgotPasswordPage` | Password recovery | Public |
| `/auth/reset-password` | `ResetPasswordPage` | Password reset form | Public (with token) |

### Dashboard Routes (Protected)

| Route | Component | Purpose | Protection |
|-------|-----------|---------|------------|
| `/` | `HomePage` | Welcome dashboard | Authenticated |
| `/apps` | `LaunchpadPage` | Application grid | Authenticated |
| `/notifications` | `NotificationsPage` | System notifications | Authenticated |
| `/profile` | `ProfilePage` | User settings | Authenticated |

### External API Integration

| Endpoint | Method | Purpose | Authentication |
|----------|--------|---------|----------------|
| `POST /auth/login` | POST | Username/password authentication | None |
| `POST /auth/ms/callback` | POST | Microsoft OAuth callback | None |
| `POST /auth/refresh` | POST | Token refresh | Bearer Token |
| `POST /auth/logout` | POST | User logout | Bearer Token |
| `POST /auth/forgot-password` | POST | Send password reset email | None |
| `POST /auth/reset-password` | POST | Reset password with token | None |
| `GET /apps` | GET | Get user's accessible apps | Bearer Token |
| `POST /apps/request-access` | POST | Request app access | Bearer Token |
| `GET /notifications` | GET | Get user notifications | Bearer Token |
| `PUT /notifications/[id]` | PUT | Mark notification as read | Bearer Token |
| `GET /user/profile` | GET | Get user profile | Bearer Token |
| `PUT /user/profile` | PUT | Update user profile | Bearer Token |
| `POST /user/change-password` | POST | Change user password | Bearer Token |

## 🧩 Component Architecture

### Layout Components

#### `RootLayout`
```typescript
interface RootLayoutProps {
  children: React.ReactNode;
}
```
- **Purpose**: Root layout with global providers
- **Features**: Auth provider, theme provider, global styles

#### `DashboardLayout`
```typescript
interface DashboardLayoutProps {
  children: React.ReactNode;
}
```
- **Purpose**: Dashboard layout with sidebar navigation
- **Features**: Sidebar, header, main content area

#### `AuthLayout`
```typescript
interface AuthLayoutProps {
  children: React.ReactNode;
}
```
- **Purpose**: Authentication pages layout
- **Features**: Split layout (form + image), branding

### Authentication Components

#### `LoginForm`
```typescript
interface LoginFormProps {
  onSubmit: (data: LoginFormData) => void;
  isLoading?: boolean;
  error?: string;
}

interface LoginFormData {
  username: string;
  password: string;
}
```

#### `MicrosoftLoginButton`
```typescript
interface MicrosoftLoginButtonProps {
  onSuccess: (user: User) => void;
  onError: (error: string) => void;
}
```

#### `ForgotPasswordForm`
```typescript
interface ForgotPasswordFormProps {
  onSubmit: (email: string) => void;
  isLoading?: boolean;
  success?: boolean;
}
```

### Dashboard Components

#### `Sidebar`
```typescript
interface SidebarProps {
  currentPath: string;
  user: User;
}

interface SidebarItem {
  id: string;
  label: string;
  icon: React.ComponentType;
  href: string;
  badge?: number;
}
```

#### `AppCard`
```typescript
interface AppCardProps {
  app: Application;
  userAccess: UserAccess;
  onRequestAccess: (appId: string) => void;
  onOpenApp: (appId: string) => void;
}

interface Application {
  id: string;
  name: string;
  description: string;
  icon: string;
  category: string;
  url?: string;
  accessType: 'iframe' | 'redirect' | 'external';
}

interface UserAccess {
  hasAccess: boolean;
  accessLevel?: 'read' | 'write' | 'admin';
  requestStatus?: 'pending' | 'approved' | 'rejected';
  expiresAt?: Date;
}
```

#### `RequestAccessModal`
```typescript
interface RequestAccessModalProps {
  isOpen: boolean;
  onClose: () => void;
  app: Application;
  onSubmit: (data: AccessRequestData) => void;
  isLoading?: boolean;
}

interface AccessRequestData {
  appId: string;
  reason: string;
  urgency: 'low' | 'medium' | 'high';
}
```

#### `NotificationCard`
```typescript
interface NotificationCardProps {
  notification: Notification;
  onMarkAsRead: (id: string) => void;
  onAction: (action: NotificationAction) => void;
}

interface Notification {
  id: string;
  title: string;
  message: string;
  type: 'info' | 'success' | 'warning' | 'error';
  isRead: boolean;
  createdAt: Date;
  actions?: NotificationAction[];
}

interface NotificationAction {
  id: string;
  label: string;
  type: 'button' | 'link';
  href?: string;
  onClick?: () => void;
}
```

### Form Components

#### `FormInput`
```typescript
interface FormInputProps {
  name: string;
  label: string;
  type?: 'text' | 'email' | 'password';
  placeholder?: string;
  required?: boolean;
  error?: string;
  disabled?: boolean;
}
```

#### `FormButton`
```typescript
interface FormButtonProps {
  type?: 'button' | 'submit' | 'reset';
  variant?: 'primary' | 'secondary' | 'ghost' | 'destructive';
  size?: 'sm' | 'md' | 'lg';
  isLoading?: boolean;
  disabled?: boolean;
  children: React.ReactNode;
}
```

## 📊 Data Models

### User Model
```typescript
interface User {
  id: string;
  email: string;
  username: string;
  firstName: string;
  lastName: string;
  avatar?: string;
  authProvider: 'email' | 'microsoft';
  isActive: boolean;
  lastLoginAt: Date;
  createdAt: Date;
  updatedAt: Date;
}
```

### Application Model
```typescript
interface Application {
  id: string;
  name: string;
  description: string;
  icon: string;
  category: ApplicationCategory;
  url?: string;
  accessType: ApplicationAccessType;
  isActive: boolean;
  requiresApproval: boolean;
  metadata?: Record<string, any>;
  createdAt: Date;
  updatedAt: Date;
}

type ApplicationCategory = 
  | 'marketing' 
  | 'analytics' 
  | 'tools' 
  | 'productivity' 
  | 'communication';

type ApplicationAccessType = 'iframe' | 'redirect' | 'external';
```

### User Access Model
```typescript
interface UserAccess {
  id: string;
  userId: string;
  applicationId: string;
  hasAccess: boolean;
  accessLevel: AccessLevel;
  grantedBy?: string;
  grantedAt?: Date;
  expiresAt?: Date;
  createdAt: Date;
  updatedAt: Date;
}

type AccessLevel = 'read' | 'write' | 'admin';
```

### Access Request Model
```typescript
interface AccessRequest {
  id: string;
  userId: string;
  applicationId: string;
  reason: string;
  urgency: RequestUrgency;
  status: RequestStatus;
  requestedAt: Date;
  reviewedBy?: string;
  reviewedAt?: Date;
  reviewNotes?: string;
}

type RequestUrgency = 'low' | 'medium' | 'high';
type RequestStatus = 'pending' | 'approved' | 'rejected' | 'cancelled';
```

### Notification Model
```typescript
interface Notification {
  id: string;
  userId: string;
  title: string;
  message: string;
  type: NotificationType;
  isRead: boolean;
  priority: NotificationPriority;
  metadata?: Record<string, any>;
  expiresAt?: Date;
  createdAt: Date;
  updatedAt: Date;
}

type NotificationType = 'info' | 'success' | 'warning' | 'error' | 'access_request';
type NotificationPriority = 'low' | 'medium' | 'high' | 'urgent';
```

## 🔧 State Management

### React Context Structure

#### `AuthContext`
```typescript
interface AuthContextType {
  user: User | null;
  isLoading: boolean;
  isAuthenticated: boolean;
  login: (credentials: LoginCredentials) => Promise<void>;
  loginWithMicrosoft: () => Promise<void>;
  logout: () => Promise<void>;
  forgotPassword: (email: string) => Promise<void>;
  resetPassword: (token: string, password: string) => Promise<void>;
}

interface LoginCredentials {
  username: string;
  password: string;
}
```

#### `AppContext`
```typescript
interface AppContextType {
  applications: Application[];
  userAccess: Record<string, UserAccess>;
  isLoading: boolean;
  error: string | null;
  fetchApplications: () => Promise<void>;
  requestAccess: (appId: string, reason: string, urgency: RequestUrgency) => Promise<void>;
  refreshAccess: () => Promise<void>;
}
```

#### `NotificationContext`
```typescript
interface NotificationContextType {
  notifications: Notification[];
  unreadCount: number;
  isLoading: boolean;
  fetchNotifications: () => Promise<void>;
  markAsRead: (id: string) => Promise<void>;
  markAllAsRead: () => Promise<void>;
  clearNotification: (id: string) => Promise<void>;
}
```

### Redux Store Structure (Future Phase)

```typescript
interface RootState {
  auth: AuthState;
  apps: AppsState;
  notifications: NotificationsState;
  ui: UIState;
}

interface AuthState {
  user: User | null;
  isLoading: boolean;
  error: string | null;
  isAuthenticated: boolean;
}

interface AppsState {
  applications: Application[];
  userAccess: Record<string, UserAccess>;
  accessRequests: AccessRequest[];
  isLoading: boolean;
  error: string | null;
}

interface NotificationsState {
  notifications: Notification[];
  unreadCount: number;
  isLoading: boolean;
  error: string | null;
}

interface UIState {
  sidebarOpen: boolean;
  currentPage: string;
  theme: 'light' | 'dark';
}
```

## 🔐 Authentication & Authorization

### NextAuth.js Configuration
```typescript
// lib/auth.ts
export const authOptions: NextAuthOptions = {
  providers: [
    CredentialsProvider({
      name: 'credentials',
      credentials: {
        username: { label: 'Username', type: 'text' },
        password: { label: 'Password', type: 'password' }
      },
      async authorize(credentials) {
        // Call external backend API to validate credentials
        const response = await fetch(`${process.env.BACKEND_API_URL}/auth/login`, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(credentials),
        });
        
        if (!response.ok) return null;
        
        const user = await response.json();
        return user;
      }
    }),
    AzureADProvider({
      clientId: process.env.AZURE_AD_CLIENT_ID!,
      clientSecret: process.env.AZURE_AD_CLIENT_SECRET!,
      tenantId: process.env.AZURE_AD_TENANT_ID!,
    })
  ],
  session: {
    strategy: 'jwt',
    maxAge: 24 * 60 * 60, // 24 hours
  },
  callbacks: {
    async jwt({ token, user }) {
      if (user) {
        token.user = user;
      }
      return token;
    },
    async session({ session, token }) {
      session.user = token.user as User;
      return session;
    },
  },
  pages: {
    signIn: '/auth/login',
    error: '/auth/error',
  },
};
```

### Route Protection Middleware
```typescript
// middleware.ts
export function middleware(request: NextRequest) {
  const token = request.cookies.get('next-auth.session-token');
  const isAuthRoute = request.nextUrl.pathname.startsWith('/auth');
  const isDashboardRoute = request.nextUrl.pathname.startsWith('/');

  if (!token && !isAuthRoute) {
    return NextResponse.redirect(new URL('/auth/login', request.url));
  }

  if (token && isAuthRoute) {
    return NextResponse.redirect(new URL('/', request.url));
  }

  return NextResponse.next();
}
```

## 🌐 External API Integration

### API Client Configuration
```typescript
// lib/api.ts
class ApiClient {
  private baseURL: string;
  private token: string | null = null;

  constructor(baseURL: string) {
    this.baseURL = baseURL;
  }

  setToken(token: string) {
    this.token = token;
  }

  private async request<T>(
    endpoint: string,
    options: RequestInit = {}
  ): Promise<T> {
    const url = `${this.baseURL}${endpoint}`;
    const config: RequestInit = {
      headers: {
        'Content-Type': 'application/json',
        ...(this.token && { Authorization: `Bearer ${this.token}` }),
        ...options.headers,
      },
      ...options,
    };

    const response = await fetch(url, config);
    
    if (!response.ok) {
      throw new Error(`API Error: ${response.status}`);
    }

    return response.json();
  }

  // Auth endpoints (external backend)
  async login(credentials: LoginCredentials): Promise<AuthResponse> {
    return this.request('/auth/login', {
      method: 'POST',
      body: JSON.stringify(credentials),
    });
  }

  async forgotPassword(email: string): Promise<void> {
    return this.request('/auth/forgot-password', {
      method: 'POST',
      body: JSON.stringify({ email }),
    });
  }

  async resetPassword(token: string, password: string): Promise<void> {
    return this.request('/auth/reset-password', {
      method: 'POST',
      body: JSON.stringify({ token, password }),
    });
  }

  // App endpoints (external backend)
  async getApplications(): Promise<Application[]> {
    return this.request('/apps');
  }

  async requestAccess(data: AccessRequestData): Promise<void> {
    return this.request('/apps/request-access', {
      method: 'POST',
      body: JSON.stringify(data),
    });
  }

  // Notification endpoints (external backend)
  async getNotifications(): Promise<Notification[]> {
    return this.request('/notifications');
  }

  async markNotificationAsRead(id: string): Promise<void> {
    return this.request(`/notifications/${id}`, {
      method: 'PUT',
      body: JSON.stringify({ isRead: true }),
    });
  }

  // User endpoints (external backend)
  async getUserProfile(): Promise<User> {
    return this.request('/user/profile');
  }

  async updateUserProfile(data: Partial<User>): Promise<User> {
    return this.request('/user/profile', {
      method: 'PUT',
      body: JSON.stringify(data),
    });
  }

  async changePassword(currentPassword: string, newPassword: string): Promise<void> {
    return this.request('/user/change-password', {
      method: 'POST',
      body: JSON.stringify({ currentPassword, newPassword }),
    });
  }
}

// Singleton instance
export const apiClient = new ApiClient(process.env.NEXT_PUBLIC_API_URL || '');
```

## 🎨 Styling & Design System

### Tailwind Configuration
```typescript
// tailwind.config.ts
module.exports = {
  content: [
    './src/pages/**/*.{js,ts,jsx,tsx,mdx}',
    './src/components/**/*.{js,ts,jsx,tsx,mdx}',
    './src/app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#f3f1ff',
          100: '#e9e5ff',
          500: '#8b5cf6',
          600: '#7c3aed',
          700: '#6d28d9',
          900: '#4c1d95',
        },
        secondary: {
          50: '#fdf4ff',
          100: '#fae8ff',
          500: '#d946ef',
          600: '#c026d3',
        },
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
      },
      spacing: {
        '18': '4.5rem',
        '88': '22rem',
      },
    },
  },
  plugins: [require('@tailwindcss/forms')],
};
```

### Component Variants
```typescript
// components/ui/button.tsx
const buttonVariants = cva(
  'inline-flex items-center justify-center rounded-md text-sm font-medium transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:opacity-50 disabled:pointer-events-none ring-offset-background',
  {
    variants: {
      variant: {
        default: 'bg-primary-600 text-white hover:bg-primary-700',
        secondary: 'bg-secondary-100 text-secondary-900 hover:bg-secondary-200',
        outline: 'border border-input hover:bg-accent hover:text-accent-foreground',
        ghost: 'hover:bg-accent hover:text-accent-foreground',
        destructive: 'bg-red-500 text-white hover:bg-red-600',
      },
      size: {
        default: 'h-10 py-2 px-4',
        sm: 'h-9 px-3 rounded-md',
        lg: 'h-11 px-8 rounded-md',
        icon: 'h-10 w-10',
      },
    },
    defaultVariants: {
      variant: 'default',
      size: 'default',
    },
  }
);
```

## 🧪 Testing Strategy

### Test Structure
```
tests/
├── __mocks__/                   # Mock implementations
├── components/                  # Component tests
├── pages/                       # Page tests
├── hooks/                       # Custom hook tests
├── utils/                       # Utility function tests
├── integration/                 # Integration tests
└── setup.ts                     # Test setup
```

### Testing Tools
- **Jest**: Unit and integration testing
- **React Testing Library**: Component testing
- **Playwright**: End-to-end testing
- **MSW**: API mocking

### Test Examples
```typescript
// tests/components/AppCard.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { AppCard } from '@/components/dashboard/AppCard';

describe('AppCard', () => {
  const mockApp = {
    id: '1',
    name: 'Test App',
    description: 'Test description',
    icon: 'test-icon',
    category: 'tools',
    accessType: 'redirect' as const,
  };

  const mockUserAccess = {
    hasAccess: false,
  };

  it('renders app information correctly', () => {
    render(
      <AppCard 
        app={mockApp} 
        userAccess={mockUserAccess}
        onRequestAccess={jest.fn()}
        onOpenApp={jest.fn()}
      />
    );

    expect(screen.getByText('Test App')).toBeInTheDocument();
    expect(screen.getByText('Test description')).toBeInTheDocument();
  });

  it('shows request access button when user has no access', () => {
    render(
      <AppCard 
        app={mockApp} 
        userAccess={mockUserAccess}
        onRequestAccess={jest.fn()}
        onOpenApp={jest.fn()}
      />
    );

    expect(screen.getByText('Request Access')).toBeInTheDocument();
  });
});
```

## 🚀 Deployment & Environment

### Environment Variables
```bash
# .env.local
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-secret-key

# External Backend API
NEXT_PUBLIC_API_URL=http://localhost:8000/api
BACKEND_API_URL=http://localhost:8000/api

# Azure AD (Microsoft OAuth)
AZURE_AD_CLIENT_ID=your-client-id
AZURE_AD_CLIENT_SECRET=your-client-secret
AZURE_AD_TENANT_ID=your-tenant-id

# Development/Production URLs
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### Build Configuration
```json
// package.json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:e2e": "playwright test",
    "type-check": "tsc --noEmit"
  }
}
```

### Docker Configuration
```dockerfile
# Dockerfile
FROM node:18-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

FROM node:18-alpine AS builder
WORKDIR /app
COPY . .
COPY --from=deps /app/node_modules ./node_modules
RUN npm run build

FROM node:18-alpine AS runner
WORKDIR /app
ENV NODE_ENV production
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/.next/static ./.next/static

EXPOSE 3000
CMD ["node", "server.js"]
```

## 📋 Development Checklist

### Phase 1: Foundation
- [ ] Next.js project setup with TypeScript
- [ ] Tailwind CSS + shadcn/ui configuration
- [ ] External API client setup
- [ ] Basic routing structure
- [ ] Layout components (RootLayout, DashboardLayout, AuthLayout)
- [ ] Environment configuration
- [ ] Basic authentication setup with NextAuth.js

### Phase 2: Authentication
- [ ] Login page with username/password
- [ ] Microsoft OAuth integration
- [ ] Forgot password flow
- [ ] Password reset functionality
- [ ] Route protection middleware
- [ ] Auth context provider
- [ ] Session management
- [ ] Integration with external backend authentication

### Phase 3: Dashboard Core
- [ ] Sidebar navigation component
- [ ] Home page implementation
- [ ] Launchpad page with app grid
- [ ] App card component with access control
- [ ] Request access modal
- [ ] Toast notification system
- [ ] Loading states and error handling
- [ ] Integration with external backend for apps data

### Phase 4: Advanced Features
- [ ] Notifications page
- [ ] Profile page with settings
- [ ] User management features
- [ ] Real-time notifications (if needed)
- [ ] Redux Toolkit integration
- [ ] Performance optimizations
- [ ] Integration with external backend for notifications and user data

### Phase 5: Testing & Polish
- [ ] Unit tests for components
- [ ] Integration tests for external API
- [ ] End-to-end tests
- [ ] Accessibility improvements
- [ ] Performance optimization
- [ ] Documentation
- [ ] Frontend deployment setup

## 🎯 Frontend Developer Considerations

### Backend Integration Strategy
- **External API**: All backend functionality is handled by a separate service
- **API Client**: Use a centralized API client to communicate with external backend
- **Authentication**: NextAuth.js handles frontend auth, validates with external backend
- **Data Fetching**: Use React Query/SWR for efficient data fetching and caching
- **Error Handling**: Implement consistent error handling for API failures

### Development Workflow
1. **Frontend Development**: Focus on UI/UX implementation
2. **API Integration**: Use mock data during development, integrate with real API later
3. **Authentication**: Implement NextAuth.js with external backend validation
4. **State Management**: Start with React Context, migrate to Redux if needed
5. **Testing**: Mock external API calls for unit/integration tests

### Key Frontend Responsibilities
- ✅ **UI/UX Implementation**: All user interface components and interactions
- ✅ **Client-side Routing**: Next.js App Router setup and navigation
- ✅ **State Management**: Frontend state for UI interactions and data
- ✅ **Authentication Flow**: Login/logout UI and session management
- ✅ **API Integration**: HTTP client setup and error handling
- ✅ **Performance**: Code splitting, lazy loading, optimization
- ✅ **Accessibility**: WCAG compliance and keyboard navigation
- ✅ **Responsive Design**: Mobile-first approach with Tailwind CSS

### External Dependencies
- **Backend API**: Separate service providing all business logic
- **Authentication Service**: External auth validation
- **Asset Management**: External CDN for images/icons
- **Analytics**: External tracking service integration

---

This development planning document provides the technical foundation for implementing the unified platform frontend. Each section can be expanded with more specific implementation details as development progresses.
