# Ecommerce Product Monitor

An automated web scraping solution for daily product monitoring across multiple ecommerce platforms.

## Overview

This project provides automated monitoring of product availability, pricing, and stock status across various ecommerce websites. It combines stealth web automation with AI-powered interaction capabilities to handle complex website structures and anti-bot measures.

## Features

- Automated login to ecommerce accounts
- Product search and data extraction
- Price and availability monitoring
- Anti-detection web scraping
- Automated report generation
- Integration with n8n workflows

## Technology Stack

- **nodriver** - Stealth browser automation (successor to undetected-chromedriver)
- **browser-use** - AI-powered browser automation with LLM integration
- **playwright** - Cross-browser automation framework
- **Python 3.11+** - Core runtime environment

## Installation

### Prerequisites
- Python 3.11 or higher
- Git

### Setup
1. Clone the repository with submodules:
```bash
git clone --recursive https://github.com/iamdanielsuresh/ecommerce-product-monitor.git
cd ecommerce-product-monitor
```

   **Note**: If you already cloned without `--recursive`, initialize submodules:
```bash
git submodule update --init --recursive
```

2. Create and activate virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
# Install the automation libraries in development mode
pip install -e ./nodriver
pip install -e ./browser-use

# Install playwright browsers for browser-use
playwright install
```

4. Configure environment variables:
```bash
cp .env.example .env
# Edit .env with your API keys and configuration
```

### Dependencies

This project uses two main automation libraries as git submodules:

- **[nodriver](https://github.com/ultrafunkamsterdam/nodriver)** - Undetected browser automation
- **[browser-use](https://github.com/browser-use/browser-use)** - AI-powered browser automation

These are included as submodules to ensure version compatibility and allow for local modifications if needed.

## Usage

### Basic Scraping with nodriver
```python
import sys
import os
sys.path.insert(0, './nodriver')
import nodriver as uc

async def scrape_product():
    browser = await uc.start()
    tab = await browser.get('https://example.com')
    # Scraping logic here
    browser.stop()
```

### AI-Powered Automation with browser-use
```python
from langchain_openai import ChatOpenAI
from browser_use import Agent

llm = ChatOpenAI(model='gpt-4o-mini')
agent = Agent(
    task='Search for product and extract price information', 
    llm=llm
)
await agent.run()
```

## Configuration

Create a `.env` file with the following variables:
```
OPENAI_API_KEY=your_openai_api_key
DATABASE_URL=sqlite:///products.db
LOG_LEVEL=INFO
```

## Project Structure

```
ecommerce-product-monitor/
├── browser-use/          # AI-powered automation library (submodule)
├── nodriver/             # Stealth browser automation library (submodule)
├── src/                  # Main application code
├── config/               # Configuration files
├── reports/              # Generated reports
├── logs/                 # Application logs
├── venv/                 # Virtual environment (not tracked)
├── .env                  # Environment variables (not tracked)
├── .env.example          # Environment template
├── .gitmodules           # Git submodules configuration
├── .gitignore           # Git ignore rules
└── README.md            # This file
```

### Submodules

This project includes two essential libraries as git submodules:

- **browser-use** ([repository](https://github.com/browser-use/browser-use)) - AI-powered browser automation
- **nodriver** ([repository](https://github.com/ultrafunkamsterdam/nodriver)) - Undetected browser automation

To update submodules to latest versions:
```bash
git submodule update --remote
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

