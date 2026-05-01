  Lightning Network — Módulo 5       /\* ======================================================================== THEME TOKENS · Swiss Modern (adaptado a Lightning Network) Paleta: azul eléctrico + amarillo (chispa) sobre fondo blanco. ======================================================================== \*/ :root { /\* Core palette \*/ --bg: #ffffff; --bg-panel: #f3f6fb; --ink: #0a0a0a; --ink-soft: #2a2f3a; --muted: #6a6f7a; --muted-2: #b0b6c0; --grid: rgba(47, 106, 255, 0.045); --grid-line: rgba(47, 106, 255, 0.10); /\* Accents — Lightning \*/ --accent: #2f6aff; /\* Electric blue (primary) \*/ --accent-2: #0a0a0a; /\* Black co-accent \*/ --accent-ln: #ffd60a; /\* Lightning yellow \*/ --accent-btc:#f7931a; /\* Bitcoin orange (sparingly, para L1) \*/ /\* Typography \*/ --font-display: "Archivo", sans-serif; --font-body: "Nunito", sans-serif; --font-mono: "JetBrains Mono", ui-monospace, monospace; /\* Motion \*/ --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1); --duration-normal: 0.7s; } /\* ======================================================================== GLOBAL RESETS + VIEWPORT FITTING (verbatim shared base) ======================================================================== \*/ \* { margin: 0; padding: 0; box-sizing: border-box; } html, body { height: 100%; overflow-x: hidden; } html { scroll-snap-type: y mandatory; scroll-behavior: smooth; } .slide { width: 100vw; height: 100vh; height: 100dvh; overflow: hidden; scroll-snap-align: start; display: flex; flex-direction: column; position: relative; } .slide-content { flex: 1; display: flex; flex-direction: column; justify-content: center; max-height: 100%; overflow: hidden; padding: var(--slide-padding); } :root { --title-size: clamp(1.5rem, 5vw, 4rem); --h2-size: clamp(1.25rem, 3.5vw, 2.5rem); --h3-size: clamp(1rem, 2.5vw, 1.75rem); --body-size: clamp(0.75rem, 1.5vw, 1.125rem); --small-size: clamp(0.65rem, 1vw, 0.875rem); --slide-padding: clamp(1rem, 4vw, 4rem); --content-gap: clamp(0.5rem, 2vw, 2rem); --element-gap: clamp(0.25rem, 1vw, 1rem); } .card, .container, .content-box { max-width: min(90vw, 1000px); max-height: min(80vh, 700px); } .feature-list, .bullet-list { gap: clamp(0.4rem, 1vh, 1rem); } .feature-list li, .bullet-list li { font-size: var(--body-size); line-height: 1.4; } .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 250px), 1fr)); gap: clamp(0.5rem, 1.5vw, 1rem); } img, .image-container { max-width: 100%; max-height: min(50vh, 400px); object-fit: contain; } @media (max-height: 700px) { :root { --slide-padding: clamp(0.75rem, 3vw, 2rem); --content-gap: clamp(0.4rem, 1.5vw, 1rem); --title-size: clamp(1.25rem, 4.5vw, 2.5rem); --h2-size: clamp(1rem, 3vw, 1.75rem); } } @media (max-height: 600px) { :root { --slide-padding: clamp(0.5rem, 2.5vw, 1.5rem); --content-gap: clamp(0.3rem, 1vw, 0.75rem); --title-size: clamp(1.1rem, 4vw, 2rem); --body-size: clamp(0.7rem, 1.2vw, 0.95rem); } .nav-dots, .keyboard-hint, .decorative { display: none; } } @media (max-height: 500px) { :root { --slide-padding: clamp(0.4rem, 2vw, 1rem); --title-size: clamp(1rem, 3.5vw, 1.5rem); --h2-size: clamp(0.9rem, 2.5vw, 1.25rem); --body-size: clamp(0.65rem, 1vw, 0.85rem); } } @media (max-width: 600px) { :root { --title-size: clamp(1.25rem, 7vw, 2.5rem); } .grid { grid-template-columns: 1fr; } } @media (prefers-reduced-motion: reduce) { \*, \*::before, \*::after { animation-duration: 0.01ms !important; transition-duration: 0.2s !important; } html { scroll-behavior: auto; } } /\* ======================================================================== BODY · BACKGROUND Blanco con una rejilla muy sutil, teñida de azul. ======================================================================== \*/ body { background: var(--bg); color: var(--ink); font-family: var(--font-body); font-size: var(--body-size); line-height: 1.5; background-image: linear-gradient(to right, var(--grid) 1px, transparent 1px); background-size: calc(100% / 12) 100%; } /\* ======================================================================== SLIDE FRAME (header + footer) ======================================================================== \*/ .slide { padding: clamp(1.25rem, 3.5vw, 3.5rem); } .slide-header { display: flex; justify-content: space-between; align-items: center; gap: 1rem; padding-bottom: clamp(0.5rem, 1vw, 0.75rem); border-bottom: 1px solid var(--grid-line); } .slide-header .left { display: flex; align-items: center; gap: 0.75rem; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.65rem, 0.95vw, 0.85rem); letter-spacing: 0.28em; text-transform: uppercase; } .slide-header .left .mark { width: clamp(0.55rem, 0.9vw, 0.8rem); height: clamp(0.55rem, 0.9vw, 0.8rem); background: var(--accent); } .slide-header .right { font-family: var(--font-display); font-weight: 700; font-size: clamp(0.65rem, 0.95vw, 0.85rem); letter-spacing: 0.28em; text-transform: uppercase; color: var(--muted); } .slide-body { flex: 1; display: flex; flex-direction: column; justify-content: center; padding: clamp(1rem, 2vw, 2rem) 0; gap: clamp(0.75rem, 1.5vw, 1.5rem); min-height: 0; } .slide-footer { display: flex; justify-content: space-between; align-items: baseline; gap: 1rem; padding-top: clamp(0.4rem, 0.8vw, 0.75rem); border-top: 1px solid var(--grid-line); font-family: var(--font-body); font-weight: 400; font-size: clamp(0.65rem, 0.9vw, 0.8rem); color: var(--muted); } .slide-footer b { color: var(--ink); font-weight: 600; } .slide-footer .page { font-family: var(--font-display); font-weight: 800; letter-spacing: 0.18em; color: var(--ink); } .slide-footer .page .sep { color: var(--muted-2); margin: 0 0.3em; } /\* ======================================================================== KICKER + HEADING ======================================================================== \*/ .kicker { display: inline-flex; align-items: center; gap: clamp(0.4rem, 0.7vw, 0.6rem); font-family: var(--font-display); font-weight: 800; font-size: clamp(0.7rem, 1vw, 0.95rem); letter-spacing: 0.25em; text-transform: uppercase; color: var(--accent); } .kicker .bar { width: clamp(1.25rem, 2.5vw, 2.5rem); height: clamp(0.15rem, 0.25vw, 0.25rem); background: var(--accent); } h2.heading { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.75rem, 5.5vw, 4.75rem); line-height: 0.95; letter-spacing: -0.025em; color: var(--ink); max-width: 18ch; } h2.heading .accent { color: var(--accent); } h2.heading .spark { color: var(--accent-ln); } h2.heading .stroke { color: transparent; -webkit-text-stroke: clamp(1px, 0.15vw, 2px) var(--ink); } /\* ======================================================================== TITLE SLIDE ======================================================================== \*/ .title-slide { background: var(--bg); } .title-slide .slide-body { display: grid; grid-template-columns: 1fr; grid-template-rows: 1fr auto; gap: clamp(1rem, 2vw, 2rem); } .title-slide .title-main { align-self: center; max-width: 24ch; } .title-slide .eyebrow-tag { display: inline-block; padding: clamp(0.3rem, 0.5vw, 0.45rem) clamp(0.65rem, 1vw, 0.95rem); background: var(--accent); color: #fff; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.7rem, 1vw, 0.9rem); letter-spacing: 0.28em; text-transform: uppercase; margin-bottom: clamp(1rem, 2vw, 1.5rem); } .title-slide h1 { font-family: var(--font-display); font-weight: 900; font-size: clamp(2.5rem, 10vw, 9rem); line-height: 0.88; letter-spacing: -0.035em; } .title-slide h1 .accent { color: var(--accent); } .title-slide h1 .spark { color: var(--accent-ln); } .title-slide .rule { margin-top: clamp(1rem, 2vw, 1.5rem); width: clamp(2.5rem, 5vw, 5rem); height: clamp(0.2rem, 0.3vw, 0.3rem); background: var(--ink); } .title-slide .subline { margin-top: clamp(0.75rem, 1.5vw, 1.25rem); font-family: var(--font-body); font-size: clamp(0.9rem, 1.4vw, 1.25rem); color: var(--ink-soft); max-width: 40ch; line-height: 1.45; } .title-slide .bolt-deco { position: absolute; top: clamp(3rem, 8vw, 7rem); right: clamp(2rem, 6vw, 6rem); width: clamp(7rem, 16vw, 17rem); height: clamp(7rem, 16vw, 17rem); border: clamp(1.5px, 0.25vw, 3px) solid var(--ink); border-radius: 50%; display: grid; place-items: center; pointer-events: none; background: radial-gradient(circle at 50% 40%, rgba(255, 214, 10, 0.18), transparent 60%); } .title-slide .bolt-deco svg { width: 45%; height: 45%; fill: var(--accent-ln); stroke: var(--ink); stroke-width: 2; filter: drop-shadow(0 0 10px rgba(47, 106, 255, 0.35)); } .title-slide .byline { display: flex; justify-content: space-between; align-items: baseline; gap: 1rem; font-family: var(--font-body); font-size: clamp(0.8rem, 1.1vw, 1rem); } .title-slide .byline .name { font-weight: 700; color: var(--ink); } .title-slide .byline .meta { font-family: var(--font-display); font-weight: 700; letter-spacing: 0.25em; text-transform: uppercase; font-size: clamp(0.65rem, 0.9vw, 0.8rem); color: var(--muted); } /\* ======================================================================== LAYOUT · TWO-COLUMN ======================================================================== \*/ .two-col { display: grid; grid-template-columns: minmax(0, 5fr) minmax(0, 7fr); gap: clamp(1.5rem, 3vw, 3rem); align-items: start; min-height: 0; } @media (max-width: 720px) { .two-col { grid-template-columns: 1fr; } } .col-left { display: flex; flex-direction: column; gap: clamp(0.75rem, 1.5vw, 1.25rem); } .col-right { display: flex; flex-direction: column; gap: clamp(0.75rem, 1.5vw, 1.25rem); min-width: 0; } /\* ======================================================================== BULLET LIST (Swiss, numerada) ======================================================================== \*/ ul.feature-list { list-style: none; display: flex; flex-direction: column; counter-reset: bullet; } ul.feature-list li { position: relative; padding: clamp(0.5rem, 1vw, 0.8rem) 0 clamp(0.5rem, 1vw, 0.8rem) clamp(2.25rem, 3.5vw, 3rem); border-bottom: 1px solid var(--grid-line); counter-increment: bullet; font-size: clamp(0.85rem, 1.2vw, 1rem); line-height: 1.5; color: var(--ink-soft); } ul.feature-list li::before { content: counter(bullet, decimal-leading-zero); position: absolute; top: clamp(0.55rem, 1.1vw, 0.9rem); left: 0; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.7rem, 1vw, 0.85rem); letter-spacing: 0.15em; color: var(--accent); } ul.feature-list li b { color: var(--ink); font-weight: 700; } /\* ======================================================================== PULL QUOTE · BLOCK (borde izquierdo en color acento) ======================================================================== \*/ .pull-quote { padding: clamp(1rem, 2vw, 1.75rem) clamp(1.25rem, 2.5vw, 2rem); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); background: var(--bg-panel); font-family: var(--font-display); font-weight: 500; font-size: clamp(1rem, 2vw, 1.5rem); line-height: 1.25; color: var(--ink); letter-spacing: -0.01em; } .pull-quote .src { display: block; margin-top: clamp(0.4rem, 0.8vw, 0.7rem); font-family: var(--font-body); font-weight: 600; font-style: italic; font-size: clamp(0.7rem, 1vw, 0.9rem); color: var(--muted); letter-spacing: 0.02em; } /\* ======================================================================== STAT STRIP ======================================================================== \*/ .stat-strip { display: grid; grid-template-columns: repeat(4, 1fr); gap: clamp(0.5rem, 1vw, 1rem); padding: clamp(0.75rem, 1.5vw, 1rem) 0; border-top: clamp(1.5px, 0.25vw, 2px) solid var(--ink); border-bottom: clamp(1.5px, 0.25vw, 2px) solid var(--ink); } @media (max-width: 720px) { .stat-strip { grid-template-columns: repeat(2, 1fr); } } .stat { display: flex; flex-direction: column; gap: 0.2rem; } .stat .num { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.4rem, 3.5vw, 3rem); line-height: 1; letter-spacing: -0.03em; color: var(--ink); } .stat .num .small { font-size: 0.55em; color: var(--muted); margin-left: 0.1em; letter-spacing: 0.05em; } .stat .lbl { font-family: var(--font-display); font-weight: 700; font-size: clamp(0.6rem, 0.85vw, 0.75rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } /\* ======================================================================== CARDS (tarjetas genéricas) ======================================================================== \*/ .card-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: clamp(0.5rem, 1vw, 0.85rem); } .card-grid.cols-2 { grid-template-columns: repeat(2, 1fr); } .card-grid.cols-4 { grid-template-columns: repeat(4, 1fr); } @media (max-width: 900px) { .card-grid, .card-grid.cols-2, .card-grid.cols-4 { grid-template-columns: 1fr; } } .p-card { padding: clamp(0.75rem, 1.2vw, 1rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.35rem, 0.6vw, 0.5rem); min-width: 0; position: relative; } .p-card.panel { background: var(--bg-panel); } .p-card.highlight { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); } .p-card.warn { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent-ln); } .p-card .idx { font-family: var(--font-mono); font-size: clamp(0.6rem, 0.8vw, 0.72rem); color: var(--accent); letter-spacing: 0.14em; } .p-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.82rem, 1.15vw, 1rem); color: var(--ink); line-height: 1.2; } .p-card .desc { font-size: clamp(0.7rem, 0.95vw, 0.82rem); color: var(--ink-soft); line-height: 1.4; } .p-card .tag { display: inline-block; padding: 0.1rem 0.45rem; background: var(--ink); color: #fff; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.55rem, 0.75vw, 0.7rem); letter-spacing: 0.15em; text-transform: uppercase; border-radius: 2px; align-self: flex-start; } .p-card .tag.warn { background: var(--accent-ln); color: var(--ink); } .p-card .tag.accent { background: var(--accent); } .p-card .mini-list { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: clamp(0.18rem, 0.35vw, 0.3rem); font-size: clamp(0.66rem, 0.85vw, 0.76rem); color: var(--ink-soft); line-height: 1.35; } .p-card .mini-list li { padding-left: 0.9em; position: relative; } .p-card .mini-list li::before { content: '▸'; color: var(--accent); position: absolute; left: 0; font-size: 0.8em; top: 0.1em; } /\* ======================================================================== CODE / MONO BLOCKS ======================================================================== \*/ .mono, code, pre { font-family: var(--font-mono); font-size: clamp(0.7rem, 0.95vw, 0.88rem); } .code-block { padding: clamp(0.6rem, 1vw, 0.9rem) clamp(0.75rem, 1.2vw, 1.1rem); background: var(--ink); color: #e6ecf7; border-radius: 2px; overflow: auto; line-height: 1.5; font-family: var(--font-mono); font-size: clamp(0.7rem, 0.95vw, 0.85rem); } .code-block .c { color: #8ca0d8; } .code-block .k { color: var(--accent-ln); } .code-block .s { color: #a6e3a1; } .code-block .n { color: #ffb86c; } /\* ======================================================================== LIGHTNING · DIAGRAMAS SVG Estilos para los SVG embebidos. ======================================================================== \*/ .diagram-wrap { border: 1px solid var(--grid-line); background: var(--bg-panel); padding: clamp(0.5rem, 1vw, 0.9rem); display: flex; justify-content: center; align-items: center; min-height: 0; } .diagram-wrap svg { width: 100%; height: auto; max-height: min(55vh, 480px); } .diagram-caption { text-align: center; font-family: var(--font-display); font-weight: 700; font-size: clamp(0.65rem, 0.9vw, 0.78rem); letter-spacing: 0.2em; text-transform: uppercase; color: var(--muted); margin-top: 0.4rem; } /\* Nodos de diagrama \*/ .svg-node { fill: var(--bg); stroke: var(--ink); stroke-width: 2; } .svg-node-alice { fill: var(--accent); stroke: var(--accent); } .svg-node-eric { fill: var(--accent-ln); stroke: var(--ink); } .svg-node-hop { fill: var(--bg-panel); stroke: var(--ink); stroke-width: 2; } .svg-label { font-family: var(--font-display); font-weight: 800; font-size: 13px; fill: var(--ink); text-anchor: middle; } .svg-label-light { fill: #fff; } .svg-sub { font-family: var(--font-body); font-size: 11px; fill: var(--muted); text-anchor: middle; } .svg-edge { stroke: var(--ink); stroke-width: 2; fill: none; } .svg-edge-active { stroke: var(--accent); stroke-width: 3; } .svg-edge-dashed { stroke-dasharray: 5,3; } .svg-amount { font-family: var(--font-mono); font-size: 11px; fill: var(--ink); } .svg-step-label { font-family: var(--font-display); font-weight: 800; font-size: 10px; letter-spacing: 0.1em; fill: var(--accent); text-transform: uppercase; } /\* ======================================================================== CHANNEL-STATE · Slide "Anatomía de un canal" ======================================================================== \*/ .channel-steps { display: grid; grid-template-columns: repeat(3, 1fr); gap: clamp(0.5rem, 1vw, 1rem); min-height: 0; } @media (max-width: 900px) { .channel-steps { grid-template-columns: 1fr; } } .ch-step { border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; padding: 0; min-height: 0; } .ch-step .ch-hdr { background: var(--ink); color: #fff; padding: clamp(0.35rem, 0.7vw, 0.5rem) clamp(0.6rem, 1vw, 0.8rem); font-family: var(--font-display); font-weight: 800; font-size: clamp(0.65rem, 0.9vw, 0.8rem); letter-spacing: 0.18em; text-transform: uppercase; display: flex; align-items: center; gap: 0.5rem; } .ch-step .ch-hdr .num { color: var(--accent-ln); } .ch-step .ch-body { padding: clamp(0.6rem, 1vw, 0.9rem); display: flex; flex-direction: column; gap: clamp(0.35rem, 0.7vw, 0.55rem); } .ch-step .ch-body .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.82rem, 1.15vw, 1rem); color: var(--ink); } .ch-step .ch-body .desc { font-size: clamp(0.7rem, 0.95vw, 0.82rem); color: var(--ink-soft); line-height: 1.4; } .ch-step .ch-body .mono { font-family: var(--font-mono); font-size: clamp(0.65rem, 0.85vw, 0.75rem); color: var(--accent); } /\* ======================================================================== COMPARATIVO · tabla ligera sin <table> ======================================================================== \*/ .compare-grid { display: grid; grid-template-columns: 1.5fr 2fr 2fr; gap: 0; min-height: 0; border: 1px solid var(--ink); } .compare-grid > div { padding: clamp(0.5rem, 0.9vw, 0.7rem) clamp(0.6rem, 1vw, 0.85rem); border-bottom: 1px solid var(--grid-line); border-right: 1px solid var(--grid-line); font-size: clamp(0.75rem, 1vw, 0.9rem); line-height: 1.4; min-width: 0; } .compare-grid > div:nth-child(3n) { border-right: none; } .compare-grid > div.hdr { background: var(--ink); color: #fff; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.65rem, 0.85vw, 0.8rem); letter-spacing: 0.18em; text-transform: uppercase; border-bottom: none; } .compare-grid > div.rowlabel { background: var(--bg-panel); font-family: var(--font-display); font-weight: 700; color: var(--ink); } /\* ======================================================================== LIQUIDITY · BARS (inbound/outbound) ======================================================================== \*/ .liq-bar { height: clamp(1.25rem, 2vw, 1.75rem); display: grid; grid-template-columns: var(--out, 50%) var(--inb, 50%); border: 1px solid var(--ink); overflow: hidden; } .liq-bar .out { background: var(--accent); position: relative; } .liq-bar .inb { background: var(--accent-ln); position: relative; } .liq-bar .out::after, .liq-bar .inb::after { content: attr(data-label); position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.8vw, 0.75rem); letter-spacing: 0.15em; text-transform: uppercase; color: var(--ink); white-space: nowrap; } .liq-bar .out::after { color: #fff; } /\* ======================================================================== INVOICE BLOCK (BOLT 11 descomposición) ======================================================================== \*/ .invoice { border: 1px solid var(--ink); background: var(--bg-panel); padding: clamp(0.6rem, 1vw, 0.9rem) clamp(0.75rem, 1.2vw, 1.1rem); font-family: var(--font-mono); font-size: clamp(0.72rem, 0.95vw, 0.85rem); color: var(--ink-soft); word-break: break-all; line-height: 1.55; } .invoice .seg-hrp { color: var(--accent); font-weight: 700; } .invoice .seg-net { color: var(--accent-btc); } .invoice .seg-amt { color: var(--ink); font-weight: 700; background: var(--accent-ln); padding: 0 2px; } .invoice .seg-sep { color: var(--muted); font-style: italic; } .invoice .seg-ts { color: var(--accent-btc); font-weight: 600; } .invoice .seg-tag { color: var(--ink-soft); } .invoice .seg-sig { color: var(--muted); opacity: 0.7; } .invoice .seg-data { color: var(--muted); } .invoice-legend { display: flex; flex-wrap: wrap; gap: clamp(0.35rem, 0.8vw, 0.7rem); margin-top: clamp(0.4rem, 0.7vw, 0.6rem); font-family: var(--font-mono); font-size: clamp(0.58rem, 0.72vw, 0.68rem); color: var(--ink-soft); text-transform: uppercase; letter-spacing: 0.08em; } .invoice-legend span { display: inline-flex; align-items: center; gap: 0.3em; } .invoice-legend i { display: inline-block; width: 0.6em; height: 0.6em; border: 1px solid var(--ink); background: var(--bg-panel); } .invoice-legend .sw-hrp { background: var(--accent); border-color: var(--accent); } .invoice-legend .sw-amt { background: var(--accent-ln); } .invoice-legend .sw-ts { background: var(--accent-btc); border-color: var(--accent-btc); } .invoice-legend .sw-tag { background: var(--ink-soft); border-color: var(--ink-soft); } .invoice-legend .sw-sig { background: var(--muted); border-color: var(--muted); opacity: 0.7; } /\* ======================================================================== DECODED INVOICE TABLE + DECODER LINK ======================================================================== \*/ .decoded-table { margin-top: clamp(0.5rem, 0.9vw, 0.8rem); border: 1px solid var(--ink); background: var(--bg-panel); font-size: clamp(0.62rem, 0.78vw, 0.72rem); line-height: 1.4; } .decoded-table .dt-row { display: grid; grid-template-columns: clamp(90px, 11vw, 130px) 1fr; gap: clamp(0.4rem, 0.8vw, 0.7rem); padding: clamp(0.2rem, 0.4vw, 0.32rem) clamp(0.5rem, 0.9vw, 0.75rem); border-bottom: 1px solid rgba(10, 10, 10, 0.08); } .decoded-table .dt-row:last-child { border-bottom: none; } .decoded-table .dt-k { font-family: var(--font-display); font-weight: 800; text-transform: uppercase; letter-spacing: 0.06em; color: var(--ink-soft); font-size: 0.92em; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; } .decoded-table .dt-v { color: var(--ink); word-break: break-all; } .decoded-table .dt-v.mono { font-family: var(--font-mono); font-size: 0.92em; color: var(--ink-soft); } .decoded-table .dt-v .sub { color: var(--muted); font-size: 0.92em; } .decoder-link { display: flex; align-items: center; gap: clamp(0.4rem, 0.8vw, 0.65rem); margin-top: clamp(0.4rem, 0.8vw, 0.6rem); padding: clamp(0.35rem, 0.6vw, 0.5rem) clamp(0.55rem, 0.9vw, 0.75rem); border: 1px dashed var(--accent); background: rgba(47, 106, 255, 0.05); font-size: clamp(0.68rem, 0.85vw, 0.78rem); flex-wrap: wrap; } .decoder-link .dl-tag { font-family: var(--font-display); font-weight: 800; color: var(--accent); letter-spacing: 0.1em; font-size: 0.78em; } .decoder-link a { font-family: var(--font-mono); color: var(--accent); font-weight: 700; text-decoration: underline; } .decoder-link .dl-desc { color: var(--ink-soft); } /\* ======================================================================== PROGRESS BAR + NAV DOTS ======================================================================== \*/ .progress-bar { position: fixed; top: 0; left: 0; height: clamp(2px, 0.3vw, 3px); width: 0%; background: var(--accent); z-index: 100; transition: width 0.3s var(--ease-out-expo); } .nav-dots { position: fixed; right: clamp(0.75rem, 1.5vw, 1.5rem); top: 50%; transform: translateY(-50%); z-index: 90; display: flex; flex-direction: column; gap: clamp(0.4rem, 0.8vw, 0.65rem); } .nav-dots button { width: clamp(0.5rem, 0.8vw, 0.65rem); height: clamp(0.5rem, 0.8vw, 0.65rem); border-radius: 50%; border: 1px solid var(--ink); background: transparent; cursor: pointer; padding: 0; transition: background 0.25s ease, transform 0.25s ease; } .nav-dots button:hover { transform: scale(1.25); } .nav-dots button.active { background: var(--accent); border-color: var(--accent); } .keyboard-hint { position: fixed; bottom: clamp(0.75rem, 1.5vw, 1.25rem); left: 50%; transform: translateX(-50%); z-index: 90; font-family: var(--font-display); font-weight: 700; font-size: clamp(0.6rem, 0.85vw, 0.75rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); display: flex; gap: clamp(0.5rem, 1vw, 0.85rem); align-items: center; pointer-events: none; } .keyboard-hint .key { display: inline-block; padding: 0.1rem 0.4rem; border: 1px solid var(--muted-2); border-radius: 3px; background: var(--bg); color: var(--ink); } /\* ======================================================================== ANIMATIONS ======================================================================== \*/ .reveal { opacity: 0; transform: translateY(26px); transition: opacity var(--duration-normal) var(--ease-out-expo), transform var(--duration-normal) var(--ease-out-expo); } .slide.visible .reveal { opacity: 1; transform: translateY(0); } .slide.visible .reveal:nth-of-type(1) { transition-delay: 0.05s; } .slide.visible .reveal:nth-of-type(2) { transition-delay: 0.15s; } .slide.visible .reveal:nth-of-type(3) { transition-delay: 0.28s; } .slide.visible .reveal:nth-of-type(4) { transition-delay: 0.42s; } .slide.visible .reveal:nth-of-type(5) { transition-delay: 0.55s; } .slide.visible .reveal:nth-of-type(6) { transition-delay: 0.68s; } /\* Lightning sparkle animation (accent) \*/ @keyframes spark { 0%, 100% { opacity: 1; filter: drop-shadow(0 0 4px rgba(255, 214, 10, 0.6)); } 50% { opacity: 0.7; filter: drop-shadow(0 0 12px rgba(255, 214, 10, 0.9)); } } .title-slide .bolt-deco svg { animation: spark 2.6s var(--ease-out-expo) infinite; } /\* ======================================================================== LN STACK DIAGRAM · Slide "Arquitectura técnica" ======================================================================== \*/ .ln-stack { display: flex; flex-direction: column; gap: clamp(0.5rem, 1vw, 0.85rem); margin: 0; width: 100%; } .ln-stack-frame { border: 1px solid var(--ink); background: linear-gradient(var(--bg-panel), var(--bg-panel)) padding-box, repeating-linear-gradient(45deg, transparent 0 6px, rgba(47,106,255,0.04) 6px 7px); padding: clamp(0.75rem, 2vw, 1.5rem) clamp(0.5rem, 1.5vw, 1.25rem); position: relative; } .ln-stack-frame::before { content: 'STACK'; position: absolute; top: -0.5rem; left: clamp(0.75rem, 1.5vw, 1.25rem); background: var(--bg); padding: 0 0.5rem; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.85vw, 0.75rem); letter-spacing: 0.28em; color: var(--accent); } .ln-stack-frame svg { width: 100%; height: auto; max-height: clamp(260px, 42vh, 420px); display: block; } .ln-stack figcaption { font-size: clamp(0.72rem, 0.95vw, 0.85rem); color: var(--ink-soft); line-height: 1.5; text-align: center; } .ln-stack figcaption b { color: var(--ink); font-weight: 700; } /\* ======================================================================== CAROUSEL · Ejemplo completo paso a paso Grafico SVG + panel lateral con descripción + balances. ======================================================================== \*/ .carousel { display: grid; grid-template-columns: minmax(0, 7fr) minmax(0, 5fr); gap: clamp(0.75rem, 1.5vw, 1.25rem); align-items: stretch; min-height: 0; flex: 1; } @media (max-width: 900px) { .carousel { grid-template-columns: 1fr; } } /\* Stage: SVG container \*/ .carousel-stage { position: relative; background: var(--bg-panel); border: 1px solid var(--ink); padding: clamp(0.5rem, 1vw, 0.85rem); display: flex; flex-direction: column; min-width: 0; min-height: 0; } .carousel-stage svg { width: 100%; height: auto; flex: 1; max-height: clamp(200px, 42vh, 360px); } /\* Nodes & links in the SVG evolve via \[data-active-step\] on the stage \*/ .ln-node circle { fill: var(--bg); stroke: var(--ink); stroke-width: 2; transition: fill 0.35s ease, stroke 0.35s ease; } .ln-node.active circle { fill: var(--accent); stroke: var(--accent); } .ln-node.origin circle { fill: var(--accent-ln); stroke: var(--ink); } .ln-node .label { font-family: var(--font-display); font-weight: 800; font-size: 14px; fill: var(--ink); text-anchor: middle; } .ln-node.active .label { fill: #fff; } .ln-link { stroke: var(--muted-2); stroke-width: 2.5; fill: none; } .ln-link.active { stroke: var(--accent); stroke-width: 3.5; } /\* Step-gated SVG elements: show only if their data-steps contains the current step \*/ .carousel-stage \[data-steps\] { opacity: 0; transition: opacity 0.3s ease; } .carousel-stage \[data-steps\].on { opacity: 1; } /\* HTLC arrow labels & balance pills \*/ .ln-htlc { font-family: var(--font-mono); font-size: 10.5px; font-weight: 600; fill: var(--accent); text-anchor: middle; } .ln-htlc.settle { fill: #0a7f3d; } .ln-arrow { stroke: var(--accent); stroke-width: 2.5; fill: none; marker-end: url(#arrowAccent); } .ln-arrow.back { stroke: #0a7f3d; marker-end: url(#arrowGreen); } /\* Bottom balances row under SVG \*/ .ln-balances { display: grid; grid-template-columns: repeat(4, 1fr); gap: clamp(0.35rem, 0.8vw, 0.6rem); margin-top: clamp(0.4rem, 0.9vw, 0.7rem); } .ln-balance { border: 1px solid var(--ink); background: var(--bg); padding: clamp(0.3rem, 0.6vw, 0.45rem) clamp(0.35rem, 0.7vw, 0.5rem); font-family: var(--font-mono); font-size: clamp(0.55rem, 0.78vw, 0.7rem); line-height: 1.3; color: var(--ink-soft); min-width: 0; display: flex; flex-direction: column; gap: clamp(0.2rem, 0.4vw, 0.3rem); } .ln-balance .pair { display: block; font-family: var(--font-display); font-weight: 800; color: var(--ink); font-size: clamp(0.55rem, 0.78vw, 0.7rem); letter-spacing: 0.06em; padding-bottom: clamp(0.15rem, 0.35vw, 0.25rem); border-bottom: 1px solid var(--grid-line); } .ln-balance .val { display: flex; flex-direction: column; gap: 0.15rem; } .ln-balance .val span { display: block; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; } .ln-balance.updated { background: rgba(47, 106, 255, 0.08); border-color: var(--accent); } /\* Right panel \*/ .carousel-panel { display: flex; flex-direction: column; gap: clamp(0.5rem, 1vw, 0.8rem); min-width: 0; min-height: 0; } .carousel-step-head { display: flex; align-items: baseline; gap: clamp(0.5rem, 1vw, 0.9rem); padding-bottom: clamp(0.35rem, 0.7vw, 0.55rem); border-bottom: 2px solid var(--ink); } .carousel-step-head .step-num { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.6rem, 3.2vw, 2.5rem); color: var(--accent); line-height: 1; letter-spacing: -0.03em; } .carousel-step-head .step-title { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.85rem, 1.35vw, 1.15rem); color: var(--ink); line-height: 1.2; } .carousel-step-desc { font-size: clamp(0.72rem, 1vw, 0.88rem); color: var(--ink-soft); line-height: 1.5; } .carousel-step-desc code, .carousel-step-desc .m { font-family: var(--font-mono); background: var(--bg-panel); padding: 0.05rem 0.3rem; border-radius: 2px; font-size: 0.92em; color: var(--ink); } .carousel-step-desc b { color: var(--ink); } /\* Step navigation \*/ .carousel-nav { display: flex; align-items: center; justify-content: space-between; gap: clamp(0.4rem, 0.8vw, 0.7rem); margin-top: auto; } .carousel-nav .dots { display: flex; gap: clamp(0.2rem, 0.4vw, 0.35rem); flex: 1; flex-wrap: wrap; } .carousel-nav .dot { width: clamp(18px, 2vw, 22px); height: clamp(18px, 2vw, 22px); border: 1px solid var(--ink); background: var(--bg); font-family: var(--font-mono); font-size: clamp(0.55rem, 0.75vw, 0.65rem); font-weight: 600; color: var(--ink-soft); cursor: pointer; display: grid; place-items: center; transition: background 0.2s ease, color 0.2s ease; padding: 0; } .carousel-nav .dot:hover { background: var(--bg-panel); } .carousel-nav .dot.active { background: var(--accent); border-color: var(--accent); color: #fff; } .carousel-nav .arrow { width: clamp(26px, 2.8vw, 32px); height: clamp(26px, 2.8vw, 32px); border: 1px solid var(--ink); background: var(--bg); font-family: var(--font-display); font-weight: 900; cursor: pointer; display: grid; place-items: center; transition: background 0.2s ease; } .carousel-nav .arrow:hover { background: var(--ink); color: #fff; } .carousel-nav .arrow:disabled { opacity: 0.25; cursor: not-allowed; } .carousel-nav .arrow:disabled:hover { background: var(--bg); color: var(--ink); } /\* ======================================================================== INLINE EDITING UI ======================================================================== \*/ .edit-hotzone { position: fixed; top: 0; left: 0; width: 80px; height: 80px; z-index: 10000; cursor: pointer; } .edit-toggle { position: fixed; top: clamp(0.75rem, 1.5vw, 1.25rem); left: clamp(0.75rem, 1.5vw, 1.25rem); width: clamp(2.25rem, 3vw, 2.75rem); height: clamp(2.25rem, 3vw, 2.75rem); border: 1px solid var(--ink); background: var(--bg); border-radius: 50%; cursor: pointer; z-index: 10001; display: grid; place-items: center; font-size: clamp(0.9rem, 1.3vw, 1.1rem); opacity: 0; pointer-events: none; transition: opacity 0.3s ease, background 0.2s ease; } .edit-toggle.show, .edit-toggle.active { opacity: 1; pointer-events: auto; } .edit-toggle.active { background: var(--accent); border-color: var(--accent); color: #fff; } .edit-banner { position: fixed; top: clamp(0.75rem, 1.5vw, 1.25rem); left: 50%; transform: translate(-50%, -120%); background: var(--ink); color: #fff; padding: clamp(0.4rem, 0.8vw, 0.55rem) clamp(0.75rem, 1.2vw, 1rem); font-family: var(--font-display); font-weight: 800; font-size: clamp(0.65rem, 0.9vw, 0.8rem); letter-spacing: 0.22em; text-transform: uppercase; border-radius: 3px; z-index: 10002; transition: transform 0.35s var(--ease-out-expo), opacity 0.25s ease; white-space: nowrap; opacity: 0; pointer-events: none; visibility: hidden; } .edit-banner.active { transform: translate(-50%, 0); opacity: 1; pointer-events: auto; visibility: visible; } .edit-banner .dot { display: inline-block; width: 0.5rem; height: 0.5rem; background: var(--accent); border-radius: 50%; margin-right: 0.55rem; vertical-align: middle; animation: pulse 1.2s ease-in-out infinite; } @keyframes pulse { 0%, 100% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.4); opacity: 0.6; } } body.edit-active \[contenteditable="true"\] { outline: 1px dashed var(--accent); outline-offset: 3px; cursor: text; border-radius: 2px; } body.edit-active \[contenteditable="true"\]:focus { outline: 2px solid var(--accent); background: rgba(47, 106, 255, 0.06); }

←→ Navegar

Módulo 05 · Lightning Network

Sesión 3 / Teoría

Segunda capa

# Lightning Network

Pagos instantáneos, privados, escalables y de bajo coste sobre la Bitcoin Network.

Manuel Montenegro Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026

Módulo 05 · Lightning Network

01 · Escalabilidad

01 · El reto

## Bitcoin es seguro, pero lento.

Confirmar cada café en la cadena principal es caro, lento y poco privado. La descentralización y la seguridad se pagan en throughput.

~10Tx / segundo

~10minPor bloque

1–4MBPeso bloque

6×conf.≈ 1 hora

*   **Cuello de botella on-chain**: cada tx consume espacio de bloque y fee. Con congestión, pagos de unos euros dejan de tener sentido.
*   **Latencia de confirmación**: una tx sin confirmar puede ser reorganizada. Esperar 10 minutos a que se confirme el bloque no hace que la transacción sea segura.
*   **Privacidad limitada**: cada transacción queda pública en la cadena para siempre.
*   **No válido para micropagos**: pagar 50 sats en on-chain cuesta más fees que el propio pago.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 02/17

Módulo 05 · Lightning Network

02 · Segunda capa

02 · Panorama de soluciones L2

## Construir sobre Bitcoin sin tocarlo.

01 · ACTIVOS RGB

Emite y transfiere **activos** (stablecoins, tokens, NFTs) con _client-side validation_. Los datos viven _off-chain_; la L1 sólo graba un hash-commitment incrustado en una UTXO (técnica _Pay-to-Contract_).

**Ventaja:** máxima privacidad — la cadena no ve nada del activo. **Reto:** emisor y receptor deben conservar la historia completa.

02 · ACTIVOS Taproot Assets

Propuesta de Lightning Labs. Emite **activos** anclados en outputs Taproot mediante _Merkle trees_. Pueden enrutarse por Lightning → stablecoins a velocidad LN.

**Ventaja:** interoperable con Lightning vía LND. **Caso típico:** Tether (USDT) pagable como sats.

03 · PAGOS Lightning Network

Red de **canales de pago** enrutados con HTLCs que permite enviar bitcoin entre cualquier par de nodos de forma **instantánea y barata**.

**Ventaja:** miles de tx/s efectivas, fees de sats, finalidad en < 1 segundo. **Madurez:** la L2 más adoptada.

¿Qué comparten?

No cambian el protocolo base. Firman operaciones _off-chain_ y, si hay conflicto, recurren a la L1 como tribunal. Herencia de **seguridad** gracias a Bitcoin.

¿En qué se diferencian?

Lightning resuelve **pagos**. RGB y Taproot Assets resuelven **emisión y transferencia de activos**. Se complementan, no compiten.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 03/17

Módulo 05 · Lightning Network

03 · Canales de pago

03 · Canales de pago · La idea clave

## Un canal de pago es un 2-of-2 multisig con saldo móvil.

Un **canal de pago** es un acuerdo financiero bilateral entre dos nodos: bloquean fondos en la cadena y después intercambian _off-chain_ actualizaciones firmadas del saldo, liquidables en cualquier momento. Es el ladrillo sobre el que se construye toda Lightning Network.

Ciclo de vida del canal

*   **Apertura on-chain**: Alice y Bob publican una _funding transaction_ que envía N BTC a un output 2-de-2 (multifirma). Esa UTXO es el canal.
*   **Intercambio off-chain**: firman una _commitment transaction_ cada vez que el saldo cambia. Nunca se difunden en la red — sólo existen entre ambos.
*   **Cierre on-chain**: cualquiera puede publicar el último estado firmado. La UTXO se gasta y los saldos finales van a cada dueño.

Seguridad

Si alguien intenta hacer trampa publicando un estado antiguo, el otro puede reclamar **todo el dinero del canal** (_fairness protocol_).

ON-CHAIN

2 transacciones: abrir + cerrar

OFF-CHAIN

Miles de pagos entre medias

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 04/17

Módulo 05 · Lightning Network

04 · Anatomía de un canal

04 · Ciclo de vida

## Apertura · Actualización · Cierre.

**Ejemplo simple ·** Alice pasa cada mañana por la cafetería de Bob a por un café. En lugar de pagar on-chain cada vez, abren un canal Lightning y liquidan todos los cafés con una única transacción al final.

01 · APERTURA funding tx (onchain) → 2-of-2 multisig ALICE BOB 🔑 🔑 2-of-2 MULTISIG · UTXO capacidad · 5 000 000 sats Alice deposita 5M sats; el output queda bajo el control conjunto de ambas claves. 1 tx on-chain 02 · ACTUALIZACIÓN N × commit\_tx (off-chain) ALICE BOB ☕ commit\_tx\_n alice 4.5M · bob 500k 1\. firma Alice → 2. Bob entrega ☕ → 3. firma Bob Cada commit\_tx redistribuye los saldos del canal. Con la tx firmada por Alice, Bob se asegura de poder cobrar al cierre del canal. 0 tx on-chain 03 · CIERRE settlement tx (onchain) · ambos firman ALICE BOB 4 500 000 sats 500 000 sats SETTLEMENT TX on-chain · minada Tras muchos cafés, ambos acuerdan cerrar. La settlement tx liquida los saldos on-chain. 1 tx on-chain

En todo el ciclo sólo **2 transacciones tocan la blockchain**: funding tx y settlement tx.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 05/17

Módulo 05 · Lightning Network

05 · Commitment & revocación

05 · Fairness protocol

## ¿Por qué no se puede hacer trampa?

Si Alice publica un _commitment_ viejo que le favorece, Bob puede castigarla y llevarse **todo** el saldo del canal.

*   **Commitment transaction**: cada vez que el saldo cambia, se firma una nueva que refleja los saldos actuales. Si Alice la publica, su output queda _time-locked_ durante un periodo; ese retraso es la ventana en la que Bob puede detectar una commitment antigua y reaccionar antes de que Alice cobre.
*   **Revocation key**: al firmar la siguiente commitment, cada parte _revela_ una clave que revoca la anterior. Ambos guardan pruebas para castigar.
*   **Justicia criptográfica**: si Alice publica una commitment antigua, esa tx reparte el canal en dos outputs. Bob gasta el suyo al instante (ya estaba firmado a su favor) y, con la revocation key que Alice le reveló al sustituir ese estado, barre también el output de Alice antes de que venza su time-lock. Bob se queda con **los dos outputs**, es decir, con el 100% del canal.
*   **Watchtowers**: servicios que observan la cadena por ti; si estás offline, ellos publican la tx de castigo cuando detectan una commitment vieja.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 06/17

Módulo 05 · Lightning Network

06 · Límites de un canal aislado

06 · El canal aislado

## Dos partes, dos problemas.

Un canal bilateral resuelve el intercambio repetido entre dos personas… _siempre que_ ambas colaboren y estén atentas. Fuera de ese escenario ideal aparecen limitaciones que frenan su uso real.

01 · DISPONIBILIDAD Si la contraparte desaparece

Para cerrar cooperativamente hace falta la firma de los dos. Si Bob se desconecta, Alice sólo puede hacer un **cierre unilateral** publicando su última commitment.

Ese output queda _time-locked_: sus fondos permanecen bloqueados durante todo el _CSV delay_ antes de que pueda gastarlos.

02 · VIGILANCIA Hay que estar mirando

El fairness protocol sólo castiga si alguien **detecta** la commitment antigua dentro del time-lock. Si nadie observa la cadena, el tramposo cobra sin consecuencias.

En la práctica obliga a tener el nodo online 24/7 o a delegar la vigilancia en _watchtowers_ de terceros.

03 · CAPITAL Fondos inmovilizados

La capacidad del canal vive en un UTXO 2-of-2. Mientras el canal esté abierto, ese capital no puede usarse para nada más.

Cuanto mayor sea el importe que quiera mover Alice, más dinero tiene que dejar encerrado por adelantado.

04 · RELACIÓN 1-A-1 Sólo sirve con esa persona

El canal entre Alice y Bob sólo permite pagarle **a Bob**. Para pagar a Carol hace falta abrir otro canal, con sus fees on-chain y su propio capital bloqueado.

Esta limitación es la que empujará hacia el **enrutado** a través de terceros, la idea clave de Lightning.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 07/17

Módulo 05 · Lightning Network

07 · Los canales directos no bastan

07 · El límite de los canales bilaterales

## Un canal por pareja: inviable.

N = 6 15 canales

Grafo completo con N = 6 nodos

*   **Coste on-chain prohibitivo**: abrir un canal entre cada par requiere _N·(N−1)/2_ transacciones on-chain. Con 1M usuarios: **500 000 M** canales.
*   **Capital bloqueado**: cada canal inmoviliza fondos. Un usuario no puede fondear un canal con todo el mundo.
*   **Mantenimiento**: cada canal requiere vigilancia, firmas, storage de commits y posibles cierres.
*   **La solución**: enrutar pagos a través de canales ya existentes, como los paquetes en Internet.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 08/17

Módulo 05 · Lightning Network

08 · HTLCs

08 · Hash Time-Locked Contracts

## El pegamento del enrutado.

Un **HTLC** (_Hash Time-Locked Contract_) es un contrato que paga al receptor _si_ revela un secreto antes de un plazo; en caso contrario, devuelve los fondos al remitente.

*   **Atomicidad**: o todos los saltos del enrutado cobran, o ninguno. **R** es el secreto que tiene que atravesar el camino completo; hasta que aparece, ningún nodo puede cobrar.
*   **Time-lock decreciente**: cada salto tiene un plazo un poco menor que el anterior, de modo que si el pago falla, cada nodo recupera sus fondos a tiempo.
*   **Onion routing**: el remitente cifra la ruta en capas, como una cebolla. Cada nodo intermedio descifra sólo _su_ capa, descubre a qué peer reenviar el pago y pasa el resto todavía cifrado. Ningún nodo conoce el camino completo: sólo ve a su predecesor y a su sucesor, nunca al remitente ni al destinatario final.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 09/17

Módulo 05 · Lightning Network

09 · ¿Qué es Lightning Network?

09 · Lightning Network

## Una red de canales enrutados.

Lightning Network es un protocolo P2P que transmite pagos en bitcoins a través de una red de canales de pago, usando enrutado en cebolla, HTLCs y técnicas de _fair exchange_ criptográficas.

2016Paper Poon-Dryja

2018Mainnet live

~5kBTCCapacidad pública

~17kNodos activos

*   **Capas complementarias**: LN no sustituye a Bitcoin. Depende de él como ancla de seguridad y liquidación.
*   **BOLTs**: especificación abierta y mantenida en GitHub (_Basis Of Lightning Technology_). Implementaciones: LND, Core Lightning, Eclair, LDK.
*   **Propiedad clave**: _trust-minimized_. El enrutado no requiere confiar en los nodos intermedios para la custodia.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 10/17

Módulo 05 · Lightning Network

10 · Beneficios de Lightning

10 · Qué se gana

## Instantáneo, barato y privado.

VELOCIDAD Sub-segundo

Los pagos se liquidan en milisegundos, no en minutos. Perfecto para TPV, POS y experiencias interactivas.

COSTE Fracción de sat

Las fees de enrutado son proporcionales al importe. Micropagos viables por primera vez.

PRIVACIDAD Onion routing

Los pagos viajan usando onion routing. Ningún intermediario conoce la ruta completa, ni quién paga a quién.

CAPACIDAD Millones de tx/s

No hay bloques: mientras haya liquidez en los canales, la red escala linealmente con nodos y capital.

NUEVO MODELO Micropagos viables

Pagar por KB de streaming, por segundo de audio, por palabra de una API. Modelos de negocio imposibles en L1.

INTERNACIONAL Remesas en minutos

Transferencias globales sin bancos, sin KYC intermedio, sin días de espera. Útil en entornos con banca frágil.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 11/17

Módulo 05 · Lightning Network

11 · Capacidad y liquidez

11 · Inbound & outbound

## Dos depósitos en un canal.

«La capacidad de un canal es la suma de los saldos de ambos lados. Lo que puedes _enviar_ es tu saldo local (outbound); lo que puedes _recibir_ es el saldo remoto (inbound).»

Canal recién abierto · 5 000 000 sats

Tras pagar 2M sats

Canal equilibrado

*   **Outbound**: sats tuyos en tu lado del canal. Se gastan al enviar.
*   **Inbound**: sats del otro lado. Determina cuánto puedes recibir.
*   **Desbalance**: canales sin inbound no pueden recibir pagos. Hay que rebalancear (circular payments, submarine swaps, LSP).

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 12/17

Módulo 05 · Lightning Network

12 · Ejemplo completo

12 · Ejemplo completo

## Alice paga 1 BTC a Eric a través de 3 intermediarios.

Invoice: H = hash (R) HTLC 1.003 · 10 bloques HTLC 1.002 · 9 bloques HTLC 1.001 · 8 bloques HTLC 1.000 · 7 bloques Revelar R · cobra 1 R · cobra 1.001 R · cobra 1.002 R · cobra 1.003 A Alice B Bob C Carol D Diana E Eric

Canal Alice ↔ Bob

Alice · 2 BTCBob · 2 BTC

Canal Bob ↔ Carol

Bob · 2 BTCCarol · 2 BTC

Canal Carol ↔ Diana

Carol · 2 BTCDiana · 2 BTC

Canal Diana ↔ Eric

Diana · 2 BTCEric · 2 BTC

01 Configuración inicial

Cada par de nodos vecinos ya ha abierto previamente un canal Lightning entre ellos. Cada nodo ha bloqueado **2 BTC** en su lado del canal, así que **cada canal arranca con 4 BTC de capacidad total** repartidos a partes iguales.

←

1 2 3 4 5 6 7 8 9 10

→

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 13/17

Módulo 05 · Lightning Network

13 · Arquitectura técnica

13 · Arquitectura técnica

## Una red P2P sobre Bitcoin.

Cada nodo Lightning mantiene conexiones cifradas con sus _peers_, vigila su subconjunto de la cadena y participa en un _gossip_ distribuido para descubrir rutas. La implementación de referencia cumple las **BOLTs**.

*   **Noise\_XK** (BOLT 08): canal cifrado y autenticado entre peers. Sin metadatos en claro.
*   **Gossip protocol** (BOLT 07): los nodos difunden _channel\_announcement_, _channel\_update_ y _node\_announcement_ para construir el grafo.
*   **Implementaciones**: LND (Go), Core Lightning (C), Eclair (Scala), LDK (Rust).
*   **Nodo Bitcoin asociado**: Lightning requiere bitcoind para publicar y observar transacciones on-chain.

Wallet del usuario móvil · web · desktop · CLI gRPC / REST Nodo Lightning lnd · CLN · eclair · LDK TCP + Noise peers Lightning otros nodos de la red RPC / ZMQ bitcoind backend Bitcoin · capa 1

El nodo Lightning habla con **tres mundos**: la wallet del usuario, sus peers Lightning y bitcoind.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 14/17

Módulo 05 · Lightning Network

14 · Wallets y custodia

14 · Wallets Lightning

## Wallets Lightning: ¿quién tiene las keys?

Toda interacción del usuario con Lightning pasa por una **wallet**. La gran división entre wallets está en **quién custodia los fondos**: el proveedor de la wallet, o el propio usuario.

Característica

Wallet custodial

Wallet self-custodial

Custodia de fondos

La tiene el proveedor (Wallet of Satoshi, exchange).

La tiene el usuario: sus claves, sus canales.

UX

Inmediata: solo descargar e iniciar sesión.

Requiere gestionar liquidez, backups, conectividad.

Privacidad

Baja: el proveedor ve todo el historial del usuario.

Alta: el usuario mantiene la información localmente.

Riesgo

Contraparte: si el proveedor falla, los fondos se pierden.

Usuario: si no gestiona backup / watchtower, puede perder saldo.

Ejemplos

Wallet of Satoshi, Strike, Cash App

Phoenix, Breez, Zeus, Mutiny

LSP Lightning Service Providers

Actores que ofrecen **liquidez entrante** bajo demanda, canales _just-in-time_ y rutas estables. Los wallets mobile dependen en gran medida de LSPs.

HÍBRIDOS Modelos intermedios

Algunos wallets delegan la conectividad y el enrutado sin tomar custodia: el usuario conserva las claves pero no opera un nodo 24/7.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 15/17

Módulo 05 · Lightning Network

15 · BOLT 11

15 · BOLT 11

## Anatomía de una invoice.

**BOLT 11** (_Basis Of Lightning Technology #11_) es la especificación abierta que define cómo se codifica una _payment request_. Empaqueta en un único string **bech32** todo lo que el remitente necesita para pagar: destino, _payment hash_, importe, expiración y pistas de ruta.

*   **HRP** (prefijo legible): `lnbc` mainnet · `lntb` testnet · `lnbcrt` regtest.
*   **Importe compacto**: base + multiplicador `m`/`u`/`n`/`p`. `2500u` = 2 500 μBTC = 250 000 sats.
*   **Single-use**: una invoice = un pago. Reutilizarla puede provocar pérdida de fondos.
*   **Distribución**: viaja fuera de Lightning — QR, NFC, email, deep-link `lightning:`.

lnbc2500u1pvjluezpp5qqqsyqcyq5rqwzqfqqqsyqcyq5rqwzqfqqqsyqcyq5rqwzqfqypqdq5xysxxatsyp3k7enxv4jsxqzpuaztrnwngzn3kdzw5hydlzf03qdgm2hdq27cqv3agm2awhz5se903vruatfhq77w3ls4evs3ch9zw97j25emudupq63nyw24cg27h2rspfj9srp

HRP Amount Timestamp Tagged fields Signature

Ejemplo real de la spec BOLT 11 · 2 500 μBTC (≈ 250 000 sats) en mainnet · _"1 cup coffee"_.

Chainbitcoin (mainnet)

Amount250 000 sats · 250 000 000 msat · 2 500 μBTC

Description"1 cup coffee"

Payee pubkey03e7156ae33b0a208d0744199163177e909e80176e55d97a2f221ede0f934dd9ad

Payment hash0001020304050607080900010203040506070809000102030405060708090102

Timestamp1 496 314 658 · 2017-06-01 10:57:38 UTC

Expiry60 s · caduca 10:58:38 UTC

Signaturee89639ba…bd750e · recovery flag 1

UTILIDAD [lightningdecoder.com](https://lightningdecoder.com/) — pega una invoice y la descompone en tiempo real.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 16/17

Módulo 05 · Lightning Network

16 · UX moderna

16 · Más allá de BOLT 11

## Experiencias reutilizables y estáticas.

Una invoice BOLT 11 sirve para **un único cobro**: quien recibe tiene que generar una nueva cada vez. Esto no encaja del todo con suscripciones, donaciones abiertas o propinas en streaming. Actualizaciones modernas añaden **tres mecanismos por encima** que cubren esos huecos sin tocar el protocolo base.

LNURL Capa HTTPS sobre Lightning

El wallet recibe una URL en bech32 o una _lightning address_ tipo `alice@dominio.com`, la resuelve contra el servidor del receptor por HTTPS y recibe una **invoice BOLT 11 fresca** para cada pago. El endpoint actúa de puente: estático por fuera, dinámico por dentro.

*   `lnurl-pay` — pagar a una dirección estática
*   `lnurl-withdraw` — tirar sats de un servicio
*   `lnurl-auth` — login sin contraseña
*   `lnurl-channel` — apertura asistida de canal

Pragmático, pero requiere HTTPS y servidor online. No está en las BOLTs.

KEYSEND Pago espontáneo sin invoice

El remitente genera él mismo un secreto `R`, deriva `H = hash(R)` como payment hash y envía el HTLC con `R` incluido en un **campo TLV** dentro del onion. El destinatario descifra `R`, comprueba el hash y cobra.

Sin acuerdo previo ni metadatos compartidos — basta conocer el _node\_id_.

*   Propinas y donaciones al vuelo
*   _Value-4-value_ en podcasts (streaming de sats)
*   Micropagos entre bots/servicios

Sin _proof of payment_ (R lo creó el remitente) y el receptor debe tener keysend activado.

BOLT 12 Offers y pagos reutilizables

Introduce las **offers**: códigos estáticos y reutilizables, como un QR de negocio. El wallet pide una invoice al destinatario vía **onion messages** — mensajería cifrada y enrutada como los pagos, pero sin bloquear fondos con HTLCs.

offer → invoice\_request → invoice → pago

*   _Blinded paths_: destino anónimo
*   Firmas Schnorr, más compactas
*   Recurrencia y refunds nativos
*   Sin HTTPS: todo por Lightning

Candidato a suceder a BOLT 11.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 17/17

/\* ======================================================================== SLIDE PRESENTATION CONTROLLER Keyboard · touch · nav dots · progress bar ======================================================================== \*/ class SlidePresentation { constructor() { this.slides = Array.from(document.querySelectorAll('.slide')); this.total = this.slides.length; this.currentSlide = 0; this.progressBar = document.getElementById('progressBar'); this.navDotsContainer = document.getElementById('navDots'); this.\_buildNavDots(); this.\_setupIntersectionObserver(); this.\_setupKeyboardNav(); this.\_setupTouchNav(); this.\_setupScrollProgress(); } \_setupIntersectionObserver() { const io = new IntersectionObserver((entries) => { entries.forEach((entry) => { if (entry.isIntersecting && entry.intersectionRatio >= 0.6) { const idx = this.slides.indexOf(entry.target); entry.target.classList.add('visible'); this.currentSlide = idx; this.\_updateNavDots(); this.\_updateProgress(); } }); }, { threshold: \[0.6\] }); this.slides.forEach((s) => io.observe(s)); } \_setupKeyboardNav() { document.addEventListener('keydown', (e) => { if (e.target && e.target.getAttribute && e.target.getAttribute('contenteditable') === 'true') return; switch (e.key) { case 'ArrowRight': case 'ArrowDown': case ' ': case 'PageDown': e.preventDefault(); this.goTo(this.currentSlide + 1); break; case 'ArrowLeft': case 'ArrowUp': case 'PageUp': e.preventDefault(); this.goTo(this.currentSlide - 1); break; case 'Home': e.preventDefault(); this.goTo(0); break; case 'End': e.preventDefault(); this.goTo(this.total - 1); break; } }); } \_setupTouchNav() { let startY = 0; document.addEventListener('touchstart', (e) => { startY = e.touches\[0\].clientY; }, { passive: true }); document.addEventListener('touchend', (e) => { const endY = e.changedTouches\[0\].clientY; const diff = startY - endY; if (Math.abs(diff) > 60) { this.goTo(this.currentSlide + (diff > 0 ? 1 : -1)); } }, { passive: true }); } \_setupScrollProgress() { window.addEventListener('scroll', () => this.\_updateProgress(), { passive: true }); } \_updateProgress() { const scrollTop = window.scrollY; const total = document.documentElement.scrollHeight - window.innerHeight; const pct = total > 0 ? (scrollTop / total) \* 100 : 0; this.progressBar.style.width = pct + '%'; } \_buildNavDots() { this.navDotsContainer.innerHTML = ''; this.slides.forEach((slide, i) => { const b = document.createElement('button'); b.setAttribute('aria-label', \`Ir a diapositiva ${i + 1}: ${slide.dataset.title || ''}\`); if (i === 0) b.classList.add('active'); b.addEventListener('click', () => this.goTo(i)); this.navDotsContainer.appendChild(b); }); } \_updateNavDots() { this.navDotsContainer.querySelectorAll('button').forEach((b, i) => { b.classList.toggle('active', i === this.currentSlide); }); } goTo(i) { const idx = Math.max(0, Math.min(this.total - 1, i)); this.slides\[idx\].scrollIntoView({ behavior: 'smooth', block: 'start' }); } } /\* ======================================================================== LIGHTNING EXAMPLE CAROUSEL 9 pasos · Mastering Bitcoin cap. 14. Actualiza SVG (data-steps) + número/título/descripción + balances de cada canal según el paso activo. ======================================================================== \*/ class LightningExampleCarousel { constructor() { this.root = document.getElementById('lnExample'); if (!this.root) return; this.total = 10; this.step = 1; this.stepNum = document.getElementById('lnStepNum'); this.stepTitle = document.getElementById('lnStepTitle'); this.stepDesc = document.getElementById('lnStepDesc'); this.prevBtn = document.getElementById('lnPrev'); this.nextBtn = document.getElementById('lnNext'); this.dots = Array.from(this.root.querySelectorAll('.dot')); this.stepEls = Array.from(this.root.querySelectorAll('\[data-steps\]')); this.balanceEls = Array.from(this.root.querySelectorAll('.ln-balance')); // Step-by-step content: title, description, updated channel balances // (array of lines per channel so each row renders in its own span), // and which channel pill(s) to highlight as "acabamos de tocarlo". this.steps = \[ { title: 'Configuración inicial', desc: 'Cada par de nodos vecinos ya ha abierto previamente un canal Lightning entre ellos. Cada nodo ha bloqueado <b>2 BTC</b> en su lado del canal, así que <b>cada canal arranca con 4 BTC de capacidad total</b> repartidos a partes iguales.', balances: { 'A-B': \['Alice · 2 BTC', 'Bob · 2 BTC'\], 'B-C': \['Bob · 2 BTC', 'Carol · 2 BTC'\], 'C-D': \['Carol · 2 BTC', 'Diana · 2 BTC'\], 'D-E': \['Diana · 2 BTC', 'Eric · 2 BTC'\] }, highlight: \[\] }, { title: 'Eric emite la invoice', desc: 'Eric genera un secreto aleatorio <code>R</code> y calcula su hash <code>H = hash(R)</code>. Con ello construye una invoice con <code>H</code> y la cantidad (1 BTC). <b>La invoice viaja por fuera del protocolo Lightning</b>: como cadena <code>lnbc1…</code> (BOLT 11), código QR, email, NFC… Alice la recibe por el canal que sea. <b>El secreto R aún no sale de Eric.</b>', balances: { 'A-B': \['Alice · 2 BTC', 'Bob · 2 BTC'\], 'B-C': \['Bob · 2 BTC', 'Carol · 2 BTC'\], 'C-D': \['Carol · 2 BTC', 'Diana · 2 BTC'\], 'D-E': \['Diana · 2 BTC', 'Eric · 2 BTC'\] }, highlight: \[\] }, { title: 'Alice → Bob · HTLC', desc: 'Alice bloquea <b>1.003 BTC</b> en un HTLC con Bob: <code>H</code> + timelock de <b>10 bloques</b>. Las 0.003 de más cubren las fees de los 3 intermediarios.', balances: { 'A-B': \['Alice · 0.997 BTC', 'Bob · 2 BTC', 'HTLC · 1.003 BTC'\], 'B-C': \['Bob · 2 BTC', 'Carol · 2 BTC'\], 'C-D': \['Carol · 2 BTC', 'Diana · 2 BTC'\], 'D-E': \['Diana · 2 BTC', 'Eric · 2 BTC'\] }, highlight: \['A-B'\] }, { title: 'Bob → Carol · HTLC', desc: 'Bob replica el HTLC hacia Carol con <b>1.002 BTC</b> y timelock de <b>9 bloques</b>. Se queda 0.001 de fee si la cadena de HTLCs se resuelve. Mismo <code>H</code>, tiempo un poco menor.', balances: { 'A-B': \['Alice · 0.997 BTC', 'Bob · 2 BTC', 'HTLC · 1.003 BTC'\], 'B-C': \['Bob · 0.998 BTC', 'Carol · 2 BTC', 'HTLC · 1.002 BTC'\], 'C-D': \['Carol · 2 BTC', 'Diana · 2 BTC'\], 'D-E': \['Diana · 2 BTC', 'Eric · 2 BTC'\] }, highlight: \['B-C'\] }, { title: 'Carol → Diana · HTLC', desc: 'Carol propaga el HTLC a Diana: <b>1.001 BTC</b> y timelock de <b>8 bloques</b>. Mismo <code>H</code>. La ruta se va estrechando en cantidad y en tiempo.', balances: { 'A-B': \['Alice · 0.997 BTC', 'Bob · 2 BTC', 'HTLC · 1.003 BTC'\], 'B-C': \['Bob · 0.998 BTC', 'Carol · 2 BTC', 'HTLC · 1.002 BTC'\], 'C-D': \['Carol · 0.999 BTC', 'Diana · 2 BTC', 'HTLC · 1.001 BTC'\], 'D-E': \['Diana · 2 BTC', 'Eric · 2 BTC'\] }, highlight: \['C-D'\] }, { title: 'Diana → Eric · HTLC final', desc: 'Diana cierra la cadena con un HTLC hacia Eric por exactamente <b>1 BTC</b> y timelock de <b>7 bloques</b>. La cantidad que llega al destino es la que pidió la invoice.', balances: { 'A-B': \['Alice · 0.997 BTC', 'Bob · 2 BTC', 'HTLC · 1.003 BTC'\], 'B-C': \['Bob · 0.998 BTC', 'Carol · 2 BTC', 'HTLC · 1.002 BTC'\], 'C-D': \['Carol · 0.999 BTC', 'Diana · 2 BTC', 'HTLC · 1.001 BTC'\], 'D-E': \['Diana · 1 BTC', 'Eric · 2 BTC', 'HTLC · 1 BTC'\] }, highlight: \['D-E'\] }, { title: 'Eric revela R · cobra 1 BTC', desc: 'Eric es el único que conoce <code>R</code>. Lo entrega a Diana para reclamar el HTLC. Diana le paga 1 BTC del lado de su canal. Eric queda con <b>3 BTC</b> en el canal Diana ↔ Eric.', balances: { 'A-B': \['Alice · 0.997 BTC', 'Bob · 2 BTC', 'HTLC · 1.003 BTC'\], 'B-C': \['Bob · 0.998 BTC', 'Carol · 2 BTC', 'HTLC · 1.002 BTC'\], 'C-D': \['Carol · 0.999 BTC', 'Diana · 2 BTC', 'HTLC · 1.001 BTC'\], 'D-E': \['Diana · 1 BTC', 'Eric · 3 BTC'\] }, highlight: \['D-E'\] }, { title: 'Diana → Carol · R se propaga', desc: 'Diana usa <code>R</code> para cobrar su HTLC con Carol: <b>1.001 BTC</b>. La fee de 0.001 BTC queda como ganancia de Diana por haber enrutado.', balances: { 'A-B': \['Alice · 0.997 BTC', 'Bob · 2 BTC', 'HTLC · 1.003 BTC'\], 'B-C': \['Bob · 0.998 BTC', 'Carol · 2 BTC', 'HTLC · 1.002 BTC'\], 'C-D': \['Carol · 0.999 BTC', 'Diana · 3.001 BTC'\], 'D-E': \['Diana · 1 BTC', 'Eric · 3 BTC'\] }, highlight: \['C-D'\] }, { title: 'Carol → Bob · R se propaga', desc: 'Carol, ya con <code>R</code>, cobra su HTLC con Bob: <b>1.002 BTC</b>. Se queda otros 0.001 BTC como fee por enrutar.', balances: { 'A-B': \['Alice · 0.997 BTC', 'Bob · 2 BTC', 'HTLC · 1.003 BTC'\], 'B-C': \['Bob · 0.998 BTC', 'Carol · 3.002 BTC'\], 'C-D': \['Carol · 0.999 BTC', 'Diana · 3.001 BTC'\], 'D-E': \['Diana · 1 BTC', 'Eric · 3 BTC'\] }, highlight: \['B-C'\] }, { title: 'Bob → Alice · pago saldado', desc: 'Bob cobra finalmente el HTLC original con Alice: <b>1.003 BTC</b>. Alice pierde 1.003, Eric gana 1, los 3 intermediarios se reparten 0.003 en fees. <b>Ningún tx on-chain: sólo cuatro actualizaciones de canal.</b>', balances: { 'A-B': \['Alice · 0.997 BTC', 'Bob · 3.003 BTC'\], 'B-C': \['Bob · 0.998 BTC', 'Carol · 3.002 BTC'\], 'C-D': \['Carol · 0.999 BTC', 'Diana · 3.001 BTC'\], 'D-E': \['Diana · 1 BTC', 'Eric · 3 BTC'\] }, highlight: \['A-B'\] } \]; this.\_wire(); this.\_render(); } \_wire() { this.prevBtn.addEventListener('click', () => this.go(this.step - 1)); this.nextBtn.addEventListener('click', () => this.go(this.step + 1)); this.dots.forEach((d) => { d.addEventListener('click', () => this.go(parseInt(d.dataset.step, 10))); }); } go(n) { if (n < 1 || n > this.total) return; this.step = n; this.\_render(); } \_render() { const data = this.steps\[this.step - 1\]; this.root.dataset.step = String(this.step); // Header this.stepNum.textContent = String(this.step).padStart(2, '0'); this.stepTitle.textContent = data.title; this.stepDesc.innerHTML = data.desc; // Dots this.dots.forEach((d) => { d.classList.toggle('active', parseInt(d.dataset.step, 10) === this.step); }); // Arrows this.prevBtn.disabled = this.step === 1; this.nextBtn.disabled = this.step === this.total; // SVG step-gated groups this.stepEls.forEach((el) => { const steps = (el.dataset.steps || '') .split(',') .map((s) => parseInt(s.trim(), 10)); el.classList.toggle('on', steps.includes(this.step)); }); // Balances: each channel renders one <span> per line (holder · amount BTC) this.balanceEls.forEach((el) => { const pair = el.dataset.pair; const rows = data.balances\[pair\] || \[\]; const valEl = el.querySelector('.val'); valEl.innerHTML = rows.map((r) => \`<span>${r}</span>\`).join(''); el.classList.toggle('updated', (data.highlight || \[\]).includes(pair)); }); } } // Boot window.addEventListener('DOMContentLoaded', () => { new SlidePresentation(); new LightningExampleCarousel(); const first = document.querySelector('.slide'); if (first) first.classList.add('visible'); });