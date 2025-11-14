What it is: A web app that scrapes job listings (from LinkedIn, Indeed, etc.), analyzes the required skills using NLP, and then uses AI to suggest project ideas tailored to those jobs.

Why it’s relevant: Many developers and students want projects that are actually aligned to market demand. There's even discussion on Reddit about this. > “build a tool that scrapes live job postings … and then use AI to generate educational project idea …” 
Reddit

Scope:

Scrape job data (or use job-board APIs)

Use NLP to extract skills / tech requirements

Use a generative AI (LLM) to generate project suggestions + link justification (“this project is relevant because job ads require X, Y, Z”)

UI for users to specify role, interest, experience level

Tech Stack: Python (for scraping + NLP), a vector DB (or just use embeddings), OpenAI / other LLM, frontend (React / Vue), backend (Node or Django).