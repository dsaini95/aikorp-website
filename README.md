# aikorp.in: setup and deployment

A fast, static website for AI Korp: free tools for Windows, M365 and AD admins.
It runs on **Azure Static Web Apps (Free plan)**, which costs nothing and includes SSL.

## What's inside

```
index.html                         Home page: hero, tools, LaptopDoctor, guides, about, signup
guides/find-inactive-m365-users.html  First guide (real, tested content for SEO)
404.html                           "Page not found" page
css/style.css                      Design
js/config.js                       ← YOUR SETTINGS + TOOL LIST (edit this)
js/main.js                         Site behaviour (no need to edit)
downloads/                         Files people download
  M365-InactiveUserReport.zip      A real, working free script (ready now)
staticwebapp.config.json           Azure settings
```

## 1. Before you go live

1. **Add LaptopDoctor:** zip your app and save it as `downloads/LaptopDoctor.zip`.
   If it's large (more than ~50 MB), upload it to a GitHub Release instead and put that URL
   in `js/config.js` → `file:`.
2. **Check the LaptopDoctor feature list** in `index.html` (the section with `id="laptopdoctor"`).
   I wrote a typical feature list, so edit it to match what your app really does.
3. **Collect emails (free):**
   - Go to <https://web3forms.com>, enter your email, and copy the **Access Key**.
   - Paste it into `js/config.js` → `web3formsKey: "..."`.
   - Every download, "notify me" and newsletter sign-up now arrives in your inbox with the
     person's name and email. Copy them into a spreadsheet, or later into a newsletter tool
     like MailerLite or Brevo (both have free plans).
4. **Contact links:** set `email`, `linkedin` and `github` in `js/config.js`.
5. **Optional support button:** put a Buy Me a Coffee or UPI link in `supportLink`.

## 2. Adding a new tool later

Add a block to `TOOLS` in `js/config.js`, put the zip in `downloads/`, and set
`status: "available"`. Tools set to `"soon"` show a **Notify me** button, which is a good
way to measure interest before you build something.

## 3. Adding a new guide

Copy `guides/find-inactive-m365-users.html`, rename it (use the search phrase as the
file name, e.g. `bulk-remove-m365-licenses.html`), and change the title, description
and content. Then link it from the Guides section in `index.html`.

## 4. Deploy to Azure

```bash
npm install -g @azure/static-web-apps-cli
swa deploy . --deployment-token YOUR_TOKEN --env production
```

Get the token from: Azure portal → your Static Web App → **Manage deployment token**.
(First time? Create the app at portal.azure.com → Static Web Apps → Create → Plan: Free,
Deployment source: Other.)

Run the same command again whenever you change the site.

## 5. Connect aikorp.in (GoDaddy)

1. Azure → Static Web App → **Custom domains** → Add → `www.aikorp.in`.
2. GoDaddy → Domain → aikorp.in → **DNS**: edit the `www` CNAME so it points to
   `xxxx.azurestaticapps.net`.
3. GoDaddy → DNS → **Forwarding**: forward `aikorp.in` to `https://www.aikorp.in`
   (Permanent 301, Forward only).

## 6. After launch

- Add the site to Google Search Console and submit `https://www.aikorp.in/`
- Share the inactive-users guide on LinkedIn, r/Office365 and r/PowerShell
- Publish one new guide or script every week. That's what builds traffic.
