# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a fork of the draw.io diagramming application repository - a web-based diagramming tool with both client-side JavaScript and server-side Java components. The project follows a hybrid architecture with:

- **Frontend**: JavaScript-based web application located in `src/main/webapp/`
- **Backend**: Java servlets for authentication, proxy, and integration services in `src/main/java/`
- **Build System**: Apache Ant with JavaScript minification via Google Closure Compiler

## Fork-Specific Changes

**Important**: This fork has deminified the main application JavaScript:
- `src/main/webapp/js/app.min.js` (original minified ~8.8MB)
- `src/main/webapp/js/app.js` (deminified readable version ~10.7MB, 109k lines)
- The application now uses the readable `app.js` instead of `app.min.js`

## Architecture

### Key Directories
- `src/main/webapp/`: Web application root containing HTML, JavaScript, CSS, and assets
- `src/main/java/com/mxgraph/online/`: Java servlets for various integrations (GitHub, Google Drive, Dropbox, etc.)
- `etc/build/`: Build configuration and Ant build scripts
- `src/main/webapp/js/`: JavaScript modules including core application (`app.js`), extensions, and third-party libraries

### Core Components
- Main application entry point: `src/main/webapp/index.html`
- Core JavaScript: `src/main/webapp/js/app.js` (deminified, editable)
- Authentication servlets for various cloud providers (Google, GitHub, Dropbox, etc.)
- Export and proxy servlets for handling external integrations

## Build Commands

The project uses Apache Ant for building:

```bash
# Build the complete application (from etc/build/)
ant all

# Build just the application components
ant app

# Create production WAR file
ant war

# Clean build artifacts
ant clean

# Compile Java servlets only
ant javac
```

**Note**: Build commands must be run from the `etc/build/` directory.

## Development Workflow

### JavaScript Development
- **Primary development file**: `src/main/webapp/js/app.js` (109k lines, fully readable)
- Other JavaScript files may still be minified (`extensions.min.js`, etc.)
- The build system concatenates and processes JavaScript using Google Closure Compiler
- Make changes directly to `app.js` for core application logic

### Java Servlet Development
- Servlets are in `src/main/java/com/mxgraph/online/`
- Common patterns: authentication (`*Auth.java`), servlets (`*Servlet.java`)
- Dependencies are managed via JAR files in `src/main/webapp/WEB-INF/lib/`

### Configuration
- Web.xml servlet mappings in `src/main/webapp/WEB-INF/web.xml`
- Client configuration includes OAuth app IDs and API endpoints
- Build properties in `etc/build/build.properties`
- Custom authentication endpoint: `https://lively-kernel.org/lively4-auth/`

## Important Notes

- This fork has made the core JavaScript readable and editable via deminification
- Authentication integration points to `https://lively-kernel.org/lively4-auth/` (customized)
- The application is designed to be deployed as a standalone web application or WAR file
- Original draw.io repository does not accept external PRs, but this is a fork for development

## Testing

No automated test framework is present in this repository. Testing is typically done manually through the web interface.