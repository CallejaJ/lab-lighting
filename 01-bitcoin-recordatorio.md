  Recordatorio · ¿Qué es Bitcoin? — Módulo 5 (presentación)       /\* ======================================================================== THEME TOKENS · Swiss Modern Change these to adjust the whole look. ======================================================================== \*/ :root { /\* Core palette \*/ --bg: #ffffff; --bg-panel: #f5f5f5; --ink: #0a0a0a; --ink-soft: #3a3a3a; --muted: #6a6a6a; --muted-2: #b0b0b0; --grid: rgba(10, 10, 10, 0.05); --grid-line: rgba(10, 10, 10, 0.08); /\* Accents \*/ --accent: #ff3300; /\* Swiss red \*/ --accent-2: #0a0a0a; /\* Black as co-accent \*/ --accent-btc:#f7931a; /\* Bitcoin orange (used very sparingly) \*/ /\* Typography \*/ --font-display: "Archivo", sans-serif; --font-body: "Nunito", sans-serif; --font-mono: "JetBrains Mono", ui-monospace, monospace; /\* Motion \*/ --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1); --duration-normal: 0.7s; } /\* ======================================================================== GLOBAL RESETS ======================================================================== \*/ \* { margin: 0; padding: 0; box-sizing: border-box; } /\* ======================================================================== VIEWPORT FITTING — MANDATORY BASE STYLES (verbatim copy of viewport-base.css; don't remove) ======================================================================== \*/ html, body { height: 100%; overflow-x: hidden; } html { scroll-snap-type: y mandatory; scroll-behavior: smooth; } .slide { width: 100vw; height: 100vh; height: 100dvh; overflow: hidden; scroll-snap-align: start; display: flex; flex-direction: column; position: relative; } .slide-content { flex: 1; display: flex; flex-direction: column; justify-content: center; max-height: 100%; overflow: hidden; padding: var(--slide-padding); } :root { --title-size: clamp(1.5rem, 5vw, 4rem); --h2-size: clamp(1.25rem, 3.5vw, 2.5rem); --h3-size: clamp(1rem, 2.5vw, 1.75rem); --body-size: clamp(0.75rem, 1.5vw, 1.125rem); --small-size: clamp(0.65rem, 1vw, 0.875rem); --slide-padding: clamp(1rem, 4vw, 4rem); --content-gap: clamp(0.5rem, 2vw, 2rem); --element-gap: clamp(0.25rem, 1vw, 1rem); } .card, .container, .content-box { max-width: min(90vw, 1000px); max-height: min(80vh, 700px); } .feature-list, .bullet-list { gap: clamp(0.4rem, 1vh, 1rem); } .feature-list li, .bullet-list li { font-size: var(--body-size); line-height: 1.4; } .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 250px), 1fr)); gap: clamp(0.5rem, 1.5vw, 1rem); } img, .image-container { max-width: 100%; max-height: min(50vh, 400px); object-fit: contain; } @media (max-height: 700px) { :root { --slide-padding: clamp(0.75rem, 3vw, 2rem); --content-gap: clamp(0.4rem, 1.5vw, 1rem); --title-size: clamp(1.25rem, 4.5vw, 2.5rem); --h2-size: clamp(1rem, 3vw, 1.75rem); } } @media (max-height: 600px) { :root { --slide-padding: clamp(0.5rem, 2.5vw, 1.5rem); --content-gap: clamp(0.3rem, 1vw, 0.75rem); --title-size: clamp(1.1rem, 4vw, 2rem); --body-size: clamp(0.7rem, 1.2vw, 0.95rem); } .nav-dots, .keyboard-hint, .decorative { display: none; } } @media (max-height: 500px) { :root { --slide-padding: clamp(0.4rem, 2vw, 1rem); --title-size: clamp(1rem, 3.5vw, 1.5rem); --h2-size: clamp(0.9rem, 2.5vw, 1.25rem); --body-size: clamp(0.65rem, 1vw, 0.85rem); } } @media (max-width: 600px) { :root { --title-size: clamp(1.25rem, 7vw, 2.5rem); } .grid { grid-template-columns: 1fr; } } @media (prefers-reduced-motion: reduce) { \*, \*::before, \*::after { animation-duration: 0.01ms !important; transition-duration: 0.2s !important; } html { scroll-behavior: auto; } } /\* ======================================================================== BODY · BACKGROUND Swiss Modern: pure white with a very subtle 12-column grid. ======================================================================== \*/ body { background: var(--bg); color: var(--ink); font-family: var(--font-body); font-size: var(--body-size); line-height: 1.5; background-image: linear-gradient(to right, var(--grid) 1px, transparent 1px); background-size: calc(100% / 12) 100%; } /\* ======================================================================== SLIDE FRAME (shared header + footer) ======================================================================== \*/ .slide { padding: clamp(1.25rem, 3.5vw, 3.5rem); } .slide-header { display: flex; justify-content: space-between; align-items: center; gap: 1rem; padding-bottom: clamp(0.5rem, 1vw, 0.75rem); border-bottom: 1px solid var(--grid-line); } .slide-header .left { display: flex; align-items: center; gap: 0.75rem; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.65rem, 0.95vw, 0.85rem); letter-spacing: 0.28em; text-transform: uppercase; } .slide-header .left .mark { width: clamp(0.55rem, 0.9vw, 0.8rem); height: clamp(0.55rem, 0.9vw, 0.8rem); background: var(--accent); } .slide-header .right { font-family: var(--font-display); font-weight: 700; font-size: clamp(0.65rem, 0.95vw, 0.85rem); letter-spacing: 0.28em; text-transform: uppercase; color: var(--muted); } .slide-body { flex: 1; display: flex; flex-direction: column; justify-content: center; padding: clamp(1rem, 2vw, 2rem) 0; gap: clamp(0.75rem, 1.5vw, 1.5rem); min-height: 0; } .slide-footer { display: flex; justify-content: space-between; align-items: baseline; gap: 1rem; padding-top: clamp(0.4rem, 0.8vw, 0.75rem); border-top: 1px solid var(--grid-line); font-family: var(--font-body); font-weight: 400; font-size: clamp(0.65rem, 0.9vw, 0.8rem); color: var(--muted); } .slide-footer b { color: var(--ink); font-weight: 600; } .slide-footer .page { font-family: var(--font-display); font-weight: 800; letter-spacing: 0.18em; color: var(--ink); } .slide-footer .page .sep { color: var(--muted-2); margin: 0 0.3em; } /\* ======================================================================== SECTION KICKER + HEADING ======================================================================== \*/ .kicker { display: inline-flex; align-items: center; gap: clamp(0.4rem, 0.7vw, 0.6rem); font-family: var(--font-display); font-weight: 800; font-size: clamp(0.7rem, 1vw, 0.95rem); letter-spacing: 0.25em; text-transform: uppercase; color: var(--accent); } .kicker .bar { width: clamp(1.25rem, 2.5vw, 2.5rem); height: clamp(0.15rem, 0.25vw, 0.25rem); background: var(--accent); } h2.heading { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.75rem, 5.5vw, 4.75rem); line-height: 0.95; letter-spacing: -0.025em; color: var(--ink); max-width: 18ch; } h2.heading .accent { color: var(--accent); } h2.heading .stroke { color: transparent; -webkit-text-stroke: clamp(1px, 0.15vw, 2px) var(--ink); } /\* ======================================================================== SLIDE 1 · TITLE ======================================================================== \*/ .title-slide { background: var(--bg); } .title-slide .slide-body { display: grid; grid-template-columns: 1fr; grid-template-rows: 1fr auto; gap: clamp(1rem, 2vw, 2rem); } .title-slide .title-main { align-self: center; max-width: 24ch; } .title-slide .eyebrow-tag { display: inline-block; padding: clamp(0.3rem, 0.5vw, 0.45rem) clamp(0.65rem, 1vw, 0.95rem); background: var(--accent); color: #fff; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.7rem, 1vw, 0.9rem); letter-spacing: 0.28em; text-transform: uppercase; margin-bottom: clamp(1rem, 2vw, 1.5rem); } .title-slide h1 { font-family: var(--font-display); font-weight: 900; font-size: clamp(2.5rem, 10vw, 9rem); line-height: 0.88; letter-spacing: -0.035em; } .title-slide h1 .accent { color: var(--accent); } .title-slide .rule { margin-top: clamp(1rem, 2vw, 1.5rem); width: clamp(2.5rem, 5vw, 5rem); height: clamp(0.2rem, 0.3vw, 0.3rem); background: var(--ink); } .title-slide .subline { margin-top: clamp(0.75rem, 1.5vw, 1.25rem); font-family: var(--font-body); font-size: clamp(0.9rem, 1.4vw, 1.25rem); color: var(--ink-soft); max-width: 34ch; line-height: 1.45; } .title-slide .circle-deco { position: absolute; top: clamp(3rem, 8vw, 7rem); right: clamp(2rem, 6vw, 6rem); width: clamp(7rem, 16vw, 17rem); height: clamp(7rem, 16vw, 17rem); border: clamp(1.5px, 0.25vw, 3px) solid var(--ink); border-radius: 50%; display: grid; place-items: center; pointer-events: none; } .title-slide .circle-deco::before { content: "₿"; font-family: var(--font-display); font-weight: 900; color: var(--accent); font-size: clamp(3rem, 8vw, 8rem); line-height: 1; } .title-slide .byline { display: flex; justify-content: space-between; align-items: baseline; gap: 1rem; font-family: var(--font-body); font-size: clamp(0.8rem, 1.1vw, 1rem); } .title-slide .byline .name { font-weight: 700; color: var(--ink); } .title-slide .byline .meta { font-family: var(--font-display); font-weight: 700; letter-spacing: 0.25em; text-transform: uppercase; font-size: clamp(0.65rem, 0.9vw, 0.8rem); color: var(--muted); } /\* ======================================================================== LAYOUT · TWO-COLUMN (heading left · content right) ======================================================================== \*/ .two-col { display: grid; grid-template-columns: minmax(0, 5fr) minmax(0, 7fr); gap: clamp(1.5rem, 3vw, 3rem); align-items: start; min-height: 0; } @media (max-width: 720px) { .two-col { grid-template-columns: 1fr; } } .col-left { display: flex; flex-direction: column; gap: clamp(0.75rem, 1.5vw, 1.25rem); } .col-right { display: flex; flex-direction: column; gap: clamp(0.75rem, 1.5vw, 1.25rem); min-width: 0; } /\* ======================================================================== BULLET LIST (Swiss style) ======================================================================== \*/ ul.feature-list { list-style: none; display: flex; flex-direction: column; counter-reset: bullet; } ul.feature-list li { position: relative; padding: clamp(0.5rem, 1vw, 0.8rem) 0 clamp(0.5rem, 1vw, 0.8rem) clamp(2.25rem, 3.5vw, 3rem); border-bottom: 1px solid var(--grid-line); counter-increment: bullet; font-size: clamp(0.85rem, 1.2vw, 1rem); line-height: 1.5; color: var(--ink-soft); } ul.feature-list li::before { content: counter(bullet, decimal-leading-zero); position: absolute; top: clamp(0.55rem, 1.1vw, 0.9rem); left: 0; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.7rem, 1vw, 0.85rem); letter-spacing: 0.15em; color: var(--accent); } ul.feature-list li b { color: var(--ink); font-weight: 700; } /\* ======================================================================== STAT STRIP (Slide 2 · Origen) ======================================================================== \*/ .stat-strip { display: grid; grid-template-columns: repeat(4, 1fr); gap: clamp(0.5rem, 1vw, 1rem); padding: clamp(0.75rem, 1.5vw, 1rem) 0; border-top: clamp(1.5px, 0.25vw, 2px) solid var(--ink); border-bottom: clamp(1.5px, 0.25vw, 2px) solid var(--ink); } @media (max-width: 720px) { .stat-strip { grid-template-columns: repeat(2, 1fr); } } .stat { display: flex; flex-direction: column; gap: 0.2rem; } .stat .num { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.75rem, 4.5vw, 3.75rem); line-height: 1; letter-spacing: -0.03em; color: var(--ink); } .stat .num .small { font-size: 0.55em; color: var(--muted); margin-left: 0.1em; letter-spacing: 0.05em; } .stat .lbl { font-family: var(--font-display); font-weight: 700; font-size: clamp(0.6rem, 0.85vw, 0.75rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } /\* ======================================================================== PULL QUOTE (Slide 3 · Cimientos) ======================================================================== \*/ .pull-quote { padding: clamp(1rem, 2vw, 1.75rem) clamp(1.25rem, 2.5vw, 2rem); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); background: var(--bg-panel); font-family: var(--font-display); font-weight: 500; font-size: clamp(1rem, 2vw, 1.5rem); line-height: 1.25; color: var(--ink); letter-spacing: -0.01em; } .pull-quote .src { display: block; margin-top: clamp(0.4rem, 0.8vw, 0.7rem); font-family: var(--font-body); font-weight: 600; font-style: italic; font-size: clamp(0.7rem, 1vw, 0.9rem); color: var(--muted); letter-spacing: 0.02em; } /\* ======================================================================== QUOTE CARD (Slide 2 · Origen) — numbered questions with attribution ======================================================================== \*/ .quote-card { padding: clamp(0.85rem, 1.5vw, 1.25rem) clamp(1rem, 1.8vw, 1.4rem); border: 1px solid var(--ink); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); background: var(--bg-panel); display: flex; flex-direction: column; gap: clamp(0.45rem, 0.9vw, 0.75rem); } .quote-card .q-head { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.62rem, 0.9vw, 0.78rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } .quote-card .q-list { list-style: none; counter-reset: q; display: flex; flex-direction: column; gap: clamp(0.3rem, 0.65vw, 0.5rem); margin: 0; padding: 0; } .quote-card .q-list li { position: relative; padding: 0 0 0 clamp(1.5rem, 2.2vw, 2rem); counter-increment: q; font-size: clamp(0.8rem, 1.1vw, 0.95rem); line-height: 1.4; color: var(--ink); border: none; } .quote-card .q-list li::before { content: counter(q); position: absolute; left: 0; top: 0.1em; font-family: var(--font-display); font-weight: 900; font-size: clamp(0.75rem, 1vw, 0.9rem); color: var(--accent); letter-spacing: 0; } .quote-card .q-list li em { color: var(--muted); font-style: italic; font-weight: 500; } .quote-card .q-src { display: block; padding-top: clamp(0.3rem, 0.6vw, 0.5rem); border-top: 1px solid var(--grid-line); font-family: var(--font-body); font-weight: 600; font-style: italic; font-size: clamp(0.68rem, 0.95vw, 0.82rem); color: var(--muted); } /\* Override the global .feature-list style when bullets are inside .quote-card (the generic feature-list rule targets .slide ul li; quote-card uses its own list) \*/ /\* ======================================================================== ADDRESS CARDS (Slide 4 · Direcciones) ======================================================================== \*/ .address-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: clamp(0.5rem, 1vw, 0.75rem); } @media (max-width: 720px) { .address-grid { grid-template-columns: 1fr; } } .addr-card { padding: clamp(0.75rem, 1.2vw, 1rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.4rem, 0.8vw, 0.6rem); min-width: 0; } .addr-card .tag { display: inline-block; padding: 0.15rem 0.45rem; background: var(--ink); color: #fff; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.85vw, 0.75rem); letter-spacing: 0.18em; text-transform: uppercase; align-self: flex-start; } .addr-card .tag.red { background: var(--accent); } .addr-card .tag.btc { background: var(--accent-btc); color: var(--ink); } .addr-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.9rem, 1.3vw, 1.1rem); color: var(--ink); } .addr-card .sample { font-family: var(--font-mono); font-size: clamp(0.65rem, 0.9vw, 0.8rem); color: var(--ink-soft); word-break: break-all; padding: clamp(0.3rem, 0.6vw, 0.5rem); background: var(--bg-panel); border-radius: 2px; line-height: 1.4; } .addr-card .desc { font-size: clamp(0.7rem, 0.95vw, 0.85rem); color: var(--muted); line-height: 1.4; } /\* ======================================================================== BLOCKCHAIN DIAGRAM (Slide 5) ======================================================================== \*/ .chain { display: grid; grid-template-columns: 1fr auto 1fr auto 1fr; align-items: center; gap: clamp(0.4rem, 0.8vw, 0.6rem); padding: clamp(0.75rem, 1.5vw, 1rem) 0; } .block { border: clamp(1.5px, 0.2vw, 2px) solid var(--ink); background: var(--bg); padding: clamp(0.5rem, 1vw, 0.85rem); display: flex; flex-direction: column; gap: clamp(0.3rem, 0.55vw, 0.45rem); min-width: 0; } .block.current { background: var(--accent); color: #fff; border-color: var(--accent); } .block.current .row b { color: #fff; } .block .head { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid currentColor; padding-bottom: clamp(0.2rem, 0.4vw, 0.3rem); font-family: var(--font-display); font-weight: 800; font-size: clamp(0.65rem, 0.9vw, 0.8rem); letter-spacing: 0.2em; text-transform: uppercase; } .block .head .n { opacity: 0.8; } .block .row { display: flex; justify-content: space-between; gap: 0.5rem; font-family: var(--font-mono); font-size: clamp(0.6rem, 0.85vw, 0.75rem); color: inherit; } .block .row b { color: var(--ink); font-weight: 500; } .block.current .row { color: #fff; } .link { display: flex; align-items: center; justify-content: center; position: relative; color: var(--ink); } .link .arrow { width: clamp(1.5rem, 3vw, 3rem); height: clamp(1px, 0.2vw, 2px); background: var(--ink); position: relative; } .link .arrow::after { content: ""; position: absolute; right: -1px; top: 50%; width: clamp(0.4rem, 0.7vw, 0.7rem); height: clamp(0.4rem, 0.7vw, 0.7rem); border-top: clamp(1px, 0.2vw, 2px) solid var(--ink); border-right: clamp(1px, 0.2vw, 2px) solid var(--ink); transform: translateY(-50%) rotate(45deg); } .link .hash-label { position: absolute; top: calc(100% + 0.25rem); font-family: var(--font-mono); font-size: clamp(0.55rem, 0.75vw, 0.65rem); color: var(--muted); white-space: nowrap; } /\* ======================================================================== CIA TRIAD (Slide 6) ======================================================================== \*/ .cia-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: clamp(0.5rem, 1vw, 0.85rem); } @media (max-width: 720px) { .cia-grid { grid-template-columns: 1fr; } } .cia-card { padding: clamp(0.8rem, 1.4vw, 1.25rem); border: clamp(1.5px, 0.2vw, 2px) solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.35rem, 0.7vw, 0.55rem); position: relative; min-width: 0; } .cia-card .letter { position: absolute; top: clamp(0.4rem, 0.8vw, 0.6rem); right: clamp(0.5rem, 1vw, 0.8rem); font-family: var(--font-display); font-weight: 900; font-size: clamp(2.5rem, 5vw, 4.5rem); line-height: 1; color: var(--accent); opacity: 0.85; } .cia-card .lbl { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.85vw, 0.72rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } .cia-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(1rem, 1.5vw, 1.25rem); line-height: 1.15; color: var(--ink); } .cia-card .desc { font-size: clamp(0.75rem, 1vw, 0.9rem); line-height: 1.45; color: var(--ink-soft); margin-top: clamp(0.2rem, 0.4vw, 0.4rem); } /\* ======================================================================== TRANSACTIONS (Slide · Transacciones y UTXO) ======================================================================== \*/ .tx-split { display: grid; grid-template-columns: 1fr 1.15fr; gap: clamp(0.6rem, 1.2vw, 1rem); align-items: stretch; } @media (max-width: 860px) { .tx-split { grid-template-columns: 1fr; } } .analogy-card, .tx-diagram { padding: clamp(0.8rem, 1.3vw, 1.1rem) clamp(0.95rem, 1.5vw, 1.3rem); border: 1px solid var(--ink); background: var(--bg-panel); display: flex; flex-direction: column; gap: clamp(0.45rem, 0.9vw, 0.75rem); min-width: 0; } .analogy-card { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent-2); } .tx-diagram { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); } .analogy-card .q-head, .tx-diagram .q-head { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.88vw, 0.74rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } .analogy-card p { font-size: clamp(0.75rem, 1vw, 0.9rem); line-height: 1.5; color: var(--ink-soft); margin: 0; } .analogy-card p b { color: var(--ink); font-weight: 700; } .analogy-card p em { font-style: italic; color: var(--accent); font-weight: 500; } .tx-flow { display: grid; grid-template-columns: 1fr auto 1fr; gap: clamp(0.25rem, 0.55vw, 0.45rem); align-items: stretch; } .tx-col { display: flex; flex-direction: column; gap: clamp(0.2rem, 0.45vw, 0.35rem); padding: clamp(0.4rem, 0.75vw, 0.6rem); border: 1px solid var(--ink); background: var(--bg); min-width: 0; } .tx-col .col-label { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.53rem, 0.72vw, 0.65rem); letter-spacing: 0.18em; text-transform: uppercase; color: var(--muted); padding-bottom: clamp(0.18rem, 0.35vw, 0.28rem); border-bottom: 1px solid var(--grid-line); } .tx-row { display: flex; justify-content: space-between; align-items: baseline; gap: 0.4rem; font-family: var(--font-mono); font-size: clamp(0.58rem, 0.82vw, 0.7rem); color: var(--ink-soft); } .tx-row .io-addr { overflow: hidden; text-overflow: ellipsis; white-space: nowrap; min-width: 0; } .tx-row .io-amt { color: var(--ink); font-weight: 600; white-space: nowrap; } .tx-total { margin-top: auto; padding-top: clamp(0.22rem, 0.45vw, 0.38rem); border-top: 1px dashed var(--grid-line); font-family: var(--font-mono); font-size: clamp(0.58rem, 0.8vw, 0.7rem); color: var(--muted); } .tx-total b { color: var(--ink); font-weight: 700; } .tx-col.outputs .tx-total b { color: var(--accent); } .tx-arrow { display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 0.25rem; color: var(--ink); padding: 0 clamp(0.2rem, 0.4vw, 0.35rem); } .tx-arrow .arrow { width: clamp(1.25rem, 2.2vw, 2rem); height: clamp(1px, 0.2vw, 2px); background: var(--ink); position: relative; } .tx-arrow .arrow::after { content: ""; position: absolute; right: -1px; top: 50%; width: clamp(0.35rem, 0.6vw, 0.55rem); height: clamp(0.35rem, 0.6vw, 0.55rem); border-top: clamp(1px, 0.2vw, 2px) solid var(--ink); border-right: clamp(1px, 0.2vw, 2px) solid var(--ink); transform: translateY(-50%) rotate(45deg); } .tx-arrow .arrow-lbl { font-family: var(--font-mono); font-size: clamp(0.52rem, 0.7vw, 0.62rem); color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; } .tx-fee { display: flex; flex-wrap: wrap; align-items: baseline; gap: clamp(0.35rem, 0.7vw, 0.6rem) clamp(0.5rem, 1vw, 0.85rem); padding: clamp(0.4rem, 0.75vw, 0.6rem) clamp(0.55rem, 1vw, 0.85rem); background: var(--ink); color: #fff; } .tx-fee .fee-tag { font-family: var(--font-display); font-weight: 900; font-size: clamp(0.58rem, 0.8vw, 0.7rem); letter-spacing: 0.25em; text-transform: uppercase; color: var(--accent); } .tx-fee .fee-math { font-family: var(--font-mono); font-size: clamp(0.65rem, 0.9vw, 0.8rem); color: #fff; } .tx-fee .fee-math b { color: var(--accent); font-weight: 700; } .tx-fee .fee-note { font-size: clamp(0.62rem, 0.85vw, 0.75rem); color: rgba(255, 255, 255, 0.72); font-style: italic; flex: 1; min-width: 12ch; line-height: 1.4; } /\* ======================================================================== NETWORK SLIDES (WMBN anatomy, node types, SPV, relay networks) ======================================================================== \*/ /\* --- Two-column split shared by network slides --- \*/ .net-split { display: grid; grid-template-columns: 1fr 1fr; gap: clamp(0.7rem, 1.3vw, 1.1rem); align-items: stretch; min-height: 0; } .net-split.lean { grid-template-columns: 1.1fr 1fr; } @media (max-width: 860px) { .net-split, .net-split.lean { grid-template-columns: 1fr; } } /\* --- WMBN module grid (2x2 of coloured circles) --- \*/ .wmbn-wrap { padding: clamp(0.8rem, 1.3vw, 1.1rem); border: 1px solid var(--ink); background: var(--bg-panel); display: flex; flex-direction: column; gap: clamp(0.5rem, 1vw, 0.85rem); min-width: 0; } .wmbn-wrap .q-head { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.88vw, 0.74rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } .wmbn-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: clamp(0.45rem, 0.9vw, 0.75rem); } .wmbn-cell { display: flex; align-items: center; gap: clamp(0.5rem, 1vw, 0.8rem); padding: clamp(0.5rem, 0.9vw, 0.75rem); border: 1px solid var(--ink); background: var(--bg); min-width: 0; } .wmbn-cell .bubble { flex: 0 0 auto; width: clamp(2rem, 3.4vw, 2.6rem); height: clamp(2rem, 3.4vw, 2.6rem); border-radius: 50%; display: grid; place-items: center; color: #fff; font-family: var(--font-display); font-weight: 900; font-size: clamp(0.85rem, 1.4vw, 1.15rem); line-height: 1; } .wmbn-cell .bubble.w { background: #4b9f63; } .wmbn-cell .bubble.m { background: #0a0a0a; } .wmbn-cell .bubble.b { background: #2f78c4; } .wmbn-cell .bubble.n { background: var(--accent-btc); color: var(--ink); } .wmbn-cell .label { display: flex; flex-direction: column; gap: clamp(0.1rem, 0.25vw, 0.2rem); min-width: 0; } .wmbn-cell .label .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.75rem, 1.05vw, 0.9rem); color: var(--ink); line-height: 1.1; } .wmbn-cell .label .desc { font-size: clamp(0.63rem, 0.85vw, 0.75rem); color: var(--muted); line-height: 1.3; } /\* --- Node-type cards (full / archive / lightweight / api) --- \*/ .node-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: clamp(0.5rem, 1vw, 0.85rem); } @media (max-width: 860px) { .node-grid { grid-template-columns: 1fr; } } .node-card { padding: clamp(0.7rem, 1.2vw, 1rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.3rem, 0.6vw, 0.5rem); min-width: 0; position: relative; } .node-card .tag { display: inline-flex; align-items: center; gap: 0.35em; align-self: flex-start; padding: 0.15rem 0.5rem; background: var(--ink); color: #fff; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.55rem, 0.78vw, 0.68rem); letter-spacing: 0.18em; text-transform: uppercase; } .node-card .tag.red { background: var(--accent); } .node-card .tag.btc { background: var(--accent-btc); color: var(--ink); } .node-card .tag.muted { background: var(--muted); } .node-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.95rem, 1.35vw, 1.15rem); color: var(--ink); line-height: 1.1; } .node-card .modules { font-family: var(--font-mono); font-size: clamp(0.6rem, 0.85vw, 0.72rem); color: var(--muted); letter-spacing: 0.04em; } .node-card .modules b { color: var(--accent); font-weight: 700; } .node-card .desc { font-size: clamp(0.7rem, 0.95vw, 0.82rem); color: var(--ink-soft); line-height: 1.42; } .node-card .desc b { color: var(--ink); font-weight: 700; } /\* --- Sybil warning card --- \*/ .warn-card { padding: clamp(0.75rem, 1.3vw, 1.1rem) clamp(0.9rem, 1.5vw, 1.25rem); border: 1px solid var(--ink); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); background: var(--bg-panel); display: flex; flex-direction: column; gap: clamp(0.35rem, 0.75vw, 0.6rem); min-width: 0; } .warn-card .tag { display: inline-flex; align-self: flex-start; padding: 0.15rem 0.55rem; background: var(--accent); color: #fff; font-family: var(--font-display); font-weight: 900; font-size: clamp(0.58rem, 0.82vw, 0.72rem); letter-spacing: 0.25em; text-transform: uppercase; } .warn-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.9rem, 1.3vw, 1.1rem); color: var(--ink); line-height: 1.15; } .warn-card .desc { font-size: clamp(0.72rem, 1vw, 0.87rem); color: var(--ink-soft); line-height: 1.45; } .warn-card .desc b { color: var(--ink); font-weight: 700; } .warn-card .desc em { color: var(--accent); font-style: italic; font-weight: 500; } /\* --- Relay network cards (BRN + FIBRE) --- \*/ .relay-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: clamp(0.5rem, 1vw, 0.85rem); } @media (max-width: 720px) { .relay-grid { grid-template-columns: 1fr; } } .relay-card { padding: clamp(0.75rem, 1.2vw, 1rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.3rem, 0.6vw, 0.5rem); min-width: 0; } .relay-card.accent { background: var(--bg-panel); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); } .relay-card .year { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.3rem, 2.2vw, 1.9rem); color: var(--accent); line-height: 1; } .relay-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.9rem, 1.3vw, 1.1rem); color: var(--ink); line-height: 1.15; } .relay-card .sub { font-family: var(--font-mono); font-size: clamp(0.6rem, 0.85vw, 0.72rem); color: var(--muted); letter-spacing: 0.04em; } .relay-card .desc { font-size: clamp(0.7rem, 0.95vw, 0.83rem); color: var(--ink-soft); line-height: 1.42; } /\* --- Inline prose card used in network overview slide --- \*/ .prose-card { padding: clamp(0.8rem, 1.3vw, 1.1rem) clamp(0.95rem, 1.5vw, 1.3rem); border: 1px solid var(--ink); background: var(--bg-panel); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent-2); display: flex; flex-direction: column; gap: clamp(0.45rem, 0.9vw, 0.75rem); min-width: 0; } .prose-card .q-head { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.88vw, 0.74rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } .prose-card p { font-size: clamp(0.75rem, 1vw, 0.9rem); line-height: 1.5; color: var(--ink-soft); margin: 0; } .prose-card p b { color: var(--ink); font-weight: 700; } .prose-card p em { color: var(--accent); font-style: italic; font-weight: 500; } /\* --- Mini feature list used tightly inside cards --- \*/ .mini-list { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: clamp(0.2rem, 0.45vw, 0.35rem); } .mini-list li { position: relative; padding-left: clamp(0.9rem, 1.4vw, 1.15rem); font-size: clamp(0.7rem, 0.95vw, 0.82rem); color: var(--ink-soft); line-height: 1.4; } .mini-list li::before { content: ""; position: absolute; left: 0; top: 0.6em; width: clamp(0.35rem, 0.6vw, 0.5rem); height: 1px; background: var(--accent); } .mini-list li b { color: var(--ink); font-weight: 700; } .closing-line { font-family: var(--font-display); font-weight: 500; font-size: clamp(0.9rem, 1.4vw, 1.15rem); color: var(--ink); line-height: 1.35; padding-top: clamp(0.4rem, 0.8vw, 0.75rem); border-top: 1px solid var(--grid-line); } .closing-line b { color: var(--accent); font-weight: 700; } /\* ======================================================================== PROGRESS BAR + NAV DOTS ======================================================================== \*/ .progress-bar { position: fixed; top: 0; left: 0; height: clamp(2px, 0.3vw, 3px); width: 0%; background: var(--accent); z-index: 100; transition: width 0.3s var(--ease-out-expo); } .nav-dots { position: fixed; right: clamp(0.75rem, 1.5vw, 1.5rem); top: 50%; transform: translateY(-50%); z-index: 90; display: flex; flex-direction: column; gap: clamp(0.4rem, 0.8vw, 0.65rem); } .nav-dots button { width: clamp(0.5rem, 0.8vw, 0.65rem); height: clamp(0.5rem, 0.8vw, 0.65rem); border-radius: 50%; border: 1px solid var(--ink); background: transparent; cursor: pointer; padding: 0; transition: background 0.25s ease, transform 0.25s ease; } .nav-dots button:hover { transform: scale(1.25); } .nav-dots button.active { background: var(--accent); border-color: var(--accent); } .keyboard-hint { position: fixed; bottom: clamp(0.75rem, 1.5vw, 1.25rem); left: 50%; transform: translateX(-50%); z-index: 90; font-family: var(--font-display); font-weight: 700; font-size: clamp(0.6rem, 0.85vw, 0.75rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); display: flex; gap: clamp(0.5rem, 1vw, 0.85rem); align-items: center; pointer-events: none; } .keyboard-hint .key { display: inline-block; padding: 0.1rem 0.4rem; border: 1px solid var(--muted-2); border-radius: 3px; background: var(--bg); color: var(--ink); } /\* ======================================================================== ANIMATIONS ======================================================================== \*/ .reveal { opacity: 0; transform: translateY(26px); transition: opacity var(--duration-normal) var(--ease-out-expo), transform var(--duration-normal) var(--ease-out-expo); } .slide.visible .reveal { opacity: 1; transform: translateY(0); } .slide.visible .reveal:nth-of-type(1) { transition-delay: 0.05s; } .slide.visible .reveal:nth-of-type(2) { transition-delay: 0.15s; } .slide.visible .reveal:nth-of-type(3) { transition-delay: 0.28s; } .slide.visible .reveal:nth-of-type(4) { transition-delay: 0.42s; } .slide.visible .reveal:nth-of-type(5) { transition-delay: 0.55s; } .slide.visible .reveal:nth-of-type(6) { transition-delay: 0.68s; } /\* ======================================================================== INLINE EDITING UI JS-controlled visibility (don't use CSS ~ sibling selector). ======================================================================== \*/ .edit-hotzone { position: fixed; top: 0; left: 0; width: 80px; height: 80px; z-index: 10000; cursor: pointer; } .edit-toggle { position: fixed; top: clamp(0.75rem, 1.5vw, 1.25rem); left: clamp(0.75rem, 1.5vw, 1.25rem); width: clamp(2.25rem, 3vw, 2.75rem); height: clamp(2.25rem, 3vw, 2.75rem); border: 1px solid var(--ink); background: var(--bg); border-radius: 50%; cursor: pointer; z-index: 10001; display: grid; place-items: center; font-size: clamp(0.9rem, 1.3vw, 1.1rem); opacity: 0; pointer-events: none; transition: opacity 0.3s ease, background 0.2s ease; } .edit-toggle.show, .edit-toggle.active { opacity: 1; pointer-events: auto; } .edit-toggle.active { background: var(--accent); border-color: var(--accent); color: #fff; } .edit-banner { position: fixed; top: clamp(0.75rem, 1.5vw, 1.25rem); left: 50%; transform: translate(-50%, -120%); background: var(--ink); color: #fff; padding: clamp(0.4rem, 0.8vw, 0.55rem) clamp(0.75rem, 1.2vw, 1rem); font-family: var(--font-display); font-weight: 800; font-size: clamp(0.65rem, 0.9vw, 0.8rem); letter-spacing: 0.22em; text-transform: uppercase; border-radius: 3px; z-index: 10002; transition: transform 0.35s var(--ease-out-expo); white-space: nowrap; } .edit-banner.active { transform: translate(-50%, 0); } .edit-banner .dot { display: inline-block; width: 0.5rem; height: 0.5rem; background: var(--accent); border-radius: 50%; margin-right: 0.55rem; vertical-align: middle; animation: pulse 1.2s ease-in-out infinite; } @keyframes pulse { 0%, 100% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.4); opacity: 0.6; } } body.edit-active \[contenteditable="true"\] { outline: 1px dashed var(--accent); outline-offset: 3px; cursor: text; border-radius: 2px; } body.edit-active \[contenteditable="true"\]:focus { outline: 2px solid var(--accent); background: rgba(255, 51, 0, 0.06); } /\* ======================================================================== MINING & CONSENSUS · Slides 11-14 ======================================================================== \*/ /\* --- Consensus four-pillars grid --- \*/ .consensus-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: clamp(0.5rem, 1vw, 0.85rem); } @media (max-width: 900px) { .consensus-grid { grid-template-columns: repeat(2, 1fr); } } .consensus-card { padding: clamp(0.7rem, 1.1vw, 0.95rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.3rem, 0.55vw, 0.45rem); min-width: 0; position: relative; } .consensus-card .idx { font-family: var(--font-mono); font-size: clamp(0.6rem, 0.8vw, 0.72rem); color: var(--accent); letter-spacing: 0.14em; } .consensus-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.78rem, 1.1vw, 0.95rem); color: var(--ink); line-height: 1.18; } .consensus-card .desc { font-size: clamp(0.66rem, 0.9vw, 0.78rem); color: var(--ink-soft); line-height: 1.4; } /\* --- Confirmation scale bar --- \*/ .confirm-scale { display: grid; grid-template-columns: repeat(6, 1fr); gap: clamp(0.3rem, 0.6vw, 0.5rem); align-items: stretch; } .confirm-step { padding: clamp(0.5rem, 0.9vw, 0.7rem) clamp(0.4rem, 0.7vw, 0.55rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.15rem, 0.35vw, 0.25rem); align-items: flex-start; min-width: 0; } .confirm-step.warn { background: #fff7f4; border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); } .confirm-step.ok { background: var(--bg-panel); border-left: clamp(3px, 0.5vw, 5px) solid var(--ink); } .confirm-step .n { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.1rem, 1.8vw, 1.5rem); color: var(--ink); line-height: 1; } .confirm-step .lbl { font-family: var(--font-mono); font-size: clamp(0.55rem, 0.75vw, 0.68rem); letter-spacing: 0.12em; text-transform: uppercase; color: var(--muted); } .confirm-step .note { font-size: clamp(0.6rem, 0.82vw, 0.72rem); color: var(--ink-soft); line-height: 1.3; } /\* --- Reward split (subsidy + fees = coinbase) --- \*/ .reward-split { display: grid; grid-template-columns: 1fr auto 1fr auto 1fr; gap: clamp(0.4rem, 0.8vw, 0.7rem); align-items: stretch; } @media (max-width: 860px) { .reward-split { grid-template-columns: 1fr; } .reward-split .op { display: none; } } .reward-card { padding: clamp(0.7rem, 1.1vw, 0.95rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.25rem, 0.5vw, 0.4rem); } .reward-card.subsidy { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent-btc); } .reward-card.fees { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); } .reward-card.total { background: var(--ink); color: var(--bg); border-color: var(--ink); } .reward-card .tag { font-family: var(--font-mono); font-size: clamp(0.55rem, 0.75vw, 0.68rem); letter-spacing: 0.14em; text-transform: uppercase; color: var(--muted); } .reward-card.total .tag { color: rgba(255,255,255,0.65); } .reward-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.85rem, 1.2vw, 1.05rem); } .reward-card .val { font-family: var(--font-mono); font-weight: 700; font-size: clamp(0.75rem, 1.05vw, 0.92rem); color: var(--accent); } .reward-card.total .val { color: var(--accent-btc); } .reward-card .desc { font-size: clamp(0.62rem, 0.85vw, 0.74rem); color: var(--ink-soft); line-height: 1.38; } .reward-card.total .desc { color: rgba(255,255,255,0.72); } .reward-split .op { display: flex; align-items: center; justify-content: center; font-family: var(--font-display); font-weight: 900; font-size: clamp(1.3rem, 2.2vw, 1.9rem); color: var(--muted); } /\* --- PoW formula card --- \*/ .pow-card { padding: clamp(0.85rem, 1.4vw, 1.2rem); border: 1px solid var(--ink); background: var(--bg-panel); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); display: flex; flex-direction: column; gap: clamp(0.45rem, 0.8vw, 0.7rem); } .pow-card .q-head { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.88vw, 0.74rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } .pow-formula { font-family: var(--font-mono); font-weight: 700; font-size: clamp(0.85rem, 1.35vw, 1.15rem); color: var(--ink); letter-spacing: 0.02em; line-height: 1.3; } .pow-formula .var { color: var(--accent); } .pow-formula .le { color: var(--accent-btc); } /\* --- Difficulty adjust callout --- \*/ .diff-strip { display: grid; grid-template-columns: repeat(3, 1fr); gap: clamp(0.4rem, 0.8vw, 0.7rem); padding: clamp(0.6rem, 1vw, 0.85rem); border: 1px solid var(--ink); background: var(--bg); } @media (max-width: 860px) { .diff-strip { grid-template-columns: 1fr; } } .diff-strip .cell { display: flex; flex-direction: column; gap: clamp(0.15rem, 0.35vw, 0.3rem); } .diff-strip .cell .big { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.1rem, 2vw, 1.7rem); color: var(--accent); line-height: 1; } .diff-strip .cell .cap { font-family: var(--font-mono); font-size: clamp(0.55rem, 0.78vw, 0.68rem); letter-spacing: 0.14em; text-transform: uppercase; color: var(--muted); } .diff-strip .cell .sub { font-size: clamp(0.65rem, 0.9vw, 0.78rem); color: var(--ink-soft); line-height: 1.35; } /\* --- Mining pool flow diagram --- \*/ .pool-diagram { display: grid; grid-template-columns: 1fr 1.2fr; gap: clamp(0.5rem, 1vw, 0.85rem); align-items: stretch; } @media (max-width: 860px) { .pool-diagram { grid-template-columns: 1fr; } } .pool-box { padding: clamp(0.7rem, 1.1vw, 0.95rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.3rem, 0.55vw, 0.45rem); min-width: 0; } .pool-box.accent { background: var(--bg-panel); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); } .pool-box .q-head { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.88vw, 0.74rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } .pool-box .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.9rem, 1.3vw, 1.1rem); color: var(--ink); line-height: 1.15; } .pool-box .desc { font-size: clamp(0.68rem, 0.92vw, 0.8rem); color: var(--ink-soft); line-height: 1.4; } .pool-box .desc b { color: var(--ink); font-weight: 700; } .pool-box .desc em { color: var(--accent); font-style: italic; font-weight: 500; } /\* --- Share / target mono snippet --- \*/ .share-target { font-family: var(--font-mono); font-size: clamp(0.6rem, 0.85vw, 0.72rem); color: var(--ink); background: var(--bg); border: 1px dashed var(--muted-2); padding: clamp(0.35rem, 0.55vw, 0.45rem) clamp(0.4rem, 0.7vw, 0.6rem); line-height: 1.5; word-break: break-all; } .share-target .lead { color: var(--accent); } .share-target .zeros { color: var(--muted); } /\* --- Fork comparison grid --- \*/ .fork-grid { display: grid; grid-template-columns: 1fr 1fr; gap: clamp(0.5rem, 1vw, 0.85rem); } @media (max-width: 860px) { .fork-grid { grid-template-columns: 1fr; } } .fork-card { padding: clamp(0.85rem, 1.3vw, 1.15rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.4rem, 0.7vw, 0.6rem); min-width: 0; } .fork-card.hard { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); background: var(--bg-panel); } .fork-card.soft { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent-btc); } .fork-card .tag { display: inline-block; font-family: var(--font-mono); font-size: clamp(0.55rem, 0.75vw, 0.68rem); letter-spacing: 0.14em; text-transform: uppercase; padding: 0.15rem 0.5rem; background: var(--ink); color: var(--bg); align-self: flex-start; } .fork-card.soft .tag { background: var(--accent-btc); } .fork-card .title { font-family: var(--font-display); font-weight: 900; font-size: clamp(1rem, 1.5vw, 1.3rem); color: var(--ink); line-height: 1.15; } .fork-card .title b { color: var(--accent); font-weight: 900; } .fork-card.soft .title b { color: var(--accent-btc); } .fork-card .desc { font-size: clamp(0.7rem, 0.95vw, 0.82rem); color: var(--ink-soft); line-height: 1.45; } .fork-card .desc b { color: var(--ink); font-weight: 700; } /\* --- Fork example callout (e.g. BCH) --- \*/ .fork-example { padding: clamp(0.55rem, 0.9vw, 0.75rem) clamp(0.7rem, 1.1vw, 0.95rem); border: 1px solid var(--muted-2); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.2rem, 0.4vw, 0.3rem); } .fork-example .ex-head { font-family: var(--font-mono); font-size: clamp(0.55rem, 0.75vw, 0.68rem); letter-spacing: 0.14em; text-transform: uppercase; color: var(--accent); } .fork-example .ex-name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.8rem, 1.1vw, 0.95rem); color: var(--ink); } .fork-example .ex-desc { font-size: clamp(0.65rem, 0.88vw, 0.76rem); color: var(--ink-soft); line-height: 1.4; } /\* --- Two-column layout utility for mining slides --- \*/ .split-2 { display: grid; grid-template-columns: 1fr 1fr; gap: clamp(0.5rem, 1vw, 0.85rem); align-items: stretch; } @media (max-width: 860px) { .split-2 { grid-template-columns: 1fr; } } /\* Stratum mini sequence diagram \*/ .stratum-seq { display: grid; grid-template-columns: auto 1fr auto; gap: 0 clamp(0.3rem, 0.6vw, 0.5rem); row-gap: clamp(0.18rem, 0.35vw, 0.3rem); align-items: center; font-family: var(--font-mono); font-size: clamp(0.6rem, 0.85vw, 0.72rem); padding: clamp(0.55rem, 0.9vw, 0.75rem) clamp(0.7rem, 1.1vw, 0.95rem); border: 1px solid var(--ink); background: var(--bg); } .stratum-seq .role { font-weight: 700; color: var(--ink); letter-spacing: 0.08em; text-transform: uppercase; } .stratum-seq .role.srv { text-align: right; } .stratum-seq .msg { text-align: center; color: var(--accent); font-weight: 600; border-bottom: 1px solid var(--muted-2); padding-bottom: 2px; } .stratum-seq .msg.up::before { content: "→ "; color: var(--muted); } .stratum-seq .msg.dn::before { content: "← "; color: var(--muted); }

←→ Navegar

Módulo 05 · Bitcoin

Sesión 1 / Teoría

Recordatorioe

# ¿Qué es Bitcoin?

Un breve repaso a los fundamentos de la primera blockchain descentralizada

Manuel Montenegro Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026

Módulo 05 · Bitcoin

01 · Origen

01 · Origen y esencia

## Dinero electrónico entre pares.

Lo que hace aceptable a una criptomoneda

1.  ¿Puedo confiar en que este dinero es auténtico y no está falsificado?
2.  ¿Puedo confiar en que solo puede gastarse una vez? _(el problema del «doble gasto»)_
3.  ¿Puedo estar seguro de que nadie más podrá reclamarlo como suyo en lugar de mío?

— A. Antonopoulos, _Mastering Bitcoin_ · cap. 1

2008 Whitepaper

2009 Red Bitcoin

21MBTC Suministro finito

~10min Ritmo de bloques

*   **Satoshi Nakamoto (2008)** publica un whitepaper de 9 páginas sobre dinero electrónico P2P.
*   **Red descentralizada** sin autoridad central, sin intermediarios y sin permisos para participar.
*   **Resuelve el doble gasto** en entornos sin confianza mediante consenso por PoW.
*   **Unidad mínima**: 1 BTC = 100 000 000 satoshis; emisión programada hasta alcanzar 21 millones (en teoría).

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 02/17

Módulo 05 · Bitcoin

02 · Criptografía

02 · Cimientos criptográficos

## Propiedad basada en claves

«Poseer bitcoins equivale a poseer la clave privada asociada a la dirección» Esa clave autoriza a gastar las **UTXOs** (_Unspent Transaction Outputs_) vinculadas a la dirección — lo que llamamos «saldo» es simplemente la suma de esas UTXOs.

*   **Criptografía asimétrica** sobre la curva elíptica secp256k1.
*   **Derivación unidireccional**: clave privada → clave pública. Lo contrario es computacionalmente inviable.
*   **SHA-256** como función hash: compromete datos, construye hashes de bloques y direcciones.
*   **Firma digital ECDSA**: demuestra autoría sin revelar la clave privada; cualquiera puede verificarla con la clave pública.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 03/17

Módulo 05 · Bitcoin

03 · Direcciones

03 · Direcciones y transacciones

## Tres formatos, un mismo propósito.

Legacy P2PKH · 1… `1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa` Pay-to-PubKey-Hash — el formato clásico basado en el hash de la clave pública.

Script P2SH · 3… `3J98t1WpEZ73CNmQviecrnyiWrnqRhWNLy` Pay-to-Script-Hash — habilita multi-firma, time-locks y otras condiciones.

SegWit Bech32 · bc1… `bc1qar0srrr7xfkvy5l643lydnw9re59gtzzwf5mdq` Nativo SegWit — tarifas más bajas, mejor detección de errores, estándar actual.

*   **Dirección** = derivada de la clave pública mediante SHA-256 + RIPEMD-160 y codificada (Base58 o Bech32).
*   **Transacción** = conjunto de inputs firmados con la clave privada + outputs que definen los nuevos propietarios.
*   **Fee** = inputs − outputs; incentivo económico que los mineros cobran por incluir la transacción en un bloque.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 04/17

Módulo 05 · Bitcoin

04 · Blockchain

04 · Cadena de bloques

## Bloques enlazados por hash.

BlockN−1

prev\_hash**…0x7a2c**

merkle**…0x9f3e**

nonce**412 877**

hash →

BlockN

prev\_hash**…0xc41e**

merkle**…0x1d88**

nonce**2 901 133**

hash →

BlockN+1

prev\_hash**…0xe502**

merkle**pending**

nonce**?**

*   **Encadenamiento por hash**: cada bloque referencia al anterior, haciendo cualquier modificación pasada visiblemente incoherente.
*   **Merkle root**: compromete todas las transacciones del bloque en un único hash; verificación eficiente en O(log N).
*   **Nonce + PoW**: los mineros prueban valores hasta que el hash cumpla la dificultad objetivo.
*   **Ritmo**: un bloque cada ~10 minutos; reajuste automático de dificultad cada 2 016 bloques.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 05/17

Módulo 05 · Bitcoin

05 · Transacciones

05 · Transacciones y UTXO

## Bitcoin es un registro, no un objeto.

Analogía · Registro de la Propiedad

Los bitcoins **no existen físicamente ni como datos digitales**. Transferir bitcoin se parece a transferir una vivienda: cuando le pasas tu casa a otra persona, _no coges la casa y la mueves a otro sitio_ — eso no tiene sentido.

En su lugar, un **registro público** (la blockchain) anota que la propiedad ahora pertenece a otra persona. «Tener bitcoins» significa, en realidad, **controlar las UTXOs que el registro te atribuye**.

Ejemplo · Transacción con fees

Inputs · UTXOs gastadas

bc1q…a3x0.60 BTC

bc1q…7fe0.42 BTC

Σ in = **1.02 BTC**

tx

Outputs · UTXOs nuevas

bc1q…b2c · pago0.80 BTC

bc1q…9cd · cambio0.21 BTC

Σ out = **1.01 BTC**

Fee Σ in − Σ out = **0.01 BTC** → la diferencia no se declara; emerge como propina implícita que cobra el minero que incluya la transacción en su bloque.

*   **UTXO** (_Unspent Transaction Output_) = cantidad de bitcoin con una condición de gasto; sólo se puede consumir **entera**.
*   **Inputs** = referencias a UTXOs anteriores que se gastan, autorizadas con la firma de la clave privada correspondiente.
*   **Outputs** = nuevas UTXOs que se crean (pago + cambio); todo sobrante vuelve al emisor como una UTXO de «cambio».
*   **Fee implícita**: Σ inputs − Σ outputs. Incentiva al minero a priorizar la transacción (ver _Mastering Bitcoin_, cap. 6).

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 06/17

Módulo 05 · Bitcoin

06 · La red Bitcoin

06 · La red Bitcoin

## Una red P2P plana y abierta.

La red · a vista de pájaro

La «red Bitcoin» es el **conjunto de nodos** que ejecutan el protocolo P2P Bitcoin e intercambian bloques y transacciones mediante _gossip_. **No existen servidores centrales, jerarquías ni intermediarios**.

*   **~10 000 nodos públicos** escuchando en la red principal.
*   **Descubrimiento**: DNS seeds + caché local + petición a pares conocidos.
*   **Handshake**, **inventario**, **getdata**, **block**, **tx**, **headers**… + _heartbeat_.
*   **BIP 324**: comunicación cifrada (no autenticada) entre pares.

Anatomía · 4 módulos funcionales

W Wallet Gestiona claves, firma transacciones.

M Miner Compite en la PoW para crear bloques.

B Blockchain Copia completa e índices locales.

N Network Routing Habla el protocolo P2P y propaga.

El **tipo** de nodo se define por **qué módulos tiene activos**: cada combinación da un perfil distinto.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 07/17

Módulo 05 · Bitcoin

07 · Tipos de nodos

07 · Tipos de nodos

## Cuatro perfiles, cuatro compromisos.

Full Node Bitcoin Core · «Satoshi Client» Módulos: **W · M\* · B · N** (\*minero desactivado por defecto) **Valida cada bloque y transacción** aplicando todas las reglas de consenso. Implementación de referencia (C++, desde 2009). Independencia y privacidad máximas; >95 % de los nodos públicos lo ejecutan.

Archive Node Full node que guarda todo el histórico Módulos: **B · N** (sin wallet, sin minado) Mantiene la **blockchain completa** sin podarla (>700 GB). Sirve datos a clientes SPV, exploradores de bloques, exchanges y procesadores de pago. Actúa como **edge router** del ecosistema.

Lightweight (SPV) Cliente ligero · móviles, wallets Módulos: **W · N** (sin blockchain) Solo descarga **cabeceras de bloques** (~80 B cada una) y usa _Simplified Payment Verification_. Verifica PoW y pruebas Merkle; **confía en nodos completos** para los datos. Menos recursos, menos seguridad.

Third-Party API Wallet delegada · REST / WebSocket Módulos: **W** (sin N, sin B) No habla el protocolo P2P: consulta un servicio externo (Electrum, Esplora, APIs de exchanges…). Saldos, historial y _broadcast_ se **delegan por completo**. Máxima comodidad, máxima dependencia.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 08/17

Módulo 05 · Bitcoin

08 · Nodos ligeros y SPV

08 · Nodos ligeros y SPV

## SPV: verificación simplificada.

Cómo funciona SPV

Un nodo ligero verifica **por profundidad**: si una transacción aparece en un bloque «enterrado» bajo suficiente PoW, se asume válida _sin reconstruir UTXOs_.

*   Descarga **solo cabeceras** (~80 B / bloque) vía mensaje `getheaders`.
*   Verifica la inclusión de una tx con una **prueba Merkle** desde el nodo al root.
*   **Limitación**: puede probar que una tx _existe_, pero no que _no existe_ — vulnerable a doble gasto.

**Filtros** para descubrir tus txs sin revelar direcciones al peer: _Bloom Filters_ (BIP 37, server-side) y _Compact Block Filters_ (BIP 157/158, client-side).

⚠ Riesgo Sybil attack **Un Sybil attack** consiste en crear **muchas identidades falsas** (nodos controlados por el mismo atacante) para _rodear_ a la víctima en la red. Si todos sus pares son hostiles, ve una realidad fabricada. Los SPV son **especialmente sensibles**: sin cadena local no pueden verificar por sí mismos, así que **dependen de sus pares**. También son vulnerables a _network partitioning_, DoS y, en última instancia, a doble gasto. **Defensa**: conectar a muchos pares aleatorios y, si es posible, apuntar al **propio nodo completo**.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 09/17

Módulo 05 · Bitcoin

09 · Relay networks

09 · Propagación y relay networks

## Minimizar la latencia entre mineros.

El problema · block-finding race

Cuando un minero encuentra un bloque, los demás siguen trabajando sobre el anterior hasta que lo reciben. **Esos segundos de retraso favorecen a los grandes mineros** y empujan hacia la centralización. La red pública ya optimiza con _Compact Block Relay_ (BIP 152), pero **algunos actores van más allá con redes privadas**.

2015 Bitcoin Relay Network Matt Corallo · VPSes globales Red privada de servidores virtuales estratégicamente distribuidos para conectar **la mayoría de mineros y pools** con muy baja latencia.

2016 FIBRE Fast Internet Bitcoin Relay Engine Sucesor del BRN. **UDP + Forward Error Correction** + _compact block_: reduce drásticamente la latencia y tolera pérdidas sin re-peticiones.

La latencia es **crítica** en minería competitiva → en las siguientes transparencias nos centraremos en **minado** y proof-of-work.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 10/17

Módulo 05 · Bitcoin

10 · Minado & consenso

10 · Minado = seguridad + consenso

## Consenso emergente, sin autoridad central.

La función real del minado

El propósito del minado **no es crear bitcoins**. Eso es el _incentivo_. El fin último es **asegurar el sistema**: validar transacciones y lograr que **miles de nodos independientes** converjan en la misma verdad sobre _quién posee qué_, sin ningún banco central ni cámara de compensación.

01 / Verificar Cada tx, cada nodo Todos los full nodes validan **independientemente** cada transacción según una lista exhaustiva de reglas.

02 / Agregar PoW + bloques Los mineros empaquetan txs en un bloque candidato y **demuestran cómputo** resolviendo el _proof of work_.

03 / Validar El bloque, por todos Cada nodo verifica el nuevo bloque independientemente y lo encadena al anterior si cumple las reglas.

04 / Elegir Más PoW acumulado Cada nodo selecciona la cadena con **mayor trabajo acumulado**. Esa es, por definición, la verdad.

**Consenso** no se vota: **emerge** de la interacción asíncrona de nodos independientes que siguen reglas simples.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 11/17

Módulo 05 · Bitcoin

11 · La mempool

11 · La mempool

## El limbo de las tx sin confirmar.

Memory pool · mempool

Casi todos los nodos mantienen una **lista temporal en memoria** con las transacciones que han sido _validadas_ y _propagadas_ por la red pero que **todavía no están en ningún bloque**. A esa lista se la llama **mempool**.

Cuando una tx llega nueva, el nodo la **valida**, la guarda en su mempool y la **retransmite** (_relay_) a sus pares. Los mineros eligen **desde la mempool** qué incluyen en su próximo bloque candidato.

~300MB Tamaño por defecto

Local A cada nodo

RAM Donde vive

*   **Mercado de fees**: si la mempool se llena, el nodo expulsa las tx con **feerate más bajo**. Así emerge el precio por byte en vivo.
*   **Perspectiva local**: cada nodo tiene su propia mempool; pueden diferir entre sí según _policy_, uptime y red.
*   **Orphan pool**: tx cuyo «padre» aún no ha llegado se guardan aparte hasta que aparezca, momento en que se promueven a la mempool.
*   **Ciclo**: validar → mempool → relay → minada en bloque → expulsada. También se expulsan por _expiración_ (~2 semanas).

La mempool es la **sala de espera** de Bitcoin — y el termómetro más honesto del estado de la red. Sin ella no habría mercado de fees ni propagación eficiente.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 12/17

Módulo 05 · Bitcoin

12 · Confirmaciones & doble gasto

12 · ¿Cuándo está "confirmada" una tx?

## Cada bloque es otra capa de seguridad.

Confirmación

Una transacción se considera **confirmada** cuando entra en un bloque minado y pasa a formar parte de la blockchain. A partir de ahí, cada bloque posterior añade una _confirmación adicional_ — y cuanta más PoW se apile encima, **más inmutable** se vuelve.

0 En mempool No confirmada · reemplazable

1 Primer bloque Café, propinas

3 Baja exposición Intercambios casuales

6 Regla estándar ~1 hora · defecto

100 Coinbase maturity Recompensa gastable

144 Alto valor ~24 h · bienes caros

Cómo se evita el double spending

Dentro de una misma cadena, las transacciones tienen un **orden topológico**: solo son válidas si gastan salidas de txs _anteriores_ y si **ninguna otra** ha gastado ya esas mismas salidas. Imposible gastar dos veces el mismo UTXO.

Si un atacante intenta reescribir la historia necesita **rehacer el PoW** de todos los bloques desde la tx objetivo — inviable a partir de ~6 confirmaciones salvo con un ataque del **51%**.

⚠ Doble gasto Ataque del 51% Un minero (o coalición) con **mayoría del hash rate** puede forkear la cadena y _reemplazar_ una tx ya confirmada por otra que devuelve el UTXO al atacante. Solo es rentable sobre txs propias y requiere un coste energético enorme. **Defensa**: esperar suficientes confirmaciones antes de entregar bienes de alto valor.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 13/17

Módulo 05 · Bitcoin

13 · Recompensa & Proof of Work

13 · Incentivos + Proof of Work

## Coinbase = subsidy + fees.

Bloque nuevo Subsidy 3,125 BTC (2024+) Bitcoins **acuñados de la nada** en cada bloque. Empezó en **50 BTC** y se _halvea_ cada 210 000 bloques (~4 años). En 2140 será cero.

+

De cada tx Transaction fees Σ(inputs) − Σ(outputs) El minero se queda la _diferencia_ entre inputs y outputs de cada transacción incluida. Con el tiempo **serán la única fuente** de recompensa.

\=

Primera tx del bloque Coinbase transaction Sin inputs reales Tx especial que **no gasta UTXOs**: tiene un _coinbase input_ implícito. Paga al minero y debe esperar **100 confirmaciones** antes de poder gastarse.

Proof of Work · SHA-256 doble

H(merkle\_root, prev\_hash, X) ≤ target

El minero varía **X** (nonce de 32 bits + extra-nonce en el coinbase + timestamp) hasta que el hash del header **cae bajo el target**. Es una lotería: billones de intentos por segundo, ganador ≈ cada 10 min.

Verificar una solución es **instantáneo**; encontrarla cuesta _energía real_. Ése es el coste que asegura la cadena.

Cada cuántos bloques 2 016 Cada ~2 semanas todos los nodos **reajustan** el target de forma independiente, con la misma fórmula.

Fórmula de retarget new\_target = old\_target × (tiempo real 2016 bloques / 20 160 min) Si se minaron **más rápido** de 10 min/bloque → el target baja (más difícil). Si más lento → sube (más fácil). Ajuste máximo ×4 por período.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 14/17

Módulo 05 · Bitcoin

14 · Mining pools & Stratum

14 · Mining pools

## Minar en solitario es una lotería.

Cómo funciona un pool Cooperar para cobrar a menudo Muchos mineros conectan su hardware a un **servidor pool**. El pool arma bloques candidato, distribuye trabajo, y cuando _alguien_ del pool encuentra la solución, el premio se reparte **proporcionalmente al trabajo aportado**.

*   **Primera pool**: Slushpool, diciembre 2010.
*   El pool cobra una comisión típica **< 2%**.
*   Un minero pequeño pasa de "un bloque cada 20 años" a **ingresos diarios** pequeños pero continuos.

Shares · cómo medir el trabajo Un share = hash bajo un target fácil El pool fija un **target más permisivo** (≥ 1 000× más fácil que el de la red). Cada vez que un minero encuentra un hash bajo ese target gana un _share_, que **prueba** que ha hecho trabajo real.

target red   0x000000000000003A30C0…0

target share 0x00000000003A30C0…0

**Reparto**: _PPS_ (pago fijo por share), _PPLNS_ (últimos N shares), _FPPS_ (PPS + incluye fees). Cada estrategia traslada distinto riesgo entre pool y minero.

Protocolo Stratum TCP + JSON-RPC · creado por Slush **No es un BIP**. El minero _no_ necesita un nodo completo: se conecta al pool, recibe **templates de bloque** y devuelve shares. **Stratum v2** añade cifrado y permite que cada minero escoja sus propias txs.

Mineroregistro (user/pass)Pool MinerosubscribePool Mineronotify · block templatePool Mineroset\_difficultyPool Minerosubmit · "share"Pool

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 15/17

Módulo 05 · Bitcoin

15 · Cambiando las reglas · Hard Forks

15 · Hard Forks

## Cuando las reglas de consenso se rompen.

Hard fork Cambio **incompatible hacia atrás**. Alguien introduce una regla nueva que hace **válidos** bloques o txs que antes eran inválidos (o al revés). Los nodos que **no actualicen** rechazarán los nuevos bloques: la red se _parte en dos cadenas_ que evolucionan por separado.

*   Requiere **coordinación casi unánime**: mineros, wallets, exchanges y nodos.
*   Una vez separadas, **no convergen**: aparecen _dos criptomonedas_.
*   Causa habitual: bug en las reglas, o cambio deliberado (tamaño de bloque, formato de firma, etc.).

Caso más famoso · Ago 2017 Bitcoin Cash (BCH) Disputa por el tamaño de bloque (1 MB). Un grupo sube el límite a 8 MB y fuerza un fork en el bloque **478 558**. Nace BCH. Después **BCH se vuelve a forkear** en Bitcoin SV (2018).

Otros casos Bitcoin Gold (2017), Bitcoin XT, Bitcoin Classic Propuestas que, o no lograron adopción (XT, Classic), o derivaron en su propia cadena minoritaria. Ilustran lo **difícil** que es mover Bitcoin por hard fork.

Incidente accidental · Mar 2013 Bug Core 0.7 → 0.8 Un cambio no intencionado en BerkeleyDB provocó un fork involuntario durante 6 bloques. Se resolvió volviendo a la versión antigua.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 16/17

Módulo 05 · Bitcoin

16 · Cambiando las reglas · Soft Forks

16 · Soft Forks

## Reglas que se estrechan, compatibles hacia atrás.

Soft fork Cambio **forward-compatible**. Se introducen reglas **más restrictivas**: todo lo válido bajo la nueva regla sigue siendo válido bajo la antigua. Los nodos sin actualizar **no notan nada** y siguen en consenso con el resto. _Técnicamente no es un fork_.

*   Solo pueden **restringir** lo válido, nunca ampliarlo (o sería un hard fork).
*   Activación por **señalización de mineros**: BIP34, BIP9, BIP8, speedy trial.
*   Críticas: deuda técnica, validación "ciega" en nodos viejos, casi **irreversibles**.

BIP 16 · Abr 2012 P2SH · Pay-to-Script-Hash Permite pagar a un **hash de script** (multifirma, contratos) en vez de a una clave pública. Origen de las direcciones que empiezan por **3…**.

BIP 141/143/147 · Ago 2017 SegWit · Segregated Witness Separa las firmas ("witness") del resto de la tx: arregla la maleabilidad, aumenta la capacidad efectiva del bloque y habilita **Lightning**. Direcciones **bc1q…**.

BIP 340/341/342 · Nov 2021 Taproot Firmas **Schnorr** + MAST: mejora privacidad y coste de contratos complejos. Direcciones **bc1p…**. Activado con _speedy trial_.

En Bitcoin, las reglas cambian **lentamente y con consenso**: los hard forks dividen la red, los soft forks la hacen evolucionar.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 17/17

/\* ======================================================================== SLIDE PRESENTATION CONTROLLER Keyboard · touch · nav dots · progress bar ======================================================================== \*/ class SlidePresentation { constructor() { this.slides = Array.from(document.querySelectorAll('.slide')); this.total = this.slides.length; this.currentSlide = 0; this.progressBar = document.getElementById('progressBar'); this.navDotsContainer = document.getElementById('navDots'); this.\_buildNavDots(); this.\_setupIntersectionObserver(); this.\_setupKeyboardNav(); this.\_setupTouchNav(); this.\_setupScrollProgress(); } \_setupIntersectionObserver() { const io = new IntersectionObserver((entries) => { entries.forEach((entry) => { if (entry.isIntersecting && entry.intersectionRatio >= 0.6) { const idx = this.slides.indexOf(entry.target); entry.target.classList.add('visible'); this.currentSlide = idx; this.\_updateNavDots(); this.\_updateProgress(); } }); }, { threshold: \[0.6\] }); this.slides.forEach((s) => io.observe(s)); } \_setupKeyboardNav() { document.addEventListener('keydown', (e) => { if (e.target && e.target.getAttribute && e.target.getAttribute('contenteditable') === 'true') return; switch (e.key) { case 'ArrowRight': case 'ArrowDown': case ' ': case 'PageDown': e.preventDefault(); this.goTo(this.currentSlide + 1); break; case 'ArrowLeft': case 'ArrowUp': case 'PageUp': e.preventDefault(); this.goTo(this.currentSlide - 1); break; case 'Home': e.preventDefault(); this.goTo(0); break; case 'End': e.preventDefault(); this.goTo(this.total - 1); break; } }); } \_setupTouchNav() { let startY = 0; document.addEventListener('touchstart', (e) => { startY = e.touches\[0\].clientY; }, { passive: true }); document.addEventListener('touchend', (e) => { const endY = e.changedTouches\[0\].clientY; const diff = startY - endY; if (Math.abs(diff) > 60) { this.goTo(this.currentSlide + (diff > 0 ? 1 : -1)); } }, { passive: true }); } \_setupScrollProgress() { window.addEventListener('scroll', () => this.\_updateProgress(), { passive: true }); } \_updateProgress() { const scrollTop = window.scrollY; const total = document.documentElement.scrollHeight - window.innerHeight; const pct = total > 0 ? (scrollTop / total) \* 100 : 0; this.progressBar.style.width = pct + '%'; } \_buildNavDots() { // Clear first in case outerHTML was captured while dots existed this.navDotsContainer.innerHTML = ''; this.slides.forEach((slide, i) => { const b = document.createElement('button'); b.setAttribute('aria-label', \`Ir a diapositiva ${i + 1}: ${slide.dataset.title || ''}\`); if (i === 0) b.classList.add('active'); b.addEventListener('click', () => this.goTo(i)); this.navDotsContainer.appendChild(b); }); } \_updateNavDots() { this.navDotsContainer.querySelectorAll('button').forEach((b, i) => { b.classList.toggle('active', i === this.currentSlide); }); } goTo(i) { const idx = Math.max(0, Math.min(this.total - 1, i)); this.slides\[idx\].scrollIntoView({ behavior: 'smooth', block: 'start' }); } } // Boot · versión presentación (sin editor inline) window.addEventListener('DOMContentLoaded', () => { new SlidePresentation(); const first = document.querySelector('.slide'); if (first) first.classList.add('visible'); });