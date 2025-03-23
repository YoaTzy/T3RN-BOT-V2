# T3RN Bridge Bot
![image](https://github.com/user-attachments/assets/31d8b73f-56c1-4161-b3e8-01f4b9bae6d8)
![image](https://github.com/user-attachments/assets/c26d0c64-bd8d-477e-9389-32036e5a8c7f) 

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
pip install web3 rich pytz requests

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
pip install web3 rich pytz requests

# Run the bot
python main.py
```

## Configuration

1. Create a `config.json` file in the root directory with the following structure:

```json
{
  "networks": {
    "Arbitrum Sepolia": {
      "rpc_url": "https://sepolia-rollup.arbitrum.io/rpc",
      "chain_id": 421614,
      "contract_address": "0x22B65d0B9b59af4D3Ed59F18b9Ad53f5F4908B54"
    },
    "Base Sepolia": {
      "rpc_url": "https://sepolia.base.org",
      "chain_id": 84532,
      "contract_address": "0xCEE0372632a37Ba4d0499D1E2116eCff3A17d3C3"
    },
    "OP Sepolia": {
      "rpc_url": "https://sepolia.optimism.io",
      "chain_id": 11155420,
      "contract_address": "0xb6Def636914Ae60173d9007E732684a9eEDEF26E"
    }
  },
  "alternative_rpcs": {
    "Base Sepolia": [
      "https://sepolia.base.org",
      "https://base-sepolia-rpc.publicnode.com",
      "https://1rpc.io/base-sepolia",
      "https://base-sepolia.blockpi.network/v1/rpc/public"
    ],
    "OP Sepolia": [
      "https://sepolia.optimism.io",
      "https://optimism-sepolia.blockpi.network/v1/rpc/public",
      "https://optimism-sepolia-rpc.publicnode.com"
    ],
    "Arbitrum Sepolia": [
      "https://sepolia-rollup.arbitrum.io/rpc",
      "https://arbitrum-sepolia.blockpi.network/v1/rpc/public",
      "https://arbitrum-sepolia-rpc.publicnode.com"
    ]
  },
  "data_bridge": {
    "OP - Arbitrum": "0x56591d59617262...",
    "OP - BASE": "0x56591d5961726274...",
    "BASE - Arbitrum": "0x56591d5961726274...",
    "BASE - OP": "0x56591d5961726274...",
    "Arbitrum - BASE": "0x56591d5961726274...",
    "Arbitrum - OP": "0x56591d596f7073..."
  },
  "accounts": [
    {
      "private_key": "YOUR_PRIVATE_KEY",
      "address": "YOUR_ADDRESS",
      "label": "Account Label"
    }
  ],
  "settings": {
    "bridge_amount": 0.1,
    "explorer_urls": {
      "Arbitrum Sepolia": "https://sepolia.arbiscan.io/tx/",
      "OP Sepolia": "https://sepolia-optimism.etherscan.io/tx/",
      "Base Sepolia": "https://sepolia.basescan.org/tx/",
      "BRN": "https://b2n.explorer.caldera.xyz/txs"
    },
    "delays": {
      "between_accounts": 1,
      "between_bridges": 10,
      "between_cycles": 30
    },
    "custom_delays": {
      "bridges": {
        "OP - Arbitrum": 15,
        "OP - BASE": 12,
        "BASE - Arbitrum": 18,
        "BASE - OP": 8,
        "Arbitrum - BASE": 14,
        "Arbitrum - OP": 10
      },
      "transactions": {
        "Arbitrum Sepolia": 8,
        "OP Sepolia": 5,
        "Base Sepolia": 6
      }
    }
  }
}
```

2. Replace `YOUR_PRIVATE_KEY` and `YOUR_ADDRESS` with your actual wallet details.

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
   ![image](https://github.com/user-attachments/assets/3ef7c049-76fa-43cb-924b-037db96ecb1c)
   - If you've previously completed a bridge transaction with the desired amount
   - Look up the transaction on the blockchain explorer
   - The `Input Data` field contains the bridge data you need

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

New users whose IPs are not in the whitelist automatically receive a 1-hour trial before they need to request full access.

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
- **Framework**: T3RN Bridge Framework
- **Libraries**: 
  - [Web3.py](https://github.com/ethereum/web3.py)
  - [Rich](https://github.com/Textualize/rich)
  - [PyTZ](https://github.com/stub42/pytz)
  - [Requests](https://github.com/psf/requests)

## License

This project is proprietary software. All rights reserved.

---

For support, feature requests, or to get whitelisted access, contact the developer on Telegram: [@yoakeid](https://t.me/yoakeid)
