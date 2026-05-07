# Spring AI Demo with Google Gemini

A simple Spring Boot application that integrates Spring AI with Google Gemini to generate AI-powered responses.

---

# Project Overview

This project demonstrates:

- Spring Boot REST API
- Spring AI integration
- Google Gemini API usage
- Thymeleaf frontend UI
- Prompt-based AI text generation

---

# Architecture

```mermaid
graph TD

    subgraph Client["Browser"]
        UI["index.html (Thymeleaf UI)"]
    end

    subgraph Backend["Spring Boot Application"]
        HC["HomeController"]
        AC["AIController"]
        AS["AIService"]
    end

    subgraph Gemini["Google Gemini API"]
        GM["gemini-2.5-flash"]
    end

    UI -->|GET /| HC
    UI -->|Prompt Request| AC
    AC -->|generateText(prompt)| AS
    AS -->|Spring AI Request| GM
    GM -->|AI Response| AS
    AS --> AC
    AC --> UI
```

---

# Components

| Component | Description |
|---|---|
| `HomeController` | Loads the homepage |
| `AIController` | Handles API requests |
| `AIService` | Connects to Gemini using Spring AI |
| `Gemini API` | Generates AI responses |

---

# User Interface

The application runs at:

```text
http://localhost:8080
```

---

## Initial Screen

```text
 -------------------------------------------------------
| Spring AI Demo - Gemini                               |
|                                                       |
| Ask anything                                          |
| ---------------------------------------------------   |
| Explain Spring AI in simple terms...                 |
| ---------------------------------------------------   |
|                                                       |
| [ Ask Gemini ]                                        |
 -------------------------------------------------------
```

---

## Loading State

```text
 -------------------------------------------------------
| Spring AI Demo - Gemini                               |
|                                                       |
| What is Spring AI?                                    |
|                                                       |
| [ Ask Gemini ] (disabled)                             |
|                                                       |
| Thinking...                                           |
 -------------------------------------------------------
```

---

## Response State

```text
 -------------------------------------------------------
| Spring AI Demo - Gemini                               |
|                                                       |
| What is Spring AI?                                    |
|                                                       |
| Spring AI is a framework that simplifies integrating  |
| AI models into Spring applications.                   |
|                                                       |
 -------------------------------------------------------
```

---

# Step 1 — Create Gemini API Key

1. Open Google AI Studio:
   https://aistudio.google.com/app/apikey

2. Login with your Google account

3. Click **Create API Key**

4. Copy the generated key

---

# Step 2 — Configure API Key

Open:

```text
src/main/resources/application.properties
```

Add:

```properties
spring.application.name=spring-ai-demo

spring.ai.google.genai.api-key=YOUR_GEMINI_API_KEY

spring.ai.google.genai.chat.options.model=gemini-2.5-flash
```

---

# Recommended Secure Setup

Instead of hardcoding the API key:

```properties
spring.ai.google.genai.api-key=${GEMINI_API_KEY}
```

## Windows CMD

```cmd
set GEMINI_API_KEY=your_api_key
```

## PowerShell

```powershell
$env:GEMINI_API_KEY="your_api_key"
```

## Linux/macOS

```bash
export GEMINI_API_KEY=your_api_key
```

---

# Step 3 — Run the Project

```bash
mvn clean install
mvn spring-boot:run
```

Application starts at:

```text
http://localhost:8080
```

---

# Step 4 — Test the API

## Browser Test

```text
http://localhost:8080/api/ai/ask?prompt=Hello
```

---

## cURL Test

```bash
curl "http://localhost:8080/api/ai/ask?prompt=What+is+Spring+AI?"
```

---

# Request Flow

```text
User enters prompt
        ↓
Frontend sends request
        ↓
AIController receives request
        ↓
AIService calls Gemini API
        ↓
Gemini generates response
        ↓
Response displayed on UI
```

---

# Technologies Used

| Technology | Purpose |
|---|---|
| Java | Backend Language |
| Spring Boot | Application Framework |
| Spring AI | AI Integration |
| Thymeleaf | Frontend UI |
| Maven | Build Tool |
| Google Gemini | AI Model |

---

# Keyboard Shortcut

- `Ctrl + Enter` → Submit prompt (Windows/Linux)
- `Cmd + Enter` → Submit prompt (macOS)

---

# Future Improvements

- Chat history
- Streaming responses
- Markdown rendering
- Multiple AI model support
- Authentication
- Docker deployment

---

# Author

Developed using Spring Boot and Spring AI with Google Gemini integration.
