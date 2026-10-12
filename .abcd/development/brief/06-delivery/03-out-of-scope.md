# Out of scope

Not built in v1. Each item says whether it is excluded for good or deferred.

| Out of scope | Status | Reason |
|---|---|---|
| Real-time action between homes (rollback or prediction over the internet) | Deferred | Couch and LAN first. The deterministic core keeps it possible (open question 7) |
| A central pack gallery, with its moderation and DMCA duties | Deferred | Federated signed indexes in v1 |
| Accounts or hosted storage for under-13s | Excluded from the hosted service | Schools self-host |
| Running the simulation on the Apple TV (standalone play) | Deferred | The Apple TV app is a display client; that would need a native core |
| Pack code outside the sandbox (plugins, engine ejection) | Excluded | Packs carry no engine code (invariant 2) |
| Third-party names, art, audio or text in any PG-Engine repository or pack | Excluded | The naming rule and IP risk |
| Training or hosting a pixel-art model | Excluded | PG-Engine uses external generators |
| LLM playtest agents as a publishing gate | Deferred | Research is early. The clear check plus replays and cheap bots come first |
| The commercial layer: store apps, hosted AI credits, paid tiers, a share of sales | Deferred | Its form is open question 2 |
| Consoles | Deferred | MPL-2.0 keeps the option open |
| Hybrid digital/physical features (camera scanning, printable components, narration, sensors) | Deferred | Needed by the future reference pool. The design must not preclude them (see the scope's design-conformance set) |
