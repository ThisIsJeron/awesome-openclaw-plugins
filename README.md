# Awesome OpenClaw Plugins [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of plugins for [OpenClaw](https://github.com/openclaw/openclaw), the open-source personal AI assistant.

<p align="center">
  <a href="https://docs.openclaw.ai/plugin">Plugin Docs</a> •
  <a href="https://github.com/openclaw/openclaw">GitHub</a> •
  <a href="https://discord.com/invite/clawd">Discord</a>
</p>

## Contents

- [Skills vs Plugins: What's the Difference?](#skills-vs-plugins-whats-the-difference)
- [Official Plugins](#official-plugins)
- [Channel Plugins](#channel-plugins)
- [Smart Home & IoT](#smart-home--iot)
- [Automotive](#automotive)
- [Utility Plugins](#utility-plugins)
- [Memory & AI](#memory--ai)
- [Security & Governance](#security--governance)
- [Multi-Agent & Coordination](#multi-agent--coordination)
- [Observability & DevOps](#observability--devops)
- [Health & Wellness](#health--wellness)
- [Meta & Self-Improvement](#meta--self-improvement)
- [Social Media & Content](#social-media--content)
- [Contributing](#contributing)

## Skills vs Plugins: What's the Difference?

OpenClaw has two extension mechanisms: **Skills** and **Plugins**. Understanding when to use each is key to building effective extensions.

### Skills

Skills are **prompt-based instructions** that teach the agent how to use external tools or follow specific workflows.

```
skills/
└── weather/
    └── SKILL.md    # Instructions for the agent
```

**Characteristics:**
- 📝 Markdown files with instructions
- 🧠 Loaded into the agent's context at runtime
- 🔧 Rely on existing tools (exec, browser, etc.)
- 🚀 Easy to create — just write a SKILL.md
- ⚡ No code execution, just prompt engineering

**Best for:**
- Teaching the agent to use CLI tools
- Defining workflows and best practices
- API integration via curl/scripts
- Quick, low-code extensions

### Plugins

Plugins are **TypeScript modules** that run in-process with the OpenClaw gateway, extending its core capabilities.

```
extensions/
└── voice-call/
    ├── index.ts              # Plugin code
    ├── openclaw.plugin.json  # Manifest
    └── package.json
```

**Characteristics:**
- 💻 Full TypeScript/JavaScript code
- ⚙️ Run in the gateway process
- 🔌 Can register new tools, channels, CLI commands, and RPC methods
- 🔐 Access to gateway internals and APIs
- 📦 Distributed via npm or git

**Best for:**
- Adding new messaging channels (Slack, Teams, etc.)
- Custom agent tools with complex logic
- Background services and scheduled tasks
- Gateway UI enhancements
- Anything requiring persistent state or network connections

### The Case for Plugins

While skills are great for quick integrations, **plugins are fundamentally more powerful**:

| Capability | Skills | Plugins |
|------------|--------|---------|
| Add new messaging channels | ❌ | ✅ |
| Register custom agent tools | ❌ | ✅ |
| Add CLI commands | ❌ | ✅ |
| Run background services | ❌ | ✅ |
| Modify gateway behavior | ❌ | ✅ |
| Persistent state management | ❌ | ✅ |
| OAuth flows & auth handlers | ❌ | ✅ |
| WebSocket connections | ❌ | ✅ |
| HTTP endpoint handlers | ❌ | ✅ |
| Ship bundled skills | ❌ | ✅ |

**Bottom line:** Skills tell the agent *how* to do things. Plugins give the agent *new abilities* it couldn't have otherwise.

<details open>
<summary><h2 style="display:inline">Official Plugins</h2></summary>

Plugins maintained by the OpenClaw team, available under the `@openclaw/*` scope.

- [voice-call](https://docs.openclaw.ai/plugins/voice-call) - Voice calling via Twilio (or log fallback for dev). `openclaw plugins install @openclaw/voice-call`
- [matrix](https://docs.openclaw.ai/channels/matrix) - Matrix chat protocol channel. `openclaw plugins install @openclaw/matrix`
- [nostr](https://docs.openclaw.ai/channels/nostr) - Nostr decentralized protocol channel. `openclaw plugins install @openclaw/nostr`
- [zalo](https://docs.openclaw.ai/channels/zalo) - Zalo messaging (Vietnam). `openclaw plugins install @openclaw/zalo`
- [zalouser](https://docs.openclaw.ai/plugins/zalouser) - Zalo Personal account integration. `openclaw plugins install @openclaw/zalouser`
- [msteams](https://docs.openclaw.ai/channels/msteams) - Microsoft Teams channel. `openclaw plugins install @openclaw/msteams`

### Bundled Plugins

These ship with OpenClaw and can be enabled via config:

- **memory-core** — Default memory search plugin
- **memory-lancedb** — LanceDB-based long-term memory with auto-recall
- **google-antigravity-auth** — Google OAuth provider
- **google-gemini-cli-auth** — Gemini CLI OAuth provider
- **qwen-portal-auth** — Qwen OAuth provider
- **copilot-proxy** — VS Code Copilot proxy bridge

</details>

<details open>
<summary><h2 style="display:inline">Channel Plugins</h2></summary>

Add new messaging platforms to OpenClaw.

- [feishu](https://github.com/m1heng/clawdbot-feishu) - Feishu/Lark (飞书) channel with Stream mode, AI cards, docs/wiki/bitable tools. By [@m1heng](https://github.com/m1heng). `openclaw plugins install @m1heng-clawd/feishu`
- [dingtalk](https://github.com/soimy/openclaw-channel-dingtalk) - DingTalk (钉钉) enterprise bot with Stream mode, AI interactive cards. By [@soimy](https://github.com/soimy). `openclaw plugins install https://github.com/soimy/openclaw-channel-dingtalk.git`
- [cliq](https://github.com/IBIZDigital/openclaw-cliq-channel) - Zoho Cliq team chat with real-time messaging and @mention support. By [@IBIZDigital](https://github.com/IBIZDigital). `openclaw plugins install https://github.com/IBIZDigital/openclaw-cliq-channel.git`
- [xmtp](https://github.com/flooredApe/openclaw-xmtp) - XMTP wallet messaging for AI agents — Web3 native communication. By [@flooredApe](https://github.com/flooredApe). `openclaw plugins install https://github.com/flooredApe/openclaw-xmtp.git`
- [irc](https://github.com/kcherry497/OpenClaw-IRC-Plugin) - IRC interface with KISS security principles. By [@kcherry497](https://github.com/kcherry497). `openclaw plugins install https://github.com/kcherry497/OpenClaw-IRC-Plugin.git`
- [qq](https://github.com/limouren01/openclaw_qq_plugin) - QQ messaging integration (Chinese). By [@limouren01](https://github.com/limouren01). `openclaw plugins install https://github.com/limouren01/openclaw_qq_plugin.git`
- [wechat](https://github.com/magicwang1111/openclaw-wechat-plugin) - WeChat messaging integration. By [@magicwang1111](https://github.com/magicwang1111). `openclaw plugins install https://github.com/magicwang1111/openclaw-wechat-plugin.git`
- [clawdtalk](https://github.com/team-telnyx/clawdtalk-client) - Phone calling and SMS for OpenClaw via Telnyx. Make and receive phone calls and SMS messages from your AI agent with full calendar, Jira, and web search integration. By [@team-telnyx](https://github.com/team-telnyx). `openclaw plugins install @team-telnyx/clawdtalk`
- [eclaw](https://github.com/HankHuang0516/openclaw-channel-eclaw) - E-Claw AI live wallpaper chat — connect your bot to animated Android wallpaper characters (lobsters, pigs). By [@HankHuang0516](https://github.com/HankHuang0516). `openclaw plugins install @eclaw/openclaw-channel`

</details>

<details open>
<summary><h2 style="display:inline">Smart Home & IoT</h2></summary>

Connect your agent to smart home platforms and IoT devices.

- [home-assistant](https://github.com/techartdev/OpenClawHomeAssistant) - Home Assistant add-on — run OpenClaw directly in your HA instance with full entity access. By [@techartdev](https://github.com/techartdev). ⭐ **34 stars**
- [webhook-bridge](https://github.com/robb99/clay-webhook-bridge) - Event-driven Home Assistant → OpenClaw webhook bridge for automations. By [@robb99](https://github.com/robb99). `openclaw plugins install https://github.com/robb99/clay-webhook-bridge.git`

</details>

<details open>
<summary><h2 style="display:inline">Automotive</h2></summary>

Control and monitor vehicles from your agent.

- [tescmd](https://github.com/Oceanswave/openclaw-tescmd) - Tesla vehicle control and telemetry via tescmd — lock/unlock, climate, charging, location. By [@Oceanswave](https://github.com/Oceanswave). `openclaw plugins install https://github.com/Oceanswave/openclaw-tescmd.git`

</details>

<details open>
<summary><h2 style="display:inline">Utility Plugins</h2></summary>

Enhance the gateway experience with quality-of-life improvements.

- [better-gateway](https://github.com/ThisIsJeron/openclaw-better-gateway) - Enhanced gateway UI with auto-reconnect, connection status indicator, network awareness. By [@ThisIsJeron](https://github.com/ThisIsJeron). `openclaw plugins install @thisisjeron/openclaw-better-gateway`
- [model-selector](https://github.com/bmbsystemsdir/openclaw-model-selector) - Smart model routing — suggest → confirm → execute → auto-return to default. By [@bmbsystemsdir](https://github.com/bmbsystemsdir). `openclaw plugins install https://github.com/bmbsystemsdir/openclaw-model-selector.git`
- [compaction-context](https://github.com/robertcuadra/compaction-context) - Preserve recent conversation context across compaction cycles. By [@robertcuadra](https://github.com/robertcuadra). `openclaw plugins install https://github.com/robertcuadra/compaction-context.git`
- [claw-turbo](https://github.com/jacobye2017-afk/claw-turbo) - Regex skill router with OpenClaw integration that short-circuits common commands locally to cut latency and improve tool-calling reliability on weaker models. By [@jacobye2017-afk](https://github.com/jacobye2017-afk). `git clone https://github.com/jacobye2017-afk/claw-turbo.git && cd claw-turbo && pip install -e . && claw-turbo install`
- [discourse-openclaw](https://github.com/pranciskus/discourse-openclaw) - Discourse forum integration — search, read, create topics/posts, find unanswered questions. By [@pranciskus](https://github.com/pranciskus). `openclaw plugins install openclaw-discourse`
- [manager](https://github.com/ClariSortAi/openclaw-manager-plugin) - Intelligent installation, configuration, and management for OpenClaw instances. By [@ClariSortAi](https://github.com/ClariSortAi). `openclaw plugins install https://github.com/ClariSortAi/openclaw-manager-plugin.git`
- [2do](https://github.com/chuckiefan/moltbot-plugin-2do) - 2Do task app integration — send tasks via natural language to 2Do's Email-to-Task feature. By [@chuckiefan](https://github.com/chuckiefan). `openclaw plugins install https://github.com/chuckiefan/moltbot-plugin-2do.git`
- [clawcollect](https://github.com/ruan11223344/clawcollect) - Hosted form collection bridge — open a form from chat, share a public link, check response progress, and summarize results. Supports managed and self-hosted (Cloudflare Workers + D1) backends. By [@ruan11223344](https://github.com/ruan11223344). `openclaw plugins install @clawcollect/clawcollect`

</details>

<details open>
<summary><h2 style="display:inline">Memory & AI</h2></summary>

Advanced memory backends and AI enhancements.

- [unified-memory](https://github.com/bmbsystemsdir/openclaw-unified-plugins) - Unified memory layer combining Graphiti knowledge graphs with Beads temporal memory. By [@bmbsystemsdir](https://github.com/bmbsystemsdir). `openclaw plugins install https://github.com/bmbsystemsdir/openclaw-unified-plugins.git`
- [memos-cloud](https://github.com/MemTensor/MemOS-Cloud-OpenClaw-Plugin) - MemOS cloud-based memory backend for cross-device persistence. By [@MemTensor](https://github.com/MemTensor). `openclaw plugins install https://github.com/MemTensor/MemOS-Cloud-OpenClaw-Plugin.git`

</details>

<details open>
<summary><h2 style="display:inline">Security & Governance</h2></summary>

Add guardrails and governance to your agent.

- [guardspine](https://github.com/DNYoussef/guardspine-openclaw) - Deny-by-default tool gating with L0-L4 risk tiers, 3-model council verification, and evidence packs. By [@DNYoussef](https://github.com/DNYoussef). `openclaw plugins install https://github.com/DNYoussef/guardspine-openclaw.git`
- [air-trust](https://github.com/airblackbox/openclaw-air-trust) - EU AI Act compliance layer — HMAC-SHA256 tamper-evident audit chains, consent gating for destructive tools, PII/credential tokenization, and 15-pattern prompt injection detection. 6 agent tools + 3 event hooks. By [@airblackbox](https://github.com/airblackbox). `npm install openclaw-air-trust`
- [codex-watchdog](https://github.com/ThisIsJeron/openclaw-codex-watchdog) - Guardrail plugin that blocks Codex narrative-loop replies when action-oriented runs make zero tool calls, replacing fake progress with an honest watchdog message. By [@ThisIsJeron](https://github.com/ThisIsJeron). `openclaw plugins install https://github.com/ThisIsJeron/openclaw-codex-watchdog.git`

</details>

<details open>
<summary><h2 style="display:inline">Multi-Agent & Coordination</h2></summary>

Run distributed agents and coordinate across instances.

- [ansible](https://github.com/likesjx/openclaw-plugin-ansible) - Distributed coordination layer — one agent, multiple bodies across machines. By [@likesjx](https://github.com/likesjx). `openclaw plugins install https://github.com/likesjx/openclaw-plugin-ansible.git`

</details>

<details open>
<summary><h2 style="display:inline">Observability & DevOps</h2></summary>

Monitor, debug, and manage your OpenClaw instances.

- [observatory](https://github.com/ThisIsJeron/openclaw-observatory) - Self-hosted observability dashboard — monitor sessions, context windows, costs, and failures across multiple gateways. By [@ThisIsJeron](https://github.com/ThisIsJeron). `openclaw plugins install @thisisjeron/openclaw-observatory`
- [Manifest](https://github.com/mnfst/manifest) - Real-time cost observability for OpenClaw agents — track tokens, costs, messages, and model usage. Self-hosted, local-first, supports 28+ LLM models. Website: [manifest.build](https://manifest.build). By [@mnfst](https://github.com/mnfst). `openclaw plugins install manifest`
- [opik-openclaw](https://github.com/comet-ml/opik-openclaw) - OpenClaw plugin that exports agent traces to Opik with LLM/tool/sub-agent spans plus usage and cost metadata. By [@comet-ml](https://github.com/comet-ml). `openclaw plugins install @opik/opik-openclaw`

</details>

<details open>
<summary><h2 style="display:inline">Health & Wellness</h2></summary>

Integrate health and fitness data into your agent conversations.

- [ouraclaw](https://github.com/rickybloomfield/OuraClaw) - Oura Ring integration — sleep, readiness, activity, stress data with scheduled summaries. By [@rickybloomfield](https://github.com/rickybloomfield). `openclaw plugins install @rickybloomfield/ouraclaw`

</details>

<details open>
<summary><h2 style="display:inline">Meta & Self-Improvement</h2></summary>

Plugins that enhance OpenClaw's ability to learn and grow.

- [foundry](https://github.com/lekt9/openclaw-foundry) - Self-writing meta-extension — observes workflows, learns patterns, writes new extensions and skills. By [@lekt9](https://github.com/lekt9). `openclaw plugins install @getfoundry/foundry-openclaw`

</details>

<details open>
<summary><h2 style="display:inline">Social Media & Content</h2></summary>

Plugins for social publishing, scheduling, and audience engagement.

- [sendit](https://www.npmjs.com/package/@senditapp/openclaw) - AI-native social publishing with 41 tools for scheduling, analytics, campaigns, CRM, inbox, and workflow automation across 32 platforms. By [@Shree-git](https://github.com/Shree-git). `openclaw plugins install @senditapp/openclaw`
- [tweetclaw](https://github.com/Xquik-dev/tweetclaw) - Post tweets, reply, like, retweet, follow, DM & more from your chat. 40+ X/Twitter endpoints via Xquik. By [@Xquik-dev](https://github.com/Xquik-dev). `openclaw plugins install @xquik/tweetclaw`

</details>

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding plugins to this list.

## Related Resources

- [Awesome OpenClaw Skills](https://github.com/VoltAgent/awesome-openclaw-skills) — Curated list of 1700+ OpenClaw skills
- [ClawHub](https://clawhub.com) — Official skill registry
- [Plugin Documentation](https://docs.openclaw.ai/plugin) — Official plugin authoring guide
- [Plugin Agent Tools](https://docs.openclaw.ai/plugins/agent-tools) — How to add agent tools in plugins

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the authors have waived all copyright and related rights to this work.
