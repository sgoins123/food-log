# Food Log

A personal calorie tracker that runs entirely in the browser. It's a static site with no backend and no build step. Your log and API keys stay in your browser's `localStorage`.

## Features

- A daily log grouped by meal (Morning, Lunch, Dinner, Snacks), with day navigation and a 7-day chart
- Food search across USDA FoodData Central and Open Food Facts
- Photo calorie estimates using Claude (needs an Anthropic API key)
- Manual entry
- JSON export and import (API keys are never exported)

## API keys

Open the app, tap the gear icon (Settings), paste your keys, and tap **Save keys**. Keys are stored only on that device, so you'll need to enter them on each phone or browser you use.

### USDA FoodData Central (free)

1. Go to <https://fdc.nal.usda.gov/api-key-signup> and fill in your name and email.
2. The key arrives by email right away.
3. Paste it into **USDA FoodData Central API key** in Settings.

If you leave this blank, the app uses `DEMO_KEY`. That works, but it's limited to about 30 searches an hour and 50 a day. Open Food Facts needs no key.

### Anthropic (for photo estimates)

1. Sign in at <https://console.anthropic.com/> and add a payment method or credits under **Billing**. API usage is pay-as-you-go. Each photo estimate costs about a cent.
2. Open **API Keys** and select **Create Key**.
3. Paste the key (it starts with `sk-ant-`) into **Anthropic API key** in Settings.

The photo tab stays disabled until a key is saved. Because the app calls the API directly from your browser, anyone who can use your browser profile can read the key. Use it only on your own devices. You can also set a monthly spend limit in the Anthropic Console.

## Sync to GitHub (recommended)

Your log is stored in the browser, so clearing Safari's website data, using Private Browsing, or switching between Safari and the home-screen app leaves you with an empty log. Sync saves the log to a private GitHub repo so it comes back on any device. API keys are never synced.

1. Create a **private** repo, for example `food-log-data`. Leave it empty. The app won't sync to a public repo.
2. On GitHub, go to **Settings → Developer settings → Personal access tokens → Fine-grained tokens** and select **Generate new token**.
3. Under **Repository access**, choose **Only select repositories** and pick your data repo.
4. Under **Permissions → Repository permissions**, set **Contents** to **Read and write**. Nothing else is needed.
5. In the app, open **Settings → GitHub sync**, enter the repo as `owner/name` with the token, and tap **Save & sync**.

The log is saved as `food-log.json` in that repo. Every add or delete syncs within a couple of seconds, and the app pulls the latest copy whenever you open it. Changes made on two devices at once are merged. If you're offline, entries are kept on the device and sync later. Enter the token once on each device. Safari and the home-screen app count as separate devices.

## Add to your home screen

- **iPhone (Safari):** tap Share, then **Add to Home Screen**.
- **Android (Chrome):** open the ⋮ menu, then select **Add to Home screen** or **Install app**.

## Backups

Your data lives in one browser. Use **Settings → Export backup** now and then. **Import backup** replaces the current log after asking you to confirm.

## Run locally

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>.
