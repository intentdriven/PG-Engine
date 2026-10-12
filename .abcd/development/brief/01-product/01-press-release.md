# Press release

**PG-Engine: make the pixel game you remember, play it on the sofa with your phones, and share it as a folder of text.**

*Staged. This is the launch the build sequence is working towards.*

Most people who loved a 1980s computer game have imagined their own version of it, and very few have built one. Game engines expect you to program. Simple "maker" tools cap what you can make. AI can now write a lot of code, but on its own it produces a pile of one-off scripts that nobody can check, share or build on.

PG-Engine separates the game from the engine. A game is a **pack**: a folder of plain JSON for the rules and maps, Markdown for the words, and pixel-art assets. Anything the data can't say goes into small handlers that run in a sandbox. The engine supplies everything else: tile maps, sprites and palettes, chiptune audio, input, saving, turns and real-time ticks, and the networking that lets a whole room play. Because a pack is just text, people and AI tools can write it together, and the engine checks every change before it runs.

The **studio** is where you start. Paint a landscape with the built-in tiles, drop in characters, press play. When you want more (a new enemy, a card deck, a different palette), ask an AI. Your own assistant connects to PG-Engine's tool layer, as does the studio's built-in chat, which can use a local model on your network. The AI's change arrives as a diff you can test straight away. Publish when you have recorded a winning run that proves the game can be beaten.

On game night, a laptop, an iPad or the Apple TV is the shared screen. Everyone else joins by scanning a QR code with their phone, and the phone becomes their private hand of cards, their secret orders or their controller. PG-Engine runs on the home network without the internet, and a school can run its own PG-Engine so pupils' games never leave the building.

> "PG-Engine is a flexible and easy-to-use engine for creating and recreating retro-style computer and video games. PG-Engine
> enables anyone interested in retro games to focus on their creativity and on game design, with PG-Engine doing everything
> else. Importantly, games reside in .json, .md, and .svg files hosted on github that PG-Engine can display."
> — the publisher

> "We played our own remake of a game from 1986 with four phones as card hands, then changed the rules in an evening by asking the AI and pressing play."
> — Carol, couch host

> "My class built three games this term on the school's own PG-Engine server, with a local AI model and no accounts."
> — Bob, teacher

**Getting started (staged):** install the PG-Engine desktop app, which hosts the server and the studio, or open a hosted studio; choose a starter pack; press play; scan the QR code with your phone.

## Product principles

What PG-Engine favours when two good goals clash. Each reads "X, even over Y": X wins. The owner confirmed all six on
2026-10-07; principles 1 and 4 were ranked against each other, principle 2 settles the build order, and the others
are not ranked. abcd's engineering principles (how PG-Engine is built) are a different set.

1. **Easy first minutes, even over every choice up front.** Alice paints a landscape within a minute on a 2D pixel
   default. Art kind, 2D or 3D, palette and tile size are there when she looks for them, never in her way.
2. **Playing together, even over the studio, when the build order has to choose.** Carol hosts a game night with
   ready-made games before creators get the studio.
3. **The creator directs, even over building by hand.** Alice describes a dragon that breathes fire every five seconds;
   the AI makes its art and rules, and she reviews and accepts the change. Her own AI assistant connects first; the
   studio's built-in chat follows.
4. **The creator's choice, even over one house style.** Pictures are SVG drawn as pixel squares, free vector art or
   pixel images, and games are 2D or 3D, chosen per game.
5. **The original and a modern take, always.** Every game offers its original style (as close as possible, with no
   original assets) and a modern take, which is the default. They differ in looks and sound only, and the player
   switches between them.
6. **Open by default: GitHub first, any host.** A game is a folder of text files. GitHub is its default home and the
   place to start; any web host or school server works too.
