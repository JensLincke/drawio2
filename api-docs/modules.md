# Module Structure Analysis

This document outlines the modular organization of the draw.io application based on the concatenated `app.js` file.

## Library Modules (in order of appearance)

### 1. spin.js (Lines 1-202)
- **Purpose**: Loading spinner animations
- **Classes**: Spinner
- **Methods**: 15+ methods for creating and controlling spinners

### 2. DOMPurify (Lines 203-755)  
- **Purpose**: HTML sanitization to prevent XSS attacks
- **Main Object**: DOMPurify
- **Methods**: sanitize(), addHook(), etc.

### 3. CryptoJS (Lines 756-1454)
- **Purpose**: Cryptographic functions
- **Main Objects**: CryptoJS, MD5, AES encryption
- **Key Features**: Hashing, encryption, key derivation

### 4. pako (Lines 1455-2888)
- **Purpose**: Zlib compression/decompression
- **Main Objects**: pako.deflate, pako.inflate
- **Usage**: XML compression for diagram storage

### 5. rough.js (Lines 2889-4443)
- **Purpose**: Hand-drawn, sketchy-style graphics rendering  
- **Main Class**: rough
- **Features**: Rough drawing algorithms, sketch styles

### 6. Draw.io Configuration (Lines 4444-4998)
- **Purpose**: App-specific configuration and utilities
- **Objects**: urlParams, mxLanguageMap, DOM_PURIFY_CONFIG
- **Features**: Localization, URL parameters, security config

### 7. mxGraph Core Library (Lines 4999+)
- **Purpose**: Main diagramming and graph visualization library
- **Major Components**:
  - **mxClient & Utilities** (Lines 4999-5500)
  - **Core Data Structures** (Lines 5500-8500)
    - mxDictionary, mxPoint, mxRectangle, mxEventSource
  - **UI Components** (Lines 8500-12500)  
    - mxWindow, mxForm, mxToolbar, mxUndoableEdit
  - **Layout Algorithms** (Lines 12500-15000)
    - mxGraphLayout hierarchy
  - **Graph Model** (Lines 15000-18500)
    - mxGraphModel, mxGraphSelectionModel, mxGraphView
  - **Main Graph Class** (Lines 18500-22000)
    - mxGraph (499 methods)
  - **Interactive Handlers** (Lines 22000+)
    - mxGraphHandler, mxConnectionHandler, etc.

## Class Distribution by Module

### Third-Party Libraries
- **spin.js**: 1 class (Spinner)
- **DOMPurify**: 1 main object  
- **CryptoJS**: ~5 objects (CryptoJS, MD5, AES, etc.)
- **pako**: 2 main objects (deflate/inflate)
- **rough.js**: 1 main class + utilities

### mxGraph Library (189 classes total)
- **Core Classes**: mxGraph (499 methods), mxGraphModel (184 methods)
- **UI Classes**: EditorUi (341 methods), Sidebar (545 methods)  
- **Layout Classes**: ~15 layout algorithm implementations
- **Handler Classes**: ~25 interactive behavior classes
- **Utility Classes**: ~50 helper and support classes
- **Shape Classes**: ~30 shape and rendering classes

## Integration Patterns

1. **Library Wrapping**: Each third-party library is wrapped in an IIFE
2. **Namespace Management**: mxGraph uses consistent `mx` prefixing  
3. **Modular Loading**: Libraries loaded in dependency order
4. **Configuration**: Central configuration objects for customization
5. **Extension Points**: Plugin architecture for custom shapes and behaviors

This modular structure allows draw.io to combine powerful third-party libraries with its custom diagramming engine while maintaining clean separation of concerns.