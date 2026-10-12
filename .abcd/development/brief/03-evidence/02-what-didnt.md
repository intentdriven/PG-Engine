# What didn't work

| What didn't work | Evidence | PG-Engine's answer |
|---|---|---|
| The engine layer carried the game's verbs | The server command list included game-specific commands. Behaviour lived in a closed `switch` over effect keys, and the loader hard-coded one game's file list | A pack manifest plus a registry from day one. Game verbs live in packs (invariant 1) |
| One stylesheet and one client file became the dumping ground | The stylesheet reached 242 KB and was touched in 111 commits; the client file in 50 | UI built from components and themes. The studio and the screen share a component library |
| A hand-maintained test chain | Every test file was chained into one `npm test` string, causing constant merge conflicts | A test runner that discovers tests |
| iPad audio broke ("like an old broken tape deck") | Scheduler stalls, audio on hidden pages, a second AudioContext, leaking nodes | Invariant 15. Real-device verification |
| Overlays sometimes drew over a black background instead of the map | An earlier "build the map before overlays" decision didn't fully hold | Rendering is driven by the display list. Overlay layering has golden frames |
| Resizing animations were drafted four times with no acceptance criteria | Four empty draft intents | Layout and transition are an engine capability with BDD criteria |
| The licence and brand-free naming decisions came late | A brand-name retrofit across about 70 files, and licence intents superseded three times | Licences and the naming rule hold from the first commit |
| The LAN address was discovered by asking the server, with no secure context | The server returned its private IPv4 for the QR code over plain HTTP | Layered LAN security. The QR code carries the address plus a typable code; TLS is available where trust can be established |
| **Research:** a central gallery that dies with its platform | A console creation suite's live support ended in 2023 | A federated, signed pack index |
| **Research:** a clear check run only on the creator's machine | A level-maker game's upload bug let unbeatable levels through | The clear check is replayed on the host |
| **Research:** a niche DSL with no example corpus | 25–30% compile rate without examples | JSON plus JavaScript handlers, both strong in AI training data |
| **Research:** sole reliance on a hosted game-backend vendor | Two backend services closed in 2026 | Player-hosted and school-hosted servers are the default |
