Mail Triage V4: Security Evaluation Environment
This repository contains Mail Triage V4, a high-fidelity evaluation environment designed for testing the decision-making capabilities of AI Security Agents. It simulates a complex email triage task where agents must classify incoming mail based on technical headers, URL reputation metadata, and content analysis.

## Overview
The environment presents the agent with a series of email objects, ranging from standard institutional communications to sophisticated spear-phishing attempts. The goal is to classify each email into one of three categories:

INBOX: Trusted, official, or expected communications.

SPAM: Unsolicited marketing or low-risk bulk mail.

QUARANTINE: Malicious threats, including phishing, credential harvesting, and malware delivery.

### Key Features
Tiered Difficulty: 15 distinct scenarios across three levels (Clear Cases, Nuanced, and Spear Phishing).

Technical Headers: Realistic Received chains and authentication results (SPF, DKIM, DMARC).

URL Reputation Modeling: Detailed metadata for embedded links, including domain age, SSL status, and reputation scores.

Explainable AI (XAI): The action space requires the agent to provide reasoning for every triage decision.

## Technical Specification
### Observation Space
The agent receives a MyEnvV4Observation object containing:

Metadata: Sender, Subject, and Body.

Headers: Raw header strings and calculated hop_count.

Auth Results: A dictionary of security protocol outcomes (e.g., {"SPF": "pass", "DKIM": "fail"}).

URL Info: A list of objects detailing is_shortened, domain_age_days, and reputation_score.

### Action Space
The agent must respond with a MyEnvV4Action:

message: The classification (INBOX, SPAM, or QUARANTINE).

reasoning: A string justification explaining the logic behind the classification.

## Project Structure
app.py: Entry point for the Uvicorn server.

env.py: Core environment logic, dataset generation, and FastAPI endpoints.

models.py: Pydantic definitions for the Observation and Action spaces.

inference.py: A sample agent implementation using the Gemini 2.0 Flash model.

openenv.yaml: Metadata for OpenEnv compliance and scoring metrics.

pyproject.toml / requirements.txt: Dependency and build management.
