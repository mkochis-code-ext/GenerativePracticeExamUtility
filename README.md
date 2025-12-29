# 🤖 Generative Practice Exam Utility

A local, standalone web application for creating and taking practice exams with AI-generated questions. This utility allows you to generate custom exams on any topic using Azure OpenAI, take timed exams, review results, and track your progress over time.

## ⚠️ Important Disclaimers

- **LOCAL USE ONLY**: This application is designed for personal, local use
- **NO SECURITY FEATURES**: Does not include robust security measures for production environments
- **NO EXTERNAL LIBRARIES**: Built with vanilla HTML, CSS, and JavaScript only
- **USE AT YOUR OWN RISK**: This is a utility tool provided as-is

## 🌟 Main Features

### 1. AI-Powered Exam Generation
- **Two Generation Methods**:
  - **Direct Integration**: Connect to your deployed Azure OpenAI model to generate exams directly within the app
  - **Manual Copy/Paste**: Copy the prompt template and use it in a separate Copilot/Agent conversation, then paste the generated JSON back into the app
- **Azure OpenAI Integration**: Optional direct connection to your Azure OpenAI deployment for automated generation
- **Flexible Topics**: Generate exams on any subject matter
- **Customizable Question Count**: Specify the number of questions you want (default: 10)
- **Two Authentication Methods** (for direct integration):
  - API Key authentication
  - Azure Access Token authentication (via Azure CLI)
- **Persistent Settings**: Endpoint and deployment name are saved locally for convenience

### 2. Question Types
- **Single Choice Questions**: Traditional multiple-choice with one correct answer
- **Multiple Choice Questions**: Select all that apply (with visual hints showing the number of correct answers)
- **Randomized Options**: Answer choices are shuffled for each question to prevent pattern memorization

### 3. Exam Taking Experience
- **Randomized Questions**: Questions are shuffled when you start to ensure varied practice
- **Timed Exams**: Visual timer with color-coded warnings:
  - Normal (blue): More than 5 minutes remaining
  - Warning (orange): 5 minutes or less
  - Critical (red): 1 minute or less
- **Section Organization**: Questions organized by topic sections
- **Answer Validation**: Real-time feedback on correct/incorrect answers
- **Detailed Explanations**: View explanations for each answer after checking
- **Copilot Integration**: Quick link to learn more about each question via Microsoft Copilot

### 4. Results & Review
- **Score Display**: Clear percentage and fraction scores (e.g., 8/10, 80%)
- **Comprehensive Review**: Detailed review of all incorrect answers including:
  - Your selected answer(s)
  - The correct answer(s)
  - Explanation for the correct answer
- **Study Prompt Generator**: Automatically generates a study guide prompt based on topics you missed

### 5. Exam History Tracking
- **Local Storage**: Tracks your last 10 exams automatically
- **Performance Metrics**: View date, time, score, and percentage for each exam
- **Retake Functionality**: Easily retake any previous exam
- **JSON Management**:
  - View the full JSON structure of any saved exam
  - Download exam JSON for backup or sharing
  - Delete individual exams from history
- **Progress Tracking**: Monitor your improvement over time

## 📋 JSON Format

Exams are defined using a structured JSON format:

### Required Structure
```json
{
  "exam": {
    "id": "unique-exam-id",
    "title": "Exam Title",
    "durationMinutes": 45,
    "totalQuestions": 10,
    "sections": [
      {
        "id": "A",
        "title": "Section Name",
        "questions": [
          {
            "id": 1,
            "type": "single_choice",
            "prompt": "Your question text?",
            "choices": [
              { "id": "A", "text": "First option" },
              { "id": "B", "text": "Second option" },
              { "id": "C", "text": "Third option" },
              { "id": "D", "text": "Fourth option" }
            ],
            "answer": { "choiceId": "A" },
            "explanation": "Detailed explanation of the correct answer."
          }
        ]
      }
    ]
  }
}
```

### Answer Format Examples

**Single Choice Question:**
```json
"answer": { "choiceId": "A" }
```

**Multiple Choice Question:**
```json
"type": "multiple_choice",
"answer": { "choiceIds": ["A", "C"] }
```

### Template
A complete JSON template is provided in `TEMPLATE.json` for reference.

## 🚀 Getting Started

### Prerequisites
- Modern web browser (Chrome, Edge, Firefox, Safari)
- For AI generation: Azure OpenAI account with deployed model

### Setup
1. Clone or download this repository
2. Open `index.html` in your web browser
3. (Optional) Configure Azure OpenAI settings for AI generation

### Using the Application

#### Option 1: Generate Exam with AI
1. Click **⚙️ Azure OpenAI Model Settings** to expand settings
2. Enter your Azure OpenAI endpoint, deployment name, and API version
3. Choose authentication method (API Key or Access Token)
4. Enter your topic and desired number of questions
5. Click **Copy** to copy the prompt
6. Use the prompt with GitHub Copilot or paste it into your Azure OpenAI playground
7. Click **Paste** to paste the generated JSON
8. Click **Load & Start Exam**

#### Option 2: Manual JSON Entry
1. Prepare your exam JSON following the template structure
2. Paste the JSON into the text area
3. Click **Load & Start Exam**

#### Taking the Exam
1. Read each question carefully
2. Select your answer(s)
3. Click **Check Answer** to see if you're correct
4. Review the explanation
5. Click **Next Question** to continue
6. Monitor the timer in the top-right corner
7. Click **End Exam** at any time to finish

#### After Completion
1. View your score and percentage
2. Review all incorrect answers
3. Generate a study prompt for missed topics
4. Access your exam history
5. Retake exams to improve your score

## 📁 File Structure

```
ExamPrep/
├── index.html           # Main application file
├── styles.css           # All styling and animations
├── README.md            # This file
└── TEMPLATE.json    # JSON template for exam creation
```

## 🎨 Features in Detail

### Timer System
- Configurable duration per exam (default: 45 minutes)
- Visual countdown with MM:SS format
- Color-coded warnings as time runs low
- Auto-submit when timer reaches zero
- Persistent across questions

### Answer Checking
- Immediate visual feedback (green for correct, red for incorrect)
- Shows correct answers even if not selected
- Supports partial credit display for multiple-choice questions
- Explanations appear after checking

### History Management
- Stores up to 10 recent exams
- Each entry includes:
  - Exam title and date/time
  - Total questions and score
  - Percentage score
  - Full exam data for retaking
- Export capability to JSON
- Individual deletion or clear all

### Study Aid Integration
- Generates context-aware study prompts
- Focuses on missed topics
- Formatted for use with AI assistants
- One-click copy to clipboard

## 🔒 Privacy & Security

- **All data stored locally** in browser localStorage
- **No server communication** except for Azure OpenAI API calls (if used)
- **No tracking or analytics**
- **Credentials not persisted** - must be re-entered each session
- **User-controlled data** - clear history at any time

## 🛠️ Technical Details

- **No Dependencies**: Pure HTML, CSS, and JavaScript
- **Browser Storage**: localStorage for persistence
- **Modern APIs**: Uses Clipboard API, Fetch API
- **Responsive Design**: Works on desktop and tablet devices
- **No Build Process**: Open and run directly in browser

## ⚙️ Configuration

### Azure OpenAI Settings
- **Endpoint**: Your Azure OpenAI resource endpoint
- **Deployment Name**: Your model deployment name (e.g., gpt-4, gpt-35-turbo)
- **API Version**: Azure OpenAI API version (default: 2024-08-01-preview)
- **Authentication**: API Key or Azure Access Token

### Exam Settings
- **Duration**: Specified in JSON `durationMinutes` field
- **Question Count**: Flexible, specified when generating or in JSON
- **Sections**: Organize questions into named sections

## 🐛 Troubleshooting

**Q: The exam won't load from JSON**
- Verify your JSON syntax is valid
- Ensure the structure matches the template
- Check browser console for specific error messages

**Q: AI generation fails**
- Verify your Azure OpenAI credentials are correct
- Check that your endpoint URL is properly formatted
- Ensure your deployment name matches your Azure configuration
- For token auth, verify your token hasn't expired (tokens expire after ~1 hour)

**Q: Timer shows incorrect time**
- Check the `durationMinutes` field in your exam JSON
- Default is 45 minutes if not specified

**Q: History isn't saving**
- Ensure browser localStorage is enabled
- Check that you're not in private/incognito mode

## 📝 License

This project is provided as-is for personal use. Use at your own risk.

## 🤝 Contributing

This is a standalone utility project. Feel free to fork and modify for your own needs.

## 📧 Support

This tool is provided without official support. Use the template and examples as guides for creating your exam content.

---

**Remember**: This utility is designed for educational and practice purposes only. Always verify critical information from authoritative sources.
