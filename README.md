# N8N Call Processing Workflow

An automated workflow that processes phone call data from ElevenLabs, extracts customer information using AI, and stores it in Google Sheets for easy tracking and follow-up.

## What It Does

This workflow automatically handles the entire lifecycle of call data processing:

- Receives callback webhooks from ElevenLabs after each phone call
- Extracts key information from call transcripts (name, email, order numbers, issues)
- Uses OpenAI GPT-4 to intelligently parse customer data and sentiment
- Stores structured data in Google Sheets for your team to access
- Sends email notifications for failed calls or important updates

## Key Features

**Smart Data Extraction**: The workflow uses both pattern matching and AI to accurately extract customer information, even from natural conversations in multiple languages.

**Sentiment Analysis**: Automatically detects whether customers are happy, neutral, or frustrated based on their language and tone.

**Call Metadata**: Captures important details like call duration, transfer status, timestamps, and termination reasons.

**Automatic Logging**: Every processed call gets logged to a Google Sheet with all relevant information organized and ready for review.

## Prerequisites

You'll need accounts and credentials for:

- N8N (self-hosted or cloud)
- ElevenLabs (for AI phone calls)
- OpenAI API (GPT-4 access)
- Google Sheets API
- Gmail API (for notifications)

## Setup

1. Import the `N8N_Workflow.json` file into your N8N instance
2. Configure the following credentials in N8N:
   - OpenAI API key
   - Google Sheets OAuth2
   - Gmail OAuth2
3. Update the webhook URL in your ElevenLabs agent settings
4. Set your target email addresses in the notification nodes
5. Activate the workflow

## How It Works

The workflow follows this process:

1. ElevenLabs sends a webhook when a call completes
2. Call status is checked - only "done" calls are processed
3. Customer data is extracted from the transcript
4. OpenAI analyzes the conversation for detailed information
5. Data is parsed and validated
6. A new row is added to Google Sheets
7. Email notifications are sent if needed

## Configuration

**Google Sheet Structure**: The workflow expects these columns:
- Name
- Email Address
- Phone Number
- Order Number
- Issue Type
- Summary
- Sentiment

**Email Notifications**: Currently configured to send failure notices to sa7979798@gmail.com and success summaries to info@altijd.nl. Update these in the Gmail nodes as needed.

## Supported Data Fields

The workflow can extract:
- Customer name and contact information
- Order or reference numbers
- Issue categorization (Order Status, Billing, Technical Support, etc.)
- Call sentiment (positive, neutral, negative)
- Whether the issue was resolved
- Full conversation transcript

## Notes

- The AI extraction works with multiple languages, including Dutch
- Failed or incomplete calls trigger separate email notifications
- All timestamps are converted to human-readable format
- The workflow maintains original call metadata for reference

## Troubleshooting

If calls aren't being processed:
- Verify the webhook URL is correct in ElevenLabs
- Check that all API credentials are valid
- Ensure the Google Sheet ID matches your target sheet
- Confirm the workflow is activated in N8N

## Future Enhancements

Consider adding:
- CRM integration for automatic ticket creation
- More detailed analytics and reporting
- Custom routing based on issue type or sentiment
- SMS notifications for urgent cases
