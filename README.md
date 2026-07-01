# Keiko — Personal AI Assistant (n8n Workflow)

Keiko is a personal AI assistant built with [n8n](https://n8n.io/) that runs through a Telegram bot. It can:

- 💬 Chat with you naturally, with short-term memory of the conversation
- 📅 Schedule meetings on Google Calendar (extracts attendees, time, title, etc. from your message)
- 📧 Send emails via Gmail (including automatic calendar invites to meeting attendees)

## How it works

```
Telegram Trigger → AI Agent → Send Telegram Reply
                      │
        ┌─────────────┼─────────────┐
    OpenAI Chat   Simple Memory   Tools:
      Model                    - Schedule Meeting (Google Calendar)
                               - Send Email (Gmail)
```

You message the bot on Telegram → the AI Agent (powered by an OpenAI model) interprets your request → it uses the right tool if needed → it replies back to you on Telegram.

## Requirements

- An [n8n](https://n8n.io/) instance (self-hosted or cloud)
- A Telegram bot ([create one via @BotFather](https://core.telegram.org/bots#botfather))
- An OpenAI API key
- A Google account (for Calendar + Gmail access)

## Setup

1. **Import the workflow**
   - In n8n: `Workflows → Import from File` → select `keiko.json`

2. **Create credentials** (n8n will prompt you to attach these to each node)

   | Node | Credential Needed |
   |---|---|
   | Telegram Trigger / Send a text message | Telegram API (Bot Token from BotFather) |
   | OpenAI Chat Model | OpenAI API Key |
   | Schedule Meeting | Google Calendar OAuth2 |
   | Send Email | Gmail OAuth2 |

3. **Set your calendar**
   - Open the **Schedule Meeting** node and select your own Google Calendar from the dropdown (replace the placeholder value).

4. **(Optional) Personalize the assistant**
   - Open the **AI Agent** node → System Message
   - Update the sign-off name/rules to match your preferences

5. **Activate the workflow**
   - Toggle it "Active" in n8n
   - Message your Telegram bot to test it!

## Notes

- Memory is session-based (`Simple Memory` node), keyed to a fixed session — good for single-user personal use. For multi-user setups, you'd want to key sessions by chat ID instead.
- No API keys or tokens are stored in this repo — n8n keeps credentials separate from the workflow JSON. You'll need to create your own credentials as described above.

## License

MIT — see [LICENSE](LICENSE) for details.
