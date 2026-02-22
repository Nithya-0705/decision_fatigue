## Decision Fatigue Guard is a privacy-first Chrome extension that works on Gmail to detect user overload and visually reduce decision stress in real time.

The extension calculates a Decision Load Score (DLS) based on user interaction patterns and applies UI interventions when cognitive load increases — all on the user’s device, with no backend and no data scraping.
## Problem Statement

People make dozens of small decisions while handling emails (open, reply, delete, undo, switch tabs).
Over time, this leads to decision fatigue, causing slower responses, mistakes, and stress.

Most tools focus on productivity after overload happens —
this project detects overload while it’s happening.

## Solution Overview

Decision Fatigue Guard:

Continuously tracks interaction metadata (not email content)

Computes a real-time Decision Load Score (0–100)

Predicts overload risk using an on-device ML model

Dynamically modifies Gmail’s UI to reduce cognitive effort

## Key Features

✅ Real-time DLS (Decision Load Score)

🟢🟡🔴 Color-coded states: GREEN / AMBER / RED

🧠 On-device Machine Learning (TensorFlow.js)

🔒 Privacy-first (no email content, no network requests)

🎯 UI interventions (guarded actions, simplified UI)

📥 Decision Inbox (“Decide later” support)

🛠️ Dev Mode for demo and testing

📊 Decision Load States
State	DLS Range	Meaning
GREEN	0–29	Normal workload
AMBER	30–60	Rising cognitive load
RED	61–100	High overload

An early-warning rule promotes RED state if:

ML Risk > 65% and

DLS ≥ 45

🤖 Machine Learning (On-Device)

Framework: TensorFlow.js

Model: Logistic Regression

Training: Local only (no server)

Inputs: Interaction features (events/min, undo rate, indecision time, context switching)

Output: Overload risk probability (%)

Users can also give manual feedback using “I feel overloaded” to improve training.

🔐 Privacy by Design

This extension does NOT:

Read email subject or body

Store recipients or sender details

Send data to any server

Only anonymous interaction metadata is stored locally using chrome.storage.local.

🧩 Tech Stack

Chrome Extension – Manifest V3

TypeScript

Vite – Build tool

TensorFlow.js – On-device ML

MutationObserver – Gmail DOM detection

CSS Interventions – UI changes

Chrome Storage API – Local persistence

📁 Project Structure
public/
  manifest.json
  icons/

src/
  content/
    gmailObserver.ts
    eventCapture.ts
    uiOverlay.ts
    interventions.ts
    styles.css
    index.ts

  background/
    service_worker.ts
    model.ts
    storage.ts

  shared/
    dls.ts
    featureEngineering.ts
    types.ts

tests/
⚙️ Installation & Setup
Prerequisites

Node.js 18+

Google Chrome

Steps
npm install
npm run build

Open chrome://extensions

Enable Developer mode

Click Load unpacked

Select the dist/ folder

Open Gmail → Extension activates automatically

🧪 Demo Tips (Hackathon)

Enable Dev Mode in the panel

Use Simulate overload to quickly show AMBER → RED

Show how Gmail UI changes in real time

Explain privacy + on-device ML clearly

🚧 Limitations (MVP)

Gmail DOM may change occasionally

Model accuracy improves with more usage

Interventions are intentionally non-destructive

🌱 Future Enhancements

Personal DLS baselines per user

Calendar + task integration

Long-term fatigue analytics

Cross-app support (Docs, Slack, Outlook)

