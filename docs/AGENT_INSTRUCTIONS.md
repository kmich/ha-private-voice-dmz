# AI Agent Prompt: Automated Smart Home Voice DMZ Setup

Use this prompt when delegating your Home Assistant & Google Assistant integration to an AI coding agent (e.g., Claude Code, Cursor, Antigravity, Copilot).

---

### Copy-Paste Prompt for Your AI Assistant

```markdown
You are an expert Home Assistant and Node-RED automation engineer.
I want you to integrate my Google Assistant with Home Assistant and Node-RED using a "Smart Home DMZ (Zero-Exposure)" architecture.

Follow these strict rules and steps:

### 1. Architectural Rules
- STRICT MANDATORY: Never expose entire domains (`exposed_domains: []`). Google must NEVER automatically see my full entity registry, cameras, alarm sensors, locks, or internal topology.
- Only expose explicitly whitelisted entities under `entity_config:`.
- For triggering Node-RED or multi-step actions from voice, use a virtual template switch backed by an input_boolean (`voice_event_bus`).
- In Node-RED, automatically reset this switch back to `off` in <150ms upon receiving a trigger to keep the event bus stateless and immediately ready for repeated commands.
- Use native aliases (`aliases:`) and room definitions (`room:`) in Home Assistant so that voice control is natural and room-aware without requiring manual routines in the Google Home app.

### 2. Implementation Tasks
1. Verify whether packages are enabled in my `configuration.yaml` (`homeassistant: packages: !include_dir_named packages`).
2. Place `service_account.json` in the target package directory and create the package file at `/config/packages/google_assistant/google_assistant_dmz.yaml` using modern `template: - switch:` syntax and the `google_assistant:` integration block.
3. Configure the whitelisted entities I specify, assigning appropriate `name:`, `room:`, and `aliases:`.
4. Run `ha core check` to ensure zero syntax or schema errors before reloading.
5. In Node-RED, configure an event listener node (`server-state-changed`) listening to the virtual switch, wired to a `call-service` node that turns the switch off immediately, and route the payload to the intended home automations.
6. Call `google_assistant.request_sync` in Home Assistant once the integration is live to populate Google HomeGraph.
```
