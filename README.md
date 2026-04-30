# News Event Reminder Bot

A Telegram bot that extracts future-dated events from news articles, schedules reminders, and re-verifies events before they fire to catch postponements or cancellations.

## The Problem

Heavy news readers encounter dozens of "this will happen on date X" mentions every week — court verdicts, product launches, earnings calls, sports rosters, movie releases — buried inside articles across AI, tech, markets, and sports. There is no easy way to track all of them without manually copying each event into a calendar.

## What It Does

Forward any news article to the bot and it automatically extracts every future-dated event mentioned in the text. It stores those events in a database, sends you a confirmation listing what it found, and schedules a reminder for each event. One to two days before each event fires, a freshness-check agent searches the web and re-fetches the source to catch postponements or cancellations — sending a proactive alert if anything changed. On the event day you receive a final reminder with a one-sentence summary and a link back to the original source.

**Typical interaction:**

1. User forwards a news article to the bot on Telegram.
2. Bot replies: "Found 3 events — WWDC keynote on Jun 9, Apple earnings on Jul 31, EU AI Act deadline on Aug 2. Reminders set."
3. Two days before WWDC: "Still on track — no changes found."
4. Day of WWDC: "Reminder: Apple WWDC keynote today (Jun 9). [source link]"

**System components:** Telegram Bot API · web fetcher · LLM with structured output (Pydantic) · relational database · scheduler · freshness-check agent with web search tools.

## Setup

1. Install uv if you don't have it yet: https://docs.astral.sh/uv/getting-started/installation/

2. Clone this repository (or download the zip and extract it).

3. Create a `.env` file from the template and add your API key:

       cp .env.example .env

4. Install dependencies:

       uv sync

5. Start Jupyter:

       uv run jupyter notebook

## Notebooks

- `notebooks/01-setup.ipynb` - smoke test that confirms your environment works
- `notebooks/02-rag.ipynb` - a minimal RAG baseline you can adapt to your own data

## Data

Put your project data in the `data/` folder. See `notebooks/02-rag.ipynb` for how to load it.
