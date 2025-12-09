# Rotating Housekeeping Checklist Widget - Setup Guide

## What This Does

This JotForm widget shows housekeeping tasks that are **due for checking** based on:
- How long since each item was last checked
- The frequency set for each item (e.g., dishwasher service every 30 days)

When a cleaner selects a property, they only see items that need attention - not the full list every time.

---

## Setup Steps

### 1. Host the Widget File

The widget needs to be accessible via a URL. Options:

**Option A: GitHub Pages (Free) - Recommended**
1. Create a GitHub repository
2. Upload `rotating-checklist-widget.html`
3. Enable GitHub Pages in repo settings (Settings > Pages > Source: main branch)
4. Your URL will be: `https://yourusername.github.io/repo-name/rotating-checklist-widget.html`

**Option B: Netlify (Free)**
1. Go to netlify.com and drag-drop the HTML file
2. You'll get a URL like: `https://random-name.netlify.app/rotating-checklist-widget.html`

**Option C: Your Own Server**
- Upload to any web server you control

---

### 2. Get Your Airtable API Key

1. Go to https://airtable.com/create/tokens
2. Click "Create new token"
3. Name it: "JotForm Housekeeping Widget"
4. Add scopes:
   - `data.records:read`
   - `data.records:write`
   - `schema.bases:read`
5. Add your FrontDesk base to "Access"
6. Click "Create token"
7. **Copy the token** (starts with `pat...`)

---

### 3. Register the Widget with JotForm

1. Go to: https://www.jotform.com/widgets/#add-widget
2. Fill in:
   - **Name**: Rotating Housekeeping Checklist
   - **Widget Type**: iFrame Widget
   - **Widget iFrame URL**: Your hosted URL from Step 1
   - **Widget Width**: 650
   - **Widget Height**: 800

3. Add these **Additional Parameters**:

   | Parameter Name | Human Readable Name |
   |---------------|---------------------|
   | `airtableApiKey` | Airtable API Key |
   | `baseId` | Airtable Base ID (optional) |

4. Submit for your own use (or approval for public)

---

### 4. Add Widget to Your Form

1. Open your housekeeping form in JotForm builder
2. Go to **Widgets** panel
3. Find "Rotating Housekeeping Checklist"
4. Add it to your form
5. When prompted, paste your Airtable API key

---

## Airtable Tables (Already Created)

### Rotating Checklist Items
Your master list of periodic tasks:

| Item | Frequency | Category |
|------|-----------|----------|
| Dishwasher Service | 30 days | Appliances |
| Tumble Dryer Service | 30 days | Appliances |
| Washing Machine Service | 30 days | Appliances |
| Aircon Service | 90 days | Appliances |
| Fridge & Freezer Check | 30 days | Appliances |
| Kettle & Toaster Descale | 45 days | Appliances |
| TV & Streaming Check | 30 days | Appliances |
| Microwave Deep Clean | 30 days | Appliances |
| Remote Batteries | 60 days | Inventory |
| Keys Audit | 30 days | Safety & Security |
| Smoke Detector Test | 30 days | Safety & Security |
| Fire Extinguisher Check | 90 days | Safety & Security |
| Door & Window Locks | 60 days | Safety & Security |
| Mattress Rotation | 90 days | Deep Clean |
| Oven Deep Clean | 60 days | Deep Clean |
| Extractor Fan Cleaning | 60 days | Deep Clean |
| Window Tracks Clean | 60 days | Deep Clean |
| Under Furniture Clean | 60 days | Deep Clean |
| Grout Inspection | 90 days | Maintenance |
| Water Pressure Test | 90 days | Maintenance |
| Showerhead Descale | 60 days | Maintenance |
| Light Bulb Check | 30 days | Maintenance |
| Drain Flow Check | 45 days | Maintenance |
| Curtains & Blinds Check | 90 days | Maintenance |
| WiFi Router Restart | 30 days | Maintenance |
| Geyser Check | 90 days | Maintenance |
| Toilet Mechanism Check | 60 days | Maintenance |
| Pillow Condition Check | 90 days | Inventory |
| Bin Condition Check | 60 days | Inventory |
| Outdoor Furniture Check | 60 days | Inventory |
| Iron & Board Check | 60 days | Inventory |

**To add more items**: Just add rows to this table with Active = checked

### Property Checklist Log
Automatically tracks when each item was last checked per property. The widget creates/updates records here on form submission.

---

## How It Works

1. Cleaner opens form -> selects property
2. Widget queries Airtable for that property's check history
3. Calculates which items are overdue or due soon
4. Shows only those items (not the full list)
5. Cleaner checks completed items
6. On form submit -> Widget updates Airtable with new "Last Checked" dates
7. Next time that property is cleaned, those items won't appear (until they're due again)

---

## Local Testing

You can test the widget locally before hosting:

1. Open `rotating-checklist-widget.html` directly in your browser
2. When prompted, paste your Airtable API key
3. The key is saved in localStorage so you don't re-enter it
4. Use the yellow "Test Submit" button to save checked items to Airtable

---

## Customization

### Add New Checklist Items
1. Go to `Rotating Checklist Items` table in Airtable
2. Add a row with:
   - Item Name
   - Frequency Days (how often to check)
   - Category
   - Instructions (optional)
   - Active = checked

### Change Frequency
Edit the "Frequency Days" field for any item

### Categories
Current categories: Appliances, Safety & Security, Deep Clean, Maintenance, Inventory

---

## Troubleshooting

**"Configuration Required" error**
- Make sure you've entered the Airtable API key in widget settings

**"Error loading widget" or 403 error**
- Check that your API key has the correct scopes (`data.records:read`, `data.records:write`, `schema.bases:read`)
- Verify the FrontDesk base is added to the token's "Access" section

**Properties not showing**
- Verify the Listings table has property names filled in

**Widget too small in JotForm**
- Increase the height in JotForm widget settings to 800+

**Items not updating after submit**
- Check browser console for errors
- Verify API key has write permissions

---

## Base/Table IDs (for reference)

- **Base ID**: `app6guGAO369FvUar` (FrontDesk)
- **Listings Table**: `tblnmc2ODzG9qK7Mn`
- **Rotating Checklist Items**: `tbltKuitiWgzDe9R6`
- **Property Checklist Log**: `tblYnYlo85WiNLJ3H`
