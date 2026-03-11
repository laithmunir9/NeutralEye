# NeutralEye — AI Media Bias Detection Chrome Extension

NeutralEye is an AI-powered Chrome extension that analyzes online news articles and highlights potential indicators of media bias.

The goal of the project is to help readers become more aware of bias patterns in news reporting while reading articles directly in their browser.

## Overview

NeutralEye analyzes article text and flags patterns that may suggest bias, including:

• loaded or emotionally charged language  
• imbalance in sources  
• demographic framing patterns  

The extension highlights these indicators directly within the browsing experience.

## Architecture

NeutralEye uses a separated frontend and backend architecture.

### Chrome Extension (Frontend)

The Chrome extension scans article text from the user's browser session and sends the content to a backend service for analysis.

### Backend Service

A FastAPI backend handles AI model requests and manages API communication.

Sensitive information such as API keys is stored securely on the backend rather than inside the browser extension.

### AI Processing

Article text is analyzed using large language model APIs.  
The system uses a consistent prompt structure to produce structured responses.

## Current Features

• Chrome extension that analyzes live news article text  
• AI-powered text analysis using large language models  
• detection of loaded language  
• detection of source imbalance  
• detection of demographic framing  
• structured response handling  
• logging and error handling for stability  

## Project Status

Current version includes:

• deployed Chrome extension  
• frontend/backend architecture separation  
• secure API key handling  
• logging and error handling  
• testing across 50+ UAE and international articles  

The extension is currently published on the Chrome Web Store.

## Additional Interface

A web interface is currently being developed that allows users to analyze articles outside the browser extension.

The website uses the same backend and AI prompt architecture as the extension.

## Technologies Used

### Programming
Python  
JavaScript  

### Web
HTML  
CSS  

### Backend
FastAPI  
REST API integration  

### AI / NLP
LLM API integration  
Prompt engineering  
Transformer-based NLP tools (Hugging Face)

### Development Tools
Git  
Render deployment  
Chrome Extensions API  

## Codebase

NeutralEye currently includes approximately **1,000+ lines of code** across frontend and backend components.

## Creator

Laith Munir  
High school student interested in artificial intelligence, machine learning, and technology.
