# IIT MADRAS TDS PROBLEM SOLVER 

## System Architecture & Technology Stack

### Core Components
- **Backend Architecture**: Python-based with FastAPI framework
- **Frontend**: Responsive single-page application using HTML5, CSS3, and vanilla JavaScript
- **Integration Layer**: Webhook support for Discord, Slack, and Telegram notifications
- **Data Processing**: Python core libraries with specialized modules for file handling
- **Question Processing Engine**: Pattern matching algorithm with specialized solvers

## Core Files
- **vicky_app.py**: Web server, API endpoints, HTML rendering, and system management
- **vicky_server.py**: Question analysis, pattern matching, and solution generation

## Technical Implementation Details

### Communication Infrastructure
#### 1. Webhook Integration System
The Webhook use here to send notification whenever someone hit [app.algaoch.tech/api](https://app.algsoch.tech/api)
- **Discord**: Rich message formatting with embedded content
- **Slack**: Interactive messages through incoming webhooks

### Pattern Matching Engine
The engine uses regex patterns for:
- **Contextual Understanding**: Detecting specific question types
- **Command Recognition**: Identifying code commands and parameters
- **Assignment Classification**: Routing questions to GA1-GA5 solvers
- **File Association**: Linking relevant uploaded files

### File Management System
- **Generates Unique IDs**: 8-character identifiers for each file
- **Stores Metadata**: Tracks filenames, timestamps, and file types
- **Provides Contextual Access**: Allows referencing files by ID
- **Type-Specific Handling**: Different processing for ZIP archives vs. README files

### Base64 Image Decoder/Encoder
- **Client-side implementation** for security and performance
- **Intelligent Format Detection** for automatic prefix correction
- **Robust Error Handling** for malformed Base64 data
- **Clipboard Integration** for direct image pasting

### HTML Viewer with CORS Proxy
- **Bypass CORS Restrictions** via third-party proxy
- **Render Live Content** in sandboxed iframe
- **Provide Source Viewing** for analysis
- **Enable HTML Copying** for modification

### API Layer & Documentation
- **Multiple Response Formats**: JSON and HTML output
- **File Upload Support**: Process questions with attached files
- **Notification Integration**: Webhook notifications for API calls
- **Security Features**: IP logging, optional rate limiting

### Authentication and Security
- **IP Logging**: Tracks API and UI interactions
- **Admin Endpoints**: Secure access to logs and analytics
- **Environment Variables**: Sensitive values stored securely
- **XSS Protection**: HTML escaping for user-generated content
- **Input Validation**: Thorough validation of user inputs

## User Interface Components

### 1. Chat Interface
- **Message History**: Displays assistant conversation
- **Code Formatting**: Syntax highlighting
- **File Uploads**: Drag-and-drop and button-based
- **Copy Functionality**: One-click copying of code blocks

### 2. Question Categories & Navigation
- **Tab-Based Navigation** for easy category switching
- **Dynamic Content Loading** based on selection
- **Active State Tracking** for visual feedback

### 3. File Management UI
- **File Listing**: Shows all uploaded files with metadata
- **File Actions**: Use or delete files
- **Upload Interface**: Simple form-based upload

## Integration Architecture

### 1. Server-Client Communication
- **RESTful API Pattern** with:
  - Form Data: `multipart/form-data` for file uploads
  - JSON Responses: Structured data
  - HTML Responses: Rendered content
- **Status Updates** for real-time monitoring

### 2. External Service Integration
- **Discord**: Webhook notifications
- **Telegram**: Bot API alerts
- **Slack**: Incoming webhook events
- **CORS Proxy**: Third-party service for HTML viewing
- **Local File System**: Persistent storage for uploads

## Data Flow Architecture
1. **User Input**: Question text + optional file upload
2. **Pattern Analysis**: Classification of intent
3. **Solver Selection**: Routing to correct solver function
4. **Response Generation**: Formatted answer creation
5. **Data Enrichment**: Code blocks and structured formatting
6. **Client Delivery**: Rendering in chat interface

## Administrative Features
- **Usage Analytics**: Feature usage statistics
- **IP Logs**: System access records
- **API Statistics**: Endpoint usage data
- **Tool Usage Tracking**: Popularity insights
- **Error Monitoring**: Centralized logging

## Conclusion
The **Vicky Data Science Assistant Platform** is a multi-layered system integrating modern web technologies with an advanced Python backend. The **modular architecture** ensures scalability and easy maintenance, while the **comprehensive API** enables external integrations. Its emphasis on **user experience** and **powerful data processing** makes it a robust tool for data science education and assistance.

---

# vicky_server.py Documentation

## Overview
**vicky_server.py** is the core component of the **Vicky Data Science Assistant Platform**, responsible for question processing, pattern matching, and executing specialized solution functions for assignments GA1-GA5.

### Module Structure
- **GA1 Solutions**: Data processing and file handling
- **GA2 Solutions**: API integration, Docker, FastAPI, and deployment
- **GA3 Solutions**: Network requests, text processing, data manipulation
- **GA4 Solutions**: Web scraping, data extraction, automation
- **GA5 Solutions**: Advanced data analysis and cleaning operations

Each function follows a **consistent structure**, with docstrings documenting parameters, return values, and purpose.

## Sample Implementations

### GA2: Image Compression
```python
def ga2_second_solution(query=None):
    """Compresses an image losslessly to be under 1,500 bytes."""
    import os
    from PIL import Image
    
    default_image_path = "E:\\data science tool\\GA2\\iit_madras.png"
    image_path = file_manager.get_file(default_image_path, query, "image")
    max_bytes = 1500
    
    def compress_image(img, output_path):
        for compression in range(9, -1, -1):
            img.save(output_path, format="PNG", optimize=True, compress_level=compression)
            if os.path.getsize(output_path) <= max_bytes:
                return True
        return False
    
    with Image.open(image_path) as img:
        compressed_path = "compressed_output.png"
        success = compress_image(img, compressed_path)
    
    return compressed_path if success else "Compression failed"
```

### GA4: IMDb Web Scraper
```python
def ga4_second_solution(query=None):
    """Extracts movie data from IMDb within a specified rating range."""
    from selenium import webdriver
    from selenium.webdriver.chrome.options import Options
    
    min_rating, max_rating = 5.0, 7.0
    if query:
        # Extract custom rating range if provided
        import re
        pattern = r'ratings?\s+(\d+\.\d*)\s*-\s*(\d+\.\d*)'
        match = re.search(pattern, query)
        if match:
            min_rating, max_rating = float(match.group(1)), float(match.group(2))
    
    options = Options()
    options.add_argument("--headless")
    driver = webdriver.Chrome(options=options)
    driver.get("https://www.imdb.com/chart/top")
    # Scrape and return movies within rating range
```

## Usage Examples
```python
from vicky_server import ga4_second_solution
result = ga4_second_solution("Find movies rated 6-8 on IMDb")
print(result)
```

## Conclusion
The **vicky_server.py** module powers the Vicky Data Science Assistant by executing solutions dynamically based on query patterns. With extensive **pattern recognition** and **specialized solvers**, it provides an efficient and scalable approach to answering data science queries.

