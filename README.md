# AI Appointment Scheduling Assistant

A sophisticated n8n workflow that creates an intelligent virtual assistant for managing consultation appointments. This system seamlessly integrates Google Calendar, Google Sheets, and Gmail to provide a complete appointment management solution.

## 🌟 Features

- **🤖 AI-Powered Chat Interface**: Natural language conversation for booking, rescheduling, and cancelling appointments
- **📅 Google Calendar Integration**: Automatic calendar event creation, updates, and deletions
- **📊 Google Sheets Logging**: Comprehensive tracking of all appointments and their status
- **📧 Email Notifications**: Automated confirmation, rescheduling, and cancellation emails
- **🕐 Natural Language Date/Time Parsing**: Understands phrases like "tomorrow at noon" or "next Friday at 2 PM"
- **📱 Multi-platform Support**: Works via chat interface accessible from any device

## 🏗️ System Architecture

```
Chat Trigger → AI Agent → Google Calendar + Google Sheets + Gmail
                ↓
        Google Gemini 2.5 Flash
              Memory Buffer
```

### Core Components

1. **Chat Trigger**: Webhook-based chat interface
2. **AI Agent**: Powered by Google Gemini 2.5 Flash with comprehensive system instructions
3. **Memory Management**: Buffer window memory for conversation context
4. **Tool Integration**: 8 specialized tools for calendar, sheets, and email operations

## 🛠️ Tools Available

| Tool Name | Purpose |
|-----------|---------|
| **New** | Create new Google Calendar events |
| **Update** | Reschedule existing calendar events |
| **Cancel** | Delete calendar events |
| **Fetch** | Retrieve user records from Google Sheets |
| **NewAppend** | Add new booking entries to Google Sheets |
| **SheetUpdate** | Update existing sheet rows |
| **Gmail** | Send appointment emails |
| **Date & Time** | Parse natural language date/time expressions |

## 📋 Workflow Operations

### 1. 📅 Booking a New Appointment

**Process Flow:**
1. Collect user details (Name, Phone, Email, Preferred Date/Time)
2. Parse and validate the requested time slot
3. Create Google Calendar event
4. Send confirmation email with calendar invite
5. Log booking details in Google Sheets

**Data Tracked:**
- Full name and contact information
- Appointment date and time
- Event ID for future reference
- Booking status (rescheduled/cancelled flags)

### 2. 🔄 Rescheduling Appointments

**Process Flow:**
1. Identify user by phone number
2. Fetch existing appointment details
3. Validate new time slot
4. Update Google Calendar event
5. Send rescheduling notification
6. Update tracking sheet

### 3. ❌ Cancelling Appointments

**Process Flow:**
1. Identify user by phone number
2. Retrieve event ID from records
3. Delete calendar event
4. Send cancellation email
5. Mark as cancelled in tracking sheet

## ⚙️ Configuration

### Business Hours
- **Days**: Monday to Friday only
- **Hours**: 11:00 AM – 2:00 PM (configurable timezone)
- **Duration**: 1-hour sessions

### Required Credentials
- **Google Gemini API**: For AI language model
- **Google Calendar OAuth2**: For calendar management
- **Google Sheets OAuth2**: For data tracking
- **Gmail OAuth2**: For email notifications

## 🔧 Setup Instructions

### Prerequisites
- n8n instance (cloud or self-hosted)
- Google Cloud Project with enabled APIs:
  - Gemini API
  - Google Calendar API
  - Google Sheets API
  - Gmail API

### 1. Import Workflow
1. Download `AI_Appointment_Scheduling.json`
2. In n8n, go to Workflows → Import from JSON
3. Upload the workflow file

### 2. Configure Credentials
Create the following credentials in n8n:

#### Google Gemini API
- Type: Google Gemini (PaLM) API
- Replace `YOUR_GEMINI_CREDENTIAL_ID` with your credential ID

#### Google Sheets OAuth2
- Type: Google Sheets OAuth2 API
- Replace `YOUR_GOOGLE_SHEETS_CREDENTIAL_ID` with your credential ID

#### Gmail OAuth2
- Type: Gmail OAuth2 API
- Configure for sending emails

### 3. Set Up Google Sheet
1. Create a new Google Sheet with the following columns:
   - `name`
   - `phone_no`
   - `email`
   - `appointment_date`
   - `appointment_time`
   - `rescheduled?`
   - `reschedule_date`
   - `reschedule_time`
   - `cancelled?`
   - `event_id`

2. Replace `YOUR_GOOGLE_SHEET_ID` in the workflow with your actual sheet ID

### 4. Configure Google Calendar
- Replace `your-calendar@example.com` with your Google Calendar email
- Ensure the calendar is accessible by your service account

### 5. Update Webhook IDs
- Replace `YOUR_WEBHOOK_ID` and `YOUR_GMAIL_WEBHOOK_ID` with actual webhook IDs
- Configure webhook URLs in your chat interface

### 6. Customize System Message (Optional)
Modify the AI agent's system message to:
- Change business hours
- Update company/service information
- Adjust conversation tone and style
- Add specific business rules

## 📱 Usage Examples

### Booking
**User**: "I'd like to book an appointment for tomorrow at 1 PM"
**Assistant**: "I'd be happy to help you book an appointment. Could you please provide:
- Your full name
- Phone number  
- Email address"

### Rescheduling
**User**: "I need to reschedule my appointment"
**Assistant**: "I can help you reschedule. What's your registered phone number?"

### Cancelling
**User**: "I want to cancel my appointment"
**Assistant**: "I can help you cancel. What's your registered phone number?"

## 🔒 Security & Privacy

- All sensitive credentials are stored securely in n8n credential store
- Phone numbers are used as unique identifiers for data privacy
- No personal data is exposed in the workflow configuration
- OAuth2 authentication ensures secure API access

## 🚀 Deployment Options

### Cloud Deployment
- n8n Cloud (recommended for quick setup)
- Google Cloud Run
- AWS ECS
- Azure Container Instances

### Self-Hosted
- Docker Compose
- Kubernetes
- PM2 with Node.js

## 🔄 Maintenance

### Regular Tasks
- Monitor webhook endpoints
- Check credential expiration
- Review appointment data in Google Sheets
- Update business hours as needed

### Monitoring
- Set up n8n workflow monitoring
- Configure error notifications
- Track API usage and limits

## 📊 Analytics & Insights

The Google Sheets integration provides valuable data for:
- Appointment booking patterns
- Rescheduling frequency
- Popular time slots
- Customer communication history

## 🛡️ Error Handling

The workflow includes robust error handling for:
- Invalid time slots
- Missing user information
- API failures
- Duplicate bookings

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

For issues and questions:
1. Check the n8n community forum
2. Review Google API documentation
3. Open an issue in this repository

## 🔮 Future Enhancements

- Multi-language support
- SMS notifications
- Video meeting integration
- Advanced analytics dashboard
- Mobile app interface
- AI-powered scheduling optimization

---

**Built with ❤️ using n8n, Google APIs, and Google Gemini AI**