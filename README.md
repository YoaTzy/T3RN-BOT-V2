# T3RN Bridge Bot
![image](https://github.com/user-attachments/assets/31d8b73f-56c1-4161-b3e8-01f4b9bae6d8)
![image](https://github.com/user-attachments/assets/c26d0c64-bd8d-477e-9389-32036e5a8c7f) 
![image](https://github.com/user-attachments/assets/2fa7d90e-8b84-44ec-a7b4-38f320b05e4e)



A powerful, user-friendly bot for automating transactions across T3RN bridge networks including Arbitrum Sepolia, Optimism Sepolia, and Base Sepolia. Features a rich terminal interface, custom delay settings, and IP-based access control.

## Features

- 🌉 Automated bridging between multiple networks (Arbitrum, Optimism, Base)
- 📊 Rich terminal UI with colorful tables and progress indicators
- ⚙️ Customizable delays for accounts, bridges, and transaction cycles
- 🔄 Retry mechanisms with intelligent error handling for transaction failures
- 💰 Multi-account support with account balance monitoring
- ⏱️ Custom bridge-specific and network-specific delay settings
- 🔐 IP whitelist system with automatic trial mode for new users
- 🌐 Time zone-aware authentication (WIB - Western Indonesian Time)

## Prerequisites

- Python 3.8 or higher
- Private keys for the accounts you want to use
- Sufficient ETH balance on source networks

## Installation

**It is mandatory to use a virtual environment (venv) for this project.**

### Linux Installation

```bash
# Clone the repository
git clone https://github.com/YoaTzy/T3RN-BOT-V2.git
cd T3RN-BOT-V2

# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate

# Install dependencies
pip install web3 rich pytz requests pyTelegramBotAPI

# Run the bot
python3 main.py
```

### Windows Installation

```powershell
# Clone the repository
git clone https://github.com/YoaTzy/T3RN-BOT-V2.git
cd T3RN-BOT-V2

# Create virtual environment
python -m venv venv

# Activate virtual environment
venv\Scripts\activate

# Install dependencies
pip install web3 rich pytz requests pyTelegramBotAPI

# Run the bot
python main.py
```

## Configuration
Replace `YOUR_PRIVATE_KEY` and `YOUR_ADDRESS` with your actual wallet details.

## Obtaining Bridge Data

The `data_bridge` section in your config.json contains the transaction data needed for each bridge operation. This data is **amount-specific**, meaning if you change the bridge amount, you must update the bridge data accordingly.

### How to obtain bridge data:

1. **Using Browser Developer Tools**:
   - Visit the T3RN bridge website (https://bridge.t2rn.io/ or https://unlock3d.t3rn.io/)
   - Open your browser's developer tools (F12 or right-click > Inspect)
   - Go to the Network tab
   - Set the amount you want to bridge (e.g., 0.1 ETH)
   - Initiate a bridge transaction (but don't confirm it in your wallet)
   - Look for web3 API calls in the Network tab (filter by "eth" or "RPC")
   - Examine the request payload - you'll find the transaction data in the `data` field
   - Copy the hex string (beginning with "0x...")

2. **From Successful Transactions**:
   - If you've previously completed a bridge transaction with the desired amount
   - Look up the transaction on the blockchain explorer
   - The `Input Data` field contains the bridge data you need

3. **From Wallet (Metamask)**:
   
![image](https://github.com/user-attachments/assets/464e63a4-ba23-4d5d-8f7d-94742f90cabb)

### Updating Bridge Data When Changing Amount
Each time you change the `bridge_amount` in your config.json, you must:

1. Obtain new bridge data for each route using the steps above
2. Update the corresponding entries in the `data_bridge` section
3. Save the config.json file

Example of bridge data for a 0.1 ETH transaction:
```
"OP - Arbitrum": "0x56591d59617262740000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002342Zh73f3452300000000000000000000000000000000000000000000000001631652d53d850000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000016345785d8a0000"
```

For a different amount, the data would be different. Always ensure your bridge data matches your intended bridge amount.

### Important Notes on Bridge Data

- The bridge data includes the amount, so if you change the amount in settings but don't update the data, the original amount will be used
- Different routes (e.g., OP → Arbitrum vs Arbitrum → OP) require different data even for the same amount
- If you're unsure, use the browser method to capture the correct data for your desired amount

## IP Whitelist System

The bot includes an IP-based access control system, which uses a whitelist stored on GitHub:

- **Whitelist Location**: https://raw.githubusercontent.com/YoaTzy/ip-whitelist/refs/heads/main/allow
- **Format**: Each line should contain an IP address and expiry date in DD-MM-YYYY format
- **Example**: `159.89.177.95 25-03-2099`

New users whose IPs are not in the whitelist automatically receive a 10 minute trial before they need to request full access.

## Usage

1. Activate your virtual environment:
   - Linux: `source venv/bin/activate`
   - Windows: `venv\Scripts\activate`

2. Run the bot:
   ```
   python main.py
   ```

3. Use the interactive menu to:
   - Run specific bridges
   - Run all bridges in sequence
   - Create custom bridge sequences
   - Configure bridge amounts
   - Set custom delay times

## Credits

- **Developer**: Yoake ([Telegram: @yoakeid](https://t.me/yoakeid))
- **Libraries**: 
  - [Web3.py](https://github.com/ethereum/web3.py)
  - [Rich](https://github.com/Textualize/rich)
  - [PyTZ](https://github.com/stub42/pytz)
  - [Requests](https://github.com/psf/requests)
  - pyTelegramBotAPI

## License

This project is proprietary software. All rights reserved.

---

For support, feature requests, or to get whitelisted access, contact the developer on Telegram: [@yoakeid](https://t.me/yoakeid)
