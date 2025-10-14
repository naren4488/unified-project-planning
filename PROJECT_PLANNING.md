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
├── Notifications: System messages and updates
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
├── Create user accounts (no self-registration)
├── Assign application permissions
├── Share login credentials with users
└── Manage access requests from users
```

### **Key Business Rules**
1. **No Self-Registration**: All user accounts are created by admins
2. **Admin-Controlled Access**: Users cannot gain access to applications without admin approval
3. **Clear Permission Visibility**: Users always know their access status for each application
4. **Request-Based Access**: Users can request access, but admins must approve
5. **Unified Authentication**: Single login provides access to the platform (individual apps may have their own auth)

### **Success Metrics**
- **User Adoption**: How many users actively use the platform
- **Access Request Volume**: Number of access requests processed
- **Time to Access**: How quickly users can get access to needed applications
- **User Satisfaction**: Feedback on the unified experience

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
- `/notifications` - System notifications
- `/profile` - User profile management

### State Management Strategy

#### Phase 1: React Context
- AuthContext (user state, login/logout)
- AppContext (apps data, access permissions)
- NotificationContext (notifications state)

#### Phase 2: Redux Toolkit
- Global state management
- Async API calls (createAsyncThunk)
- Caching and optimistic updates

## 📋 Functional Requirements

### Authentication System
- ✅ **Sign-in only** (no public registration)
- ✅ **Admin-controlled accounts** (credentials shared directly by admin)
- ✅ **Dual authentication methods**: Username/Password + Microsoft OAuth
- ✅ **Password recovery** for email-based accounts
- ✅ **Graceful error handling** for unauthorized access attempts

### Dashboard Navigation
```
Sidebar Navigation:
├── 🏠 Home (/)
├── 📱 Launchpad (/apps)
├── 🔔 Notifications (/notifications)
└── 👤 Profile (/profile)
```

### Page Specifications

#### Home Page
- Simple welcome message
- Placeholder for future content (announcements, user details)
- Clean, minimal design

#### Launchpad Page (`/apps`)
- **Grid layout** of available applications
- **Access control indicators**:
  - ✅ Has access → Action button with arrow
  - 🚫 No access → "Request Access" button with padlock icon
- **Request Access Flow**:
  - Dialog modal confirmation
  - Send request to backend via API
  - Show toast notification with response
- **Support scenarios**: All access, partial access, no access
- **UI States**: Loading skeletons, error states, empty states

#### Notifications Page (`/notifications`)
- System and app-level notifications
- **Features**: Read/unread indicators, timestamps, action links, mark as read
- **Status**: Design pending

#### Profile Page (`/profile`)
- User information display
- Password management (email users only)
- Microsoft account info (read-only)
- Sign-out functionality
- **Status**: Design pending

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

## 📊 Success Metrics

- **User Experience**: Fast loading, intuitive navigation
- **Security**: Robust authentication, proper access control
- **Maintainability**: Clean code structure, scalable architecture
- **Performance**: Optimized bundle size, efficient rendering

## 🎨 Design Reference Analysis

### Current Design Observations (from shared references)

#### Login Page Design
- **Split layout**: Login form (60%) + lifestyle image (40%)
- **Brand elements**: Circular purple logo with white 'V', dotted arc
- **Typography hierarchy**: "Welcome back" (large bold), "Please login to continue" (smaller)
- **Form styling**: Rounded white inputs, purple accent color
- **Authentication options**: Email/password + Microsoft OAuth button
- **UX elements**: "Forgot Password?" link, clean separator with "or"

#### Dashboard/Home Page Design
- **Sidebar navigation**: Dark purple background, white icons
- **Personalized greeting**: "Good morning, Jason 👋" in pinkish-purple
- **AI assistant integration**: Central input field with attachment/microphone icons
- **Insight cards**: Purple star icons, data-driven recommendations
- **Feature cards**: Three-column grid with icons, descriptions, and action buttons

#### Apps Page Design
- **"viamedia Launchpad" branding**: Consistent with login page
- **Access control UI**: Clear "Request access" vs action buttons with arrows
- **Permission messaging**: "Your account doesn't have permission to access this application"
- **App card structure**: Icon, title, description, action button, status message
- **Recommendation system**: "Recommended for you" with personalized suggestions
- **Tips section**: Bulleted advice with lightbulb icon

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
- **Responsive considerations**: Split layouts for larger screens

## ✅ Clarified Requirements (From Team Discussion)

### **Confirmed Features for Initial Phase**
- ✅ **Authentication**: Username/password + Microsoft OAuth only
- ✅ **Admin-controlled access**: No signup, credentials shared by admin
- ✅ **Request Access Flow**: Dialog modal → API call → Toast notification
- ✅ **Basic Navigation**: Home, Launchpad, Notifications, Profile
- ✅ **Launchpad**: App cards with access control and request flow

### **Features Removed from Initial Phase**
- ❌ **Chat functionality**: All chat-related features deferred
- ❌ **AI Assistant**: AI insights, suggestions, and assistant features deferred
- ❌ **Useful Tips**: AI-generated tips on launchpad deferred
- ❌ **Signup Screen**: Not needed (admin-controlled only)

### **Key Implementation Details**
- **Request Access**: Modal dialog → Backend API → Toast notification
- **Route Structure**: Clear paths defined for all main pages
- **Authentication Flow**: Separate routes for different login methods
- **Access Control**: Clear visual distinction between accessible and restricted apps

## 🚀 Implementation Phases

### Phase 1: Foundation
- [ ] Next.js project setup with TypeScript
- [ ] Tailwind CSS + shadcn/ui configuration
- [ ] Basic authentication flow
- [ ] Core layout and navigation

### Phase 2: Core Features
- [ ] Apps page with access control
- [ ] Notifications system
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

#### High Priority (Blocking Development)
1. **Forgot Password Page Design**
   - Form layout and styling
   - Success/error state designs
   - Email confirmation flow

2. **Profile Page Design**
   - User information layout
   - Password change form
   - Microsoft account info display
   - Settings organization

3. **Notifications Page Design**
   - List layout and styling
   - Read/unread indicators
   - Notification types and icons
   - Action buttons and interactions

4. **Request Access Modal Design**
   - Modal layout and styling
   - Confirmation message
   - Loading states
   - Success/error feedback

#### Medium Priority (Can Start with Placeholders)
5. **Toast Notification Design**
   - Success, error, warning, info variants
   - Animation and positioning
   - Auto-dismiss behavior

6. **Loading States Design**
   - Skeleton loaders for app cards
   - Page loading indicators
   - Button loading states

7. **Error States Design**
   - 404, 500, network error pages
   - Form validation error styling
   - Empty state illustrations

### 🔧 **Technical Questions for Team Discussion**

#### Backend Integration
1. **API Endpoints & Authentication**
   - What are the exact API endpoints for user authentication?
   - How are JWT tokens managed and refreshed?
   - What's the API base URL and environment setup?
   - How are Microsoft OAuth tokens handled?

2. **Request Access API**
   - What's the endpoint for submitting access requests?
   - What data needs to be sent (user ID, app ID, reason)?
   - What response format should we expect?
   - How are request statuses tracked?

3. **App Data Management**
   - How is the list of available apps fetched?
   - What's the data structure for app information?
   - How are user permissions checked for each app?
   - Are there different app categories or types?

#### App Navigation & Integration
4. **Application Launch Flow**
   - When users click "Open App", what happens?
   - Do apps open in new tabs, iframes, or redirect?
   - How are apps integrated (separate domains, subdomains)?
   - Is there a unified app authentication system?

5. **User Management**
   - How are user accounts created by admins?
   - What user information is stored and displayed?
   - How are user permissions managed?
   - Is there a user role system beyond access/no-access?

#### Infrastructure & Deployment
6. **Environment Configuration**
   - What are the development, staging, and production environments?
   - How are environment variables managed?
   - What's the deployment strategy (Vercel, AWS, etc.)?
   - Are there any CDN or asset management requirements?

### 🎯 **Business Logic Questions**

#### Access Control
7. **Permission Management**
   - Are there different permission levels (read, write, admin)?
   - How granular are app permissions (feature-level access)?
   - Can users have temporary access or expiration dates?
   - Is there an approval workflow for access requests?

8. **Notification System**
   - What types of notifications will be shown?
   - How are notifications generated (system, admin, app-based)?
   - Should notifications be real-time or periodic?
   - How long should notifications be retained?

#### User Experience
9. **Personalization**
   - How dynamic is the home page greeting?
   - Should there be user preferences or settings?
   - Are there any user-specific recommendations?
   - How is user activity tracked?

10. **Content Management**
    - Who writes and manages app descriptions?
    - How are app icons and images managed?
    - Are there content approval workflows?
    - How is the app catalog updated?

### 📱 **Design System Questions**

#### Brand & Styling
11. **Official Brand Guidelines**
    - What are the exact brand colors and hex codes?
    - What fonts should be used (Google Fonts, custom fonts)?
    - What are the official spacing and sizing tokens?
    - Are there any brand-specific icons or imagery?

12. **Responsive Design**
    - What are the breakpoints for mobile, tablet, desktop?
    - How should the sidebar behave on mobile devices?
    - Should there be a mobile app or PWA version?
    - What's the minimum supported screen size?

13. **Accessibility Requirements**
    - What WCAG compliance level is required (AA, AAA)?
    - Are there specific accessibility testing requirements?
    - Should there be keyboard navigation support?
    - Are there any screen reader considerations?

### 🔄 **Development Process Questions**

#### Team Coordination
14. **Design Handoff Process**
    - How will designs be delivered (Figma, Zeplin, etc.)?
    - What's the design approval workflow?
    - How are design changes communicated?
    - Who are the design stakeholders?

15. **Development Timeline**
    - What's the target launch date?
    - Are there any critical milestones or deadlines?
    - What's the priority order for features?
    - Are there any dependencies on other teams?

#### Quality Assurance
16. **Testing Requirements**
    - What types of testing are required (unit, integration, e2e)?
    - Are there any specific testing tools or frameworks?
    - What's the browser and device support matrix?
    - Are there performance requirements or benchmarks?

### 📊 **Success Metrics & Analytics**

17. **Tracking & Analytics**
    - What user behavior should be tracked?
    - Are there any analytics tools to integrate?
    - What metrics define success for this platform?
    - How should user feedback be collected?

## 📝 Notes

- **Admin-controlled access** ensures security and proper user management
- **Phased state management** allows for quick start while maintaining scalability
- **Design system approach** ensures consistency and maintainability
- **Access control strategy** provides clear user experience for different permission levels
- **Design references** show a clean, modern aesthetic with strong purple branding
- **AI integration** appears to be a key differentiator in the user experience

This planning document serves as the foundation for implementation decisions and can be updated as requirements evolve. The design references provide valuable context for component specifications and user experience patterns.
