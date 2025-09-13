# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

This is a React 19.1.1 application bootstrapped with Create React App (CRA) 5.0.1. The project follows standard CRA conventions and structure.

## Development Commands

### Core Development
- `npm start` - Start development server on http://localhost:3000
- `npm run build` - Create production build in `build/` folder  
- `npm test` - Run tests in interactive watch mode
- `npm run eject` - Eject from CRA (irreversible operation)

### Testing
- `npm test -- --coverage` - Run tests with coverage report
- `npm test -- --watchAll=false` - Run tests once without watch mode
- `npm test -- --testPathPattern=ComponentName` - Run specific test file

## Project Structure

```
├── public/          # Static assets (favicon, index.html, manifest)
├── src/
│   ├── App.js       # Main application component
│   ├── index.js     # Application entry point
│   ├── App.css      # Main application styles
│   ├── index.css    # Global styles
│   └── *.test.js    # Test files
└── build/           # Production build output (generated)
```

## Architecture & Patterns

### React Setup
- **React Version**: 19.1.1 with React DOM 19.1.1
- **Entry Point**: `src/index.js` renders `App` component into `#root` element
- **Strict Mode**: Enabled by default for development checks
- **Performance Monitoring**: Uses `reportWebVitals()` for Core Web Vitals tracking

### Testing Framework
- **Testing Library**: React Testing Library with Jest DOM matchers
- **Test Runner**: Jest (via react-scripts)
- **User Events**: @testing-library/user-event for interaction testing
- **Configuration**: ESLint extends `react-app` and `react-app/jest` configurations

### Build & Development Tools
- **Build Tool**: Webpack (via react-scripts)
- **Dev Server**: Webpack Dev Server with hot reloading
- **Browser Support**: Modern browsers (see `browserslist` in package.json)
- **Code Splitting**: Supported via React.lazy() and dynamic imports

## Development Notes

### Adding New Components
- Create components in `src/` directory
- Follow existing naming conventions (PascalCase for components)
- Include corresponding `.test.js` files for new components
- Import CSS modules or regular CSS files as needed

### Environment Variables
- Use `REACT_APP_` prefix for custom environment variables
- Variables are embedded at build time, not runtime
- Access via `process.env.REACT_APP_VARIABLE_NAME`

### Code Organization
- Keep components modular and focused on single responsibilities  
- Use functional components with hooks (React 19 patterns)
- Follow Create React App's recommended folder structure for scaling

### Browser Compatibility
- **Production**: >0.2% usage, not dead, not op_mini
- **Development**: Latest versions of Chrome, Firefox, Safari
- Polyfills included automatically by react-scripts

### Performance Considerations
- Code splitting available via React.lazy() and Suspense
- Static assets cached with hashed filenames in production
- Service worker registration available but not enabled by default
- Web Vitals reporting configured in `reportWebVitals.js`