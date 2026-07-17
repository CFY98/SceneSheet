# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/):

- `Added` for new features.
- `Changed` for changes in existing functionality.
- `Deprecated` for soon-to-be removed features.
- `Fixed` for any bug fixes.
- `Improved` for performance improvements.
  
## v0.1.2 - Database Implementation
### Added
- Implemented a robust database sytem for parsing and summarising scences, ensuring data integrity and long-term storage.
- Introduced background data cleanup policies to optimise storage efficiency.

### Changed
- Enhanced data integrity via a centraalised database connection to resolve concurrency issues, ensuring thread-safe operations during high-load processing.
- Optimised export pipelines by migrating in-memory processing to relational database queries.
- Shifted heavy parsing tasks to persistent storage, significantly reducing RAM usage during long-running operations. 

### Improved
- Decoupled job tracking from persistent storage layer, improving system responsiveness and stablity.

### Fixed 
- Resolved thread-contention erros in the database layer using advanced locking and timeout strategies to ensure 100% stability.

## v0.1.1 - Frontend UI/UX Integration
### Added
- Integrated desktop UI wrapper, enabling a native experience across Windows, MacOS, and Linux.
- Automated system profiling to detect and configure GPU-accelerated computing (CUDA, Metal, SYCL, Vulkan) on first-run.
- Implemented comprehensive RESTful endpoints for configuration and state management.
- Designed export engines for JSON and XLSX for interopability. 

### Changed
- Migrated core PDF extraction to a high performance, license-compliant engine, improving document parsing accuracy and order preservation.
- Refactored the core pipeline to discrete, class-based modules, significantly improving maintainability and testing.

### Improved
- Lazy-loading for heavyweight third-party dependencies, reducing initial application boot time to near-instantaneous.
- Leveraged advanced data modelling for network communications, minimising memory overhead.
- Added sophisiticated process management to handle job cancellations and completions gracefully, preventing "hanging" tasks.

## v0.1.0 - Core Engine & NLP Pipeline
### Added
- Built high-performance parsers for FDX, PDF, and Fountain script formats with low-memory streaming strategies.
- Implemented an NLP-driven entity extraction system to identify and track characters and props across complex document structures.
- Integrated automated model discovery and downloading via Hugging Face.
- Developed export engines for DOCX and PDF, enabling professional-grade report generation.
- 

### Improved
- Transitioned from DOM-based XML parsing to stream-based iteration `iterparse`, allowing the application to process large production scripts with minimal memory consumption.
