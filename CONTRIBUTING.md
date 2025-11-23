# Contributing to Link360

Thank you for your interest in contributing to Link360! This guide will help you understand the codebase structure and development workflow.

## 📁 Project Structure

```
Link360/
├── public/                      # Frontend assets and code
│   ├── css/                     # Stylesheets
│   │   └── styles.css          # Main application styles
│   ├── js/                      # JavaScript modules
│   │   ├── app.js              # Main application logic & navigation
│   │   ├── auth.js             # Firebase authentication handlers
│   │   ├── qr-generator.js     # QR code generation module
│   │   ├── firebase-config.js  # Firebase web SDK configuration
│   │   └── firebase-config.example.js  # Example config template
│   ├── assets/                  # Static assets
│   │   ├── images/             # Images (logo, favicon, thumbnails)
│   │   └── icons/              # Icon files
│   └── index.html              # Main HTML entry point
├── server.js                    # Express server & API endpoints
├── .env                         # Environment variables (not in git)
├── .env.example                 # Environment variables template
├── .gitignore                   # Git ignore rules
├── package.json                 # Dependencies & scripts
├── vercel.json                  # Vercel deployment config
└── README.md                    # Project documentation

```

## 🔧 Tech Stack

### Backend
- **Node.js** - JavaScript runtime
- **Express.js** - Web framework
- **Socket.IO** - Real-time communication
- **Firebase Admin SDK** - Backend Firebase operations
- **nanoid** - Short code generation

### Frontend
- **Vanilla JavaScript** - No framework dependencies
- **Firebase Web SDK** - Client authentication
- **QRCode.js** - QR code generation
- **Socket.IO Client** - Real-time updates

### Database
- **Firebase Firestore** - NoSQL cloud database
- **Firebase Authentication** - Google OAuth

## 📝 Code Organization

### `/public/js/app.js`
Main application logic including:
- Page navigation & routing
- Link creation & management
- Analytics dashboard
- Real-time updates via Socket.IO
- Search & filtering
- Bug reporting

**Key Functions:**
- `navigateToPage(page)` - Client-side routing
- `loadLinks()` - Fetch and display user links
- `loadAnalytics()` - Load analytics data
- `initializeAuth()` - Handle authentication state

### `/public/js/auth.js`
Authentication handlers:
- Google Sign-in
- Sign-out functionality
- Token management
- User session handling

### `/public/js/qr-generator.js`
QR code generation module:
- Pattern customization (15+ styles)
- Brand overlay
- Event frames
- Color picker
- Download functionality

**Main Object:**
```javascript
QRGenerator = {
    init()              // Initialize module
    generateQR()        // Generate QR code
    drawQRWithPattern() // Apply pattern styles
    downloadQR()        // Export QR code
    loadUserLinks()     // Load quick links
}
```

### `/server.js`
Backend API server:
- Express routes
- Firebase Admin operations
- Socket.IO event handling
- Link shortening logic
- Analytics tracking

**API Endpoints:**
- `POST /api/links` - Create short link
- `GET /api/links` - Get user links
- `GET /api/analytics/:shortCode` - Get analytics
- `GET /:shortCode` - Redirect & track click
- `POST /api/github/bug-report` - Create GitHub issue

### `/public/css/styles.css`
Application styles organized by:
1. CSS Variables & Theme
2. Reset & Base styles
3. Layout (Sidebar, Topbar, Grid)
4. Components (Cards, Buttons, Forms)
5. Pages (Home, Analytics, QR Generator)
6. Landing Page
7. Responsive breakpoints

## 🚀 Development Setup

### Prerequisites
- Node.js 16+
- Firebase project
- Git

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/xthxr/Link360.git
   cd Link360
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure Firebase**
   - Copy `js/firebase-config.example.js` to `js/firebase-config.js`
   - Add your Firebase web config
   - Copy `.env.example` to `.env`
   - Add Firebase Admin SDK credentials

4. **Run development server**
   ```bash
   npm start
   ```

5. **Access the app**
   ```
   http://localhost:3000
   ```

## 🔨 Making Changes

### Adding a New Feature

1. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes**
   - Follow existing code style
   - Add comments for complex logic
   - Keep functions small and focused

3. **Test your changes**
   - Test locally with `npm start`
   - Verify real-time features work
   - Check mobile responsiveness

4. **Commit your changes**
   ```bash
   git add .
   git commit -m "Add: your feature description"
   ```

5. **Push and create PR**
   ```bash
   git push origin feature/your-feature-name
   ```

### Code Style Guidelines

**JavaScript:**
- Use `const` for variables that don't change
- Use `let` for variables that change
- Avoid `var`
- Use arrow functions for callbacks
- Add JSDoc comments for complex functions
- Keep functions under 50 lines when possible

```javascript
/**
 * Generate a short code for URL
 * @param {number} length - Length of the code
 * @returns {string} Generated short code
 */
function generateShortCode(length = 7) {
    return nanoid(length);
}
```

**CSS:**
- Use CSS variables for colors and spacing
- Mobile-first approach
- BEM naming convention for clarity
- Group related styles together

```css
/* Component: Card */
.card {
    background: var(--card-bg);
    border-radius: var(--radius-md);
    padding: var(--space-md);
}

.card__header { }
.card__body { }
.card__footer { }
```

**HTML:**
- Semantic HTML5 elements
- Accessible markup (ARIA labels, alt text)
- Consistent indentation (4 spaces)

### File Naming Conventions

- **JavaScript**: `kebab-case.js` (e.g., `qr-generator.js`)
- **CSS**: `kebab-case.css` (e.g., `styles.css`)
- **Images**: `kebab-case.png` (e.g., `logo.png`)
- **Config**: `.env`, `vercel.json`

## 🧪 Testing

### Manual Testing Checklist

Before submitting a PR, test:

- [ ] Sign in with Google works
- [ ] Creating a link works
- [ ] Analytics update in real-time
- [ ] QR code generation works
- [ ] Download QR code works
- [ ] Mobile responsive design
- [ ] No console errors
- [ ] Links redirect correctly

### Browser Testing

Test in:
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Android)

## 📦 Adding Dependencies

Before adding a new npm package:

1. Check if existing libraries can solve the problem
2. Ensure it's actively maintained
3. Check bundle size impact
4. Update `package.json` with exact version

```bash
npm install package-name --save
```

## 🐛 Bug Fixes

1. **Identify the bug**
   - Reproduce the issue
   - Check browser console for errors
   - Note steps to reproduce

2. **Create an issue** (if not exists)
   - Clear title
   - Steps to reproduce
   - Expected vs actual behavior
   - Screenshots if applicable

3. **Fix and test**
   - Create a branch: `fix/bug-description`
   - Make minimal changes to fix the bug
   - Test thoroughly
   - Add comments explaining the fix

4. **Submit PR**
   - Reference the issue number
   - Explain what caused the bug
   - Explain how you fixed it

## 📚 Documentation

When adding features:

- Update README.md if it's user-facing
- Add JSDoc comments to functions
- Update CONTRIBUTING.md if it affects developers
- Add inline comments for complex logic

## 🎨 UI/UX Changes

For design changes:

- Follow existing design system
- Use CSS variables for colors
- Maintain accessibility (contrast, focus states)
- Test on mobile devices
- Include before/after screenshots in PR

## 🔐 Security

- Never commit `.env` files
- Don't expose API keys in client code
- Validate all user inputs
- Sanitize data before database operations
- Use Firebase security rules

## 📊 Performance

- Minimize bundle size
- Lazy load when possible
- Optimize images (compress, use appropriate formats)
- Use CDN for external libraries
- Debounce expensive operations

## 🤝 Pull Request Process

1. **Update documentation** if needed
2. **Ensure no console errors** in browser
3. **Test on mobile** devices
4. **Write clear PR description**:
   - What changed
   - Why it changed
   - How to test it
5. **Link related issues**
6. **Wait for review** - be responsive to feedback
7. **Squash commits** if requested

## ❓ Questions?

- Check existing [Issues](https://github.com/xthxr/Link360/issues)
- Ask in [Discussions](https://github.com/xthxr/Link360/discussions)
- Read the [README](README.md)

## 📄 License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

Thank you for contributing to Link360! 🙏
