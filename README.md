# Voce AI

An AI-powered voice conversation platform for practicing interviews, learning languages, attending lectures, preparing Q&A, and guided meditation. Users speak naturally, receive intelligent AI responses via text-to-speech, and get detailed feedback on their sessions.

## Features

- **Lecture on Topic** -- Structured AI-delivered talks on any subject with follow-up questions
- **Mock Interview** -- Simulated interview scenarios with industry-relevant questions and constructive feedback
- **Q&A Prep** -- Interactive question-and-answer practice with critical thinking prompts
- **Learn Language** -- Pronunciation guidance, vocabulary tips, and conversational language exercises
- **Meditation** -- Guided meditation sessions with breathing techniques and mindfulness practices

Each session includes:
- Real-time speech-to-text transcription via the browser's Web Speech API
- AI-generated conversational responses via OpenRouter (default model: DeepSeek R1)
- Text-to-speech playback via ElevenLabs
- Post-session feedback and summary generation saved to the database

## Tech Stack

| Layer          | Technology                                                    |
| -------------- | ------------------------------------------------------------- |
| Framework      | [Next.js 16](https://nextjs.org) (App Router)                |
| UI             | [Tailwind CSS 4](https://tailwindcss.com), [Radix UI](https://www.radix-ui.com), [Lucide Icons](https://lucide.dev) |
| Auth           | [Stack Auth](https://stack-auth.com)                          |
| Database       | [Convex](https://www.convex.dev)                              |
| AI             | [OpenRouter](https://openrouter.ai) (DeepSeek R1 by default) |
| Speech-to-Text | Browser Web Speech API                                        |
| Text-to-Speech | [ElevenLabs](https://elevenlabs.io)                           |
| Markdown       | [react-markdown](https://github.com/remarkjs/react-markdown)  |

## Getting Started

### Prerequisites

- Node.js 18+
- A [Convex](https://www.convex.dev) project
- API keys for [OpenRouter](https://openrouter.ai), [AssemblyAI](https://www.assemblyai.com), and [ElevenLabs](https://elevenlabs.io)
- A [Stack Auth](https://stack-auth.com) project

### Environment Variables

Create a `.env.local` file in the project root:

```env
# Convex
NEXT_PUBLIC_CONVEX_URL=<your-convex-deployment-url>

# OpenRouter
OPENROUTER_API_KEY=<your-openrouter-key>
OPENROUTER_MODEL=deepseek/deepseek-r1   # optional, this is the default

# AssemblyAI (streaming token generation)
ASSEMBLY_API_KEY=<your-assemblyai-key>

# ElevenLabs (text-to-speech)
ELEVENLABS_API_KEY=<your-elevenlabs-key>
ELEVENLABS_VOICE_ID=<voice-id>           # optional, defaults to JBFqnCBsd6RMkjVDRZzb
```

### Install and Run

```bash
# Install dependencies
npm install

# Start the Convex dev server (in a separate terminal)
npx convex dev

# Start the Next.js dev server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the app.

## Project Structure

```
app/
  page.jsx                        # Landing page
  layout.js                       # Root layout (Stack Auth + Convex providers)
  AuthProvider.jsx                 # User creation/login via Stack Auth + Convex
  (main)/
    dashboard/                    # Dashboard with session history and assistant selection
    discussion-room/[roomid]/     # Live voice conversation room
    view-summery/[roomid]/        # Post-session feedback and summary view
  api/
    getToken/                     # Generates AssemblyAI streaming token
    sendToAI/                     # Sends user message to OpenRouter AI
    sendToAIFeedback/             # Generates session feedback via OpenRouter
    speech/                       # Text-to-speech via ElevenLabs API
convex/
  schema.js                       # Database schema (users, DiscussionRoom)
  users.js                        # User creation mutation
  DiscussionRoom.jsx              # Room CRUD mutations and queries
lib/
  openrouter.js                   # OpenRouter client and streaming helper
services/
  Options.jsx                     # Expert/coaching option definitions and prompts
  GlobalServices.jsx              # Client-side API wrappers
stack/
  client.js                       # Stack Auth client config
  server.js                       # Stack Auth server config
```

## License

All rights reserved.
