# Amazon Price Tracker

An n8n workflow that monitors Amazon product prices using the ScrapeOps API and alerts you when prices drop or increase beyond your specified thresholds.

## Features

- Monitor prices of multiple Amazon products simultaneously
- Calculate both absolute and percentage price changes
- Set custom thresholds for price increase and decrease alerts
- Receive email notifications with detailed price information
- Maintain historical price data for trend analysis
- Zero-maintenance design with automatic error handling

## Prerequisites

- [n8n](https://n8n.io/) instance (cloud or self-hosted)
- [ScrapeOps API Key](https://scrapeops.io/app/register/main)
- Google account (for Google Sheets)
- SMTP email account for notifications

## Setup Instructions

1. **Import the workflow**
   - Download the `Amazon_Product_Price_Tracker.json` file
   - In your n8n instance, go to "Workflows" → "Import from file"
   - Select the downloaded JSON file

2. **Configure Google Sheets**
   - Create a copy of [this template spreadsheet](https://docs.google.com/spreadsheets/d/1hRv-TBXrpN6rkIU65WorttNHt-IPWas_An0sF4Of39U) or create your own with the required structure
   - Set up the "Products to Monitor" sheet with your Amazon ASINs
   - Configure the Google Sheets nodes in the workflow to connect to your spreadsheet

3. **Add your ScrapeOps API key**
   - Get your API key from [ScrapeOps Dashboard](https://scrapeops.io/app/dashboard)
   - Update the "Scrapeops - Amazon Product" node with your API key

4. **Configure email notifications**
   - Update the "Send Email" node with your SMTP credentials
   - Customize the email template if desired

5. **Set the schedule**
   - Adjust the "Schedule Trigger" node to your preferred frequency
   - Recommended: Every 6-12 hours for optimal balance between timeliness and API usage

## How It Works

1. The workflow reads product ASINs from your Google Sheet
2. For each product, it fetches current pricing data from Amazon via ScrapeOps API
3. It calculates price changes compared to previous values
4. If price changes exceed your defined thresholds, it triggers email notifications
5. All price data is recorded in the history sheet for later analysis

## Customization Options

- **Alert Thresholds**: Adjust the percentage values in the spreadsheet columns `alert_threshold_low` and `alert_threshold_high`
- **Email Template**: Modify the HTML in the "Send Email" node
- **Additional Notifications**: Add nodes for Slack, Telegram, or other platforms

## Troubleshooting

- **No data retrieved**: Verify your ScrapeOps API key is correct and has sufficient credits
- **No emails received**: Check your SMTP configuration and email spam folder
- **Google Sheets errors**: Ensure you have proper permissions on the spreadsheet

## API Documentation

For more details on the ScrapeOps Amazon Product API used in this workflow, see:
https://scrapeops.io/docs/data-api/amazon-product-api/