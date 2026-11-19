# Install an agent in your tenant

You need a Microsoft 365 work account with access to Microsoft 365 Copilot Chat and Agent Builder. Your organization's policy decides whether you may create and share agents.

## Option 1: rebuild in Agent Builder (any user)

1. Open https://copilot.cloud.microsoft, select **Agents** > **New agent**, then switch to **Configure**.
2. Open the agent's `agent.md` in this repository.
3. Copy into Agent Builder:
   - **Name**: the heading at the top of `agent.md`.
   - **Description**: the Description section.
   - **Instructions**: the Instructions section, unchanged.
4. **Knowledge**: add each website listed in the Knowledge section. If the section says "web search on (no site list)", leave web search on and add no sites.
5. **Skills**: for each folder under the agent's `skills/` folder, zip the folder contents (SKILL.md at the root of the zip, plus `references/` and `examples/` if present) and upload the zip under **Skills** > **Add** > **Upload**.
6. **Suggested prompts**: add each conversation starter. Agent Builder limits titles to 30 characters.
7. Select **Create**, then test with the starters before you share the agent.

The OT agent has two skills. Upload both and keep the routing lines in its instructions as they are.

## Option 2: app package for your admin

Ask the author (open an issue) for the agent's app package. It is the `.zip` that Agent Builder exports: `manifest.json`, `declarativeAgent_0.json`, two icons and the skill folders. Your Microsoft 365 admin can upload it as a custom app in your tenant and choose who gets it.

The package has not yet been tested in a second tenant. Report any problem in an issue.

## Test prompts

Each `agent.md` lists conversation starters. For the OT agent, a good end-to-end test is a water treatment case: the HMI shows a normal tank level while the field shows near overflow, and there are unexpected Modbus writes after a contractor VPN login. A correct answer starts with safety, scores severity with five factors and a total, recommends manual or local control and suspension of the VPN session after log export, and prints the NIS2 24 hour, 72 hour and one month deadlines.
