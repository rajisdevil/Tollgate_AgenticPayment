
Toll_Gate Agentic_Payment

# 🚦 TollGate
**Autonomous payment rails for machines, built on HTTP 402 (`x402`).**

> *Machines decide at machine speed, but cannot pay at machine speed. TollGate fixes that.*

### 📌 Project Brief
**TollGate** is an autonomous machine-to-machine (M2M) payment operating layer built around the open **HTTP 402 (`Payment Required`) / x402** standard. Traditional payment rails fail autonomous machines due to **human gates** (passwords, OTPs, CAPTCHAs), **high fixed fees** that dwarf sub-cent API calls, and **billing mismatches** where monthly invoices cannot price a single GPU-second or sensor reading.

TollGate enables AI agents and constrained IoT devices to pay for APIs, compute, and live data feeds in **two standard HTTP requests**—with no account creation, no pre-shared API key, no OTP, and no human in the loop:

1. **Request:** An AI agent or IoT sensor calls a paid API, GPU node, or data endpoint.
2. **Quote (`402 Payment Required`):** The server replies `402` with the exact price, stablecoin token, payee address, and a short-lived nonce.
3. **Pay & Retry:** The buyer wallet verifies its local spend policy, cryptographically signs within its owner-backed mandate, and resends the request with payment proof.
4. **Verify (`200 OK`):** The Facilitator confirms the proof via Redis in milliseconds, queues the voucher for batched settlement, and the server returns `200 OK` with the resource.

### ✨ What TollGate Adds Around the Standard
- 🛡️ **Spend Policies & Security:** Per-call caps, daily budgets, payee allowlists, owner-backed mandates, replay protection (nonces), price lock, automatic refund hooks, and an emergency **Agent Kill Switch**.
- ⚡ **Batched Stablecoin Settlement:** Aggregates thousands of sub-cent micro-calls into a single low-fee stablecoin transaction so network fees stay strictly below call prices.
- 📡 **IoT Gateway (MQTT & HTTP Bridge):** Enables constrained microcontrollers (e.g., ESP32/Arduino sensors) too small to hold cryptographic keys to pay autonomously through a local gateway.
- 💻 **Drop-In SDKs & Control Plane:** Few-line TypeScript seller paywall middleware, Python buyer agent wallet SDK, a Discovery Registry, and a React Control Plane backed by PostgreSQL and Redis.

### 🛠️ Tech Stack
- **Protocol:** HTTP 402 (`x402` open standard)
- **SDKs:** TypeScript & Python
- **Backend & Facilitator:** PostgreSQL (ledger & audit log) + Redis (fast balance, voucher & nonce checks)
- **Control Plane:** React Dashboard
- **IoT Layer:** Lightweight MQTT & HTTP Bridge
- **Settlement:** Stablecoin on a low-fee network (testnet first)

### 👥 Team CtrlC_CtrlV — Academy of Technology
- **Sayan Kr. Shyamal** (Team Leader) — `sayan.kumarshyamal.25@aot.edu.in`
- **Rajesh Mondal** (Team Member)
- **Suhrit Ghosh** (Team Member)
- **Kanchan Dey** (Team Member)


## 🙏 Acknowledgements
🏫 Academy of Technology (AOT): Faculty mentors and fellow student innovators for supporting Team CtrlC_CtrlV.

🌐 The Open x402 Community: For championing the revival of RFC 9110 HTTP 402 Payment Required for autonomous machine commerce.

🛠️ Open-Source Ecosystem: Built with TypeScript, Python, PostgreSQL, Redis, React, Tailwind CSS, Lucide Icons, and Eclipse Mosquitto MQTT.

## API Reference

#### Get all items

```http
  GET /api/items
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `api_key` | `string` | **Required**. 🔑 X-402-Nonce|

#### Get item

```http
  GET /api/items/${id}
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. 🔏 X-402-Proof |

#### add(num1, num2)

Takes two numbers and returns the sum.


## 📎 Appendix
A. 3-Phase Implementation Feasibility Summary

🚀 PHASE 1 | PROVE (Testnet MVP): Paywall middleware for a sample API, agent client with a spend-policy wallet, and a live demo where an AI agent buys data and an IoT sensor buys compute.

🛡️ PHASE 2 | HARDEN (Sessions & Devices): Batched session settlement, MQTT/HTTP IoT gateway for constrained devices, React policy dashboard, and full PostgreSQL audit log.

🌍 PHASE 3 | PILOT (Real-World Traffic): Partner with a data marketplace or GPU provider, integrate a fiat on/off-ramp via a regulated partner, and complete an end-to-end security review before mainnet launch.


B. Feasibility Pillars

⚙️ Technical: The handshake is the open x402 standard; TollGate builds the enterprise operating layers around it.

💰 Economic: Batched settlement keeps network transaction fees strictly below the price of an individual sub-cent API call.

⚖️ Regulatory: Regulated partners handle KYC and fiat on/off-ramps at the edges while strict payee allowlists enforce counterparty compliance.## Color Reference

| Color             | Hex                                                                |
| ----------------- | ------------------------------------------------------------------ |
| Example Color | ![#0a192f](https://dummyimage.com/10/0a192f/white?text=+) #0a192f |
| Example Color | ![#f8f8f8](https://dummyimage.com/10/f8f8f8/white?text=+) #f8f8f8 |
| Example Color | ![#00b48a](https://dummyimage.com/10/00b48a/white?text=+) #00b48a |
| Example Color | ![#00d1a0](https://dummyimage.com/10/00d1a0/white?text=+)) #00d1a0 |
## 🤝 Contributing

Contributions are always welcome!

Contributions, issues, and feature requests from the open-source agentic commerce community are welcome!

	1.	🍴 Fork the Project
	2.	🌿 Create your Feature Branch (git checkout -b feature/AmazingPaymentFeature)
	3.	📝 Commit your Changes (git commit -m 'feat: add new spend policy rule')
	4.	🚀 Push to the Branch (git push origin feature/AmazingPaymentFeature)
	5.	🔀 Open a Pull Request
    
Please ensure all TypeScript (@tollgate/seller-sdk) and Python (tollgate-sdk) changes include unit tests for replay protection and spend-cap enforcement.


## 🚀 Deployment


1. Deploy the Interactive Web Showcase (index.html)
Because index.html is a self-contained single-file application, it deploys in seconds with zero build configuration:

```
# Deploy via Vercel CLI
npx vercel --prod

# Deploy via Netlify CLI
npx netlify deploy --prod --dir=.

```

2. Deploy the Full Backend Stack (Docker Compose)
```
# Clone the repository
git clone [https://github.com/CtrlC-CtrlV/tollgate-x402.git](https://github.com/CtrlC-CtrlV/tollgate-x402.git)
cd tollgate-x402

# Copy environment variables
cp .env.example .env

# Start PostgreSQL, Redis, MQTT Broker, Facilitator API, and React Control Plane
docker compose up -d --build


```
## 📚 Documentation

Project Presentation Deck (https://www.google.com/search?q=./docs/TollGate_Project_Deck.pdf): Full 9-slide Ideathon deck covering the problem statement, 4-step x402 flow, system architecture, tech stack justification, security plan, and 3-phase feasibility analysis.

https://www.google.com/search?q=./(SHOWCASE_README.md): Step-by-step walkthrough for demonstrating the live HTTP 402 simulator to Ideathon judges.

Buyer & Seller SDK Quickstarts:
Seller Middleware (@tollgate/seller-sdk): Wrap any Express/Fastify endpoint with tollgatePaywall({ price, token, payee, facilitatorUrl }).
Buyer Agent Client (tollgate-sdk): Initialize AgentWalletClient(owner_mandate, per_call_cap_usdc, daily_budget_usdc, allowlist) in Python or TypeScript to automatically negotiate 402 responses.

IoT Gateway (iot-gateway): Publish JSON payloads over MQTT (device_id, target_url, max_price_usdc, payload) from ESP32/Arduino sensors.

## 🔐 Environment Variables
To run the Facilitator backend, Seller Paywall Middleware, Buyer Agent SDK, and IoT Gateway, create a .env file in the root directory and configure the following variables:

    # --- Facilitator Backend (PostgreSQL + Redis) ---
PORT=8080
DATABASE_URL=postgresql://tollgate_user:password@localhost:5432/tollgate_ledger
REDIS_URL=redis://localhost:6379
QUOTE_TTL_SECONDS=30
BATCH_SETTLEMENT_THRESHOLD_USDC=1.00

# --- Settlement Layer (Low-Fee Stablecoin Network) ---
STABLECOIN_NETWORK=testnet-l2
STABLECOIN_RPC_URL=[https://rpc.testnet.tollgate.network](https://rpc.testnet.tollgate.network)
STABLECOIN_TOKEN_ADDRESS=0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48
FACILITATOR_SIGNER_PRIVATE_KEY=0x_YOUR_FACILITATOR_TESTNET_KEY

# --- Seller Paywall Middleware ---
SELLER_PAYEE_ADDRESS=0x71C89A000000000000000000000000000000F42B
FACILITATOR_API_URL=http://localhost:8080/api/v1

# --- Buyer Agent Wallet & Spend Policy ---
OWNER_MANDATE_SIGNATURE=sig_owner_0x99a8f7c6b5e4d3...
AGENT_PRIVATE_KEY=0x_YOUR_ISOLATED_AGENT_KEY
DEFAULT_PER_CALL_CAP_USDC=0.015
DAILY_BUDGET_USDC=5.00
PAYEE_ALLOWLIST=api.marketfeed.io,gpu.compute.sh

# --- IoT Gateway (MQTT -> HTTP 402 Bridge) ---
MQTT_BROKER_URL=mqtt://localhost:1883
IOT_GATEWAY_TOPIC=tollgate/iot/requests


## Features

- Light/dark mode toggle
- Live previews
- Fullscreen mode
- Cross platform


## Installation

Install my-project with npm

```bash
  npm install my-project
  cd my-project
```
    
## Lessons Learned

What did you learn while building this project? What challenges did you face and how did you overcome them?


## License

[MIT](https://choosealicense.com/licenses/mit/)

## Related

Here are some related projects

[Awesome README](https://github.com/matiassingers/awesome-readme)


## Roadmap

- Additional browser support

- Add more integrations


## Run Locally

Clone the project

```bash
  git clone https://link-to-project
```

Go to the project directory

```bash
  cd my-project
```

Install dependencies

```bash
  npm install
```

Start the server

```bash
  npm run start
```


## Support

For support, email letsmailrajeshmondal@gmail.com or join our Slack channel.


## Tech Stack

**Client:** React, Redux, TailwindCSS

**Server:** Node, Express


## Running Tests

To run tests, run the following command

```bash
  npm run test
```


## Usage/Examples

```javascript
import Component from 'my-project'

function App() {
  return <Component />
}
```


## Used By

TollGate is designed to be used by autonomous machines, AI agents, automated scripts, and resource-constrained IoT devices that need to make sub-cent micro-transactions at machine speed without human intervention.
Specifically, the ecosystem serves:

- Company 1: AI Agents & LLM Frameworks (Buyer Side): Autonomous software agents built in Python or TypeScript that query paid APIs, LLM endpoints, or data feeds and automatically negotiate HTTP 402 payment quotes using policy-constrained wallets.

- Company 2: Resource-Constrained IoT Sensors (IoT Gateway): Microcontrollers and edge sensors (such as ESP32 and Arduino nodes) that are too small to store cryptographic private keys, using the lightweight MQTT-to-HTTP bridge to pay for compute and data feeds autonomously.

- Company 3: API & GPU Compute Providers (Seller Side): Developers and infrastructure providers who protect endpoints with TollGate's paywall middleware to monetize API calls, GPU seconds, and real-time data feeds per request.

- Company 4: Enterprise Finance & Compliance Teams (Control Plane): Engineering managers and finance officers who use the unified React dashboard to set spend caps, monitor live agent telemetry, inspect immutable PostgreSQL audit logs, and trigger emergency kill switches.


## 👥 Authors
Team Name: CtrlC_CtrlV

Institution: Academy of Technology (AOT)

Ideathon Theme: Agentic Payment Rails

    🧑‍💻 Rajesh Mondal — Team Member 1 • Academy of Technology
    👨‍💻 Sayan Kr. Shyamal — Team Member 2 • Academy of Technology
    🧑‍💻 Suhrit Ghosh — Team Member 3 • Academy of Technology
    🧑‍💻 Kanchan Dey — Team Member 4 • Academy of Technology


[@Rajesh_Mondal](https://www.github.com/rajisdevil)


## 🚀 About Me
I'm a full stack developer...


# Hi, I'm Rajesh! 👋


## 🔗 Links
[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://rajesh-portfolio-silk.vercel.app/)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rajeshtechie)
[![twitter](https://img.shields.io/badge/twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/)


## Other Common Github Profile Sections
👩‍💻 I'm currently working on developing TollGate, an autonomous machine-to-machine payment protocol built on HTTP 402 for AI agents and IoT sensors, alongside ESP32-based hardware telemetry displays.

🧠 I'm currently learning advanced embedded systems firmware optimization, secure cryptographic voucher verification, and real-time serial communication protocols.

👯‍♀️ I'm looking to collaborate on open-source AI agent tooling, autonomous M2M payment rails, and physical computing/microcontroller prototyping projects.

🤔 I'm looking for help with scaling low-fee stablecoin batch-settlement architectures and building robust TypeScript/Python SDK wrappers for agent wallets.

💬 Ask me about working with ESP32-S3 boards, Arduino prototyping, SSD1306 OLED interfaces, Processing GUI data visualizers, and HTTP 402 machine commerce architecture.

📫 How to reach me reach out via email at rajesh.mondal.25@aot.edu.in or connect through Team CtrlC_CtrlV!

😄 Pronouns: He/Him

⚡️ Fun fact: I love combining physical hardware sensors with custom software interfaces, and when I'm away from the IDE, you can usually find me out riding my commuter motorcycle.


## 🛠 Skills
Javascript, HTML, CSS...


## Badges

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
[![GPLv3 License](https://img.shields.io/badge/License-GPL%20v3-yellow.svg)](https://opensource.org/licenses/)
[![AGPL License](https://img.shields.io/badge/license-AGPL-blue.svg)](http://www.gnu.org/licenses/agpl-3.0)


## ❓ FAQ

#### Question 1: Why use HTTP 402 (x402) instead of API keys or monthly Stripe subscriptions?

Answer: API keys and monthly subscriptions require a human to sign up, enter credit card details, pass CAPTCHAs/OTPs, and commit to a recurring bill. With HTTP 402, an autonomous AI agent can discover a brand-new API or GPU node and pay $0.002 for a single call on the fly in two HTTP requests without human intervention.


#### Question 2: How do you prevent network fees from costing more than a sub-cent API call?

Answer: TollGate uses Batched Settlement. Individual calls are verified off-chain in milliseconds using signed cryptographic vouchers cached in Redis, and thousands of micro-calls are rolled into one stablecoin transaction on a low-fee network.

#### Question 3: How can a tiny microcontroller (like an ESP32 or Arduino sensor) pay if it cannot hold private keys?

Answer: Constrained devices communicate with the TollGate IoT Gateway over a lightweight MQTT/HTTP bridge. The gateway holds the keys, enforces the device's spend policy, and executes the HTTP 402 handshake on behalf of the sensor.

#### Question 4: What happens if an AI agent hallucinates, loops infinitely, or gets hijacked?

Answer: Every agent operates under strict Spend Policies (hard per-call caps, daily budgets, and payee allowlists) tied to an Owner-Backed Mandate. If an agent exceeds its cap, the wallet refuses to sign. Owners can also trigger the 1-Click Emergency Kill Switch in the React Control Plane to revoke an agent's key immediately.

#### Question 5: What happens if a seller's API crashes after the agent has already paid?

Answer: TollGate includes Refund Hooks in the Facilitator layer. If the downstream server fails to deliver a valid 200 OK response within the timeout window, the voucher is voided and credited back to the buyer's balance automatically.


## 💬 Feedback

If you have any feedback, questions from the judging panel, or partnership inquiries regarding GPU/data marketplace pilots, please reach out to:
✉️ Email: rajesh.mondal.25@aot.edu.in (Rajesh Mondal — Team CtrlC_CtrlV)

🐛 GitHub Issues: Open an issue in this repository for bug reports or protocol proposals.
