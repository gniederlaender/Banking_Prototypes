# Banking Prototypes

Autonomous agent-managed repository for banking UI prototypes.

## Overview

This project contains HTML/CSS/JS prototypes for banking interfaces. An autonomous development agent runs daily at 9:20 AM to:

- Check for new prototype requests in `feedback.json`
- Implement requested UI prototypes
- Deploy directly to the web server
- Commit and push changes to GitHub

## Structure

```
Banking_Prototypes/
├── feedback.json          # Task queue for the agent
├── prototypes/           # HTML prototype files
├── assets/               # Shared assets
│   ├── css/             # Stylesheets
│   ├── js/              # JavaScript files
│   └── images/          # Images
├── index.html           # Prototype directory listing
└── README.md            # This file
```

## Live URL

Prototypes are accessible at:
**https://smartprototypes.net/UI_Prototypes/Banking_Prototypes/**

## Adding New Prototype Requests

Edit `feedback.json` and add a new item:

```json
{
  "id": "unique-id",
  "type": "feature",
  "status": "open",
  "priority": "medium",
  "title": "Short title",
  "description": "Detailed requirements...",
  "created_at": "2026-01-06"
}
```

The agent will pick it up on the next run (daily at 9:20 AM).

## Agent Details

- **Agent Repository:** https://github.com/gniederlaender/autonomous-dev-agent
- **Config:** `config/banking_prototypes.yaml`
- **Schedule:** Daily at 9:20 AM
- **Execution:** Autonomous with verification

## Technology Stack

- Pure HTML5/CSS3/JavaScript
- No build process required
- Directly served by Apache
- Version controlled with Git

---

*Managed by Autonomous Dev Agent*
