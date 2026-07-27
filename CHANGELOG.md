# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/):

Types of changes:
- `Added` for new features.
- `Changed` for changes in existing functionality.
- `Deprecated` for soon-to-be removed features.
- `Removed` for now removed features.
- `Fixed` for any bug fixes.
- `Security` in case of vulnerabilities.

## v0.1.4 - Demo Preparation
### Added
- Change models directly via the CLI, with automatic fallback checks against the saved config settings.
- Standardised status cards across model management and downloads for clearer setup progress.
- Enhanced location parsing in scrip sluglines for better recognition of time-of-day indicators.

### Changed
- Caching and global state reuse for WordNet and location look-ups to speed-up repeated queries.
- Optimised model initialisation so LLMs load in the background smoothly before parsing and summarisations begins.
- Implemented file locking to prevent data corruption or conflicts in case of multiple app instances are opened simultaneously.
- Destination flag for output has been updated to better conform with CLI standards

### Removed
- Removed manual GPU prompting option to fully rely on the automatic process.

## v0.1.3 - Setup Wizard Implementation
### Added
- Streamlined first-time application setup via an interactive setup wizard.
- New menu option to download supported Hugging Face LLMs.
- Immediate UI validation to choose export format selector during first run setup.

### Changed
- GPU and CPU hardware detection is now completely automatic, removing setup friction for less tech-savvy users.
- Unified house styles and layout rules across setup and configuration screens.

### Fixed
- Synchronised initial setup states between the desktop app and local server setup
  
## v0.1.2 - Database Implementation
### Added
- Implemented a robust database system for parsing and summarising scenes, ensuring data integrity and long-term storage.
- Introduced background data cleanup policies to optimise storage efficiency.

### Changed
- Enhanced data integrity via a centralised database connection to resolve concurrency issues, ensuring thread-safe operations during high-load processing.
- Optimised export pipelines by migrating in-memory processing to relational database queries.
- Shifted heavy parsing tasks to persistent storage, significantly reducing RAM usage during long-running operations. 
- Decoupled job tracking from persistent storage layer, improving system responsiveness and stability.

### Fixed 
- Resolved thread-contention errors in the database layer using advanced locking and timeout strategies to ensure 100% stability.

## v0.1.1 - Frontend UI/UX Integration
### Added
- Integrated desktop UI wrapper, enabling a native experience across Windows, MacOS, and Linux.
- Automated system profiling to detect and configure GPU-accelerated computing (CUDA, Metal, SYCL, Vulkan) on first-run.
- Implemented comprehensive RESTful endpoints for configuration and state management.
- Designed export engines for JSON and XLSX for interoperability. 

### Changed
- Migrated core PDF extraction to a high performance, license-compliant engine, improving document parsing accuracy and order preservation.
- Refactored the core pipeline to discrete, class-based modules, significantly improving maintainability and testing.
- Lazy-loading for heavyweight third-party dependencies, reducing initial application boot time to near-instantaneous.
- Leveraged advanced data modelling for network communications, minimising memory overhead.
- Added sophisiticated process management to handle job cancellations and completions gracefully, preventing "hanging" tasks.

## v0.1.0 - Core Engine & NLP Pipeline
### Added
- Built high-performance parsers for FDX, PDF, and Fountain script formats with low-memory streaming strategies.
- Implemented an NLP-driven entity extraction system to identify and track characters and props across complex document structures.
- Integrated automated model discovery and downloading via Hugging Face.
- Developed export engines for DOCX and PDF, enabling professional-grade report generation.
  
### Changed
- Transitioned from DOM-based XML parsing to stream-based iteration, allowing the application to process large production scripts with minimal memory consumption.
