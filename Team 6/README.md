# LinkedIn Automation System for Atolls GmbH

## Team Members
- Barbara 
- Aicha
- Li Jingyan
- Phatjira
- Samira

**Technical Consultant:** Youssef Elserougi

**Client:** Atolls GmbH (Maria Wurzer, Sarah Belaid, Karla Maryed Blanco Rodríguez)

---

## Project Overview

An AI-powered LinkedIn content automation system that generates, approves, and publishes three types of content:
- **Recruitment posts** - Job openings and employer branding
- **Product showcase** - Company services and solutions
- **Employee engagement** - Team culture and achievements

The system uses a multi-agent AI architecture with Slack-based approval workflows, ensuring no content publishes without human review.

---

## Architecture

### Two-Workflow System

#### **Workflow 1: AI Content Generation & Coordination**
- **Triggers:** Slack mentions and webhook callbacks
- **Functions:**
  - Content generation via AI agents
  - Content categorization (recruitment/showcase/engagement)
  - Image generation (Gemini AI)
  - Image hosting (Cloudinary)
  - Sequential approval coordination
- **Nodes:** 28 nodes

#### **Workflow 2: Slack Approval System**
- **Trigger:** Slack button interactions
- **Functions:**
  - Switch-based routing (6 action types)
  - Actions: approve_post, reject_post, regenerate_post, approve_image, reject_image, regenerate_image
  - LinkedIn publication
  - Callback webhook management
- **Nodes:** 12 nodes

---

## Key Features

### Two-Stage Approval Process
1. **Text Content Approval** → Triggers image generation
2. **Image Approval** → Enables LinkedIn publication

### Interactive Slack Interface
- Formatted messages with Block Kit
- Action buttons for each approval stage
- Real-time status updates
- Thread-based editing capability

### AI-Powered Content
- Multi-agent architecture for content generation
- Brand voice preservation via "emotional assets" analysis
- Content-type-specific KPIs tracking

---

## Technical Stack

- **Automation Platform:** n8n (Docker)
- **Communication:** Slack API + Block Kit
- **AI Services:** Gemini AI (image generation)
- **Media Management:** Cloudinary (hosting), CloudConvert (processing)
- **Publishing:** LinkedIn API (Share on LinkedIn)
- **Infrastructure:** ngrok (webhook tunneling)

---

## Setup Requirements

### Prerequisites
1. n8n instance (Docker recommended)
2. ngrok account for webhook tunneling
3. Slack workspace with app configuration
4. LinkedIn API access (Share on LinkedIn)
5. Gemini AI API key
6. Cloudinary account

### Credentials Needed (Not Included)
The workflow JSON files have been cleaned of all sensitive data. You will need to configure:

- **Slack:**
  - Bot User OAuth Token
  - Signing Secret
  - Webhook URLs
  - Interactive Components endpoint

- **LinkedIn:**
  - OAuth Client ID
  - OAuth Client Secret
  - Redirect URIs

- **Gemini AI:**
  - API Key

- **Cloudinary:**
  - Cloud Name
  - API Key
  - API Secret

- **n8n:**
  - Webhook URLs (via ngrok)
  - Environment variables for webhook functionality

---

## Workflow Files

- `workflow_1_CLEAN.json` - AI Content Generation & Coordination (28 nodes)
- `workflow_2_CLEAN.json` - Slack Approval System (12 nodes)

**Note:** All sensitive information (API keys, tokens, webhook URLs, credentials) has been removed from these files for security. You will need to reconfigure these values when importing into your n8n instance.

---

## Implementation Notes

### Slack Configuration
- Webhook URLs must use ngrok public domains
- Interactive Components and Event Subscriptions require the same ngrok URL
- URL changes require app reinstallation
- Thread-based editing used for post modifications (due to Slack trigger_id limitations)

### LinkedIn API Limitations
- **Current Access:** "Share on LinkedIn" for personal accounts
- **Required for Production:** Community Management API (restricted to registered businesses)
- **Workaround:** Atolls must apply directly for enterprise API access

### Data Flow
1. User mentions Slack bot with content request
2. Workflow 1 generates content via AI agents
3. Content sent to Slack with approval buttons
4. User approves/rejects/regenerates text
5. Upon text approval, image generation triggered
6. User approves/rejects/regenerates image
7. Upon image approval, content published to LinkedIn
8. Callbacks handled via webhook communication between workflows

---

## Known Limitations

1. **LinkedIn API Access:** Community Management API for demographic analytics unavailable to student accounts
2. **Demonstration Mode:** Currently uses personal LinkedIn accounts due to API restrictions
3. **Edit Functionality:** Uses thread-based editing rather than modal interfaces
4. **Webhook Dependencies:** Requires ngrok tunneling, which may disconnect

---

## Future Enhancements

- Airtable integration for project tracking and historical records
- LinkedIn Company Page access via Atolls enterprise API application
- Enhanced edit functionality with Slack modals
- Production deployment with stable webhook endpoints
- Comprehensive analytics dashboard

---

## Academic Context

This project serves dual purposes:
1. **Functional Delivery:** Working automation system for Atolls GmbH
2. **Academic Requirements:** Weekly design logs and course presentations at Hochschule München (MUC.DAI Department)

**Course:** Projektmodul Web  
**Institution:** Hochschule München  
**Semester:** Winter 2024/2025

---

## Contact

For questions about this project:
- **Course Instructor:** youssef.elserougi@hm.edu
- **Team Lead:** Barbara (Integration & Quality)

---

## License

This project was developed as part of an academic course at Hochschule München in collaboration with Atolls GmbH.

---

## Acknowledgments

Special thanks to:
- Youssef Elserougi for n8n expertise and technical guidance
- Atolls GmbH team for project opportunity and collaboration
- Hochschule München MUC.DAI Department for academic support
