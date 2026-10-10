# 🏙 MINNA LIFESTYLE — Multiplayer Simulation MMORPG

**Phase 1 (Core MVP)** built from the *Minna Lifestyle Blueprint*.
DOM + Tailwind client · Node.js/Express · Socket.io · JSON payload schemas · persisted world state.

## ▶ Run it

```bash
npm install
npm start          # → http://localhost:3000
npm run dev        # auto-reload server
npm test           # two-player e2e smoke test (server must be running)
```

Open two browser tabs to see multiplayer live.

## ✅ What's in Phase 1 (blueprint §1–§4)

| Blueprint spec | Status | Where |
|---|---|---|
| Peer-to-Peer Assistance Matrix (reason + Naira modal) | ✅ | 🆘 button on any player in your sector |
| Gifts **and** loans with payback days + interest | ✅ | Request type selector → terms fields |
| Borrowing & Lending Ledger, defaults → Street Cred drop | ✅ | 📒 LEDGER panel + loan tick |
| Unpaid loans block elite venues (Tunga) | ✅ | `canEnterTunga()` — debtors + cred < 30 gated |
| Chat: Global / Local (per node) / Direct whispers | ✅ | Chat tabs + 💬 on players |
| Yan Sara-Suka night spawns (10PM–5AM, Maitumbi/Chanchaga/Kpakungu) | ✅ | `nightSpawns()` + roam/arrival rolls |
| Parties split risk | ✅ | 👥 invite — crew cuts mugging odds, travels together |
| NPF checkpoints + Suspicion Meter + settle-or-jail | ✅ | Jail locks UI 5 real minutes (with smuggled-phone chat) |
| JTF curfew 11:30PM → 95% Energy drain, no fine bypass | ✅ | `travel()` curfew intercept |
| Yansakai levy → offline looting to 0% | ✅ | Buy shop at IBB → pay levy |
| 7 map nodes with risk tiers & economies | ✅ | 🗺️ travel map with live player counts |
| `REQUEST_ASSISTANCE` JSON schema (§4) | ✅ | `assist:request` payload, tested in e2e |
| Suspicion from apparel / vehicles / high payouts | ✅ | Designer suit +15 👁 · Camry +12 👁 · jackpots +6 👁 |
| Bank vaults (mug-proof storage) | ✅ | 🏦 panel, Tunga only |
| Inventory / consumables | ✅ | 🎒 BAG + 🛍 MARKET |

**Not yet in Phase 1** (Phase 2/3 per §5): Canvas/Phaser 2D world & sprite movement, faction hierarchies, corporate ventures, real payments.

## 🎮 How to play

1. **Enter Minna** — pick a street name, residence (your curfew-safe hub), spawn node. You start with ₦30,000, 💚50, ⚡100.
2. **Hustle** in your zone (each node has its own gigs and pay grades).
3. **Open the map** and travel — Tunga gates you by Street Cred; risky routes after 11:30PM.
4. **Night is the real game** — high-danger nodes spawn muggers; band together in parties.
5. **Social economy** — 🆘 any player in your sector for gifts/loans; 📒 track everything.
6. **Survive suspicion** — Lay Low, First Aid Wraps, or settle checkpoints before jail.

## 🏗 Architecture

```
server/
  index.js            Express + Socket.io wiring, rooms, chat channels
  game/config.js      Zones, hustles, items, residences, tunables
  game/state.js       Players, loans, parties, JSON persistence (server/data/save.json)
  game/mechanics.js   Clock tick, travel, risk encounters, economy, arrests
  game/assistance.js  Assistance matrix, ledger defaults, parties
public/               Tailwind CDN client (HUD, panels, modals, chat)
scripts/e2e.test.js   Two-player integration test (14 checks)
```

- **World clock:** 1 real second = 1 game minute (full day ≈ 24 real min). Server-authoritative.
- **Persistence:** auto-saves every 30s; characters resume by name on rejoin.

## 🚀 Going online (Phase 1 deploy)

The blueprint's Vercel plan works for the **static client**, but Socket.io needs a long-lived process:

1. **Client** → deploy `public/` to Vercel/Netlify.
2. **State worker** → deploy the Node server to Render / Railway / Fly.io (`npm start`, set `PORT`).
3. Point the client at the server: change `io()` → `io('https://your-worker.onrender.com')` in `public/js/app.js`.

## 📍 Roadmap

- **Phase 1 (now):** text/button MVP, chat, assistance, risk matrices, ledger ✅
- **Phase 2:** Phaser.js Canvas layer — avatars walking Tunga/Bosso/IBB, sprite sync over websockets
- **Phase 3:** faction ladders (Government House politics, Yansakai command), multi-user corporate ventures
