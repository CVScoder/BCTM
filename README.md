Here’s an enhanced, polished, and more professional version of your **README** file for the **Crypto Wallet** project. This version improves clarity, structure, grammar, and tone while preserving all technical details:

---

# 🔐 Crypto Wallet

**Crypto Wallet** is a Flask-based web application designed for managing Ethereum wallets on the **Sepolia testnet**. It allows users to register securely, configure Ethereum wallets, view balances, send and receive transactions, and access transaction history — all through an elegant and responsive UI.

The application features modern design aesthetics using **Tailwind CSS**, **Alpine.js**, and **Anime.js**, with support for **dark mode**, responsive layouts, and animated interactions.

---

## 🚀 Features

* **🔐 User Authentication**: Register, login, and logout with secure password hashing.
* **👛 Wallet Management**: Add and manage your Ethereum wallet (private key is encrypted and securely stored).
* **💸 Send Transactions**: Transfer ETH on the Sepolia testnet.
* **🧾 Transaction History**: View detailed records of your past transactions.
* **📷 QR Code Support**: Generate a QR code for easily receiving funds.
* **🌙 Dark Mode**: Toggle light/dark themes with persistent local storage support.
* **🎨 Modern UI**: Designed with Tailwind CSS and glassmorphism, animated using Anime.js.
* **⚠️ Client-side Validation**: Forms include visual feedback and animations for invalid inputs.

---

## 🛠 Prerequisites

Before setting up the project, ensure the following tools are installed:

* Python 3.8+
* pip (Python package manager)
* Git
* Code editor (e.g., VS Code)
* Ethereum wallet (e.g., MetaMask with Sepolia testnet ETH)
* [Infura](https://infura.io/) account for Sepolia testnet access

---

## ⚙️ Installation Guide

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/crypto-wallet.git
cd crypto-wallet
```

> Replace `your-username` with your actual GitHub username or use the correct repository URL.

### 2. Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

If `requirements.txt` is missing, create one with:

```
Flask==2.3.2
Flask-SQLAlchemy==3.0.5
Flask-Bcrypt==1.0.1
Flask-Login==0.6.2
web3==6.11.0
qrcode==7.4.2
cryptography==42.0.8
```

Then run the install command again.

### 4. Initialize Databases

* **User Database (`users.db`)**: Created automatically on first app launch.
* **Transaction Database (`wallet.db`)**: Created when `init_db()` is triggered in `app.py`.

### 5. Configure Environment Variables

Update the Infura URL in `app.py`:

```python
INFURA_URL = "https://sepolia.infura.io/v3/YOUR_INFURA_PROJECT_ID"
```

To secure secrets:

1. Install `python-dotenv`:

```bash
pip install python-dotenv
```

2. Create a `.env` file in the root:

```
INFURA_PROJECT_ID=your_infura_project_id
FLASK_SECRET_KEY=your_secret_key
```

3. Load it in `app.py`:

```python
from dotenv import load_dotenv
import os

load_dotenv()
app.secret_key = os.getenv('FLASK_SECRET_KEY', 'crypto')
INFURA_URL = f"https://sepolia.infura.io/v3/{os.getenv('INFURA_PROJECT_ID')}"
```


---

## ▶️ Running the Application

Activate the virtual environment:

```bash
source venv/bin/activate  # Windows: venv\Scripts\activate
```

Start the server:

```bash
python app.py
```

Open your browser at:
📍 `http://127.0.0.1:5000`

---

## 🧭 Usage Instructions

### 1. Register

Visit `/register` to create a new user account.

### 2. Wallet Setup

After registering, input your Ethereum address and private key (from MetaMask). Make sure your wallet is funded with Sepolia testnet ETH ([Get it here](https://sepoliafaucet.com)).

### 3. Dashboard (`/`)

* **👁️ View Wallet**: Displays your address and real-time ETH balance.
* **📤 Send ETH**: Transfer ETH to any Ethereum address.
* **🧾 Transaction History**: View previous transactions.
* **📥 Receive ETH**: Get a QR code for your wallet address.

### 4. Dark Mode

Use the toggle in the navbar to switch between light and dark themes.

---

## 🔧 Customization

### 🔑 Infura API Key

* Update `INFURA_URL` in `.env` or `app.py`.

### 🔐 Flask Secret Key

Generate a secure key using:

```python
import secrets
print(secrets.token_hex(16))
```

Add it to `.env`:

```
FLASK_SECRET_KEY=your_new_secure_key
```

### 🌐 Network Configuration

To switch from Sepolia to another Ethereum network, update:

```python
INFURA_URL = "https://mainnet.infura.io/v3/YOUR_KEY"
'chainId': w3.eth.chain_id  # Ensures correct chain ID
```

⚠️ Mainnet requires **real ETH**, use with caution.

### 🎨 Styling & Animations

* Tailwind colors: Customize in `base.html` or `tailwind.config`.
* Anime.js parameters: Modify duration, easing, delay for desired effects.

---

## 📁 Project Structure

```
crypto-wallet/
├── static/
│   └── logo.png
├── templates/
│   ├── base.html
│   ├── index.html
│   ├── login.html
│   ├── register.html
│   ├── setup_wallet.html
│   ├── wallet.html
│   ├── send_transaction.html
│   ├── transaction_history.html
│   ├── receive.html
│   └── transaction_result.html
├── app.py
├── wallet.py
├── requirements.txt
├── users.db
├── wallet.db
└── .env
```

---

## 🛠 Troubleshooting

| Issue                    | Solution                                                         |
| ------------------------ | ---------------------------------------------------------------- |
| Invalid Ethereum address | Must start with `0x` and be 42 characters long                   |
| Invalid private key      | Should start with `0x` and be 66 characters                      |
| Insufficient funds       | Use [Sepolia faucet](https://sepoliafaucet.com)                  |
| Wallet not set up        | Go to `/setup_wallet` after registering                          |
| Dark Mode not working    | Ensure Tailwind's `darkMode: 'class'` is configured              |
| Database errors          | Delete `users.db` & `wallet.db` to reset (all data will be lost) |

---

## 🔐 Security Best Practices

* **Private Key Encryption**: Encrypted with the user’s password. For production, consider hardware wallets or vaults.
* **Environment Variables**: Never hard-code secrets in source code.
* **HTTPS**: Always deploy with SSL for secure data transmission.
* **Server-side Validation**: Add backend validation to complement frontend checks.

---

## 🚀 Deployment Guide

To deploy on Heroku, Render, or AWS:

1. Use a WSGI server:

```bash
pip install gunicorn
gunicorn -w 4 app:app
```

2. Switch to a production-grade database like PostgreSQL:

```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://user:pass@host:port/dbname'
```

3. Serve static assets with a reverse proxy (e.g., Nginx).

---

## 🤝 Contributing

1. Fork this repository.
2. Create your branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m "Add feature"`
4. Push to your branch: `git push origin feature/my-feature`
5. Open a pull request.

---

## 📄 License

This project is licensed under the **MIT License**.
See the [LICENSE](./LICENSE) file for more information.

---

## 📬 Contact

Have questions, suggestions, or feedback?
Open an issue on GitHub or reach out at **\[[your-email@example.com](mailto:your-email@example.com)]**

---

Let me know if you’d like this as a downloadable `README.md` file or need badges (e.g., build status, license, version).
