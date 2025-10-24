# 🧩 Component Structure & Repository Organization

## 📋 Complete Component List

Based on the Figma designs and project requirements, here are all the components that will be needed:

### **Authentication Components**
- `LoginForm` - Email/password login form
- `MicrosoftLoginButton` - Microsoft OAuth button with logo
- `ForgotPasswordModal` - Modal for password reset request
- `PasswordResetForm` - New password creation form
- `PasswordStrengthIndicator` - Visual password strength bar
- `PasswordRequirementsList` - Checklist of password requirements
- `AuthLayout` - Split layout for auth pages (form + image)
- `AuthHeader` - Logo and branding for auth pages

### **Dashboard Components**
- `Sidebar` - Main navigation sidebar
- `SidebarLogo` - Purple logo with dotted arc
- `SidebarNavItem` - Individual navigation items (Home, Apps)
- `UserProfileDropdown` - Profile picture with dropdown menu
- `DashboardLayout` - Main dashboard layout wrapper
- `WelcomeGreeting` - Personalized greeting component
- `FeatureCard` - Home page feature cards
- `CallToActionButton` - Main CTA button with gradient

### **Launchpad Components**
- `LaunchpadHeader` - "viamedia Launchpad" header with branding
- `AppCard` - Individual application card
- `AppIcon` - Application icon component
- `AccessButton` - App access button (Open/Request Access)
- `RequestAccessModal` - Modal for access requests
- `UsefulTipsSection` - Tips section with lightbulb icon
- `TipItem` - Individual tip bullet point

### **Profile Components**
- `ProfileTabs` - Tab navigation (Account info, Change password)
- `ProfileHeader` - "My Account" page header
- `ProfilePicture` - User profile picture with hover menu
- `ProfilePictureMenu` - Upload/Remove options menu
- `UserInfoDisplay` - Name and email display
- `AccountInfoForm` - Editable user information form
- `ChangePasswordForm` - Password change form
- `FormField` - Reusable form input component
- `CountryCodeDropdown` - Mobile number country selector
- `GenderDropdown` - Gender selection dropdown
- `TimezoneDropdown` - Timezone selection dropdown
- `PasswordVisibilityToggle` - Eye icon for password fields
- `FormActionButtons` - Save/Cancel button group

### **Shared/Common Components**
- `Button` - Base button component with variants
- `Input` - Base input component
- `Modal` - Base modal component
- `Toast` - Toast notification component (shadcn/ui)
- `LoadingSpinner` - Loading indicator
- `ErrorBoundary` - Error handling component
- `Skeleton` - Loading skeleton component
- `Icon` - Icon wrapper component
- `Card` - Base card component
- `Badge` - Status badge component
- `Separator` - Visual separator line
- `Label` - Form label component

### **Layout Components**
- `RootLayout` - Root application layout
- `PageContainer` - Main content container
- `Header` - Page header component
- `Footer` - Page footer (if needed)

---

## 🏗️ Repository Structure Options

### **Option 1: Centralized Components Structure (Current)**

```
src/
├── app/                          # Next.js App Router
│   ├── (auth)/                   # Auth route group
│   │   ├── login/
│   │   ├── ms-login/
│   │   └── forgot-password/
│   ├── (dashboard)/              # Protected dashboard routes
│   │   ├── page.tsx             # Home page
│   │   ├── apps/                # Launchpad page
│   │   └── profile/             # Profile page
│   ├── globals.css
│   ├── layout.tsx
│   └── middleware.ts
├── components/                   # All components centralized
│   ├── ui/                      # shadcn/ui components
│   │   ├── button.tsx
│   │   ├── input.tsx
│   │   ├── modal.tsx
│   │   ├── toast.tsx
│   │   └── ...
│   ├── auth/                    # Authentication components
│   │   ├── LoginForm.tsx
│   │   ├── MicrosoftLoginButton.tsx
│   │   ├── ForgotPasswordModal.tsx
│   │   ├── PasswordResetForm.tsx
│   │   ├── PasswordStrengthIndicator.tsx
│   │   ├── PasswordRequirementsList.tsx
│   │   ├── AuthLayout.tsx
│   │   └── AuthHeader.tsx
│   ├── dashboard/               # Dashboard components
│   │   ├── Sidebar.tsx
│   │   ├── SidebarLogo.tsx
│   │   ├── SidebarNavItem.tsx
│   │   ├── UserProfileDropdown.tsx
│   │   ├── DashboardLayout.tsx
│   │   ├── WelcomeGreeting.tsx
│   │   ├── FeatureCard.tsx
│   │   └── CallToActionButton.tsx
│   ├── launchpad/               # Launchpad components
│   │   ├── LaunchpadHeader.tsx
│   │   ├── AppCard.tsx
│   │   ├── AppIcon.tsx
│   │   ├── AccessButton.tsx
│   │   ├── RequestAccessModal.tsx
│   │   ├── UsefulTipsSection.tsx
│   │   └── TipItem.tsx
│   ├── profile/                 # Profile components
│   │   ├── ProfileTabs.tsx
│   │   ├── ProfileHeader.tsx
│   │   ├── ProfilePicture.tsx
│   │   ├── ProfilePictureMenu.tsx
│   │   ├── UserInfoDisplay.tsx
│   │   ├── AccountInfoForm.tsx
│   │   ├── ChangePasswordForm.tsx
│   │   ├── FormField.tsx
│   │   ├── CountryCodeDropdown.tsx
│   │   ├── GenderDropdown.tsx
│   │   ├── TimezoneDropdown.tsx
│   │   ├── PasswordVisibilityToggle.tsx
│   │   └── FormActionButtons.tsx
│   ├── shared/                  # Shared/common components
│   │   ├── LoadingSpinner.tsx
│   │   ├── ErrorBoundary.tsx
│   │   ├── Skeleton.tsx
│   │   ├── Icon.tsx
│   │   ├── Card.tsx
│   │   ├── Badge.tsx
│   │   ├── Separator.tsx
│   │   └── Label.tsx
│   └── layout/                  # Layout components
│       ├── RootLayout.tsx
│       ├── PageContainer.tsx
│       ├── Header.tsx
│       └── Footer.tsx
├── lib/                         # Utility functions and configs
├── hooks/                       # Custom React hooks
├── store/                       # State management
├── types/                       # TypeScript type definitions
└── constants/                   # Application constants
```

### **Option 2: Co-located Components Structure (Recommended)**

```
src/
├── app/                          # Next.js App Router
│   ├── (auth)/                   # Auth route group
│   │   ├── _components/          # Auth-specific components
│   │   │   ├── LoginForm.tsx
│   │   │   ├── MicrosoftLoginButton.tsx
│   │   │   ├── ForgotPasswordModal.tsx
│   │   │   ├── PasswordResetForm.tsx
│   │   │   ├── PasswordStrengthIndicator.tsx
│   │   │   ├── PasswordRequirementsList.tsx
│   │   │   ├── AuthLayout.tsx
│   │   │   └── AuthHeader.tsx
│   │   ├── login/
│   │   ├── ms-login/
│   │   └── forgot-password/
│   ├── (dashboard)/              # Protected dashboard routes
│   │   ├── _components/          # Dashboard-specific components
│   │   │   ├── Sidebar.tsx
│   │   │   ├── SidebarLogo.tsx
│   │   │   ├── SidebarNavItem.tsx
│   │   │   ├── UserProfileDropdown.tsx
│   │   │   ├── DashboardLayout.tsx
│   │   │   ├── WelcomeGreeting.tsx
│   │   │   ├── FeatureCard.tsx
│   │   │   └── CallToActionButton.tsx
│   │   ├── apps/
│   │   │   ├── _components/      # Apps-specific components
│   │   │   │   ├── LaunchpadHeader.tsx
│   │   │   │   ├── AppCard.tsx
│   │   │   │   ├── AppIcon.tsx
│   │   │   │   ├── AccessButton.tsx
│   │   │   │   ├── RequestAccessModal.tsx
│   │   │   │   ├── UsefulTipsSection.tsx
│   │   │   │   └── TipItem.tsx
│   │   │   └── page.tsx
│   │   ├── profile/
│   │   │   ├── _components/      # Profile-specific components
│   │   │   │   ├── ProfileTabs.tsx
│   │   │   │   ├── ProfileHeader.tsx
│   │   │   │   ├── ProfilePicture.tsx
│   │   │   │   ├── ProfilePictureMenu.tsx
│   │   │   │   ├── UserInfoDisplay.tsx
│   │   │   │   ├── AccountInfoForm.tsx
│   │   │   │   ├── ChangePasswordForm.tsx
│   │   │   │   ├── FormField.tsx
│   │   │   │   ├── CountryCodeDropdown.tsx
│   │   │   │   ├── GenderDropdown.tsx
│   │   │   │   ├── TimezoneDropdown.tsx
│   │   │   │   ├── PasswordVisibilityToggle.tsx
│   │   │   │   └── FormActionButtons.tsx
│   │   │   └── page.tsx
│   │   └── page.tsx              # Home page
│   ├── components/               # Global shared components only
│   │   ├── ui/                  # shadcn/ui components
│   │   │   ├── button.tsx
│   │   │   ├── input.tsx
│   │   │   ├── modal.tsx
│   │   │   ├── toast.tsx
│   │   │   └── ...
│   │   ├── LoadingSpinner.tsx
│   │   ├── ErrorBoundary.tsx
│   │   ├── Skeleton.tsx
│   │   ├── Icon.tsx
│   │   ├── Card.tsx
│   │   ├── Badge.tsx
│   │   ├── Separator.tsx
│   │   └── Label.tsx
│   ├── globals.css
│   ├── layout.tsx
│   └── middleware.ts
├── lib/                         # Utility functions and configs
├── hooks/                       # Custom React hooks
├── store/                       # State management
├── types/                       # TypeScript type definitions
└── constants/                   # Application constants
```

---

## 🎯 **Recommendation: Option 2 (Co-located Components)**

### **Why Option 2 is Better:**

1. **Better Organization**: Components are co-located with the pages that use them
2. **Easier Maintenance**: When working on a feature, all related components are in one place
3. **Clear Boundaries**: Each route group has its own component namespace
4. **Reduced Imports**: Shorter import paths for page-specific components
5. **Team Collaboration**: Different developers can work on different sections without conflicts
6. **Scalability**: Easy to add new features without cluttering the global components folder

### **Component Distribution:**

- **Global Components** (`/app/components/`): Only truly shared components used across multiple sections
- **Auth Components** (`/app/(auth)/_components/`): All authentication-related components
- **Dashboard Components** (`/app/(dashboard)/_components/`): Shared dashboard components
- **Apps Components** (`/app/(dashboard)/apps/_components/`): Launchpad-specific components
- **Profile Components** (`/app/(dashboard)/profile/_components/`): Profile-specific components

### **Import Examples:**

```typescript
// From page.tsx in /app/(dashboard)/apps/
import { AppCard } from './_components/AppCard'
import { LaunchpadHeader } from './_components/LaunchpadHeader'

// From page.tsx in /app/(auth)/login/
import { LoginForm } from '../_components/LoginForm'
import { AuthLayout } from '../_components/AuthLayout'

// Global components
import { LoadingSpinner } from '@/app/components/LoadingSpinner'
import { Button } from '@/app/components/ui/button'
```

This structure provides the best balance of organization, maintainability, and developer experience for the unified platform frontend project.

