# Mavi Kanat

A one-tap flying game for the Bay Mavi Telegram bot. It is a single static page
(`index.html`: canvas, no build step, no dependencies besides Telegram's Web App SDK)
hosted on GitHub Pages.

## How scores work

There is no game server. The page runs as a Telegram Mini App opened from the bot's
**🎮 Oyna** reply-keyboard button:

1. The bot builds the button URL as `index.html?kb=1&lb=<base64url JSON>`, where the
   JSON is `{"top": [[name, score], ...], "me": [rank, best]}` (the current top 10).
2. After a run the player taps **Skoru Gönder**. The page calls
   `Telegram.WebApp.sendData('{"t":"mk1","score":N,"secs":S}')`; Telegram closes the
   game and delivers the data to the bot as a `web_app_data` message.
3. The bot stores the player's best score, then replies with the top 10 and a fresh
   button.

Opened outside the bot's keyboard button, the page still plays: inside Telegram it
points the player to the bot; in a normal browser it keeps a top 10 on the device.

## Files

- `index.html` – the whole game (art is drawn in code; the logo is embedded).
- `assets/logo128.jpg` – source of the embedded logo.
