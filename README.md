# Game Study

## Running Locally

Audio recording requires HTTPS. Generate a certificate and start the server:

```bash
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes -subj "/CN=localhost"

python3 https_server.py
```

Then visit https://localhost:8443/game.html (accept the certificate warning).

## Data Format

Exported JSON contains:
- `session`: gameId, startTime, duration
- `frames`: keystroke actions with game state
- `gaze`: array of `[gridX, gridY, timestamp]` tuples (null values = off-grid)

## Known Inconsistencies

### game2.html
- Uses 1-indexed grid coordinates (1-5) while game.html (0-5) and game3.html (0-6) use 0-indexed
- Does not have a `generateGameStateMatrix()` function like the other games; grid state is captured differently in `getGameState()`
