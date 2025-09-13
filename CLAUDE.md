# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a React 19.1.1 application designed as a Zoom App (extension) hello world client. The project is bootstrapped with Create React App 5.0.1 and integrates with the Zoom Apps SDK. The application runs on `http://localhost:3001` instead of the default `3000` port.

## Development Commands

### Core Development
- `npm start` - Start development server on http://localhost:3001
- `npm run build` - Create production build in `build/` folder  
- `npm test` - Run tests in interactive watch mode
- `npm run eject` - Eject from CRA (irreversible operation, use with caution)

### Testing Commands
- `npm test -- --coverage` - Run tests with coverage report
- `npm test -- --watchAll=false` - Run tests once without watch mode
- `npm test -- --testPathPattern=ComponentName` - Run specific test file

## Architecture & Key Integration Points

### Zoom Apps SDK Integration
- **SDK Loading**: Zoom Apps SDK is loaded via CDN in `public/index.html:16`
- **SDK URL**: `https://appssdk.zoom.us/sdk.min.js`
- **Access**: Available globally as `window.ZoomApp` or similar after SDK loads
- **Port Configuration**: Application runs on port 3001 to align with Zoom Apps development requirements

### React Application Structure
- **Entry Point**: `src/index.js` renders App component with React.StrictMode enabled
- **Main Component**: `src/App.js` contains the main application logic
- **Styling**: Uses standard CSS files (`App.css`, `index.css`)
- **Performance**: Web Vitals tracking configured via `reportWebVitals()`

### Dependencies & Libraries
- **HTTP Client**: Axios 1.12.1 available for API calls
- **Testing**: React Testing Library with Jest DOM matchers
- **React Version**: 19.1.1 with concurrent features and modern patterns

## Development Notes

### Zoom App Development
- When developing Zoom Apps features, ensure SDK is loaded before using any Zoom APIs
- Test Zoom-specific functionality within the Zoom client environment
- Follow Zoom Apps SDK documentation for proper integration patterns

### Component Development
- Follow functional component patterns with React hooks
- Create corresponding `.test.js` files for new components
- Use existing CSS organization patterns (`App.css` for component styles)

### Environment & Configuration
- Custom port (3001) configured for Zoom Apps compatibility
- Standard Create React App build and development tooling
- ESLint configuration extends `react-app` and `react-app/jest`

### Browser Support
- **Production**: Modern browsers (>0.2% usage, not dead, not op_mini)
- **Development**: Latest Chrome, Firefox, Safari versions
- Polyfills handled automatically by react-scripts

## Deployment & Security

### DigitalOcean Apps Platform
- **Configuration**: Uses `.do/app.yaml` for deployment settings
- **Static Serving**: Uses `serve` package to serve built files
- **Port**: Deployment runs on port 8080

### Security Headers (Required for Zoom Apps)
Zoom Apps require specific OWASP security headers that are configured in `.do/app.yaml`:

- **Strict-Transport-Security**: `max-age=31536000; includeSubDomains`
- **X-Content-Type-Options**: `nosniff`
- **Content-Security-Policy**: Configured to allow Zoom SDK scripts and connections
- **Referrer-Policy**: `strict-origin-when-cross-origin`
- **X-Frame-Options**: `SAMEORIGIN`
- **X-XSS-Protection**: `1; mode=block`

### Content Security Policy Details
The CSP is specifically configured for Zoom Apps:
- `script-src`: Allows `'self'`, `'unsafe-inline'`, and `https://appssdk.zoom.us`
- `connect-src`: Allows connections to `'self'` and Zoom domains
- `frame-ancestors`: Allows embedding in Zoom clients

### Deployment Files
- **`.do/app.yaml`**: DigitalOcean Apps configuration with security headers
- **`static.json`**: Alternative static site configuration (if needed)
- **`serve` dependency**: Added to package.json for production serving