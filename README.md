Excrow

Excrow is a secure escrow system that holds payments between buyers and sellers until both parties fulfill agreed conditions. Designed for safe transactions and dispute-free settlements.

🚀 Features

Buyer–Seller escrow with optional arbitrator

Secure fund holding and release

Webhook-based payment updates

Dispute handling and resolution

API-ready and modular

🧩 Tech Stack

Backend: Django / Laravel / Node.js

Database: PostgreSQL or MySQL

Queue: Redis

Payments: Paystack / Flutterwave / Stripe

Container: Docker

⚙️ Setup
# Clone the repo
git clone https://github.com/YOUR_USERNAME/excrow.git
cd excrow

# Create environment file
cp .env.example .env

# Install dependencies (example: Django)
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver


For Laravel:

composer install
php artisan migrate
php artisan serve


For Node:

npm install
npm run dev

🔑 Environment Variables
APP_ENV=development
DB_HOST=127.0.0.1
DB_NAME=excrow
DB_USER=excrow
DB_PASS=password
PAYSTACK_SECRET_KEY=sk_test_xxx
REDIS_URL=redis://127.0.0.1:6379

📘 API Overview
Endpoint	Method	Description
/api/escrows	POST	Create new escrow
/api/escrows/{id}	GET	Retrieve escrow details
/api/escrows/{id}/fund	POST	Fund escrow
/api/escrows/{id}/release	POST	Release funds
/api/escrows/{id}/dispute	POST	Open a dispute
🧾 Webhooks

Excrow sends real-time updates for:
escrow.created, escrow.funded, escrow.released, escrow.refunded, and escrow.dispute.opened.
Each event is signed using WEBHOOK_SIGNING_SECRET.

🔒 Security

HTTPS enforced

Input validation

Role-based permissions

Signed webhooks and tokens

🛠️ Testing
pytest
# or
php artisan test
# or
npm test

📦 Deployment

Deploy using Docker or your preferred service (Render, Koyeb, AWS, etc.).
Ensure .env and DB credentials are correctly set.

📅 Roadmap

 Milestone releases

 Multi-currency support

 Payout batching
