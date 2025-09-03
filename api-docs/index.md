# Draw.io App.js API Documentation

This document provides an organized index of all classes and their methods extracted from `app.js`, organized by module structure.

## Module Structure Overview

The app.js file contains multiple concatenated libraries organized into the following module structure:

### Third-Party Libraries


### mxGraph Library

- **[mxGraph Core - Data Structures & Utilities](mxgraph/core/index.md)** - 24 classes
- **[mxGraph Handlers - Interaction Logic](mxgraph/handlers/index.md)** - 13 classes
- **[mxGraph Layout - Graph Arrangement Algorithms](mxgraph/layout/index.md)** - 24 classes
- **[mxGraph Model - Graph Data & State](mxgraph/model/index.md)** - 28 classes
- **[mxGraph Shapes - Drawing Primitives](mxgraph/shapes/index.md)** - 20 classes
- **[mxGraph UI - User Interface Components](mxgraph/ui/index.md)** - 14 classes

### Draw.io Application

- **[Draw.io Files - File Management](application/files/index.md)** - 14 classes
- **[Draw.io Integrations - Cloud Services](application/integrations/index.md)** - 14 classes
- **[Draw.io UI - Application Interface](application/ui/index.md)** - 38 classes

## Quick Navigation

### Most Important Classes
- **[mxGraph](mxgraph/model/mxGraph.md)** - Main graph class (central to all operations)
- **[EditorUi](application/ui/EditorUi.md)** - Primary application UI controller
- **[Graph](application/ui/Graph.md)** - Enhanced graph implementation  
- **[Sidebar](application/ui/Sidebar.md)** - Shape palette and stencil management

### Key Architectural Components
- **Model Layer**: [mxgraph/model/](mxgraph/model/index.md) - Graph data structures
- **View Layer**: [mxgraph/ui/](mxgraph/ui/index.md) - Rendering and display
- **Controller Layer**: [mxgraph/handlers/](mxgraph/handlers/index.md) - User interactions
- **Application Layer**: [application/ui/](application/ui/index.md) - Draw.io specific UI

## Documentation Files

- **[modules.md](modules.md)** - Detailed module structure analysis
- **[functions.txt](functions.txt)** - All standalone functions (535 total)
- **[methods_sorted.txt](methods_sorted.txt)** - All methods sorted alphabetically

## Summary Statistics

- **Total Classes**: 189
- **Total Methods**: 4515
- **Total Functions**: 535
- **File Size**: 10.7MB (109,067 lines)
- **Module Distribution**:
  - Third-party libraries: 0 classes
  - mxGraph library: 123 classes
  - Draw.io application: 66 classes

---
*Generated from app.js using automated API extraction with modular organization*
