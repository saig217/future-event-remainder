# News Event Reminder Bot

A Telegram bot that extracts future-dated events from news articles, schedules reminders, and re-verifies events before they fire to catch postponements or cancellations.

## The Problem

Heavy news consumers — people who follow AI, tech, markets, and sports across many sources — regularly read articles that mention future-dated events (court verdicts, product launches, earnings calls, sports roster announcements, movie releases) and then forget those dates by the time they arrive. There is no tool that extracts these dates, reminds them on the day, and verifies the date hasn't shifted before firing the reminder. The initial user is me, but the pattern fits any information-heavy knowledge worker who tracks unfolding stories.

## What It Does

The user forwards a news article (URL or text) to a Telegram bot. Within seconds, the bot replies with a confirmation listing the future-dated events it extracted — for example, "I'll remind you about: (1) Adani SEBI verdict on May 15, 2026, (2) hearing on July 3, 2026."

One to two days before each event, a freshness-check agent searches for recent news and decides whether the date has shifted, the event was cancelled, or it's still on track. If anything has changed, the user gets a proactive Telegram alert ("Heads up — the verdict has been postponed to June 2") and the reminder reschedules itself. On the event day the bot sends the final reminder with a one-line summary and a link back to the original source.

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
