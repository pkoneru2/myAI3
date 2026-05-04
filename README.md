# FitCoachAI
A personalized AI fitness and workout assistant built with Next.js, featuring web search capabilities, vector database integration, and content moderation. Created by Pranay Koneru.

## Live Demo
🏋️ [https://naynayai.vercel.app/](https://naynayai.vercel.app/)

## Overview
FitCoachAI is an AI-powered fitness chatbot that can:

- Provide personalized workout plans and exercise guidance tailored to the user's fitness level and goals
- Answer fitness, strength training, and general nutrition questions
- Search the web for up-to-date fitness information using Exa API
- Search a curated vector database (Pinecone) for trusted fitness knowledge
- Moderate content to ensure safe and appropriate interactions
- Provide inline citations and sources for all responses

## Knowledge Base
FitCoachAI is powered by a curated set of authoritative fitness resources including:
- **US Physical Activity Guidelines (2nd Edition)** — Official US government physical activity recommendations
- **ACSM Resistance Training Guidelines** — American College of Sports Medicine strength training standards
- **Massachusetts Physical Fitness Preparation Guide** — Government fitness preparation and training guide
- **US Dietary Guidelines** — Official US nutrition and dietary recommendations
- **UNM Home Workout Guide** — University of New Mexico home exercise routines
- **Powerlifting Training Plans** — Structured strength and powerlifting programming

## Key Files to Customize
### `config.ts` - Application Configuration
The primary file for customizing your AI assistant:
- **AI Identity:** `AI_NAME` and `OWNER_NAME`
- **Welcome Message:** `WELCOME_MESSAGE` — greeting users see when they open the chat
- **UI Text:** `CLEAR_CHAT_TEXT` — label for the new chat button
- **Moderation Messages:** Custom messages shown when content is flagged
- **Model Configuration:** `MODEL` — AI model being used (GPT-4.1)
- **Vector Database Settings:** `PINECONE_TOP_K` and `PINECONE_INDEX_NAME`

### `prompts.ts` - AI Behavior and Instructions
Controls how FitCoachAI behaves and responds:
- **Identity Prompt:** Defines FitCoachAI as a fitness assistant
- **Tool Calling Prompt:** Instructions for when to search web or database
- **Tone & Style:** Friendly, motivating, and supportive like a personal trainer
- **Guardrails:** Restricts to fitness topics, bans medical advice, dangerous practices
- **Fitness Context:** Goal-based advice, experience level adaptation, injury prevention
- **Citations:** Inline markdown citations required for all sourced responses
- **Disclaimer:** Reminds users FitCoachAI is not a substitute for professional advice

### `app/terms/page.tsx` - Terms of Use
Fitness-specific terms of use and disclaimer page including:
- Not medical advice disclaimer
- Physical risk acknowledgment
- Nutrition guidance limitations
- User responsibilities and prohibited conduct

## Project Structure
FitCoachAI/
├── app/                          # Next.js application files
│   ├── api/chat/                 # Chat API endpoint
│   │   ├── route.ts              # Main chat handler
│   │   └── tools/                # AI tools (web search, vector search)
│   ├── page.tsx                  # Main chat interface (UI)
│   ├── parts/                    # UI components
│   └── terms/                    # Terms of Use page
├── components/                   # React components
│   ├── ai-elements/              # AI-specific UI components
│   ├── messages/                 # Message display components
│   └── ui/                       # Reusable UI components
├── lib/                          # Utility libraries
│   ├── moderation.ts             # Content moderation logic
│   ├── pinecone.ts               # Vector database integration
│   ├── sources.ts                # Source/citation handling
│   └── utils.ts                  # General utilities
├── types/                        # TypeScript type definitions
├── config.ts                     # ⭐ MAIN CONFIGURATION FILE
├── prompts.ts                    # ⭐ AI BEHAVIOR CONFIGURATION
└── package.json                  # Dependencies and scripts

## Tech Stack
- **Frontend:** Next.js
- **AI Model:** OpenAI GPT-4.1
- **Vector Database:** Pinecone (RAG)
- **Web Search:** Exa API
- **Hosting:** Vercel
- **Content Moderation:** OpenAI Moderation API

## Architecture Overview
The application follows a simple request-response flow:

1. User sends message → `app/page.tsx` (UI)
2. Message sent to API → `app/api/chat/route.ts`
3. Content moderation check → `lib/moderation.ts`
4. AI processes with tools → Model uses web search and/or vector search as needed
5. Response streamed back → UI displays response in real-time

The AI autonomously decides to:
- Answer directly from its training
- Search the web for current fitness information
- Search the Pinecone vector database for curated knowledge
- Combine multiple sources

All responses include inline citations when sources are used.

## Environment Setup (Vercel)
Configure environment variables in your Vercel project settings (Settings → Environment Variables):

| Variable | Required | Purpose |
|---|---|---|
| `OPENAI_API_KEY` | ✅ Required | AI model and moderation |
| `PINECONE_API_KEY` | Recommended | Vector database search |
| `EXA_API_KEY` | Recommended | Web search functionality |

Where to get API keys:
- OpenAI: https://platform.openai.com/api-keys
- Pinecone: https://app.pinecone.io/
- Exa: https://dashboard.exa.ai/

## Guardrails and Safety
FitCoachAI is built with safety as a core design principle:
- **Topic Restriction:** Only answers fitness, exercise, and nutrition questions
- **No Medical Advice:** Never diagnoses injuries or provides medical treatment
- **No Dangerous Practices:** Explicitly prohibits steroids, extreme diets, unsafe supplements
- **Injury Awareness:** Always recommends stopping if pain occurs and consulting a professional
- **Professional Referral:** Always recommends consulting doctors, trainers, and dietitians
- **Content Moderation:** All messages checked before processing

## Troubleshooting
**AI not responding:**
- Verify `OPENAI_API_KEY` is set correctly in Vercel environment variables
- Check browser console for error messages
- Ensure the API key has sufficient credits

**Web search not working:**
- Verify `EXA_API_KEY` is set in Vercel environment variables
- Check Exa API dashboard for usage limits

**Vector search not working:**
- Verify `PINECONE_API_KEY` is set in Vercel environment variables
- Check that `PINECONE_INDEX_NAME` in `config.ts` matches your Pinecone index name (`my-ai`)
- Ensure your Pinecone index exists and has data

**Deployment issues:**
- Check Vercel deployment logs for build errors
- Verify all environment variables are set in Vercel project settings

## Disclaimer
FitCoachAI is an independent student project. It is not endorsed by the University of North Carolina at Chapel Hill, any fitness organization, or medical institution. FitCoachAI is an AI assistant and not a substitute for professional medical, fitness, or nutritional advice. Always consult a qualified professional before starting any new exercise or nutrition program. Use at your own risk.

## License
MIT License
