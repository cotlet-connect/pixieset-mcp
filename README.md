# How to connect Pixieset to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Pixieset account.** As of November 2026, Pixieset has no official app in ChatGPT and no official connector in Claude. Cotlet.dev connects your own signed-in Pixieset account to any AI agent, so you can ask in plain words and the AI delivers galleries, books sessions and follows up with clients for you.

## What you can ask

> Send the Martinez wedding gallery to Elena and set it to expire in 30 days.

> Which sessions are booked next week? List the client, date, time and package.

> Book Jordan Lee for a 1-hour family session on Saturday at 10 am and send the contract and invoice.

> Which galleries delivered in the last 14 days haven't been viewed yet? Draft a friendly reminder for each client.

> List unpaid invoices over $500 and email those clients a payment reminder.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Pixieset tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"pixieset":{"command":"uvx","args":["pixieset-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t pixieset-mcp .
docker run -i --rm -e COTLET_API_KEY pixieset-mcp
```

Tools: `pixieset_guide`, `pixieset_status`, `pixieset_open`, `pixieset_read`, `pixieset_click`, `pixieset_type`, `pixieset_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install pixieset-mcp        # or run it once: uvx pixieset-mcp connect
pixieset-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 pixieset_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 pixieset_agent.py status    # is Pixieset ready in your Cotlet.dev account
python3 pixieset_agent.py guide     # Pixieset screens and sign-in link
python3 pixieset_agent.py read      # open Pixieset, read the page, close the browser
python3 pixieset_agent.py tools     # list Cotlet.dev tools
python3 pixieset_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Pixieset users

**Does Pixieset have an API?**

You don't need one. Cotlet.dev works in your own signed-in Pixieset account, so your AI agent can deliver galleries, manage bookings and follow up with clients without a Pixieset API key.

**How do I connect Pixieset to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Pixieset once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Pixieset API key.

**Is there a way to use Claude with Pixieset?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Pixieset account.

**Is there a Pixieset MCP server?**

Pixieset's Apps & Plugins page lists no ChatGPT or Claude integration. Cotlet.dev is a hosted MCP server that works in Pixieset for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Pixieset on Cotlet.dev](https://cotlet.dev/integrations/pixieset-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=pixieset&utm_content=find)
- [PyPI package pixieset-mcp](https://pypi.org/project/pixieset-mcp/)
- [Odel](https://odel.app/modules/cotlet/pixieset)
- [mcpbeat](https://mcpbeat.com/mcp-servers/cotlet/pixieset/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-pixieset-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [AroFlo MCP](https://github.com/cotlet-connect/aroflo-mcp)
- [Simpro MCP](https://github.com/cotlet-connect/simpro-mcp)
- [Workiz MCP](https://github.com/cotlet-connect/workiz-mcp)
- [Kickserv MCP](https://github.com/cotlet-connect/kickserv-mcp)
- [Service Autopilot MCP](https://github.com/cotlet-connect/service-autopilot-mcp)
- [Boulevard MCP](https://github.com/cotlet-connect/boulevard-mcp)
- [Mindbody MCP](https://github.com/cotlet-connect/mindbody-mcp)
- [Meevo MCP](https://github.com/cotlet-connect/meevo-mcp)
- [DaySmart MCP](https://github.com/cotlet-connect/daysmart-mcp)
- [Acuity Scheduling MCP](https://github.com/cotlet-connect/acuity-scheduling-mcp)
- [Jane App MCP](https://github.com/cotlet-connect/jane-app-mcp)
- [FieldEdge MCP](https://github.com/cotlet-connect/fieldedge-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [Invoice Simple MCP](https://github.com/cotlet-connect/invoice-simple-mcp)
- [PhotoShelter MCP](https://github.com/cotlet-connect/photoshelter-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [ShootProof MCP](https://github.com/cotlet-connect/shootproof-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Appointy MCP](https://github.com/cotlet-connect/appointy-mcp)
- [Contractor+ MCP](https://github.com/cotlet-connect/contractor-plus-mcp)
- [Petpooja MCP](https://github.com/cotlet-connect/petpooja-mcp)
- [Teachers Pay Teachers MCP](https://github.com/cotlet-connect/teachers-pay-teachers-mcp)
- [Bloom MCP](https://github.com/cotlet-connect/bloom-mcp)
- [AestheticsPro MCP](https://github.com/cotlet-connect/aestheticspro-mcp)
- [Club OS MCP](https://github.com/cotlet-connect/club-os-mcp)
- [EZ Lawn Biller MCP](https://github.com/cotlet-connect/ez-lawn-biller-mcp)
- [Eversports Studio Manager MCP](https://github.com/cotlet-connect/eversports-studio-manager-mcp)
- [Exercise.com MCP](https://github.com/cotlet-connect/exercise-com-mcp)
- [Gymdesk MCP](https://github.com/cotlet-connect/gymdesk-mcp)
- [Iris Works MCP](https://github.com/cotlet-connect/iris-works-mcp)
- [CoachingPortal MCP](https://github.com/cotlet-connect/coachingportal-mcp)
- [CrewNest MCP](https://github.com/cotlet-connect/crewnest-mcp)
- [Paired Plus MCP](https://github.com/cotlet-connect/paired-plus-mcp)
- [ClubReady MCP](https://github.com/cotlet-connect/clubready-mcp)
- [Joist MCP](https://github.com/cotlet-connect/joist-mcp)
- [Trainerize MCP](https://github.com/cotlet-connect/trainerize-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/pixieset-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=pixieset

Start free: https://cotlet.dev/signup?app=pixieset&utm_source=github&utm_medium=readme&utm_campaign=pixieset
