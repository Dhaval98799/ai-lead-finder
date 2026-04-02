# AI Buyer Research Agent — Setup Guide
# (Beginner Friendly | 100% Free Trial | Every Step Explained)

=============================================================
## PHASE 1 — GOOGLE SHEET SETUP
=============================================================

### 1.1 — Sheet બનાવો
1. Browser માં ખોલો: https://sheets.google.com
2. "+ Blank" click કરો — નવી sheet ખુલ્શે
3. Top-left માં "Untitled spreadsheet" click કરો
4. Name type કરો: Buyer Research Agent
5. Enter press કરો

---

### 1.2 — Row 1 માં EXACT Headers Type કરો
Cell A1 click કરો, પછી Tab press કરી આગળ વધો:

A1  = Status
B1  = Row_Number
C1  = Company_Name
D1  = Country
E1  = Country_Code
F1  = Industry
G1  = Domain
H1  = Domain_Verified
I1  = Website_URL
J1  = Company_Full_Name
K1  = Company_Description
L1  = Owner_Name
M1  = Owner_Confidence
N1  = Owner_LinkedIn
O1  = Director_Name
P1  = CEO_Name
Q1  = Founder_Name
R1  = Verified_Emails
S1  = Personal_Emails
T1  = Generic_Emails
U1  = Unverified_Emails
V1  = Total_Emails_Found
W1  = Phone_Numbers
X1  = LinkedIn_Company
Y1  = Overall_Confidence
Z1  = Research_Notes
AA1 = Last_Updated

---

### 1.3 — Test Data Add કરો (3 rows)
Row 2:
  A2 = Pending
  B2 = 2
  C2 = Reliance Industries
  D2 = India
  E2 = in
  F2 = Conglomerate

Row 3:
  A3 = Pending
  B3 = 3
  C3 = Tata Steel
  D3 = India
  E3 = in
  F3 = Manufacturing

Row 4:
  A4 = Pending
  B4 = 4
  C4 = Infosys
  D4 = India
  E4 = in
  F4 = IT Services

---

### 1.4 — Sheet ID Copy કરો
Browser URL bar જુઓ:
https://docs.google.com/spreadsheets/d/[THIS_IS_YOUR_ID]/edit#gid=0
                                        ^^^^^^^^^^^^^^^^^^^^
આ ID copy કરો — later n8n માં use થશે


=============================================================
## PHASE 2 — SERPAPI FREE KEY
=============================================================

### 2.1 — Account બનાવો
1. ખોલો: https://serpapi.com
2. "Start Free Trial" click કરો
3. Email + Password enter કરો → Sign up
4. Email verify કરો

### 2.2 — API Key Copy કરો
1. Login થઈ Dashboard ખુલ્શે
2. Right side: "Your Private API Key" box જુઓ
3. Key copy કરો (something like: abc123def456...)
4. Notepad/Notes app માં save કરો — SERPAPI_KEY = xxxx

FREE Plan: 100 searches/month
(3 rows test = 12 searches = FREE)


=============================================================
## PHASE 3 — CLAUDE API KEY (FREE $5 CREDIT)
=============================================================

### 3.1 — Account બનાવો
1. ખોલો: https://console.anthropic.com
2. "Sign up" click કરો
3. Email verify, Phone verify
4. $5 free credit automatically મળશે

### 3.2 — API Key બનાવો
1. Left menu: "API Keys" click કરો
2. "Create Key" button click કરો
3. Name type: buyer-agent
4. "Create Key" click → Key show થશે
5. IMMEDIATELY COPY — ફરી show નહીં થાય!
6. Notepad: CLAUDE_KEY = sk-ant-xxx...


=============================================================
## PHASE 4 — SNOV.IO TOKEN
=============================================================

### 4.1 — Token Copy કરો
1. ખોલો: https://app.snov.io
2. Login → Left menu: Settings (gear icon)
3. "API" tab click કરો
4. "Access Token" copy કરો
5. Notepad: SNOV_TOKEN = xxx...


=============================================================
## PHASE 5 — N8N SETUP
=============================================================

### 5.1 — Free Account બનાવો
1. ખોલો: https://n8n.io
2. "Get started free" click કરો
3. Email + Password → Sign up
4. Email verify
5. Dashboard ખુલ્શે

---

### 5.2 — JSON Import કરો
1. Dashboard: "+ Add workflow" click કરો
2. Empty workflow canvas ખુલ્શે
3. Top-right: "..." (3 dots) menu click કરો
4. "Import from file" click કરો
5. File picker: AI_Buyer_Agent_FINAL.json select
6. "Import" click — 15 nodes automatically load થઈ જશે!

---

### 5.3 — Google Sheets Credential Connect કરો

STEP A: Credential Create
1. n8n Left sidebar: "Credentials" click
2. "+ Add credential" click
3. Search box: "Google Sheets" type
4. "Google Sheets OAuth2 API" select
5. "Connect my account" click
6. Google popup: Your account select
7. "Allow" click
8. Credential name: Google Sheets Account
9. Save

STEP B: Nodes ને Credential Assign
ત્રણ nodes ને Google credential જોઈ:
- STEP 2 - Read Pending Row
- STEP 4 - Mark as Processing
- STEP 14 - Write to Google Sheet

દરેક node ખોલો:
1. Node ઉપર double-click
2. "Credential" dropdown: "Google Sheets Account" select
3. Save

---

### 5.4 — Google Sheet ID Replace કરો

ત્રણ Google Sheets nodes માં Sheet ID replace:
(STEP 2, STEP 4, STEP 14)

1. STEP 2 - Read Pending Row ઉપર double-click
2. "Document ID" field: PASTE_YOUR_GOOGLE_SHEET_ID_HERE delete
3. Phase 1.4 માં copy કરેલ ID paste
4. Save

5. STEP 4 - Mark as Processing: same replacement
6. STEP 14 - Write to Google Sheet: same replacement

---

### 5.5 — SerpAPI Key Replace કરો

4 HTTP Request nodes ને SerpAPI key:
- STEP 5A - Search Official Website
- STEP 5B - Search Owner Director
- STEP 5C - Search Phone Email
- STEP 5D - Search Business Databases

દરેક node:
1. Double-click
2. "Query Parameters" section
3. "api_key" row: PASTE_YOUR_SERPAPI_KEY_HERE → actual key paste
4. Save

---

### 5.6 — Claude API Key Replace કરો

1. STEP 7 - Claude AI Extract Data ઉપર double-click
2. "Header Parameters" section
3. "x-api-key" row value: PASTE_YOUR_CLAUDE_API_KEY_HERE → actual key paste
4. Save

---

### 5.7 — Snov.io Token Replace કરો

2 nodes ને Snov token:
- STEP 10B - Snov Get Domain Emails
- STEP 12 - Snov Verify Emails

દરેક node:
1. Double-click
2. "Header Parameters" section
3. "Authorization" row: Bearer PASTE_YOUR_SNOV_TOKEN_HERE
   Replace: "PASTE_YOUR_SNOV_TOKEN_HERE" → actual token
   (Bearer word રહેવા દો, ફક્ત token replace)
4. Save


=============================================================
## PHASE 6 — NODE CONNECTIONS VERIFY
=============================================================

JSON import પછી connections automatic હોય, but verify:

STEP 1 → STEP 2
STEP 2 → STEP 3
STEP 3 (TRUE/YES branch) → STEP 4
STEP 4 → STEP 5A, 5B, 5C, 5D (ચારેય parallel)
STEP 5A → STEP 6
STEP 5B → STEP 6
STEP 5C → STEP 6
STEP 5D → STEP 6
STEP 6 → STEP 7
STEP 7 → STEP 8
STEP 8 → STEP 9
STEP 9 (TRUE/YES branch) → STEP 10A + STEP 10B (parallel)
STEP 9 (FALSE/NO branch) → STEP 10C
STEP 10A → STEP 11A
STEP 10B → STEP 11B
STEP 11B → STEP 12
STEP 12 → STEP 13
STEP 11A → STEP 13
STEP 10C → STEP 13
STEP 13 → STEP 14

### Missing Connection? — આ રીતે add:
1. Source node ના right side નો dot (circle) ઉપર hover
2. Click + drag → Target node સુધી
3. Arrow draw આ ગઈ


=============================================================
## PHASE 7 — FIRST TEST (1 ROW)
=============================================================

### 7.1 — Single Row Test
1. Google Sheet: ફક્ત Row 2 Status = Pending રાખો
   Row 3, 4: Status = Hold (temporarily)

2. n8n: Workflow canvas ઉપર
3. "Test workflow" button click (play icon, top right)
4. Watch nodes turn green one by one
5. Takes about 1-2 minutes

### 7.2 — Result Check
Google Sheet Row 2 check:
- Status = Done? ✅ Working!
- Domain filled? ✅
- Emails filled? ✅
- Owner name filled? ✅

### 7.3 — Common Errors + Fix

ERROR: "Authentication failed" on Google Sheets
FIX: Credentials → Delete old → Re-create → Re-authorize

ERROR: "401 Unauthorized" on SerpAPI
FIX: API key wrong — double check serpapi.com dashboard

ERROR: "401" on Claude API
FIX: Key starts with "sk-ant-" — check you copied full key

ERROR: "Invalid domain" on domain verify
FIX: Normal — some companies don't have website, agent continues

ERROR: Node shows red X
FIX: Click node → Check error message → Fix the specific field


=============================================================
## PHASE 8 — RUN ALL 12,000 ROWS
=============================================================

### 8.1 — Sheet Prepare
1. All rows Status column = Pending
2. Row_Number column = 2, 3, 4, 5... (sequential numbers)

### 8.2 — Activate Agent
1. n8n workflow top-right: "Active" toggle click
2. Toggle turns blue/green
3. Agent starts automatically every 5 minutes

### 8.3 — Monitor Progress
- n8n: "Executions" tab = see each run
- Google Sheet: watch rows fill automatically
- Status changes: Pending → Processing → Done

### 8.4 — Speed Up (Optional)
STEP 1 node → change interval: 5 min → 1 min
This processes faster (1 row per minute)


=============================================================
## QUICK REFERENCE — What Each Step Does
=============================================================

STEP 1  = Timer: every 5 minutes trigger
STEP 2  = Read next "Pending" row from sheet
STEP 3  = Check: is Company_Name empty? (skip if yes)
STEP 4  = Mark row as "Processing" in sheet
STEP 5A = Google Search: official website
STEP 5B = Google Search: owner/director/CEO on LinkedIn
STEP 5C = Google Search: phone/email/contact
STEP 5D = Google Search: crunchbase/zoominfo database
STEP 6  = Combine all 4 search results into one
STEP 7  = Send to Claude AI → extract domain/people/contact
STEP 8  = Parse AI response, drop LOW confidence data
STEP 9  = Check: did AI find a domain?
STEP 10A= YES path: visit website to confirm it's live
STEP 10B= YES path: ask Snov.io for all emails on that domain
STEP 10C= NO path: skip Snov, use search emails only
STEP 11A= Store domain live/dead result
STEP 11B= Clean up Snov email list
STEP 12 = Snov verifies each email (valid/invalid/unknown)
STEP 13 = Combine everything into final clean output
STEP 14 = Write all data to Google Sheet row
STEP 15 = If any error → mark row as "Error" in sheet


=============================================================
## NOTES ON FREE LIMITS
=============================================================

SerpAPI:     100 searches free = ~8 complete rows (4 searches x row)
             For full 12,000 rows → upgrade to $50/mo plan (5000 searches)
             But for TESTING: free is enough

Claude API:  $5 free credit = ~1,600 rows
             ($0.003 per row approximately)

Snov.io:     Your paid plan = unlimited (already have)

n8n:         Free tier = 5 active workflows, 2,500 executions/month
             For 12,000 rows → use self-hosted n8n (completely free)
             Self-host guide: https://docs.n8n.io/hosting/

Google Sheets: Completely free forever


=============================================================
## SUPPORT
=============================================================

Problem screenshot સાથે Claude ને share કરો
Exact error message copy-paste કરો
Which STEP number error show: mention that step

=============================================================
