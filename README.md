# 🎨 Frontend Documentation

This document provides comprehensive information about the phonebook frontend application, including component architecture, state management, and development guidelines.

## 🏗️ Architecture Overview

The frontend is built with React 19 and follows a modern component-based architecture:

```
frontend/src/
├── components/            # Reusable UI components
├── context/
│   └── AuthContext.jsx   # Authentication state management
├── pages/
│   ├── Login.jsx         # User login page
│   ├── Signup.jsx        # User registration page
│   └── Contacts.jsx      # Main contacts management page
├── api.jsx               # API service functions
├── App.jsx               # Main application component
├── main.jsx              # Application entry point
├── index.css             # Global styles and Tailwind CSS
└── App.css               # Component-specific styles
```

## 🚀 Quick Setup

### Prerequisites
- Node.js (v18 or higher)
- npm or yarn
- Backend server running on `http://localhost:3000`

### Installation

1. **Install Dependencies:**
   ```bash
   npm install
   ```

2. **Start Development Server:**
   ```bash
   npm run dev
   ```

3. **Access the Application:**
   Open your browser to `http://localhost:5173`

## 🎯 Key Features

### 🔐 Authentication System
- **User Registration:** Email and password signup
- **User Login:** Secure authentication with JWT
- **Protected Routes:** Automatic redirection based on auth status
- **Token Management:** Automatic token storage and retrieval

### 👥 Contact Management
- **Add Contacts:** Modal-based contact creation
- **Edit Contacts:** In-place editing with modal
- **Delete Contacts:** Confirmation-based deletion
- **Search Functionality:** Real-time contact filtering
- **Responsive Design:** Mobile-first approach

### 🎨 User Interface
- **Modern Design:** Beautiful gradient backgrounds
- **Smooth Animations:** CSS transitions and animations
- **Icon Integration:** Lucide React icons
- **Loading States:** Spinner animations
- **Error Handling:** User-friendly error messages

## 🧩 Component Architecture

### Core Components

#### Authentication Context (`context/AuthContext.jsx`)
Manages global authentication state and provides auth functions.

**Key Features:**
- User state management
- Login/signup/logout functions
- Token storage in localStorage
- Loading state management

**Usage:**
```javascript
import { useAuth } from '../context/AuthContext';

const { user, login, logout, loading } = useAuth();
```

#### API Service (`api.jsx`)
Centralized API communication layer.

**Features:**
- Axios instance with base configuration
- Automatic token injection
- Error handling
- Request/response interceptors

**Available Functions:**
```javascript
// Authentication
authAPI.signup(userData)
authAPI.login(userData)

// Contacts
contactsAPI.getContacts()
contactsAPI.addContact(contactData)
contactsAPI.updateContact(id, contactData)
contactsAPI.deleteContact(id)
```

### Page Components

#### Login Page (`pages/Login.jsx`)
User authentication interface.

**Features:**
- Email and password input fields
- Show/hide password functionality
- Form validation
- Error message display
- Loading states
- Navigation to signup

**Props:** None (uses context for auth)

#### Signup Page (`pages/Signup.jsx`)
User registration interface.

**Features:**
- Email, password, and confirm password fields
- Password strength validation
- Password confirmation matching
- Form validation
- Error handling
- Navigation to login

**Props:** None (uses context for auth)

#### Contacts Page (`pages/Contacts.jsx`)
Main contact management interface.

**Features:**
- Contact grid display
- Search functionality
- Add contact modal
- Edit contact modal
- Delete confirmation
- Loading states
- Empty state handling
- Responsive design

**State Management:**
```javascript
const [contacts, setContacts] = useState([]);
const [loading, setLoading] = useState(true);
const [searchTerm, setSearchTerm] = useState('');
const [showAddModal, setShowAddModal] = useState(false);
const [editingContact, setEditingContact] = useState(null);
const [formData, setFormData] = useState({ name: '', phone: '' });
const [error, setError] = useState('');
```

## 🎨 Styling System

### Tailwind CSS Integration
The application uses Tailwind CSS for utility-first styling.

**Configuration:**
```javascript
// tailwind.config.js
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          // ... more shades
        },
      },
      animation: {
        'fade-in': 'fadeIn 0.3s ease-out',
        'slide-up': 'slideUp 0.3s ease-out',
      },
    },
  },
}
```

### Design System

#### Color Palette
- **Primary Blue:** `#3b82f6` (blue-600)
- **Background:** Gradient from blue-50 to indigo-100
- **Text:** Gray scale (gray-900, gray-600, gray-400)
- **Success:** Green scale for positive actions
- **Error:** Red scale for errors and warnings

#### Typography
- **Font Family:** Inter (system fallbacks)
- **Headings:** Bold weights (font-bold)
- **Body Text:** Regular weights
- **Sizes:** Responsive text sizing

#### Spacing
- **Container:** max-w-6xl for main content
- **Padding:** Consistent spacing with Tailwind utilities
- **Margins:** Responsive margin system

## 🔄 State Management

### Authentication State
```javascript
// AuthContext state
{
  user: null | { id, email, token },
  loading: boolean,
  login: function,
  signup: function,
  logout: function
}
```

### Contact State
```javascript
// Contacts page state
{
  contacts: Contact[],
  loading: boolean,
  searchTerm: string,
  showAddModal: boolean,
  editingContact: Contact | null,
  formData: { name: string, phone: string },
  error: string
}
```

## 🛠️ Development

### Available Scripts
```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint .",
    "preview": "vite preview"
  }
}
```

### Development Workflow

1. **Start Development Server:**
   ```bash
   npm run dev
   ```

2. **Build for Production:**
   ```bash
   npm run build
   ```

3. **Preview Production Build:**
   ```bash
   npm run preview
   ```

4. **Lint Code:**
   ```bash
   npm run lint
   ```

### Environment Configuration
The frontend automatically connects to the backend API at `http://localhost:3000`.

To change the API URL, update the `API_BASE_URL` in `src/api.jsx`:
```javascript
const API_BASE_URL = 'http://localhost:3000/api';
```

## 🧪 Testing

### Component Testing
```bash
npm test
```

### Manual Testing Checklist

#### Authentication Flow
- [ ] User can register with valid email/password
- [ ] User can login with existing credentials
- [ ] Invalid credentials show error messages
- [ ] User is redirected to contacts after login
- [ ] User is redirected to login when accessing protected routes

#### Contact Management
- [ ] User can add new contacts
- [ ] User can edit existing contacts
- [ ] User can delete contacts with confirmation
- [ ] Search functionality filters contacts
- [ ] Empty state shows appropriate message

#### Responsive Design
- [ ] Application works on desktop
- [ ] Application works on tablet
- [ ] Application works on mobile
- [ ] Modals are properly sized on all devices

## 🚀 Deployment

### Build Process
1. **Create Production Build:**
   ```bash
   npm run build
   ```

2. **Deploy `dist` Folder:**
   - Upload to static hosting service
   - Configure for SPA routing

### Environment Variables
For production deployment, consider these environment variables:
```env
VITE_API_URL=https://your-api-domain.com/api
```

### Static Hosting
The application is a Single Page Application (SPA) and can be deployed to:
- **Netlify**
- **Vercel**
- **GitHub Pages**
- **AWS S3**
- **Firebase Hosting**

## 🔒 Security Considerations

### Frontend Security
- **Input Validation:** Client-side form validation
- **XSS Prevention:** React's built-in XSS protection
- **CSRF Protection:** Token-based authentication
- **Secure Storage:** localStorage for tokens (consider httpOnly cookies for production)

### Best Practices
- **Error Handling:** Graceful error display
- **Loading States:** User feedback during operations
- **Form Validation:** Real-time validation
- **Accessibility:** ARIA labels and keyboard navigation

## 🐛 Troubleshooting

### Common Issues

1. **API Connection Errors:**
   ```
   net::ERR_CONNECTION_REFUSED
   ```
   **Solution:** Ensure backend server is running on port 3000

2. **Authentication Errors:**
   ```
   401 Unauthorized
   ```
   **Solution:** Check token storage and API configuration

3. **Build Errors:**
   ```
   Module not found
   ```
   **Solution:** Run `npm install` and check import paths

4. **Styling Issues:**
   ```
   Tailwind classes not working
   ```
   **Solution:** Ensure Tailwind CSS is properly configured

### Debug Mode
```bash
# Enable React DevTools
npm install -g react-devtools

# Start with debug logging
DEBUG=* npm run dev
```

## 📱 Responsive Design

### Breakpoints
- **Mobile:** < 640px
- **Tablet:** 640px - 1024px
- **Desktop:** > 1024px

### Mobile-First Approach
- Base styles for mobile
- Responsive utilities for larger screens
- Touch-friendly interface elements

## 🎯 Performance Optimization

### Code Splitting
- Route-based code splitting with React Router
- Lazy loading for better initial load times

### Bundle Optimization
- Vite for fast development and optimized builds
- Tree shaking for unused code elimination
- Minification for production builds

### Image Optimization
- Optimized SVG icons from Lucide React
- Responsive images where applicable

## 🤝 Contributing

### Code Style
- **ESLint:** Pre-configured linting rules
- **Prettier:** Consistent code formatting
- **React Hooks:** Functional components with hooks

### Component Guidelines
1. **Functional Components:** Use hooks for state management
2. **Props Validation:** Use TypeScript or PropTypes
3. **Error Boundaries:** Implement error boundaries for production
4. **Accessibility:** Include ARIA labels and keyboard navigation

### Testing Guidelines
1. **Unit Tests:** Test individual components
2. **Integration Tests:** Test component interactions
3. **E2E Tests:** Test complete user flows

## 📚 Additional Resources

### Documentation
- [React Documentation](https://react.dev/)
- [Vite Documentation](https://vitejs.dev/)
- [Tailwind CSS Documentation](https://tailwindcss.com/)
- [React Router Documentation](https://reactrouter.com/)

### Tools
- [React DevTools](https://react.dev/learn/react-developer-tools)
- [Vite DevTools](https://vitejs.dev/guide/troubleshooting.html)
- [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

---

**For API documentation, see the backend README.**
