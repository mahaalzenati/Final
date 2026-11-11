
# 🛡️ ScamSpotter | Digital Scam Detection Bot

[English](README.md) | [العربية](README.ar.md)

## 📌 Overview

**ScamSpotter** is an Arabic-language Telegram bot built using n8n to help users detect digital scam messages and assess suspicious links.

Users can send a text message, a link, or an image of a suspicious message. The bot analyzes the content and provides a risk classification along with practical guidance on how to handle it.

The project combines AI-powered text analysis, image text extraction, link checking using VirusTotal, and measures to mask sensitive information.

## ⚠️ Problem Statement

Digital scams are widespread and take many forms, including:

- Fake prizes and competitions.
- Phishing messages and suspicious links.
- Job offers that require upfront payments.
- Impersonation of banks and trusted institutions.

Users may find it difficult to evaluate these messages using simple tools that are readily available in their language.

## 💡 Proposed Solution

ScamSpotter provides a simple interface through Telegram, allowing users to submit suspicious content and receive a brief Arabic assessment explaining the risk level and recommended actions.

The bot does not classify messages as definitively safe. Instead, it distinguishes between clear risk indicators, signs of suspicion, and cases where there is insufficient information to provide a reliable assessment.

## 👥 Target Audience

- People who receive suspicious messages or links through Telegram or other platforms.
- Users who need help identifying phishing attempts and online scams.
- Individuals who want an initial assessment before interacting with suspicious content.

## 🧰 Technologies and Tools

- **n8n:** Builds the workflow and automates the analysis stages.
- **Telegram Bot API:** Receives user messages and sends analysis results.
- **OpenRouter:** Provides access to AI models for text analysis and image text extraction.
- **AI Agent:** Analyzes messages and coordinates the use of checking tools.
- **VirusTotal:** Checks links against known unsafe website data.
- **Code Node:** Masks sensitive information and extracts links.
- **Simple Memory:** Maintains conversation context to support continuous interaction.

## ⚙️ System Architecture

```text
User
  |
  v
Telegram Bot
  |
  v
Telegram Trigger
  |
  v
IF: Detect Message Type
  |
  +--------------------------+
  |                          |
  v                          v
Text Message               Image
  |                          |
  |                      Download Image
  |                          |
  |                      Vision Model
  |                      via OpenRouter
  |                          |
  +------------+-------------+
               |
               v
           Edit Fields
        Unify text into rawText
               |
               v
             Code
       Mask Sensitive Data
         and Extract Links
               |
               v
            AI Agent
               |
         +-----+-----+
         |           |
         v           v
    Text Analysis  Virus Total
         |           |
         +-----+-----+
               |
               v
       Merge Analysis Results
               |
               v
    Telegram Send Message
               |
               v
       Send Assessment to User
```

## 🔄 Workflow Explanation

### 1. 📩 Message Reception

The Telegram Trigger node receives messages sent by users to the bot.

### 2. 🔀 Message Type Detection

The IF node determines whether the submitted content is a text message or an image and routes it to the appropriate processing path.

### 3. 🖼️ Image Text Extraction

For image messages, the image is downloaded and sent to an image-capable model through OpenRouter to extract the text it contains before analysis.

### 4. 📝 Data Unification

The Edit Fields node combines the original text or the text extracted from the image into a single field named `rawText`.

### 5. 🔒 Privacy Protection and Link Extraction

The Code node masks sensitive information before sending the text to the AI Agent, including:

- Email addresses.
- Phone numbers.
- Bank card numbers.
- Verification codes.

It also extracts links found in the text for subsequent checking.

### 6. 🤖 Content Analysis and Link Checking

The AI Agent analyzes the message content using a model through OpenRouter. It uses the Google Safe Browsing tool to check link reputation and can use conversation memory when needed.

### 7. 📤 Sending the Result

The Telegram Send Message node sends a brief Arabic assessment containing the risk classification and appropriate user guidance.

## ✨ Key Features

### 🚦 Four-Level Risk Classification

The bot uses four classifications for its analysis results:

| Classification | Meaning |
|---|---|
| 🔴 Dangerous | Strong indicators of fraud are present, or the link has been identified as dangerous. |
| 🟠 Suspicious | There are warning signs that require caution, but insufficient evidence for a definitive conclusion. |
| 🟢 No Clear Risk Indicators Found | No clear risk indicators were detected in the content available for analysis. |
| ⚪ Insufficient Information | The submitted content does not contain enough information to provide an appropriate assessment. |

> **Note:** Not detecting risk indicators does not guarantee that a message is safe.

### 💬 Concise Arabic Responses

- Provides results in clear Modern Standard Arabic.
- Supports the analysis of messages written in Arabic and its dialects.
- Presents results and guidance in a brief and direct format.
- Avoids emojis and decorative formatting in its responses.

### 🔐 Sensitive Data Protection

- Masks sensitive information in the text before sending it to the AI Agent.
- Avoids reproducing private numbers and complete message URLs in responses.
- Reduces personal data exposure during the analysis stages.

### 🛡️ Protection Against Instruction Manipulation

The AI Agent's instructions are designed to treat the suspicious message text as **data to be analyzed, not instructions to be followed**. This helps reduce attempts to manipulate the model's instructions, commonly known as Prompt Injection.

### 🔗 Combining AI Analysis and Link Checking Results

The system combines message content analysis with link-checking results.

If Google Safe Browsing identifies a link as dangerous, the final classification becomes **Dangerous**, regardless of the initial assessment provided by the AI model.

## 🔏 Privacy and Security

The system design considers several privacy and security aspects:

- Masking sensitive information in the text before sending it to the AI Agent.
- Checking links using Google Safe Browsing.
- Instructing the model not to repeat sensitive information in its responses.
- Recognizing that image processing takes place before sensitive data masking, meaning the original image is sent to the vision model.
- Considering data processing and retention policies of external AI model providers.

Users are encouraged not to submit unnecessary personal information. Data masking reduces exposure, but it does not guarantee complete privacy.

## ⚠️ Known Limitations

- **Link Checking:** VirusTotal relies on known threat data, so it may not detect newly created malicious links or links that have not yet been reported.
- **Image Text Extraction:** The vision model may misread certain characters, especially when image quality is low or text is small. This may affect link extraction and subsequent analysis.
- **Image Privacy:** The original image reaches the vision model before sensitive information masking is applied.
- **Third-Party Data Processing:** Data retention and processing policies may vary between AI model providers.
- **Possibility of Errors:** The system may produce an incorrect assessment. Therefore, its result should not be treated as a guarantee that a message is fraudulent or safe.

## 🧪 Testing

### Tests

- Testing text message analysis.
- Testing the analysis of messages submitted as images.
- Testing link extraction and checking.
- Testing eight image-based message cases.
- Testing text cases containing fraudulent or suspicious messages.

## 🚀 Future Improvements

- Add support for receiving voice messages so users can describe suspicious messages using their voice.
- Prepare a test dataset containing 50 to 100 messages.
- Measure classification accuracy and error rates.
- Improve link extraction from images.
- Strengthen privacy controls and review data retention policies of service providers.
- Expand testing to cover Arabic dialects and different scam patterns.

## ✅ Conclusion

ScamSpotter demonstrates how AI and workflow automation can help Arabic-speaking users assess suspicious messages through Telegram.

By combining text analysis, image content extraction, link checking, and sensitive data masking, the project provides an accessible initial tool for digital scam awareness while accounting for the limitations of automated analysis and the possibility of errors.

[Project Workflow](./Json/X5LceqigjtCas8nc-ScamSpotter.json)
