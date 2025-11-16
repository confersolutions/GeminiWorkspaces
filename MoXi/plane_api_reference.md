# Plane API Integration Reference (MoXi Project)

## Overview

This document captures *all* relevant context, configuration, URLs, IDs,
API keys, cURL commands, and learnings from our Plane setup on
**https://plane.confer.today**.\
It is designed so that: 1. You can start a brand-new ChatGPT session and
paste this file to instantly restore full context. 2. You can give this
file to Cursor, Windsurf, or any coding assistant to generate a Python
project without repeating earlier mistakes.

------------------------------------------------------------------------

## 1. Plane Instance Details

### **Plane Base URL**

    https://plane.confer.today

### **Workspace (Slug)**

    confer-solutions-ai

### **MoXi Project**

-   **Project ID:** `06c53d54-4036-4da9-affe-71ed4bd781b6`

-   **Project UI URL:**

        https://plane.confer.today/confer-solutions-ai/projects/06c53d54-4036-4da9-affe-71ed4bd781b6/issues/

------------------------------------------------------------------------

## 2. Authentication

### **Plane PAT / API Key**

> Valid for one week starting **Nov 14, 2025**\
> (Replace with a fresh one when expired.)

    plane_api_8d45db56e7da412dbf7b5578f94073b3

### Correct HTTP Header

    x-api-key: plane_api_8d45db56e7da412dbf7b5578f94073b3

------------------------------------------------------------------------

## 3. MoXi Workflow State IDs

Retrieved via:

    GET https://plane.confer.today/api/v1/workspaces/confer-solutions-ai/projects/06c53d54-4036-4da9-affe-71ed4bd781b6/states/

### **States**

  State Name    UUID
  ------------- ----------------------------------------
  Backlog       `68b5cc66-7379-4782-a90d-49a868401bdb`
  Todo          `2f6ee4f3-e9e7-4ab1-8918-027a8c688a9f`
  In Progress   `db34d781-9dd0-4e18-82ab-58e798a16795`
  Done          `6228c7a0-97a6-41c4-9660-ab7e0425da23`
  Cancelled     `647470cd-8c45-44d0-8b72-2c71a13b917f`

------------------------------------------------------------------------

## 4. Verified Working cURL Commands

### **4.1 GET states (sanity check)**

``` bash
curl --request GET   "https://plane.confer.today/api/v1/workspaces/confer-solutions-ai/projects/06c53d54-4036-4da9-affe-71ed4bd781b6/states/"   --header "x-api-key: plane_api_8d45db56e7da412dbf7b5578f94073b3"
```

### **4.2 Create Issue (explicit Backlog)**

This successfully created `MOXI-3`.

``` bash
curl --request POST   "https://plane.confer.today/api/v1/workspaces/confer-solutions-ai/projects/06c53d54-4036-4da9-affe-71ed4bd781b6/issues/"   --header "Content-Type: application/json"   --header "x-api-key: plane_api_8d45db56e7da412dbf7b5578f94073b3"   --data '{
    "name": "MoXi API test – Backlog (explicit state, new domain)",
    "description": "Created in MoXi via API using https://plane.confer.today",
    "state": "68b5cc66-7379-4782-a90d-49a868401bdb"
  }'
```

------------------------------------------------------------------------

## 5. Complete Python Script for Importing the Excel Sheet

This script imports the Monday.com export
`Vendor_Subscription_Tracker_1763166440.xlsx` into Plane MoXi backlog.

``` python
import pandas as pd
import requests

PLANE_BASE_URL = "https://plane.confer.today"
WORKSPACE_SLUG = "confer-solutions-ai"
PROJECT_ID = "06c53d54-4036-4da9-affe-71ed4bd781b6"
API_KEY = "plane_api_8d45db56e7da412dbf7b5578f94073b3"
BACKLOG_STATE_ID = "68b5cc66-7379-4782-a90d-49a868401bdb"

EXCEL_FILE = "Vendor_Subscription_Tracker_1763166440.xlsx"

df_raw = pd.read_excel(EXCEL_FILE)
headers = df_raw.iloc[1]
df = df_raw[2:].copy()
df.columns = headers
df = df[df["Name"].notna()]

def build_description(row):
    parts = []
    def add(label, col):
        val = row.get(col)
        if pd.notna(val):
            parts.append(f"**{label}:** {val}")

    add("Account Number", "Account Number")
    add("Account Manager / Contact", "Account Manager / Phone / Email")
    add("In Contract", "In Contract (Yes/No)")
    add("Department", "Department")
    add("Renewal / Billing Schedule", "Renewal / Billing Schedule")
    add("Price", "Price")
    add("Payment Type", "Payment Type")
    add("P-Card Holder", "P-Card Holder")
    add("Notes", "Notes")
    add("Confer Feedback", "Confer Feedback")

    return "
".join(parts)

session = requests.Session()
session.headers.update({
    "Content-Type": "application/json",
    "x-api-key": API_KEY,
})

endpoint = f"{PLANE_BASE_URL}/api/v1/workspaces/{WORKSPACE_SLUG}/projects/{PROJECT_ID}/issues/"

created = 0
for _, row in df.iterrows():
    name = str(row["Name"]).strip()
    payload = {
        "name": name,
        "description": build_description(row),
        "state": BACKLOG_STATE_ID,
    }

    resp = session.post(endpoint, json=payload)
    if resp.ok:
        created += 1
        print(f"✓ Created: {name}")
    else:
        print(f"✗ Failed for {name}: {resp.status_code} {resp.text}")

print(f"Done. Created {created} issues.")
```

------------------------------------------------------------------------

## 6. All Key Learnings to Avoid Repeating Mistakes

### **6.1 Authentication mistakes we corrected**

-   Must use `x-api-key`, **not** `Authorization: Bearer`
-   PAT must start with `plane_api_`
-   API key works for both GET + POST

### **6.2 Endpoint path must start with `/api/v1/`**

Incorrect:

    /api/...

Correct:

    /api/v1/...

### **6.3 State must be a UUID, not text**

Wrong:

    "state": "backlog"

Correct:

    "state": "68b5cc66-7379-4782-a90d-49a868401bdb"

### **6.4 Cloudflare SSL issue (Error 526)**

-   Happens if Cloudflare → Origin SSL mismatch
-   Resolved by switching to `plane.confer.today` (Coolify-managed
    HTTPS)
-   Confirmed `/api/v1/...` works over HTTPS

### **6.5 Avoid line continuation backslash errors**

Backslash must be the **last** character on the line:

Correct:

    ...issues/" ```

    Wrong:

...issues/" ␣ \`\`\`

------------------------------------------------------------------------

## 7. What ChatGPT Should Assume When Opening This File

When this MD is pasted into a new chat, ChatGPT should assume:

-   You already have a working Plane instance at
    `https://plane.confer.today`
-   You are managing the **MoXi** project inside workspace
    `confer-solutions-ai`
-   You already verified API connectivity using working cURL commands
-   You want to automate importing / syncing / managing Plane issues
    programmatically
-   You may want Cursor to generate a full Python automation project
    based on this MD

ChatGPT should not repeat earlier mistakes: - No use of `Authorization:`
header - No plain `"backlog"` strings for state - Always include
`/api/v1` - Always use correct workspace and project IDs - Always format
multi-line cURL correctly - Always assume Python requests + pandas
workflow unless instructed otherwise

------------------------------------------------------------------------

## 8. Next Steps You Can Ask For in a Fresh Chat

Examples of follow-up tasks ChatGPT should immediately understand:

-   "Generate a complete Python CLI to bulk import items into Plane."
-   "Create FastAPI endpoints that sync Plane issues bi-directionally."
-   "Transform the Excel import into an automated daily ingestion job."
-   "Build a Cursor-ready project with this Plane context."

------------------------------------------------------------------------

## End of Document
