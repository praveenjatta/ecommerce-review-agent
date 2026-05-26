# Google Sheets Setup — E-Commerce Negative Review Detection & Response Agent

## Spreadsheet Name
`E-commerce Reviews`

## Tab 1 — Reviews (Only Tab Needed)

**Headers (Row 1):**
| review_id | product_name | reviewer_name | review_text | rating | Mail Draft |

**Important:**
- Column name must be exactly `Mail Draft` with capital M and D
- Leave Mail Draft column empty for all rows before running
- Agent detects empty Mail Draft = not yet processed

## Zapier Tools to Add

| Tool | Purpose |
|------|---------|
| Google Sheets: Lookup Spreadsheet Rows (Advanced) | Read all reviews, filter empty Mail Draft |
| Google Sheets: Update Spreadsheet Row | Write email draft to Mail Draft column |

## After Agent Runs

| Sentiment | Mail Draft Output |
|-----------|-----------------|
| NEGATIVE | Full professional email body |
| POSITIVE | `No response required` |
| NEUTRAL | `No response required` |
| Empty review_text | `No review found. No action taken.` |
