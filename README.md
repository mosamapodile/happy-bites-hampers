# happy-bites-hampers

# 🧺 Happy Bites Hampers

> **The "Uber of Snacks"** — A custom, high-performance web platform that turns custom snack curation into an instant, interactive experience. Customers can buy signature boxes or use our **interactive AI Snack Assistant** to design bespoke boxes starting at a strict baseline of **R100**, processed instantly via local South African payment gateways.

---

## ✨ Features

* 🤖 **AI Snack Assistant:** A conversational slide-out interface that negotiates, adds custom treats, and dynamically calculates hampers in real-time.
* 🛑 **R100 Minimum Enforcement:** A programmatic backend guardrail preventing any custom order from being checked out below R100.
* 💳 **ZAR Payment Gateways:** Seamless integration with **Yoco** and **PayFast** supporting Card, Instant EFT, and Capitec Pay.
* 📈 **Automated Revenue Share:** A built-in transaction-fee tracking ledger that calculates a lifetime platform fee (e.g., 5%) for the developer on every checkout.
* 📱 **Mobile-First Design:** Fully responsive templates inspired directly by Happy Bites' official design assets.

---

## 🏗️ Tech Stack

* **Backend:** Python 3.11+ / Django 5.0
* **Frontend:** HTML5, Tailwind CSS, Alpine.js / Vanilla JS
* **Database:** PostgreSQL (Production) / SQLite (Local Dev)
* **APIs:** OpenAI (GPT-4o-mini) or Gemini API
* **Payment Gateways:** PayFast SDK / Yoco Webhooks

---

## 📂 Repository Structure

```text
happy-bites-hampers/
├── config/                 # Main project configuration (settings, routes)
├── core/                   # Homepages, static assets (Tailwind input/output, custom JS)
├── hampers/                # Catalog database, custom snack items, & AI service logic
├── orders/                 # Cart logic, transactional models, & gateway payment handling
├── templates/              # Base layout, structural components, and chatbot overlays
├── manage.py               # Django utility script
├── package.json            # Node scripts for Tailwind CSS compiler pipelines
└── tailwind.config.js      # Tailwind scan paths and brand theme extensions

```

---

## ⚡ Quick Start (WSL / Linux)

### 1. Clone the repository & set up your environment

```bash
git clone https://github.com/your-username/happy-bites-hampers.git
cd happy-bites-hampers

# Spin up virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Install Python dependencies
pip install -r requirements.txt

```

### 2. Configure Local Environment Variables

Create a `.env` file in the project root:

```env
DEBUG=True
SECRET_KEY=your_django_secret_key
DATABASE_URL=sqlite:///db.sqlite3

# AI & Payments
OPENAI_API_KEY=your_openai_api_key
YOCO_SECRET_KEY=sk_test_...
PAYFAST_MERCHANT_ID=your_merchant_id
PAYFAST_MERCHANT_KEY=your_merchant_key

```

### 3. Compile the Frontend (Tailwind CLI)

Ensure you have Node.js installed in your workspace environment, then run:

```bash
npm install
npm run tailwind-watch

```

### 4. Migrate & Launch Django

In a separate terminal tab:

```bash
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver

```

Your application will be live at `[http://127.0.0.1:8000/](http://127.0.0.1:8000/)`.

---

## 🪙 Lifetime Commission & Financial Safety

To secure your lifetime ownership, the backend utilizes an immutable, server-side ledger. Rather than relying on frontend code (which can be modified in the browser console), the final pricing and your platform share are computed directly on the server before hitting the gateway:

```python
# From orders/models.py
def save(self, *args, **kwargs):
    # Enforces transaction calculations server-side
    self.developer_commission = (self.total_price * self.platform_fee_percentage) / 100
    super().save(*args, **kwargs)

```

Payments are flagged as `paid` only when a secure SHA-256 signed webhook is returned from PayFast or Yoco, protecting the business from unauthorized price alterations.

---

## 📜 License

Designed & Developed by [Mosa](https://www.google.com/search?q=https://github.com/your-username). All rights reserved to the platform creator. Licensing agreements for codebase usage and lifetime commissions are bound to the signed Service Level Agreement (SLA).
