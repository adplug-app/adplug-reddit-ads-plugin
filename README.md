# Reddit Ads MCP by AdPlug, for Grok Bot and Cursor

AdPlug is a hosted MCP server that safely connects Reddit Ads to Grok Bot and Cursor.

Your agent can check campaigns, flag what needs attention and, on a paid plan, make the changes you approve.

The plugin adds one remote MCP server, `https://api.adplug.app/mcp/reddit-ads`, and nothing else. There's no code, no script and no hook in it.

## Install in Grok Bot

Send your Bot this message:

> Add a custom MCP server called AdPlug Reddit Ads at https://api.adplug.app/mcp/reddit-ads

Click **Authorize** on the card it posts, then **Continue**, then sign in to AdPlug in the browser tab that opens and click **Approve**. The approval screen says "Cursor wants to access your AdPlug account". That's expected: Grok Bot connects apps through Cursor.

## Install in Cursor

Add `https://api.adplug.app/mcp/reddit-ads` as a server in Cursor's MCP settings, or put this in `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "adplug-reddit-ads": {
      "url": "https://api.adplug.app/mcp/reddit-ads"
    }
  }
}
```

The first time you connect, a browser tab opens on AdPlug's sign-in. Sign in, or create a free account, and click **Approve**.

## What you need

- An AdPlug account. The free plan connects one ad platform, comes with a monthly request limit and is view only: your agent can read your accounts and preview changes, but not apply them. A paid plan lets the agent make changes: see [adplug.app/pricing](https://adplug.app/pricing).
- Reddit Ads connected once in AdPlug, at [adplug.app/dashboard/connections](https://adplug.app/dashboard/connections), with your own Reddit sign-in.

There's no API key or client ID to set up. Sign-in is OAuth 2.1 with dynamic client registration and PKCE.

## What your agent can do

- **Accounts:** businesses, ad accounts, the profiles your ads post as, and pixels.
- **Reports:** account, campaign, ad group, ad, daily, hourly, community, keyword, interest, country, region, placement, device, gender, language, video and conversion reports, with period comparison.
- **Account data:** campaigns, ad groups (with full targeting), ads (with rejection reasons and preview links), posts, audiences, pixels, funding, lead forms, catalogues and change history.
- **Targeting:** community search and suggestions (with subscriber counts), keyword suggestions, interests, locations, audience estimates and suggested bids.
- **Diagnosis:** a delivery check for when ads aren't spending or conversions stop.
- **Changes:** create and edit campaigns, ad groups, posts and ads, block communities or keywords that waste spend, and build a whole campaign in one go.

`adplug_get_status` tells the agent whether Reddit Ads is connected and what your plan allows.

## Example prompts

- "How did my Reddit campaigns do last week, by community?"
- "Which communities and keywords wasted spend last month? Suggest exclusions."
- "Why isn't my Reddit ad delivering?"
- "Create a paused campaign for my launch. Show me the preview first."

## How changes are kept safe

- Change tools come in pairs: a preview, which shows the exact change without making it, and an execute, which makes it. AdPlug's tool descriptions tell the agent to preview first and run the change only after you confirm. That's an instruction to the agent, not a block on the server.
- New campaigns, ad groups and ads start paused unless you ask for them to be active.
- On the free plan, the change tools refuse to apply anything.
- On Max and Agency plans, a team owner can set a teammate to View only for Reddit Ads. AdPlug then hides and blocks the change tools for that teammate.
- Grok Bot and Cursor can also ask you before a tool runs, depending on your settings.
- Every call is logged on the [usage page](https://adplug.app/dashboard/usage) of your AdPlug dashboard.

## Your data and where it goes

Every tool call goes to one endpoint, `https://api.adplug.app/mcp/reddit-ads`. Sign-in goes through AdPlug's pages on adplug.app and its sign-in provider, Supabase (named in api.adplug.app's OAuth metadata). The plugin adds no software and runs no scripts on your computer.

Account data travels between Reddit Ads and your agent through AdPlug's servers at api.adplug.app. Reports are fetched live and not kept. AdPlug logs each call's tool, ad account and time for your usage page, never its arguments or results. Reddit sign-in tokens are stored encrypted.

- Privacy policy: [adplug.app/privacy](https://adplug.app/privacy)
- Terms: [adplug.app/terms](https://adplug.app/terms)
- Data processing agreement: [adplug.app/dpa](https://adplug.app/dpa)

## Support and links

- Email [support@adplug.app](mailto:support@adplug.app) and Daniel Popa, AdPlug's founder, will reply, usually the same business day.
- Website: [adplug.app/integrations/reddit-ads](https://adplug.app/integrations/reddit-ads)
- Setup guide: [adplug.app/guides/reddit-ads](https://adplug.app/guides/reddit-ads)
- Every ad platform in one connector: [adplug-app/adplug-cursor-plugin](https://github.com/adplug-app/adplug-cursor-plugin)

## Licence

MIT, see [LICENSE](LICENSE). Published by AdPlug, the trading name of MEANDATA IT SRL.
