> **Note:** This project is a fork of [sarim-hk/CS2Stats](https://github.com/sarim-hk/CS2Stats), originally created by Sarim.

<p align="center">
  <img src="https://css.scorix.ro/images/metrics2.png" alt="METRICS2 Metrics" />
</p>

# METRICS2

A Counter-Strike 2 server plugin for advanced match statistics, demo recording, and ELO tracking.  
Stores match, round, player, and event data in a MySQL database for analysis and web integration.

---

## Features

- Tracks all match rounds, player stats, and in-game events (kills, assists, deaths, damage, flashes, grenades, clutches, duels, etc.)
- Records and manages match demos
- Integrates with Steam API for player info and avatars
- ELO rating system for teams and players
- Real-time live data tables for web overlays or dashboards

---

## Requirements

- .NET 8.0
- MySQL server
- CounterStrikeSharp API
- Steam API key

---

## Installation

1. **Build the plugin**  
   Clone the repository and build with .NET 8.0 SDK:
   ```sh
   dotnet build -c Release Deploy
   ```
   Copy the compiled plugin files to your Counter-Strike 2 server's plugin directory.

2. **Configure**  
   Edit the generated config file (e.g., `config.json`) with your MySQL and Steam API credentials.

   Example `config.json`:
   ```json
   {
     "MySQLServer": "localhost",
     "MySQLDatabase": "cs2stats",
     "MySQLUsername": "user",
     "MySQLPassword": "password",
     "SteamAPIKey": "YOUR_STEAM_API_KEY",
     "DemoRecordingEnabled": "1"
   }
   ```
   - `DemoRecordingEnabled`: Set to `"1"` to enable demo recording, `"0"` to disable.

3. **Database**  
   Execute the provided SQL script to create the necessary tables in your MySQL database.

---

## Usage

### Console Commands

| Command             | Description                       |
|---------------------|-----------------------------------|
| `cs2s_start_match`  | Start a new match                 |
| `cs2s_cancel_match` | Cancel the current match (no save)|

- Only the server console can run these commands (not players).
- Match data is automatically saved at the end of a match.

---

## How it works

- On `cs2s_start_match`, the plugin collects all human players, assigns them to teams, and starts tracking the match.
- All rounds, events, and player actions are logged to the database.
- At match end, ELO is updated and results are stored.
- If enabled, a demo is recorded for the match.

---

## Database

The plugin creates and uses several tables (e.g., `CS2S_Match`, `CS2S_Round`, `CS2S_PlayerInfo`, etc.).  
See the source code and SQL scripts for schema details.

---

## Development

- Requires .NET 8.0 SDK and MySQL.
- Uses CounterStrikeSharp API.
- Contributions welcome! Open issues or pull requests for improvements.

---

## License

MIT  
Original author: Sarim (https://github.com/sarim-hk)
