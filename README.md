*Intuz — Your automation partner, one workflow at a time.*

<p align="center">
  <picture>
    <img alt="Banner Image" src="https://github.com/user-attachments/assets/210f97fc-0fce-404a-b647-7dfe1302cd37" />
  </picture>
</p>

[Intuz](https://www.intuz.com) helps organizations orchestrate AI, automation, and enterprise systems through scalable workflows. Our repository showcases proven implementations across healthcare, operations, customer support, document processing, sales, and back-office functions, enabling teams to accelerate automation initiatives without starting from scratch.

[N8N Creator](https://n8n.io/creators/intuz/) · [AI Automation Company](https://www.intuz.com/company/) · [AI Chatbot Development](https://www.intuz.com/ai-agents-for-business-automation/) · [For Custom Workflow Automation](https://www.intuz.com/get-started/)

# Summarize meeting transcripts with GPT-4o, Jira, Notion, Slack, and Sheets

## Quick overview

This workflow ingests meeting transcripts from a Fathom webhook or a Google Drive folder, uses OpenAI to extract structured notes, creates Jira issues for action items, writes a formatted meeting page to Notion, posts a recap to Slack, and schedules 24-hour-before-due Slack reminders via Google Sheets.

## How it works

1. Receives a meeting transcript via a Fathom POST webhook or triggers when a new transcript file is created in a watched Google Drive folder.
2. If the input is a Drive file, downloads it and extracts plain text (including DOCX conversion or PDF extraction) before normalizing the transcript, metadata, and destination settings.
3. Sends the transcript to OpenAI (GPT-4o) to extract a 3-bullet summary, decisions, action items, open questions, and risks in JSON, then parses and validates the structured output.
4. Loads a roster from Google Sheets to match action-item owners to Jira account IDs and Slack member IDs, and resolves relative due-date phrases into YYYY-MM-DD dates.
5. Creates one Jira issue per action item, merges the resulting issue keys back into the meeting record, and builds a Notion page payload containing the recap sections plus the full transcript.
6. Creates the meeting page in Notion and posts a formatted recap to the configured Slack channel, including Jira links/keys, owner mentions, due dates, and the Notion URL.
7. If any owners are unmatched, posts a Slack warning, and if reminders are enabled, appends reminder rows to a Google Sheets tab and an hourly schedule later sends due reminders to Slack and marks them as sent.

## Setup

1. Add credentials for OpenAI, Google Drive OAuth2, Google Sheets OAuth2, Jira Software Cloud, Notion, and Slack.
2. Choose a single transcript intake path by configuring either the Fathom webhook (with `include_transcript=true`) or the Google Drive folder trigger and its folder ID.
3. Update the Google Sheets document and ensure you have a roster sheet with `name`, `aliases`, `jira_account_id`, and `slack_member_id`, plus a reminders sheet with `task`, `owner`, `slack_member_id`, `channel`, `jira_key`, `due_date`, `reminder_datetime`, and `sent`.
4. Share your target Notion database with the Notion integration used by the workflow and set the correct database ID (and ensure it has at least `Title` and optionally `Date` properties).
5. Set the Jira project/issue type and confirm the Slack channel ID where recaps and reminders should be posted, and ensure the Slack app/bot has access to that channel.

## Requirements

- Credentials: OpenAI, Google Drive, Google Sheets, Jira, Notion, Slack
- Roster sheet columns: name, aliases, jira_account_id, slack_member_id
- Reminders sheet columns: task, owner, slack_member_id, channel, jira_key, due_date, reminder_datetime, sent
- Notion database shared with your integration (properties: Title, Date)
- Slack bot invited to the target channel

## FAQ

**What input sources does the workflow support for meeting transcripts?**  
It supports meeting transcripts from a Fathom webhook or a Google Drive folder.

**Which services does the workflow integrate with to manage meeting notes and action items?**  
It integrates with OpenAI (GPT-4o), Jira, Notion, Slack, and Google Sheets.

**How does the workflow handle reminders for action items?**  
It schedules 24-hour-before-due Slack reminders via Google Sheets and sends due reminders to Slack on an hourly schedule.

## Related n8n templates from Intuz

- [Scrape Y Combinator company and founder data with Apify and log it into Google Sheets — a ready prospecting list from any filtered YC search. Self-hosted n8n only.](https://github.com/Intuz-production/Y-Combinator-Startup-Scraper)
- [An n8n workflow that automates Jira support ticket follow-ups by sending acknowledgements and CSAT surveys via WhatsApp and Gmail, saving responses back to Jira, and optionally adding HubSpot CRM notes.](https://github.com/Intuz-production/Jira-Support-CSAT-Automation)
- [INTUZ introduces React Native IoT Device Onboarding Module component which helps you with the Onboarding of the IoT device using the WiFi network You can directly use this in your react native project by following the below steps](https://github.com/Intuz-production/React-Native-IoT-Device-Onboarding)

[See all of Intuz's free n8n templates](https://www.intuz.com/n8n-workflow-automation-templates/)

## Connect with us

Intuz is a USA-based AI & workflow automation company with 16+ years of experience building custom AI-enabled workflow automations for SMBs and Enterprises, specializing in agentic AI, LLM integrations, and CRM/ERP sync across Healthcare, FinTech, eCommerce, Manufacturing, and Real Estate.

* **Website:** [https://www.intuz.com](https://www.intuz.com)
* **Email:** [getstarted@intuz.com](mailto:getstarted@intuz.com)
* **LinkedIn:** https://www.linkedin.com/company/intuz/
* **Get Started:** https://n8n.partnerlinks.io/intuz

## For Custom Workflow Automation

[Click here - Get Started](https://www.intuz.com/get-started/)
