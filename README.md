# Night Heist

A browser-based multiplayer Police & Thieves game. One or more **Nightguards** patrol a dark office at night with a vision cone; everyone else is a **Thief** trying to loot $2,000 worth of valuables before daybreak without getting caught. No server to deploy — it's a single HTML file that talks directly to Firebase Realtime Database from the browser.

Built with [Phaser 3](https://phaser.io/) for rendering/physics and Firebase Realtime Database for multiplayer sync.

## How to play

1. Open `index.html` in a browser (or the hosted link, if this repo has GitHub Pages enabled).
2. One player clicks **Create Room** and shares the 4-letter room code with everyone else.
3. Everyone else enters that code and clicks **Join Room**.
4. Once at least 2 players are in, the host clicks **Start Match**.
5. Move with **WASD** or the **arrow keys**.

Role split scales with player count: 2-3 players → 1 Nightguard, 4-7 → 2, 8-10 → 3. Everyone else is a Thief.

- **Thieves**: see a short distance in every direction. Walk into loot piles to collect them. Get caught by stepping into a Nightguard's vision cone and line of sight — caught Thieves spectate from the locker room for the rest of the round.
- **Nightguard(s)**: only see inside a forward-facing vision cone, blocked by walls and furniture. Your vision cone shrinks when you get drowsy (a fatigue meter drains over time) — stand at the coffee machine in the Break Room for a few uninterrupted seconds to refill it.
- A round ends when the Thieves hit the loot target, every Thief is caught, or the clock runs out at daybreak. After a round ends, the host can start another round without anyone needing to rejoin.

## Running your own instance

The file ships with a working Firebase config for a demo project, but if you want your own persistent room server:

1. Go to the [Firebase console](https://console.firebase.google.com) → **Add project** (Google Analytics isn't needed).
2. **Build → Realtime Database → Create Database** → start in test mode.
3. **Project settings** (gear icon) → **Your apps** → register a Web app → copy the `firebaseConfig` object it gives you.
4. Paste those values into the `firebaseConfig` object near the top of the `<script>` tag in `index.html`.

These values identify your Firebase project — they aren't secret credentials, so it's fine to commit them in a plain HTML file.

## Project structure

This is intentionally a single-file game (`index.html`) — all HTML, CSS, and JS live together since it's a small game-jam-style project with no build step.
