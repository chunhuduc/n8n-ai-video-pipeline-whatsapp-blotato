# n8n AI Video Pipeline with WhatsApp Approval Gates

End-to-end automated daily video content pipeline for DTC e-commerce brands.

**Stack:** n8n · Claude/OpenAI API · HeyGen · ElevenLabs · Blotato · WhatsApp Business API · Google Drive

---

## How it works

```
07:00 UTC daily
  └─ n8n Schedule Trigger
       └─ Claude API → platform-optimized script (TikTok hook, Reels body, CTA)
            └─ WhatsApp Business API → interactive message (Approve / Reject / Revise)
                 └─ [GATE 1: owner approval]
                      └─ HeyGen API → avatar video render (owner Voice ID + Avatar ID)
                           └─ Google Drive scan → B-roll by script tags
                                └─ Gap fill → AI-generated video for missing footage
                                     └─ WhatsApp → draft video URL (Approve & Post / Reject & Revise)
                                          └─ [GATE 2: owner approval]
                                               └─ Blotato API → simultaneous publish (TikTok, Reels, Shorts, Facebook)
                                                    └─ Google Drive write-back → /Completed Assets/
```

Two human approval gates ensure nothing posts without explicit sign-off.
Every approved video grows the asset library for future automated assembly.

---

## Milestones

| # | Scope | Price |
|---|-------|-------|
| 1 | Daily script generation + WhatsApp Gate 1 | $100 |
| 2 | HeyGen avatar render + Drive scan + gap fill + WhatsApp Gate 2 | $100 |
| 3 | Blotato multi-platform publish + Drive write-back + error handling | $100 |

---

## Workflow files

| File | Description |
|------|-------------|
| `src/milestone-1-script-generation.json` | n8n workflow: cron, Claude API, WhatsApp delivery, revision loop |
| `src/milestone-2-video-assembly.json` | n8n workflow: HeyGen render, Drive scan, gap fill, WhatsApp gate |
| `src/milestone-3-publish-writeback.json` | n8n workflow: Blotato publish, Drive write-back, error handling |

Import each JSON into your n8n cloud instance via **Settings > Import workflow**.

---

## Prerequisites

- n8n cloud account with HTTP Request node access
- Claude API key (or OpenAI)
- HeyGen account with your Avatar ID and ElevenLabs Voice ID configured
- WhatsApp Business API access (Meta Cloud API or approved BSP)
- Google Drive API credentials (Service Account or OAuth2)
- Blotato account with connected social platforms

---

## Environment / credentials needed

| Credential | Used in |
|------------|---------|
| `ANTHROPIC_API_KEY` | Milestone 1 — script generation |
| `HEYGEN_API_KEY` | Milestone 2 — avatar render |
| `HEYGEN_AVATAR_ID` | Milestone 2 — your specific clone |
| `ELEVENLABS_VOICE_ID` | Milestone 2 — your specific voice |
| `WHATSAPP_PHONE_NUMBER_ID` | Milestones 1 + 2 — message delivery |
| `WHATSAPP_ACCESS_TOKEN` | Milestones 1 + 2 — Meta Cloud API |
| `GOOGLE_DRIVE_FOLDER_ID` | Milestone 2 — asset library root |
| `BLOTATO_API_KEY` | Milestone 3 — publish |

---

## Setup

1. Import workflow JSONs into n8n
2. Configure credentials in n8n Credentials panel
3. Set your Avatar ID, Voice ID, and Drive folder IDs in the workflow variables
4. Activate Milestone 1 workflow and trigger a test run
5. Confirm WhatsApp message arrives and revision loop works
6. Proceed to Milestones 2 and 3 after Gate 1 is verified live

---

## Demo

Live walkthrough: [chunhuduc.github.io/n8n-ai-video-pipeline-whatsapp-blotato](https://chunhuduc.github.io/n8n-ai-video-pipeline-whatsapp-blotato)

---

Built by [Duc](https://chunhuduc.com) — Solution Architect, hands-on delivery.
