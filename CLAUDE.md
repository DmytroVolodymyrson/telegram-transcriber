# Telegram Voice Transcriber - Project Instructions

## Overview
n8n workflow that transcribes Telegram voice messages using OpenAI Whisper.

## Architecture
```
Telegram Trigger → IF (voice?) → Telegram Get File → OpenAI Transcribe → Telegram Send Message
                       ↓ (no)
                  Send Instructions
```

## Nodes (6 total, all native)
1. **Telegram Trigger** - Receives messages, extracts `chat.id` for replies
2. **Is Voice Message** (IF node) - Checks `$json.message.voice` exists
3. **Download Voice File** - Gets file using `voice.file_id`
4. **Transcribe Recording** - OpenAI Whisper API
5. **Send Transcription** - Replies with `$json.text`
6. **Send Instructions** - Fallback for non-voice messages

## Key Expressions
- Chat ID: `{{ $('Telegram Trigger').item.json.message.chat.id }}`
- Voice file ID: `{{ $json.message.voice.file_id }}`
- Transcription text: `{{ $json.text }}`

## Required Credentials
1. **Telegram API** - Bot token from [@BotFather](https://t.me/botfather)
2. **OpenAI API** - API key with Whisper access

## Multi-User Support
- Works with any user automatically
- `chat.id` extracted from each message
- No hardcoded IDs

## Limits
- Telegram voice messages: ~1-5 MB typical
- OpenAI Whisper: 25 MB max
- Voice format: OGG/Opus (native Telegram format, Whisper compatible)

## Extending the Workflow
- Add language detection: Use OpenAI response metadata
- Store transcripts: Add database node after transcription
- Translate: Add OpenAI translate node before sending
