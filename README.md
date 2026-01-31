# Telegram Voice Transcriber

Telegram bot that transcribes voice messages using OpenAI Whisper. Built with n8n.

```
Voice Message → Download → Transcribe → Reply with Text
```

## Setup

**Prerequisites:** n8n instance, Telegram bot token, OpenAI API key

1. Import `workflow.json` into n8n
2. Add credentials (Telegram API + OpenAI API)
3. Activate workflow

## Usage

Send a voice message to your bot → receive transcription.

Works with any user, including forwarded voice messages.
