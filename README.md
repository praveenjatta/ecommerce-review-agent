# ⭐ E-Commerce Negative Review Detection & Response Agent

An AI agent that automatically scans product reviews in Google Sheets, analyzes sentiment to classify each review as NEGATIVE, POSITIVE, or NEUTRAL, and generates a professional empathetic email draft for every negative review — ready for the support team to send with one click.

---

## 🎯 Problem Statement

Negative product reviews left unaddressed damage brand reputation and reduce customer trust. E-commerce businesses receive hundreds of reviews daily and manually drafting responses is time-consuming and inconsistent. This agent instantly detects negative sentiment and generates a warm, empathetic, professional response draft — ready for a team member to review and send.

---

## ⚡ How It Works

```
Read Reviews → Filter Empty Mail Draft → Check Review Text → Analyze Sentiment → Generate Response → Write to Mail Draft Column
```

### Sentiment Classification

| Classification | Condition | Action | Output |
|---------------|-----------|--------|--------|
| NEGATIVE | Strong dissatisfaction expressed | Generate email draft | Professional empathetic email body |
| POSITIVE | Satisfaction or praise expressed | No response needed | `No response required` |
| NEUTRAL | Factual or indifferent tone | No response needed | `No response required` |
| Empty review | review_text cell is empty | Skip row | `No review found. No action taken.` |

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────┐
│         Google Sheets: Reviews Tab       │
│  review_id | review_text | Mail Draft    │
│  (Mail Draft empty = not yet processed)  │
└──────────────────────────────────────────┘
                      │
                      ▼
┌──────────────────────────────────────────┐
│     Negative Review Detection Agent      │
│          (Zapier Automation)             │
│                                          │
│  1. Read all rows from Reviews tab       │
│  2. Filter rows where Mail Draft = empty │
│  3. Check if review_text exists          │
│  4. Analyze sentiment of review text     │
│  5. Generate email draft (if NEGATIVE)   │
│  6. Write response to Mail Draft column  │
│  7. Repeat for all unprocessed rows      │
└──────────────────────────────────────────┘
                      │
                      ▼
┌──────────────────────────────────────────┐
│     Mail Draft Column Updated            │
│  NEGATIVE → Professional email body     │
│  POSITIVE → "No response required"      │
│  NEUTRAL  → "No response required"      │
│  EMPTY    → "No review found."          │
└──────────────────────────────────────────┘
```

---

## 📊 Google Sheets Structure

**Spreadsheet Name:** `E-commerce Reviews`

| Tab | Purpose |
|-----|---------|
| `Reviews` | All customer reviews + email draft output |

### Reviews Tab Schema
```
review_id | product_name | reviewer_name | review_text | rating | Mail Draft
```

### Sample Data

| review_id | product_name | review_text | rating | Mail Draft |
|-----------|-------------|-------------|--------|------------|
| REV001 | Wireless Earbuds | Stopped working after 2 days. Very disappointed. | 1 | *(empty — agent processes this)* |
| REV002 | Phone Case | Great case! Fits perfectly and looks amazing. | 5 | *(empty — agent processes this)* |
| REV003 | USB Hub | Terrible quality. Broke on first use. Waste of money. | 1 | *(empty — agent processes this)* |

### After Agent Runs

| review_id | Mail Draft |
|-----------|------------|
| REV001 | *"Dear Valued Customer, Thank you for your feedback..."* (full email draft) |
| REV002 | `No response required` |
| REV003 | *"Dear Valued Customer, We sincerely apologize..."* (full email draft) |

---

## 🔧 Zapier Tools Used

| Tool | Purpose |
|------|---------|
| `Google Sheets: Lookup Spreadsheet Rows (Advanced)` | Read all reviews, filter empty Mail Draft |
| `Google Sheets: Update Spreadsheet Row` | Write email draft to Mail Draft column |

---

## 📝 Email Draft Rules

- Address the **specific issue** mentioned in the review — no generic templates
- Maintain a **warm, empathetic, professional** tone
- Acknowledge the customer's frustration genuinely
- Offer to help resolve the issue
- Never invent facts or details not in the review
- Write **only the email body** — no subject line, labels, or formatting tags

---

## 🔒 Strict Processing Rules

- **Never** process rows where Mail Draft column already has content
- **Never** rewrite, summarize, or modify the original review text
- **Never** add labels or explanations outside the Mail Draft cell
- **Only** use information present in the review — never invent details
- **Always** write exact phrase for positive/neutral: `No response required`
- **Always** write exact phrase for empty reviews: `No review found. No action taken.`

---

## 🚀 How to Run

1. Set up the Google Sheet with Reviews tab and 6 columns
2. Add product review rows — leave Mail Draft column empty
3. Configure Zapier agent with 2 tools
4. Run agent: type `Process new product reviews` in Agent Preview
5. Verify:
   - Negative reviews have professional email drafts
   - Positive/neutral reviews show `No response required`
   - Original review_text column was NOT modified

---

## 🔄 How to Rerun

- **New reviews:** Add new rows with empty Mail Draft column
- **Reprocess a row:** Manually clear the Mail Draft cell for that row
- **Existing rows** with content in Mail Draft are automatically skipped

---

## 🛠️ Tech Stack

![Zapier](https://img.shields.io/badge/Zapier-FF4A00?style=flat&logo=zapier&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?style=flat&logo=google-sheets&logoColor=white)
![NLP](https://img.shields.io/badge/Sentiment_Analysis-NLP-purple)

---

## 👤 Author

**Praveen Kumar Jatta** — AI Automation Consultant & Technical Program Manager

- 🌐 [jattaai.com](https://jattaai.com)
- 💼 [linkedin.com/in/praveenjatta](https://linkedin.com/in/praveenjatta)
- 📧 jattaaihq@gmail.com

---

*Built as part of the EdgeUp for TPMs — Applied Agentic AI program by Interview Kickstart*
