# IT Setup Assistant — install & run

A minimal single-agent Neuro SAN Studio network. One LLM agent, no sub-agents,
no coded tools. It helps a new hire get their tech working: laptop, email/SSO,
password & MFA, VPN, and software access.

## Files in this bundle

    registries/it_setup.hocon      the agent definition
    registries/manifest.hocon      how to register it (snippet)

## Install into your project

Your project root is:
    C:\Users\user\Documents\GitHub\neuro_san_studio

1. Copy the network file:
   Put `it_setup.hocon` into
       C:\Users\user\Documents\GitHub\neuro_san_studio\registries\

2. Register it in the manifest:
   Open C:\Users\user\Documents\GitHub\neuro_san_studio\registries\manifest.hocon
   and add this line inside the existing { } block:
       "it_setup.hocon": true,
   (Do NOT replace the whole file — just add the line.)

## Run

From a terminal in the project root, with your venv active and your key set
(e.g. set OPENAI_API_KEY=...):

    python -m run

Then open the nsflow UI at:
    http://127.0.0.1:4173

Pick "it_setup" from the agent dropdown and try:
- "Hi, it's my first day — how do I set up my laptop?"
- "How do I turn on multi-factor authentication?"
- "I can't connect to the VPN, what do I do?"
- "How do I get access to the design software my team uses?"

## Customising

- Model: change `model_name` at the top of the .hocon to any model your
  config/llm_config.hocon supports.
- Company specifics: the agent is told NEVER to invent portal URLs, ticket queue
  names, or credentials. To make it concrete, add your real IT contacts / portal
  links directly into the instructions block.
- Grow it later: to add actions (e.g. actually raising an access ticket), give the
  agent a coded tool — add a tool block with a `class` and list its name in this
  agent's "tools" array.
