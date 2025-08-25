# FB Marketplace Scraper + Telegram Reporter

An advanced tool that continuously monitors **Facebook Marketplace** for chosen products keywords and instantly reports new listings to **Telegram**.  
It comes with a sleek **dashboard** for control and insights, making it easy to run and manage automated scraping jobs.

---

## 📸 Preview

### Dashboard

![Dashboard Preview](./previews/dashboard.jpg)

### History

![Histories](./previews/history.jpg)

### Telegram Alerts

![Telegram Alerts](./previews/alerts.jpg)

---

## ✨ Key Features

- 🔍 **Smart Scraping**  
  Uses Playwright to collect listings efficiently fallback.
- 🍪 **Secure Authentication**  
  Works with fresh cookie JSON (Cookie-Editor / Playwright storageState).
- 📬 **Telegram Delivery**  
  Sends rich media messages, captions, and buttons to your chosen chats.
- 📊 **Interactive Dashboard**  
  Tailwind + EJS dashboard with logs, history, config editor, and system status.
- 📈 **Observability**  
  Health at `/health`, Prometheus metrics at `/metrics`, logs and detailed run stats.
- 🗄 **Persistence & History**  
  MongoDB stores seen listings to avoid duplicates and provides history view.
- ⚡ **Performance**  
  Designed for continuous scraping with concurrency control, retry logic, and fast diff-and-report pipeline.

---

## 🚀 How It Works

1. **Authentication**  
   Import Facebook cookies (JSON) into the dashboard. The scraper will reuse these cookies for headless sessions.

2. **Scraping**

   - Define Products keywords in the dashboard.
   - The scraper performs parallel searches on Marketplace and fetches listings.
   - Configurable interval (default 5 minutes).

3. **Filtering & Deduplication**

   - All listings are checked against the MongoDB `history` collection.
   - Only **new/unseen** items are processed.

4. **Reporting**

   - Each new item is formatted and sent via the Telegram Bot API.
   - Images, description, attributes, and inline button to open the listing.

5. **Monitoring**
   - `/dashboard` — status, uptime, config, history.
   - `/health` — JSON snapshot with uptime, runs, failures, DB, Telegram config.
   - `/metrics` — Prometheus-ready stats.

---

## ⚙️ Usage

### Local Setup

```bash
git clone https://github.com/tas33n/fb-marketplace-scraper.git
cd fb-marketplace-scraper
npm install
npx playwright install
```

### Configuration

- Copy `.env.example` → `.env`
- Edit `config.json` with your:

  - Cookies path (`fb-cookies.json`)
  - Telegram bot token and chat IDs
  - MongoDB URI and DB name
  - Scrape keywords and interval

### Running

```bash
npm run dev   # Development (headful Playwright, verbose logs)
npm start     # Production (headless, optimized)
```

### Docker

```bash
docker build -t fb-mp-scraper .
docker run -it --rm -p 3000:3000 \
  -v $(pwd)/data:/app/data \
  fb-mp-scraper
```

---

## 📊 Performance & Scalability

- Designed to handle **multiple keywords** concurrently.
- Concurrency is configurable (default: 3).
- Automatic retries and timeout handling for enrichment requests.
- Streamlined diff-and-report pipeline: new items are **sent instantly** without waiting for the entire batch to finish.
- MongoDB ensures deduplication and quick lookups.

---

## 📬 Contact

For inquiries, demos, or deployment details, feel free to reach out:

- Email: [farhanisteak84@gmail.com](mailto:farhanisteak84@gmail.com)
- Telegram: [@lamb3rt](https://t.me/lamb3rt)
- GitHub: [Tas33n](https://github.com/tas33n)

```
