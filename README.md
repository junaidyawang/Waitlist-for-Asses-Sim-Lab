# Waitlist form: Vercel page + Google Sheet

**How it works:** the page is hosted on Vercel. When someone submits it, the details go to a small Apps Script attached to your Google Sheet. The script saves the row, emails the person a thank-you with the Health Check demo, and sends you an alert.

```
waitlist-vercel/
├── web/                 ← upload this folder to Vercel
│   ├── index.html       ← the form (edit WEBAPP_URL at the bottom)
│   ├── og.png           ← image shown when the link is shared on LinkedIn
│   ├── favicon.svg
│   └── vercel.json
└── sheet-backend/
    └── Code.gs          ← paste into Apps Script in your Google Sheet
```

## Step 1: Google Sheet backend (about 5 minutes)
1. Create a Google Sheet, for example "Waitlist – AI Assessments & Simulations".
2. Open **Extensions → Apps Script**, delete the sample code, and paste in all of `sheet-backend/Code.gs`.
3. Optional: edit `CONFIG` at the top (sender name, programme title, alert email).
4. Choose `setup` from the function menu, click **Run** and approve the permissions. A "Waitlist" tab appears in the Sheet.
5. Go to **Deploy → New deployment → Web app**. Set Execute as **Me** and Who has access **Anyone**, then click **Deploy**.
6. Copy the **Web app URL** (it ends in `/exec`).

## Step 2: Connect the page
Open `web/index.html`, find `WEBAPP_URL` near the bottom, and paste your URL between the quotes.

## Step 3: Deploy to Vercel
**Option A: GitHub (recommended, auto-updates when you change the page)**
1. Create a new GitHub repository and upload the files from `web/`.
2. In Vercel: **Add New → Project → Import** that repository. Keep the framework preset as **Other**, then click **Deploy**.

**Option B: Vercel CLI**
```
npm i -g vercel
cd web
vercel --prod
```

## Step 4: Finishing touches
- **LinkedIn preview image:** in `index.html`, change `<meta property="og:image" content="/og.png">` to the full address, e.g. `https://your-project.vercel.app/og.png`. Then check the link in LinkedIn's Post Inspector.
- **Track which post works:** add `?src=` to links, e.g. `https://your-project.vercel.app/?src=post1` or `?src=video`. The label appears in the Sheet's **Source** column.

## If you change the Apps Script later
Use **Deploy → Manage deployments → Edit (pencil) → Version: New version**. This keeps the same URL, so you don't need to update the page.
