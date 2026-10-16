# Automated PDF Invoice Parsing Pipeline (n8n & Google Sheets)

An event-driven automation pipeline built in **n8n** that monitors a Google Drive folder for incoming PDF invoices, extracts raw binary text, parses key transactional fields using custom JavaScript regex, and logs the structured data directly into a Google Sheets database.

## Architecture Overview

1. **Trigger:** Google Drive (`File Created` / Polling mode) monitors the designated target folder for incoming PDF attachments.
2. **Download Node:** Dynamically retrieves the binary file using the unique file ID (`{{ $json.id }}`).
3. **Extraction Node:** Uses the built-in **Extract From File** utility to process the binary PDF structure into raw text.
4. **Processing Node (JavaScript / Regex):** A custom Code node parses the raw text layout to extract specific transactional entities:
   * Invoice Number
   * Client Name
   * Issue Date
   * Total Amount
5. **Output Node:** Automatically appends the structured record as a new row in a target Google Sheets document.

## Tech Stack

* **Workflow Automation:** n8n
* **Cloud Storage & Data Sink:** Google Drive API, Google Sheets API
* **Data Processing:** JavaScript, Regular Expressions (RegEx)

## Setup & Deployment

1. Import the provided workflow JSON file into your self-hosted or cloud n8n instance.
2. Connect your Google Drive and Google Sheets credentials.
3. Configure the Google Drive Trigger node to point to your target invoice folder.
4. Create a target Google Sheet with columns matching: **Invoice Number**, **Client**, **Date**, and **Total**.
5. Activate the workflow to enable background event processing.
