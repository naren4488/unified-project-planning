# Project Setup Guide

## Initial Project Setup Commands

### 1. Create Next.js Project
```bash
# Create new Next.js project with TypeScript and Tailwind CSS
npx create-next-app@latest unified-project-planning --typescript --tailwind --eslint --app --src-dir --import-alias "@/*"

# Navigate to project directory
cd unified-project-planning
```

### 2. Install Core Dependencies
```bash
# Install shadcn/ui CLI
npx shadcn-ui@latest init

# Install shadcn/ui components
npx shadcn-ui@latest add button
npx shadcn-ui@latest add input
npx shadcn-ui@latest add label
npx shadcn-ui@latest add card
npx shadcn-ui@latest add tabs
npx shadcn-ui@latest add dialog
npx shadcn-ui@latest add dropdown-menu
npx shadcn-ui@latest add avatar
npx shadcn-ui@latest add toast
npx shadcn-ui@latest add form
npx shadcn-ui@latest add select
npx shadcn-ui@latest add checkbox
npx shadcn-ui@latest add radio-group
npx shadcn-ui@latest add switch
npx shadcn-ui@latest add textarea
npx shadcn-ui@latest add badge
npx shadcn-ui@latest add separator
npx shadcn-ui@latest add skeleton
npx shadcn-ui@latest add progress
npx shadcn-ui@latest add alert
npx shadcn-ui@latest add alert-dialog
npx shadcn-ui@latest add sheet
npx shadcn-ui@latest add popover
npx shadcn-ui@latest add tooltip
npx shadcn-ui@latest add command
npx shadcn-ui@latest add calendar
npx shadcn-ui@latest add date-picker
npx shadcn-ui@latest add table
npx shadcn-ui@latest add pagination
npx shadcn-ui@latest add breadcrumb
npx shadcn-ui@latest add navigation-menu
npx shadcn-ui@latest add menubar
npx shadcn-ui@latest add context-menu
npx shadcn-ui@latest add hover-card
npx shadcn-ui@latest add accordion
npx shadcn-ui@latest add collapsible
npx shadcn-ui@latest add scroll-area
npx shadcn-ui@latest add resizable
npx shadcn-ui@latest add slider
npx shadcn-ui@latest add toggle
npx shadcn-ui@latest add toggle-group
npx shadcn-ui@latest add aspect-ratio
npx shadcn-ui@latest add sonner
```

### 3. Install Authentication Dependencies
```bash
# Install NextAuth.js and Azure AD provider
npm install next-auth @auth/core
npm install @auth/azure-ad-provider

# Install JWT and session management
npm install jose
npm install @types/jose
```

### 4. Install State Management Dependencies
```bash
# Install Redux Toolkit (for future use)
npm install @reduxjs/toolkit react-redux
npm install @types/react-redux

# Install React Context dependencies (already included with React)
```

### 5. Install Development Dependencies
```bash
# Install TypeScript types
npm install @types/node @types/react @types/react-dom

# Install development tools
npm install --save-dev @typescript-eslint/eslint-plugin
npm install --save-dev @typescript-eslint/parser
npm install --save-dev eslint-config-next
npm install --save-dev prettier
npm install --save-dev eslint-config-prettier
npm install --save-dev eslint-plugin-prettier
```

### 6. Install Additional Utilities
```bash
# Install utility libraries
npm install clsx tailwind-merge
npm install class-variance-authority
npm install lucide-react
npm install @radix-ui/react-icons
npm install date-fns
npm install react-hook-form
npm install @hookform/resolvers
npm install zod
npm install axios
npm install @types/axios
```

### 7. Create Project Structure
```bash
# Create directory structure
mkdir -p src/app/\(auth\)/login
mkdir -p src/app/\(auth\)/forgot-password
mkdir -p src/app/\(auth\)/reset-password
mkdir -p src/app/\(dashboard\)/dashboard
mkdir -p src/app/\(dashboard\)/apps
mkdir -p src/app/\(dashboard\)/profile
mkdir -p src/app/\(dashboard\)/change-password
mkdir -p src/components/ui
mkdir -p src/components/auth
mkdir -p src/components/dashboard
mkdir -p src/components/profile
mkdir -p src/components/common
mkdir -p src/lib
mkdir -p src/types
mkdir -p src/contexts
mkdir -p src/hooks
mkdir -p src/utils
mkdir -p src/constants
mkdir -p src/middleware
mkdir -p src/styles
mkdir -p public/images
mkdir -p public/icons
```

### 8. Create Configuration Files
```bash
# Create TypeScript config
cat > tsconfig.json << 'EOF'
{
  "compilerOptions": {
    "target": "es5",
    "lib": ["dom", "dom.iterable", "es6"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
EOF

# Create Tailwind config
cat > tailwind.config.ts << 'EOF'
import type { Config } from "tailwindcss"

const config: Config = {
  darkMode: ["class"],
  content: [
    './pages/**/*.{ts,tsx}',
    './components/**/*.{ts,tsx}',
    './app/**/*.{ts,tsx}',
    './src/**/*.{ts,tsx}',
  ],
  prefix: "",
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      keyframes: {
        "accordion-down": {
          from: { height: "0" },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: "0" },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
} satisfies Config

export default config
EOF

# Create ESLint config
cat > .eslintrc.json << 'EOF'
{
  "extends": [
    "next/core-web-vitals",
    "@typescript-eslint/recommended",
    "prettier"
  ],
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "rules": {
    "@typescript-eslint/no-unused-vars": "error",
    "@typescript-eslint/no-explicit-any": "warn",
    "prefer-const": "error"
  }
}
EOF

# Create Prettier config
cat > .prettierrc << 'EOF'
{
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 80,
  "endOfLine": "lf"
}
EOF

# Create .gitignore
cat > .gitignore << 'EOF'
# See https://help.github.com/articles/ignoring-files/ for more about ignoring files.

# dependencies
/node_modules
/.pnp
.pnp.js
.yarn/install-state.gz

# testing
/coverage

# next.js
/.next/
/out/

# production
/build

# misc
.DS_Store
*.pem

# debug
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# local env files
.env*.local
.env

# vercel
.vercel

# typescript
*.tsbuildinfo
next-env.d.ts
EOF
```

### 9. Create Environment Files
```bash
# Create environment template
cat > .env.example << 'EOF'
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
EOF

# Create local environment file
cp .env.example .env.local
```

### 10. Create Basic Files
```bash
# Create NextAuth configuration
cat > src/lib/auth.ts << 'EOF'
import { NextAuthOptions } from "next-auth"
import AzureADProvider from "next-auth/providers/azure-ad"

export const authOptions: NextAuthOptions = {
  providers: [
    AzureADProvider({
      clientId: process.env.AZURE_AD_CLIENT_ID!,
      clientSecret: process.env.AZURE_AD_CLIENT_SECRET!,
      tenantId: process.env.AZURE_AD_TENANT_ID!,
    }),
  ],
  callbacks: {
    async jwt({ token, account }) {
      if (account) {
        token.accessToken = account.access_token
      }
      return token
    },
    async session({ session, token }) {
      session.accessToken = token.accessToken
      return session
    },
  },
  pages: {
    signIn: '/login',
    error: '/login',
  },
}
EOF

# Create middleware
cat > src/middleware.ts << 'EOF'
import { withAuth } from "next-auth/middleware"

export default withAuth(
  function middleware(req) {
    // Add any additional middleware logic here
  },
  {
    callbacks: {
      authorized: ({ token }) => !!token,
    },
  }
)

export const config = {
  matcher: ["/dashboard/:path*", "/apps/:path*", "/profile/:path*"]
}
EOF

# Create utility functions
cat > src/lib/utils.ts << 'EOF'
import { type ClassValue, clsx } from "clsx"
import { twMerge } from "tailwind-merge"

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}
EOF

# Create types
cat > src/types/index.ts << 'EOF'
export interface User {
  id: string
  email: string
  name: string
  firstName: string
  lastName: string
  mobileNumber?: string
  gender?: string
  timezone?: string
  profilePicture?: string
  createdAt: string
  updatedAt: string
}

export interface Application {
  id: string
  name: string
  description: string
  icon: string
  url: string
  hasAccess: boolean
  category: string
}

export interface AccessRequest {
  id: string
  applicationId: string
  userId: string
  status: 'pending' | 'approved' | 'rejected'
  requestedAt: string
  processedAt?: string
  processedBy?: string
  reason?: string
}
EOF
```

### 11. Create Basic Pages
```bash
# Create root layout
cat > src/app/layout.tsx << 'EOF'
import type { Metadata } from 'next'
import { Inter } from 'next/font/google'
import './globals.css'

const inter = Inter({ subsets: ['latin'] })

export const metadata: Metadata = {
  title: 'Unified Project Planning',
  description: 'Unified project planning application',
}

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body className={inter.className}>{children}</body>
    </html>
  )
}
EOF

# Create global CSS
cat > src/app/globals.css << 'EOF'
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
    --primary: 221.2 83.2% 53.3%;
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96%;
    --secondary-foreground: 222.2 84% 4.9%;
    --muted: 210 40% 96%;
    --muted-foreground: 215.4 16.3% 46.9%;
    --accent: 210 40% 96%;
    --accent-foreground: 222.2 84% 4.9%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 221.2 83.2% 53.3%;
    --radius: 0.5rem;
  }

  .dark {
    --background: 222.2 84% 4.9%;
    --foreground: 210 40% 98%;
    --card: 222.2 84% 4.9%;
    --card-foreground: 210 40% 98%;
    --popover: 222.2 84% 4.9%;
    --popover-foreground: 210 40% 98%;
    --primary: 217.2 91.2% 59.8%;
    --primary-foreground: 222.2 84% 4.9%;
    --secondary: 217.2 32.6% 17.5%;
    --secondary-foreground: 210 40% 98%;
    --muted: 217.2 32.6% 17.5%;
    --muted-foreground: 215 20.2% 65.1%;
    --accent: 217.2 32.6% 17.5%;
    --accent-foreground: 210 40% 98%;
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 210 40% 98%;
    --border: 217.2 32.6% 17.5%;
    --input: 217.2 32.6% 17.5%;
    --ring: 224.3 76.3% 94.1%;
  }
}

@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply bg-background text-foreground;
  }
}
EOF

# Create home page
cat > src/app/page.tsx << 'EOF'
import { redirect } from 'next/navigation'

export default function HomePage() {
  redirect('/login')
}
EOF
```

### 12. Initialize Git Repository
```bash
# Initialize git repository
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: Project setup with Next.js, TypeScript, Tailwind CSS, and shadcn/ui"

# Create main branch
git branch -M main

# Add remote origin (replace with your repository URL)
# git remote add origin https://github.com/your-username/unified-project-planning.git

# Push to remote (uncomment when ready)
# git push -u origin main
```

### 13. Create Package.json Scripts
```bash
# Add additional scripts to package.json
npm pkg set scripts.lint="next lint"
npm pkg set scripts.lint:fix="next lint --fix"
npm pkg set scripts.format="prettier --write ."
npm pkg set scripts.format:check="prettier --check ."
npm pkg set scripts.type-check="tsc --noEmit"
npm pkg set scripts.build:analyze="ANALYZE=true npm run build"
```

### 14. Final Setup Commands
```bash
# Install all dependencies
npm install

# Run type checking
npm run type-check

# Run linting
npm run lint

# Format code
npm run format

# Build project
npm run build

# Start development server
npm run dev
```

## Post-Setup Checklist

- [ ] Update `.env.local` with actual Azure AD credentials
- [ ] Configure Azure AD app registration
- [ ] Test authentication flow
- [ ] Verify all shadcn/ui components are working
- [ ] Check TypeScript compilation
- [ ] Run ESLint and fix any issues
- [ ] Test build process
- [ ] Set up remote repository
- [ ] Push initial commit

## Development Commands

```bash
# Start development server
npm run dev

# Build for production
npm run build

# Start production server
npm start

# Run linting
npm run lint

# Fix linting issues
npm run lint:fix

# Format code
npm run format

# Check formatting
npm run format:check

# Type checking
npm run type-check

# Add new shadcn/ui component
npx shadcn-ui@latest add [component-name]
```

## Notes

- Replace placeholder values in `.env.local` with actual credentials
- Configure Azure AD app registration in Azure portal
- Update repository URL in git remote commands
- All commands assume you're in the project root directory
- The setup creates a complete Next.js 14+ project with App Router, TypeScript, and Tailwind CSS

