# API Documentation Scripts

This document describes the automated scripts used to extract and organize the draw.io API documentation from the massive `app.js` file.

## Overview

The draw.io application uses a single concatenated JavaScript file (`app.js`) containing 109,067 lines and 10.7MB of code. This includes multiple third-party libraries and the core mxGraph diagramming framework. These scripts automatically extract, organize, and format the API documentation into a navigable modular structure.

## Scripts

### 1. `bin/api-extraction.sh`

The main API extraction and organization script.

**Purpose:**
- Extracts all classes, methods, and functions from `app.js`
- Organizes classes into logical module directories
- Generates module index files with method counts
- Creates summary statistics

**Usage:**
```bash
./bin/api-extraction.sh
```

**What it does:**
1. **Creates Directory Structure:** Sets up 9 module directories:
   - `third-party/` - Third-party library modules
   - `mxgraph/core/` - Core data structures & utilities (24 classes)
   - `mxgraph/model/` - Graph data & state management (28 classes)
   - `mxgraph/shapes/` - Drawing primitives (20 classes)
   - `mxgraph/handlers/` - Interaction logic (13 classes)
   - `mxgraph/layout/` - Graph arrangement algorithms (24 classes)
   - `mxgraph/ui/` - User interface components (14 classes)
   - `application/ui/` - Draw.io interface (38 classes)
   - `application/files/` - File management (14 classes)
   - `application/integrations/` - Cloud services (14 classes)

2. **Extracts API Elements:**
   - Finds all classes using prototype pattern matching
   - Extracts method signatures with parameters
   - Identifies standalone functions
   - Filters out minified variable names (single letters)

3. **Organizes by Module:**
   - Uses intelligent classification logic based on class names and functionality
   - Places each class in the appropriate module directory
   - Creates individual `.md` files for each class

4. **Generates Module Indices:**
   - Creates `index.md` files for each module
   - Lists all classes with method counts
   - Provides module descriptions and statistics

**Output Files:**
- `methods.txt` - All extracted methods (4,515 total)
- `functions.txt` - All standalone functions (535 total)  
- `methods_sorted.txt` - Methods sorted alphabetically
- Individual class documentation files in module directories
- Module `index.md` files

### 2. `bin/generate-modular-index.sh`

Generates the main navigation index for the modular documentation structure.

**Purpose:**
- Creates the main `index.md` file
- Provides comprehensive navigation to all modules
- Highlights key architectural components
- Generates summary statistics

**Usage:**
```bash
./bin/generate-modular-index.sh
```

**What it creates:**
- **Module Structure Overview:** Links to all module indices with class counts
- **Quick Navigation:** Direct links to most important classes
- **Key Architectural Components:** Organized by software layers
- **Documentation Files:** Links to supporting files
- **Summary Statistics:** Total counts and module distribution

**Key Features:**
- Automatically calculates class and method counts
- Updates whenever module structure changes
- Provides multiple navigation pathways
- Highlights architectural relationships

### 3. `bin/update-api-format.sh`

Cleans up formatting issues in the generated documentation.

**Purpose:**
- Removes trailing `{` characters from method signatures
- Ensures consistent bullet point formatting
- Works across the entire modular directory structure

**Usage:**
```bash
./bin/update-api-format.sh
```

**What it fixes:**
- Converts `mxGraph.method() {` → `mxGraph.method()`
- Ensures proper markdown bullet point formatting
- Processes all `.md` files in module directories
- Excludes index and configuration files

## Module Classification Logic

The scripts use intelligent classification to organize classes:

### mxGraph Library Classes
- **Core:** Data structures, utilities, canvas classes (`mx*`)
- **Model:** Graph data, state management, change tracking
- **Shapes:** Drawing primitives and geometric shapes
- **Handlers:** User interaction and event handling
- **Layout:** Graph arrangement and positioning algorithms
- **UI:** User interface components and visual feedback

### Application Classes  
- **UI:** Draw.io-specific interface components
- **Files:** File format handling and storage
- **Integrations:** Cloud service connections and APIs

### Third-Party Libraries
- Currently empty but structured for:
  - spin.js, DOMPurify, CryptoJS, pako, rough.js

## Workflow

### Complete Documentation Generation
```bash
# 1. Extract and organize all API documentation
./bin/api-extraction.sh

# 2. Generate the main navigation index  
./bin/generate-modular-index.sh

# 3. Clean up any formatting issues
./bin/update-api-format.sh
```

### Updating Documentation
If the `app.js` file changes:
```bash
# Re-extract everything (will overwrite existing docs)
./bin/api-extraction.sh

# Regenerate the main index
./bin/generate-modular-index.sh

# Clean formatting
./bin/update-api-format.sh
```

## Technical Details

### Pattern Matching
The scripts use ripgrep (`rg`) for high-performance pattern matching:

```bash
# Extract prototype methods
rg "^[[:space:]]*([a-zA-Z_$][a-zA-Z0-9_$]*)\.prototype\.([a-zA-Z_$][a-zA-Z0-9_$]*)[[:space:]]*=[[:space:]]*function[[:space:]]*\(([^)]*)\)"

# Filter legitimate classes (not minified variables)
grep -E "^(mx|[A-Z][a-zA-Z]|Date)"
```

### Module Classification
Uses a comprehensive case statement matching:
- Naming patterns (mx*, specific prefixes)
- Functionality indicators (*Handler, *Layout, *Dialog)
- Architectural role (core utilities vs application features)

### File Organization
- **Hierarchical Structure:** Mirrors software architecture
- **Consistent Naming:** All files use `.md` extension
- **Index Files:** Each directory has navigational `index.md`
- **Cross-References:** Links maintain relative paths

## Statistics

**Current extraction results:**
- **Total Classes:** 189 real classes (filtered from 275+ total matches)
- **Total Methods:** 4,515 documented methods
- **Total Functions:** 535 standalone functions
- **Module Directories:** 9 organized categories
- **Documentation Files:** 200+ individual class files

**Largest Classes:**
1. Sidebar - 537 methods
2. mxGraph - 499 methods  
3. EditorUi - 487 methods
4. Graph - 277 methods

## Maintenance

### Adding New Modules
To add new module categories:
1. Update directory creation in `api-extraction.sh`
2. Extend the `get_module_dir()` function
3. Add module descriptions in `generate-modular-index.sh`

### Customizing Classification
Modify the case statements in `get_module_dir()` function to adjust which classes belong to which modules.

### Performance Notes
- Processing time: ~30 seconds for full extraction
- Uses ripgrep for optimal performance on large files
- Modular approach allows partial regeneration

---

*These scripts were developed to make the massive draw.io codebase navigable and understandable for developers working with the mxGraph diagramming library and draw.io application framework.*