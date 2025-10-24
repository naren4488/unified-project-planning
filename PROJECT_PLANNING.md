# 🧩 Unified Platform Frontend - Project Planning

## 🎯 Project Understanding & Business Overview

### **What is this project?**
A **unified frontend platform** that serves as a centralized dashboard for users to access multiple applications through a single interface. Think of it as a "launchpad" where users can discover, request access to, and launch various business applications.

### **Core Business Problem Being Solved**
- **Fragmented Access**: Users currently need to access multiple applications through different URLs, logins, and interfaces
- **Access Control Complexity**: Managing who has access to which applications is currently manual and inconsistent
- **User Experience**: No centralized place for users to discover available tools and manage their access

### **Business Value Proposition**
- **Single Sign-On Experience**: Users authenticate once and access multiple applications
- **Centralized Access Management**: Admins can control user permissions from one place
- **Improved User Discovery**: Users can see all available applications and their access status
- **Streamlined Onboarding**: New users get a clear view of what's available to them

### **Target Users**
- **End Users**: Employees who need access to various business applications
- **Admins/Ops Team**: Personnel who manage user accounts and application access

### **Overall User Flow**

#### **1. Authentication Flow**
```
User visits platform → Login page → Choose authentication method:
├── Username/Password → Validate credentials
└── Microsoft OAuth → Redirect to Microsoft → Return with token
↓
Success → Redirect to Dashboard
Failure → Show error message
```

#### **2. Dashboard Experience**
```
User lands on Dashboard → See sidebar navigation:
├── Home: Welcome message, basic info
├── Launchpad: Grid of available applications
└── Profile: User settings and account management
```

#### **3. Application Access Flow**
```
User visits Launchpad → See app cards with different states:
├── ✅ Has Access → "Open App" button → Launch application
├── 🚫 No Access → "Request Access" button → Modal confirmation → API call → Toast notification
└── ⏳ Pending → "Access Requested" status
```

#### **4. Admin Workflow**
```
Admin needs to grant access → 
├── Create user accounts via backend APIs (no self-registration)
├── Assign application permissions via backend systems
├── Share login credentials with users directly
└── Manage access requests via backend admin tools
```
**Note**: No admin UI screens required - all admin functionality handled by backend team

### **Key Business Rules**
1. **No Self-Registration**: All user accounts are created by admins via backend APIs
2. **Admin-Controlled Access**: Users cannot gain access to applications without admin approval (handled via backend)
3. **Clear Permission Visibility**: Users always know their access status for each application
4. **Request-Based Access**: Users can request access, but admins must approve via backend systems
5. **Unified Authentication**: Single login provides access to the platform (individual apps may have their own auth)
6. **No Admin UI Required**: Admin functionality handled by backend team through APIs manually

### **Success Metrics**
- **User Adoption**: How many users actively use the platform
- **Access Request Volume**: Number of access requests processed
- **Time to Access**: How quickly users can get access to needed applications
- **User Satisfaction**: Feedback on the unified experience
- **Technical Performance**: Fast loading, intuitive navigation, robust security
- **Code Quality**: Clean architecture, maintainable code structure

---

## 🛠️ Technical Architecture

### Technology Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Framework** | Next.js 14+ (App Router) | Modern React framework with SSR/SSG |
| **Language** | TypeScript | Type safety and developer experience |
| **Styling** | Tailwind CSS + shadcn/ui | Utility-first CSS with pre-built components |
| **State Management** | React Context → Redux Toolkit | Progressive state management evolution |
| **Authentication** | NextAuth.js + Azure AD | Email/password + Microsoft OAuth |
| **Design System** | Custom Tailwind theme | Consistent design tokens and theming |

### Application Structure

#### Authentication Routes
- `/auth/login` - Username & Password login
- `/auth/login/ms` - Microsoft OAuth login
- `/auth/forgot-password` - Password recovery

#### Dashboard Routes
- `/` - Home page
- `/apps` - Launchpad (application grid)
- `/profile` - User profile management

### State Management Strategy

#### Phase 1: React Context
- AuthContext (user state, login/logout)
- AppContext (apps data, access permissions)

#### Phase 2: Redux Toolkit
- Global state management
- Async API calls (createAsyncThunk)
- Caching and optimistic updates

## 📋 Functional Requirements

### Authentication System
- ✅ **Sign-in only** (no public registration)
- ✅ **Admin-controlled accounts** (credentials shared directly by admin via backend)
- ✅ **Dual authentication methods**: Username/Password + Microsoft OAuth
- ✅ **Password recovery** for email-based accounts
- ✅ **Graceful error handling** for unauthorized access attempts
- ✅ **No admin UI required** (admin functionality handled by backend team)

### Authentication Flow Details (From Figma Designs)

#### Login Page (`/auth/login`)
- **Layout**: Split design with form (60%) and lifestyle image (40%)
- **Form Elements**:
  - Purple circular logo with white 'V' and dotted arc
  - "Welcome back" heading with "Please login to continue" subtitle
  - Email input with placeholder "Enter your email"
  - Password input with placeholder "Enter your Password"
  - "Forgot Password?" link (right-aligned)
  - Purple "Sign In" button
  - "or" separator line
  - White "Sign in with Microsoft" button with Microsoft logo

#### Forgot Password Flow
- **Trigger**: "Forgot Password?" link on login page
- **Modal Dialog**: "Password reset" overlay with:
  - Close (X) button in top-right
  - Success message: "We have sent an email with a password reset link to your registered email address. If you haven't received the email, be sure to check your spam folder."
  - "Back to login" link with left arrow

#### Password Reset Page (`/auth/reset-password`)
- **Layout**: Centered white card on gradient background
- **Form Elements**:
  - Purple logo with dotted arc
  - "Choose a new password" title
  - Password input with eye icon for visibility toggle
  - Confirm Password input with eye icon
  - Password strength indicator (visual bar with color coding)
  - Requirements checklist with purple checkmarks:
    - Minimum 8 characters
    - One uppercase and one lowercase
    - One number
    - One special character
    - Confirm new password matches
  - Submit button (purple when enabled, grey when disabled)
  - "Go to login" link

#### Password Reset Success
- **Success Dialog**: Centered modal with:
  - Green circular checkmark icon
  - "Password reset successful!" message
  - Purple "Login" button

### Dashboard Navigation
```
Sidebar Navigation:
├── 🏠 Home (/)
├── 📱 Launchpad (/apps)
└── 👤 Profile (/profile)
```

### Page Specifications

#### Home Page ✅ **COMPLETED**
- **Personalized Welcome**: "Good morning, Jason 👋" in pinkish-purple
- **Main Value Proposition**: "Your unified space to plan, target, and optimize campaigns"
- **Call-to-Action**: "Explore our apps →" button with gradient styling
- **Feature Cards**: Three horizontal cards highlighting key capabilities:
  - **Review Geo Performance**: Globe icon, geo-targeting insights
  - **Top Audience Segments**: Target icon, audience analysis
  - **Setup a new Campaign**: Puzzle piece icon, campaign creation
- **Clean Design**: White background with subtle purple gradient

#### Launchpad Page (`/apps`) ✅ **COMPLETED**
- **Header**: "viamedia Launchpad" with dotted arc branding
- **Application Cards**: Three main applications in horizontal layout:
  - **Omnichannel Planning**:
    - Purple globe icon with network lines
    - Description: "Recommends the optimal budget, channel mix, and projected outcomes to help marketers maximize efficiency and impact."
    - Access: "Request access" button with padlock icon
    - Status: "Your account doesn't have permission to access this application"
  - **LFID Geo Graph Targeting**:
    - Yellow diamond icon with black outline and arrow
    - Description: "An AI-powered geo-targeting tool that maps audience clusters and helps you focus spend where campaigns perform best."
    - Access: "Target audiences →" button with gradient
  - **Attention+**:
    - Blue circular icon with white 'C' shape
    - Description: "A creative builder tool that enables you to design, customize, and manage ad creatives seamlessly across channels, ensuring consistency and impact."
    - Access: "Create engaging ads →" button with gradient
- **Useful Tips Section**:
  - Lightbulb icon with "Useful tips for you" title
  - Three optimization tips for campaign management
- **Request Access Modal**:
  - Title: "Request access"
  - Message: "We have sent your request to administrator. You will be notified via email once your request is approved."
  - Close button and overlay styling


#### Profile Page (`/profile`) ✅ **COMPLETED**
- **Page Title**: "My Account" in large bold text
- **Tab Navigation**: 
  - "Account info" tab (active with purple underline)
  - "Change password" tab (inactive)
- **Account Info Tab**:
  - User Profile Summary with circular profile picture and hover menu
  - Name display: "John Mathews" in bold text
  - Email display: "johnmathews@gmail.com" in smaller text
  - Purple "Edit" button with pencil icon for profile editing
  - Two-column layout with editable form fields
  - Fields: First name, Last name, Email, Mobile number (with country code), Gender (dropdown), Time zone (dropdown)
  - Action buttons: Purple "Save" and grey "Cancel"
- **Change Password Tab**:
  - Current Password field with eye icon for visibility toggle
  - New Password field with placeholder "Enter new password"
  - Confirm New Password field with placeholder "Re-enter new password"
  - Password strength indicator with visual bar (Weak/Strong)
  - Password requirements checklist with purple checkmarks
  - Submit button (purple when enabled, grey when disabled)
  - Error handling: "Invalid password!" message for current password
- **Password Change Success Modal**:
  - Green checkmark icon with "Password reset successful!" message
  - Purple "Go to profile" button
- **User Dropdown Menu**: Profile picture in sidebar shows "My Account" and "Logout" options

## 🎨 Design System & UI Strategy

### Styling Architecture
```
Tailwind CSS (Base)
├── shadcn/ui (Components)
├── Custom Theme (Brand Colors)
└── Design Tokens (Typography, Spacing)
```

### Implementation Approach
- **Tailwind Config Extensions**: Custom colors, spacing, radius
- **Centralized Tokens**: Typography and spacing consistency
- **Component Library**: shadcn/ui as foundation
- **Custom Theme**: Brand-specific styling layer

### UI State Management
| Scenario | Component | Implementation |
|----------|-----------|----------------|
| **Loading** | Skeleton | shadcn `Skeleton` component |
| **Error** | Error Boundary | Custom `ErrorMessage` component |
| **Empty State** | Placeholder | Informational messages |

## 🔐 Security & Access Control

### Route Protection Strategy
- **Middleware-based**: Protect routes at the edge
- **Layout Guards**: Component-level access control
- **Permission Checks**: Before rendering app cards

### User Experience Principles
- **Graceful Degradation**: Friendly messages for restricted access
- **Clear Indicators**: Visual feedback for access status
- **Consistent Behavior**: Unified access control across all apps


## 🎨 Design Reference Analysis

### Current Design Observations (from shared references)

#### Login Page Design ✅ **COMPLETED**
- **Layout**: Split design with form (60%) and lifestyle image (40%)
- **Brand Elements**: Purple circular logo with white 'V' and dotted arc
- **Typography**: "Welcome back" heading with "Please login to continue" subtitle
- **Form Fields**: Email and Password inputs with placeholders
- **Authentication**: Email/password + Microsoft OAuth with logo
- **UX Elements**: "Forgot Password?" link, "or" separator

#### Dashboard/Home Page Design ✅ **COMPLETED**
- **Layout**: Purple sidebar (left) + white main content area
- **Sidebar**: Logo, Home/Apps navigation, user profile with dropdown menu
- **Main Content**: Personalized greeting, value proposition, CTA button
- **Feature Cards**: Three horizontal cards (Geo Performance, Audience Segments, Campaign Setup)

#### Apps Page Design ✅ **COMPLETED**
- **Layout**: Purple sidebar + white main content with "viamedia Launchpad" header
- **Application Cards**: Three apps (Omnichannel Planning, LFID Geo Graph Targeting, Attention+)
- **Access Control**: Request access buttons with permission status messages
- **Useful Tips**: Lightbulb section with campaign optimization advice

### Design System Insights

#### Color Palette (Observed)
- **Primary Purple**: `#8B5CF6` (approximate) - used for buttons, accents, logo
- **Secondary Purple**: Darker shade for sidebar background
- **Accent Pink**: Pinkish-purple for greetings and highlights
- **Neutral**: White backgrounds, light gray borders, dark text

#### Component Patterns
- **Cards**: White background, rounded corners, consistent spacing
- **Buttons**: Purple primary, white secondary with borders
- **Icons**: Consistent white icons on purple backgrounds
- **Typography**: Clear hierarchy with bold headings and regular body text

#### Layout Patterns
- **Sidebar width**: Narrow, fixed width with dark background
- **Main content**: Wide, light background with generous padding
- **Grid systems**: Three-column layouts for feature/app cards
- **Screen support**: Large screen only (desktop/laptop)

## ✅ Clarified Requirements (From Team Discussion)

### **Confirmed Features for Initial Phase**
- ✅ **Authentication**: Username/password + Microsoft OAuth only
- ✅ **Admin-controlled access**: No signup, credentials shared by admin via backend
- ✅ **Request Access Flow**: Dialog modal → API call → Toast notification
- ✅ **Basic Navigation**: Home, Launchpad, Profile
- ✅ **Launchpad**: App cards with access control and request flow
- ✅ **No Admin UI**: Admin functionality handled by backend team through APIs


### **Key Implementation Details**
- **Request Access**: Modal dialog → Backend API → Toast notification
- **Route Structure**: Clear paths defined for all main pages
- **Authentication Flow**: Separate routes for different login methods
- **Access Control**: Clear visual distinction between accessible and restricted apps
- **App Launch**: Opens in new tab with authentication tokens passed
- **Screen Support**: Large screen only (no responsive/mobile design required)

### **Available Applications**
1. **Omnichannel Planning** - Budget optimization tool (requires admin approval)
2. **LFID Geo Graph Targeting** - AI-powered geo-targeting (available to user)
3. **Attention+** - Creative builder and ad management (available to user)

### **Profile & Account Management** ✅ **COMPLETED**
- **Account Info Tab**: User profile summary, editable form fields, save/cancel actions
- **Change Password Tab**: Current/new/confirm password fields, strength indicator, requirements checklist
- **User Dropdown**: Profile picture menu with "My Account" and "Logout" options
- **Success Modals**: Password change confirmation with "Go to profile" action

## 🚀 Implementation Phases

### Phase 1: Foundation
- [ ] Next.js project setup with TypeScript
- [ ] Tailwind CSS + shadcn/ui configuration
- [ ] Basic authentication flow
- [ ] Core layout and navigation

### Phase 2: Core Features
- [ ] Apps page with access control
- [ ] Profile management
- [ ] Error handling and loading states

### Phase 3: Enhancement
- [ ] Redux Toolkit integration
- [ ] Advanced state management
- [ ] Performance optimizations
- [ ] Testing implementation

### Phase 4: Polish
- [ ] UI/UX refinements
- [ ] Accessibility improvements
- [ ] Documentation
- [ ] Deployment setup

---

## 📋 Team Discussion Points & Pending Items

### 🎨 **Pending UI/UX Designs**

#### Medium Priority (Can Start with Placeholders)
1. **Loading States** - Skeleton loaders, page indicators, button states
2. **Error States** - 404/500 pages, form validation, empty states

### 🔧 **Key Technical Questions**

#### Backend Integration
- API endpoints for authentication and app data
- JWT token management and Microsoft OAuth handling
- Request access API endpoints and data structure
- User permission checking and app integration flow

#### Infrastructure & Deployment
- Environment configuration (dev/staging/prod)
- Deployment strategy and CDN requirements
- Environment variable management

#### Business Logic
- Permission levels and access control granularity
- User personalization and activity tracking

#### Design & Development
- Official brand guidelines and design tokens
- Development timeline and team coordination

## 📝 Key Notes

- **Admin functionality** handled by backend team via APIs (no admin UI required)
- **Phased state management** allows quick start while maintaining scalability
- **Design system approach** ensures consistency and maintainability
- **Access control strategy** provides clear user experience for different permission levels
- **Purple branding** with clean, modern aesthetic throughout the platform

This planning document serves as the foundation for implementation decisions and can be updated as requirements evolve.
