  Infraestructura Bitcoin — Módulo 5 (presentación)       /\* ======================================================================== THEME TOKENS · Swiss Modern ======================================================================== \*/ :root { --bg: #ffffff; --bg-panel: #f5f5f5; --ink: #0a0a0a; --ink-soft: #3a3a3a; --muted: #6a6a6a; --muted-2: #b0b0b0; --grid: rgba(10, 10, 10, 0.05); --grid-line: rgba(10, 10, 10, 0.08); --accent: #ff3300; --accent-2: #0a0a0a; --accent-btc:#f7931a; --font-display: "Archivo", sans-serif; --font-body: "Nunito", sans-serif; --font-mono: "JetBrains Mono", ui-monospace, monospace; --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1); --duration-normal: 0.7s; } /\* ======================================================================== GLOBAL RESETS + VIEWPORT FITTING (verbatim shared base) ======================================================================== \*/ \* { margin: 0; padding: 0; box-sizing: border-box; } html, body { height: 100%; overflow-x: hidden; } html { scroll-snap-type: y mandatory; scroll-behavior: smooth; } .slide { width: 100vw; height: 100vh; height: 100dvh; overflow: hidden; scroll-snap-align: start; display: flex; flex-direction: column; position: relative; } .slide-content { flex: 1; display: flex; flex-direction: column; justify-content: center; max-height: 100%; overflow: hidden; padding: var(--slide-padding); } :root { --title-size: clamp(1.5rem, 5vw, 4rem); --h2-size: clamp(1.25rem, 3.5vw, 2.5rem); --h3-size: clamp(1rem, 2.5vw, 1.75rem); --body-size: clamp(0.75rem, 1.5vw, 1.125rem); --small-size: clamp(0.65rem, 1vw, 0.875rem); --slide-padding: clamp(1rem, 4vw, 4rem); --content-gap: clamp(0.5rem, 2vw, 2rem); --element-gap: clamp(0.25rem, 1vw, 1rem); } .card, .container, .content-box { max-width: min(90vw, 1000px); max-height: min(80vh, 700px); } .feature-list, .bullet-list { gap: clamp(0.4rem, 1vh, 1rem); } .feature-list li, .bullet-list li { font-size: var(--body-size); line-height: 1.4; } .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 250px), 1fr)); gap: clamp(0.5rem, 1.5vw, 1rem); } img, .image-container { max-width: 100%; max-height: min(50vh, 400px); object-fit: contain; } @media (max-height: 700px) { :root { --slide-padding: clamp(0.75rem, 3vw, 2rem); --content-gap: clamp(0.4rem, 1.5vw, 1rem); --title-size: clamp(1.25rem, 4.5vw, 2.5rem); --h2-size: clamp(1rem, 3vw, 1.75rem); } } @media (max-height: 600px) { :root { --slide-padding: clamp(0.5rem, 2.5vw, 1.5rem); --content-gap: clamp(0.3rem, 1vw, 0.75rem); --title-size: clamp(1.1rem, 4vw, 2rem); --body-size: clamp(0.7rem, 1.2vw, 0.95rem); } .nav-dots, .keyboard-hint, .decorative { display: none; } } @media (max-height: 500px) { :root { --slide-padding: clamp(0.4rem, 2vw, 1rem); --title-size: clamp(1rem, 3.5vw, 1.5rem); --h2-size: clamp(0.9rem, 2.5vw, 1.25rem); --body-size: clamp(0.65rem, 1vw, 0.85rem); } } @media (max-width: 600px) { :root { --title-size: clamp(1.25rem, 7vw, 2.5rem); } .grid { grid-template-columns: 1fr; } } @media (prefers-reduced-motion: reduce) { \*, \*::before, \*::after { animation-duration: 0.01ms !important; transition-duration: 0.2s !important; } html { scroll-behavior: auto; } } /\* ======================================================================== BODY ======================================================================== \*/ body { background: var(--bg); color: var(--ink); font-family: var(--font-body); font-size: var(--body-size); line-height: 1.5; background-image: linear-gradient(to right, var(--grid) 1px, transparent 1px); background-size: calc(100% / 12) 100%; } /\* ======================================================================== SLIDE FRAME (shared header + footer) ======================================================================== \*/ .slide { padding: clamp(1.25rem, 3.5vw, 3.5rem); } .slide-header { display: flex; justify-content: space-between; align-items: center; gap: 1rem; padding-bottom: clamp(0.5rem, 1vw, 0.75rem); border-bottom: 1px solid var(--grid-line); } .slide-header .left { display: flex; align-items: center; gap: 0.75rem; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.65rem, 0.95vw, 0.85rem); letter-spacing: 0.28em; text-transform: uppercase; } .slide-header .left .mark { width: clamp(0.55rem, 0.9vw, 0.8rem); height: clamp(0.55rem, 0.9vw, 0.8rem); background: var(--accent); } .slide-header .right { font-family: var(--font-display); font-weight: 700; font-size: clamp(0.65rem, 0.95vw, 0.85rem); letter-spacing: 0.28em; text-transform: uppercase; color: var(--muted); } .slide-body { flex: 1; display: flex; flex-direction: column; justify-content: center; padding: clamp(1rem, 2vw, 2rem) 0; gap: clamp(0.75rem, 1.5vw, 1.5rem); min-height: 0; } .slide-footer { display: flex; justify-content: space-between; align-items: baseline; gap: 1rem; padding-top: clamp(0.4rem, 0.8vw, 0.75rem); border-top: 1px solid var(--grid-line); font-family: var(--font-body); font-weight: 400; font-size: clamp(0.65rem, 0.9vw, 0.8rem); color: var(--muted); } .slide-footer b { color: var(--ink); font-weight: 600; } .slide-footer .page { font-family: var(--font-display); font-weight: 800; letter-spacing: 0.18em; color: var(--ink); } .slide-footer .page .sep { color: var(--muted-2); margin: 0 0.3em; } /\* ======================================================================== KICKER + HEADING ======================================================================== \*/ .kicker { display: inline-flex; align-items: center; gap: clamp(0.4rem, 0.7vw, 0.6rem); font-family: var(--font-display); font-weight: 800; font-size: clamp(0.7rem, 1vw, 0.95rem); letter-spacing: 0.25em; text-transform: uppercase; color: var(--accent); } .kicker .bar { width: clamp(1.25rem, 2.5vw, 2.5rem); height: clamp(0.15rem, 0.25vw, 0.25rem); background: var(--accent); } h2.heading { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.75rem, 5.5vw, 4.75rem); line-height: 0.95; letter-spacing: -0.025em; color: var(--ink); max-width: 18ch; } h2.heading .accent { color: var(--accent); } h2.heading .stroke { color: transparent; -webkit-text-stroke: clamp(1px, 0.15vw, 2px) var(--ink); } /\* ======================================================================== TITLE SLIDE ======================================================================== \*/ .title-slide { background: var(--bg); } .title-slide .slide-body { display: grid; grid-template-columns: 1fr; grid-template-rows: 1fr auto; gap: clamp(1rem, 2vw, 2rem); } .title-slide .title-main { align-self: center; max-width: 24ch; } .title-slide .eyebrow-tag { display: inline-block; padding: clamp(0.3rem, 0.5vw, 0.45rem) clamp(0.65rem, 1vw, 0.95rem); background: var(--accent); color: #fff; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.7rem, 1vw, 0.9rem); letter-spacing: 0.28em; text-transform: uppercase; margin-bottom: clamp(1rem, 2vw, 1.5rem); } .title-slide h1 { font-family: var(--font-display); font-weight: 900; font-size: clamp(2.5rem, 10vw, 9rem); line-height: 0.88; letter-spacing: -0.035em; } .title-slide h1 .accent { color: var(--accent); } .title-slide .rule { margin-top: clamp(1rem, 2vw, 1.5rem); width: clamp(2.5rem, 5vw, 5rem); height: clamp(0.2rem, 0.3vw, 0.3rem); background: var(--ink); } .title-slide .subline { margin-top: clamp(0.75rem, 1.5vw, 1.25rem); font-family: var(--font-body); font-size: clamp(0.9rem, 1.4vw, 1.25rem); color: var(--ink-soft); max-width: 34ch; line-height: 1.45; } .title-slide .circle-deco { position: absolute; top: clamp(3rem, 8vw, 7rem); right: clamp(2rem, 6vw, 6rem); width: clamp(7rem, 16vw, 17rem); height: clamp(7rem, 16vw, 17rem); border: clamp(1.5px, 0.25vw, 3px) solid var(--ink); border-radius: 50%; display: grid; place-items: center; pointer-events: none; } .title-slide .circle-deco::before { content: "₿"; font-family: var(--font-display); font-weight: 900; color: var(--accent); font-size: clamp(3rem, 8vw, 8rem); line-height: 1; } .title-slide .byline { display: flex; justify-content: space-between; align-items: baseline; gap: 1rem; font-family: var(--font-body); font-size: clamp(0.8rem, 1.1vw, 1rem); } .title-slide .byline .name { font-weight: 700; color: var(--ink); } .title-slide .byline .meta { font-family: var(--font-display); font-weight: 700; letter-spacing: 0.25em; text-transform: uppercase; font-size: clamp(0.65rem, 0.9vw, 0.8rem); color: var(--muted); } /\* ======================================================================== LAYOUT · TWO-COLUMN ======================================================================== \*/ .two-col { display: grid; grid-template-columns: minmax(0, 5fr) minmax(0, 7fr); gap: clamp(1.5rem, 3vw, 3rem); align-items: start; min-height: 0; } @media (max-width: 720px) { .two-col { grid-template-columns: 1fr; } } .col-left { display: flex; flex-direction: column; gap: clamp(0.75rem, 1.5vw, 1.25rem); } .col-right { display: flex; flex-direction: column; gap: clamp(0.75rem, 1.5vw, 1.25rem); min-width: 0; } /\* ======================================================================== FEATURE LIST (Swiss numbered) ======================================================================== \*/ ul.feature-list { list-style: none; display: flex; flex-direction: column; counter-reset: bullet; } ul.feature-list li { position: relative; padding: clamp(0.5rem, 1vw, 0.8rem) 0 clamp(0.5rem, 1vw, 0.8rem) clamp(2.25rem, 3.5vw, 3rem); border-bottom: 1px solid var(--grid-line); counter-increment: bullet; font-size: clamp(0.85rem, 1.2vw, 1rem); line-height: 1.5; color: var(--ink-soft); } ul.feature-list li::before { content: counter(bullet, decimal-leading-zero); position: absolute; top: clamp(0.55rem, 1.1vw, 0.9rem); left: 0; font-family: var(--font-display); font-weight: 800; font-size: clamp(0.7rem, 1vw, 0.85rem); letter-spacing: 0.15em; color: var(--accent); } ul.feature-list li b { color: var(--ink); font-weight: 700; } ul.feature-list li code, ul.feature-list li .mono { font-family: var(--font-mono); color: var(--ink); font-size: 0.95em; } /\* ======================================================================== STAT STRIP ======================================================================== \*/ .stat-strip { display: grid; grid-template-columns: repeat(4, 1fr); gap: clamp(0.5rem, 1vw, 1rem); padding: clamp(0.75rem, 1.5vw, 1rem) 0; border-top: clamp(1.5px, 0.25vw, 2px) solid var(--ink); border-bottom: clamp(1.5px, 0.25vw, 2px) solid var(--ink); } @media (max-width: 720px) { .stat-strip { grid-template-columns: repeat(2, 1fr); } } .stat { display: flex; flex-direction: column; gap: 0.2rem; } .stat .num { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.4rem, 3.5vw, 2.8rem); line-height: 1; letter-spacing: -0.03em; color: var(--ink); } .stat .num .small { font-size: 0.55em; color: var(--muted); margin-left: 0.1em; letter-spacing: 0.05em; } .stat .lbl { font-family: var(--font-display); font-weight: 700; font-size: clamp(0.6rem, 0.85vw, 0.75rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } /\* ======================================================================== PULL QUOTE ======================================================================== \*/ .pull-quote { padding: clamp(1rem, 2vw, 1.75rem) clamp(1.25rem, 2.5vw, 2rem); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); background: var(--bg-panel); font-family: var(--font-display); font-weight: 500; font-size: clamp(1rem, 2vw, 1.5rem); line-height: 1.25; color: var(--ink); letter-spacing: -0.01em; } .pull-quote .src { display: block; margin-top: clamp(0.4rem, 0.8vw, 0.7rem); font-family: var(--font-body); font-weight: 600; font-style: italic; font-size: clamp(0.7rem, 1vw, 0.9rem); color: var(--muted); letter-spacing: 0.02em; } /\* ======================================================================== CLOSING LINE ======================================================================== \*/ .closing-line { padding-top: clamp(0.5rem, 1vw, 0.85rem); border-top: 1px solid var(--grid-line); font-family: var(--font-body); font-size: clamp(0.8rem, 1.1vw, 1rem); color: var(--ink-soft); } .closing-line b { color: var(--ink); font-weight: 700; } /\* ======================================================================== REVEAL animations ======================================================================== \*/ .reveal { opacity: 0; transform: translateY(12px); transition: opacity var(--duration-normal) var(--ease-out-expo), transform var(--duration-normal) var(--ease-out-expo); } .slide.visible .reveal { opacity: 1; transform: translateY(0); } .slide.visible .reveal:nth-child(1) { transition-delay: 0.05s; } .slide.visible .reveal:nth-child(2) { transition-delay: 0.15s; } .slide.visible .reveal:nth-child(3) { transition-delay: 0.25s; } .slide.visible .reveal:nth-child(4) { transition-delay: 0.35s; } /\* ======================================================================== PROGRESS BAR + NAV DOTS + KEYBOARD HINT ======================================================================== \*/ .progress-bar { position: fixed; top: 0; left: 0; height: 3px; background: var(--accent); z-index: 100; transition: width 0.2s ease-out; } .nav-dots { position: fixed; right: clamp(0.75rem, 1.5vw, 1.5rem); top: 50%; transform: translateY(-50%); display: flex; flex-direction: column; gap: clamp(0.35rem, 0.7vw, 0.6rem); z-index: 50; } .nav-dots button { width: clamp(0.4rem, 0.65vw, 0.55rem); height: clamp(0.4rem, 0.65vw, 0.55rem); border-radius: 50%; border: 1px solid var(--ink); background: transparent; cursor: pointer; transition: background 0.2s, transform 0.2s; padding: 0; } .nav-dots button.active { background: var(--accent); border-color: var(--accent); transform: scale(1.25); } .keyboard-hint { position: fixed; bottom: clamp(0.5rem, 1vw, 0.9rem); left: 50%; transform: translateX(-50%); display: flex; align-items: center; gap: clamp(0.35rem, 0.7vw, 0.6rem); font-family: var(--font-display); font-weight: 700; font-size: clamp(0.55rem, 0.8vw, 0.72rem); letter-spacing: 0.2em; text-transform: uppercase; color: var(--muted); z-index: 40; } .keyboard-hint .key { display: inline-grid; place-items: center; min-width: 1.2em; padding: 0.1em 0.35em; border: 1px solid var(--muted-2); border-radius: 3px; font-size: 0.95em; color: var(--ink); } /\* ======================================================================== EDIT MODE ======================================================================== \*/ .edit-hotzone { position: fixed; top: 0; right: 0; width: 80px; height: 80px; z-index: 60; } .edit-toggle { position: fixed; top: 1rem; right: 1rem; width: 2.5rem; height: 2.5rem; border: 1px solid var(--ink); border-radius: 50%; background: var(--bg); color: var(--ink); font-size: 1.1rem; cursor: pointer; opacity: 0; transform: translateY(-6px); pointer-events: none; transition: opacity 0.3s, transform 0.3s; z-index: 70; } .edit-toggle.show { opacity: 1; transform: translateY(0); pointer-events: auto; } .edit-toggle.active { background: var(--accent); color: #fff; border-color: var(--accent); } .edit-banner { position: fixed; top: -3rem; left: 50%; transform: translateX(-50%); padding: 0.5rem 1rem; background: var(--accent); color: #fff; font-family: var(--font-display); font-weight: 800; font-size: 0.75rem; letter-spacing: 0.18em; text-transform: uppercase; z-index: 80; transition: top 0.3s; display: flex; align-items: center; gap: 0.5rem; } .edit-banner.active { top: 0.5rem; } .edit-banner .dot { width: 0.5rem; height: 0.5rem; background: #fff; border-radius: 50%; animation: pulse 1.5s infinite; } @keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.4; } } \[contenteditable="true"\] { outline: 1px dashed var(--accent); outline-offset: 3px; min-width: 1ch; } \[contenteditable="true"\]:focus { outline: 2px solid var(--accent); background: rgba(255,51,0,0.04); } /\* ======================================================================== CUSTOM COMPONENTS · Infraestructura ======================================================================== \*/ /\* --- Agenda grid (slide 2) --- \*/ .agenda-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: clamp(0.5rem, 1vw, 0.85rem); } @media (max-width: 860px) { .agenda-grid { grid-template-columns: 1fr 1fr; } } @media (max-width: 600px) { .agenda-grid { grid-template-columns: 1fr; } } .agenda-cell { padding: clamp(0.6rem, 1vw, 0.85rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.2rem, 0.4vw, 0.35rem); min-width: 0; } .agenda-cell .idx { font-family: var(--font-mono); font-size: clamp(0.55rem, 0.75vw, 0.68rem); letter-spacing: 0.18em; color: var(--accent); } .agenda-cell .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.85rem, 1.2vw, 1rem); color: var(--ink); line-height: 1.2; } .agenda-cell .desc { font-size: clamp(0.65rem, 0.88vw, 0.78rem); color: var(--ink-soft); line-height: 1.35; } /\* --- Client card grid (slide 3) --- \*/ .client-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: clamp(0.4rem, 0.8vw, 0.7rem); } @media (max-width: 960px) { .client-grid { grid-template-columns: repeat(3, 1fr); } } @media (max-width: 600px) { .client-grid { grid-template-columns: 1fr 1fr; } } .client-card { padding: clamp(0.65rem, 1vw, 0.9rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.25rem, 0.5vw, 0.4rem); min-width: 0; } .client-card.core { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); background: var(--bg-panel); } .client-card.knots { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent-btc); } .client-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.85rem, 1.2vw, 1.05rem); color: var(--ink); line-height: 1.15; } .client-card .lang { font-family: var(--font-mono); font-size: clamp(0.55rem, 0.72vw, 0.66rem); letter-spacing: 0.12em; text-transform: uppercase; color: var(--muted); } .client-card .share { font-family: var(--font-display); font-weight: 900; font-size: clamp(1rem, 1.7vw, 1.5rem); color: var(--accent); line-height: 1; letter-spacing: -0.02em; } .client-card.knots .share { color: var(--accent-btc); } .client-card .desc { font-size: clamp(0.62rem, 0.85vw, 0.74rem); color: var(--ink-soft); line-height: 1.38; } .client-card .desc b { color: var(--ink); font-weight: 700; } /\* --- Datadir tree (slide 4) --- \*/ .datadir { font-family: var(--font-mono); font-size: clamp(0.7rem, 0.95vw, 0.85rem); padding: clamp(0.75rem, 1.2vw, 1rem); border: 1px solid var(--ink); background: var(--bg-panel); color: var(--ink); line-height: 1.6; white-space: pre; overflow-x: auto; } .datadir .dir { color: var(--accent); font-weight: 600; } .datadir .file { color: var(--ink-soft); } .datadir .cmt { color: var(--muted); font-style: italic; } /\* --- Process list (slide 4) --- \*/ .proc-grid { display: grid; grid-template-columns: 1fr 1fr; gap: clamp(0.4rem, 0.75vw, 0.6rem); } @media (max-width: 720px) { .proc-grid { grid-template-columns: 1fr; } } .proc-card { padding: clamp(0.5rem, 0.9vw, 0.75rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: 0.2rem; min-width: 0; } .proc-card .bin { font-family: var(--font-mono); font-weight: 600; font-size: clamp(0.75rem, 1.05vw, 0.92rem); color: var(--accent); } .proc-card .desc { font-size: clamp(0.65rem, 0.88vw, 0.76rem); color: var(--ink-soft); line-height: 1.35; } /\* --- Config code block (slide 5) --- \*/ .config-block { font-family: var(--font-mono); font-size: clamp(0.7rem, 0.95vw, 0.85rem); padding: clamp(0.75rem, 1.2vw, 1rem); border: 1px solid var(--ink); background: var(--bg-panel); color: var(--ink); line-height: 1.55; white-space: pre-wrap; overflow-x: auto; } .config-block .cmt { color: var(--muted); font-style: italic; } .config-block .k { color: var(--accent); font-weight: 600; } .config-block .v { color: var(--ink); } .config-block .sect { display: inline-block; font-weight: 700; color: var(--accent-btc); letter-spacing: 0.06em; } /\* --- Hardware compare (slide 6) --- \*/ .hw-split { display: grid; grid-template-columns: 1fr 1fr; gap: clamp(0.5rem, 1vw, 0.85rem); } @media (max-width: 720px) { .hw-split { grid-template-columns: 1fr; } } .hw-card { padding: clamp(0.85rem, 1.3vw, 1.15rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.3rem, 0.6vw, 0.5rem); min-width: 0; } .hw-card.archive { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); background: var(--bg-panel); } .hw-card.pruned { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent-btc); } .hw-card .tag { display: inline-block; align-self: flex-start; padding: 0.15rem 0.5rem; background: var(--ink); color: var(--bg); font-family: var(--font-mono); font-size: clamp(0.55rem, 0.72vw, 0.66rem); letter-spacing: 0.14em; text-transform: uppercase; } .hw-card.pruned .tag { background: var(--accent-btc); } .hw-card .title { font-family: var(--font-display); font-weight: 900; font-size: clamp(1rem, 1.5vw, 1.3rem); color: var(--ink); line-height: 1.15; } .hw-card .size { font-family: var(--font-mono); font-weight: 700; font-size: clamp(0.85rem, 1.2vw, 1.05rem); color: var(--accent); } .hw-card.pruned .size { color: var(--accent-btc); } .hw-card .desc { font-size: clamp(0.7rem, 0.95vw, 0.82rem); color: var(--ink-soft); line-height: 1.45; } .hw-card .desc b { color: var(--ink); font-weight: 700; } /\* --- Interface grid (slide 7) --- \*/ .iface-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: clamp(0.4rem, 0.8vw, 0.7rem); } @media (max-width: 860px) { .iface-grid { grid-template-columns: 1fr 1fr; } } @media (max-width: 600px) { .iface-grid { grid-template-columns: 1fr; } } .iface-card { padding: clamp(0.65rem, 1vw, 0.9rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.25rem, 0.5vw, 0.4rem); min-width: 0; } .iface-card .tag { font-family: var(--font-mono); font-size: clamp(0.55rem, 0.72vw, 0.66rem); letter-spacing: 0.14em; text-transform: uppercase; color: var(--muted); } .iface-card .name { font-family: var(--font-display); font-weight: 900; font-size: clamp(0.95rem, 1.4vw, 1.2rem); color: var(--ink); line-height: 1.15; letter-spacing: -0.01em; } .iface-card .name .accent { color: var(--accent); } .iface-card .port { font-family: var(--font-mono); font-weight: 600; font-size: clamp(0.7rem, 0.95vw, 0.82rem); color: var(--accent); } .iface-card .desc { font-size: clamp(0.65rem, 0.88vw, 0.76rem); color: var(--ink-soft); line-height: 1.4; } .iface-card .desc b { color: var(--ink); font-weight: 700; } /\* --- CLI cheatsheet (slides 8-9) --- \*/ .cli-grid { display: grid; grid-template-columns: 1fr 1fr; gap: clamp(0.45rem, 0.9vw, 0.8rem); } @media (max-width: 720px) { .cli-grid { grid-template-columns: 1fr; } } .cli-group { padding: clamp(0.65rem, 1vw, 0.9rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.25rem, 0.5vw, 0.4rem); min-width: 0; } .cli-group.accent { background: var(--bg-panel); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); } .cli-group .q-head { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.85vw, 0.72rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } .cli-group ul { list-style: none; display: flex; flex-direction: column; gap: 0.15rem; } .cli-group ul li { font-family: var(--font-mono); font-size: clamp(0.63rem, 0.88vw, 0.76rem); color: var(--ink); line-height: 1.45; } .cli-group ul li .cmd { color: var(--accent); font-weight: 500; } .cli-group ul li .cmt { color: var(--muted); font-style: italic; } /\* --- Network table (slide 10) --- \*/ .net-table { display: grid; grid-template-columns: 1fr 1fr 1fr 1.1fr; border-top: clamp(1.5px, 0.25vw, 2px) solid var(--ink); border-bottom: clamp(1.5px, 0.25vw, 2px) solid var(--ink); background: var(--bg); } @media (max-width: 860px) { .net-table { grid-template-columns: 1fr; } } .net-table .cell { padding: clamp(0.45rem, 0.8vw, 0.7rem) clamp(0.4rem, 0.75vw, 0.6rem); border-right: 1px solid var(--grid-line); border-bottom: 1px solid var(--grid-line); font-size: clamp(0.65rem, 0.88vw, 0.78rem); color: var(--ink-soft); line-height: 1.35; min-width: 0; } .net-table .cell:last-child { border-right: none; } .net-table .row-head { background: var(--ink); color: var(--bg); font-family: var(--font-display); font-weight: 800; letter-spacing: 0.14em; text-transform: uppercase; font-size: clamp(0.55rem, 0.75vw, 0.68rem); } .net-table .cell b { color: var(--ink); font-weight: 700; } .net-table .net-name { font-family: var(--font-display); font-weight: 800; color: var(--accent); letter-spacing: 0.02em; text-transform: uppercase; font-size: clamp(0.7rem, 0.95vw, 0.82rem); } .net-table .net-name.btc { color: var(--accent-btc); } /\* --- Signet variants (slide 11) --- \*/ .signet-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: clamp(0.45rem, 0.9vw, 0.8rem); } @media (max-width: 860px) { .signet-grid { grid-template-columns: 1fr; } } .signet-card { padding: clamp(0.75rem, 1.2vw, 1rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.3rem, 0.55vw, 0.45rem); min-width: 0; } .signet-card.global { background: var(--bg-panel); border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); } .signet-card.mutiny { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent-btc); } .signet-card .tag { font-family: var(--font-mono); font-size: clamp(0.55rem, 0.72vw, 0.66rem); letter-spacing: 0.14em; text-transform: uppercase; color: var(--muted); } .signet-card .name { font-family: var(--font-display); font-weight: 900; font-size: clamp(0.95rem, 1.4vw, 1.2rem); color: var(--ink); line-height: 1.15; } .signet-card .hi { font-family: var(--font-mono); font-weight: 700; color: var(--accent); font-size: clamp(0.72rem, 0.95vw, 0.82rem); } .signet-card.mutiny .hi { color: var(--accent-btc); } .signet-card .desc { font-size: clamp(0.66rem, 0.88vw, 0.78rem); color: var(--ink-soft); line-height: 1.42; } /\* --- Regtest flow (slide 12) --- \*/ .regtest-flow { display: grid; grid-template-columns: 1fr auto 1fr auto 1fr; align-items: stretch; gap: clamp(0.3rem, 0.6vw, 0.5rem); padding: clamp(0.5rem, 1vw, 0.85rem) 0; } @media (max-width: 860px) { .regtest-flow { grid-template-columns: 1fr; } .regtest-flow .arr { display: none; } } .regtest-step { padding: clamp(0.55rem, 1vw, 0.85rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.2rem, 0.4vw, 0.3rem); min-width: 0; } .regtest-step .n { font-family: var(--font-display); font-weight: 900; font-size: clamp(1.2rem, 2vw, 1.7rem); color: var(--accent); line-height: 1; } .regtest-step .t { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.75rem, 1vw, 0.88rem); color: var(--ink); } .regtest-step .c { font-family: var(--font-mono); font-size: clamp(0.62rem, 0.85vw, 0.74rem); color: var(--ink-soft); line-height: 1.4; white-space: pre-line; } .regtest-flow .arr { align-self: center; font-family: var(--font-display); font-weight: 900; color: var(--muted); font-size: clamp(1rem, 1.6vw, 1.4rem); } /\* --- Simulation comparison (slide 13) --- \*/ .sim-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: clamp(0.45rem, 0.9vw, 0.8rem); } @media (max-width: 860px) { .sim-grid { grid-template-columns: 1fr; } } .sim-card { padding: clamp(0.75rem, 1.2vw, 1rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.3rem, 0.55vw, 0.45rem); min-width: 0; } .sim-card .name { font-family: var(--font-display); font-weight: 900; font-size: clamp(1rem, 1.5vw, 1.3rem); color: var(--accent); line-height: 1.1; } .sim-card .sub { font-family: var(--font-mono); font-size: clamp(0.6rem, 0.8vw, 0.72rem); letter-spacing: 0.1em; text-transform: uppercase; color: var(--muted); } .sim-card .desc { font-size: clamp(0.66rem, 0.88vw, 0.78rem); color: var(--ink-soft); line-height: 1.42; } .sim-card .desc b { color: var(--ink); font-weight: 700; } .sim-card .best { padding: clamp(0.25rem, 0.5vw, 0.4rem) clamp(0.4rem, 0.7vw, 0.55rem); background: var(--ink); color: var(--bg); font-family: var(--font-display); font-weight: 700; font-size: clamp(0.58rem, 0.78vw, 0.68rem); letter-spacing: 0.12em; text-transform: uppercase; align-self: flex-start; } /\* --- Ecosystem diagram (slide 14) --- \*/ .eco-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: clamp(0.4rem, 0.8vw, 0.7rem); } @media (max-width: 860px) { .eco-grid { grid-template-columns: 1fr 1fr; } } @media (max-width: 500px) { .eco-grid { grid-template-columns: 1fr; } } .eco-card { padding: clamp(0.55rem, 0.95vw, 0.8rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.2rem, 0.4vw, 0.3rem); min-width: 0; } .eco-card.core { background: var(--ink); color: var(--bg); border-color: var(--ink); } .eco-card .cat { font-family: var(--font-mono); font-size: clamp(0.55rem, 0.72vw, 0.66rem); letter-spacing: 0.14em; text-transform: uppercase; color: var(--accent); } .eco-card.core .cat { color: var(--accent-btc); } .eco-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.82rem, 1.15vw, 0.98rem); line-height: 1.15; } .eco-card .desc { font-size: clamp(0.62rem, 0.85vw, 0.74rem); color: var(--ink-soft); line-height: 1.4; } .eco-card.core .desc { color: rgba(255,255,255,0.72); } .eco-card .desc b { color: var(--ink); font-weight: 700; } .eco-card.core .desc b { color: var(--bg); } /\* --- Distro table (slide 15) --- \*/ .distro-table { display: grid; grid-template-columns: 1.2fr 2fr 1.5fr; border-top: clamp(1.5px, 0.25vw, 2px) solid var(--ink); border-bottom: clamp(1.5px, 0.25vw, 2px) solid var(--ink); background: var(--bg); } @media (max-width: 720px) { .distro-table { grid-template-columns: 1fr; } } .distro-table .cell { padding: clamp(0.45rem, 0.8vw, 0.7rem) clamp(0.4rem, 0.75vw, 0.6rem); border-right: 1px solid var(--grid-line); border-bottom: 1px solid var(--grid-line); font-size: clamp(0.67rem, 0.9vw, 0.8rem); color: var(--ink-soft); line-height: 1.4; min-width: 0; } .distro-table .cell:last-child { border-right: none; } .distro-table .row-head { background: var(--ink); color: var(--bg); font-family: var(--font-display); font-weight: 800; letter-spacing: 0.14em; text-transform: uppercase; font-size: clamp(0.55rem, 0.75vw, 0.68rem); } .distro-table .d-name { font-family: var(--font-display); font-weight: 800; color: var(--accent); letter-spacing: 0.02em; font-size: clamp(0.78rem, 1.05vw, 0.92rem); } .distro-table .cell b { color: var(--ink); font-weight: 700; } /\* --- Mining stack (slide 16) --- \*/ .mining-split { display: grid; grid-template-columns: 1fr 1fr; gap: clamp(0.45rem, 0.9vw, 0.8rem); } @media (max-width: 720px) { .mining-split { grid-template-columns: 1fr; } } .mining-card { padding: clamp(0.65rem, 1vw, 0.9rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.25rem, 0.5vw, 0.4rem); min-width: 0; } .mining-card.client { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); background: var(--bg-panel); } .mining-card.pool { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent-btc); } .mining-card .q-head { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.6rem, 0.85vw, 0.72rem); letter-spacing: 0.22em; text-transform: uppercase; color: var(--muted); } .mining-card ul { list-style: none; display: flex; flex-direction: column; gap: 0.15rem; } .mining-card ul li { font-size: clamp(0.66rem, 0.88vw, 0.78rem); color: var(--ink-soft); line-height: 1.4; } .mining-card ul li b { color: var(--ink); font-weight: 700; } .mining-card ul li .mono { font-family: var(--font-mono); color: var(--accent); font-weight: 500; } /\* --- Controversy split (slide 17) --- \*/ .contro-split { display: grid; grid-template-columns: 1fr 1fr; gap: clamp(0.5rem, 1vw, 0.85rem); align-items: stretch; } @media (max-width: 720px) { .contro-split { grid-template-columns: 1fr; } } .contro-card { padding: clamp(0.85rem, 1.3vw, 1.15rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.4rem, 0.7vw, 0.6rem); min-width: 0; } .contro-card.policy { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent); background: var(--bg-panel); } .contro-card.consensus { border-left: clamp(3px, 0.5vw, 5px) solid var(--accent-btc); } .contro-card .tag { align-self: flex-start; padding: 0.15rem 0.5rem; background: var(--ink); color: var(--bg); font-family: var(--font-mono); font-size: clamp(0.55rem, 0.72vw, 0.66rem); letter-spacing: 0.14em; text-transform: uppercase; } .contro-card.consensus .tag { background: var(--accent-btc); } .contro-card .name { font-family: var(--font-display); font-weight: 900; font-size: clamp(1rem, 1.5vw, 1.3rem); color: var(--ink); line-height: 1.15; } .contro-card .desc { font-size: clamp(0.7rem, 0.95vw, 0.82rem); color: var(--ink-soft); line-height: 1.45; } .contro-card .desc b { color: var(--ink); font-weight: 700; } /\* --- Resources grid (slide 18) --- \*/ .res-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: clamp(0.4rem, 0.8vw, 0.7rem); } @media (max-width: 600px) { .res-grid { grid-template-columns: 1fr; } } .res-card { padding: clamp(0.6rem, 1vw, 0.85rem); border: 1px solid var(--ink); background: var(--bg); display: flex; flex-direction: column; gap: clamp(0.2rem, 0.4vw, 0.3rem); min-width: 0; } .res-card .cat { font-family: var(--font-mono); font-size: clamp(0.55rem, 0.72vw, 0.66rem); letter-spacing: 0.14em; text-transform: uppercase; color: var(--accent); } .res-card .name { font-family: var(--font-display); font-weight: 800; font-size: clamp(0.82rem, 1.15vw, 0.98rem); color: var(--ink); line-height: 1.15; } .res-card .url { font-family: var(--font-mono); font-size: clamp(0.6rem, 0.82vw, 0.72rem); color: var(--ink-soft); word-break: break-all; }

←→ Navegar

Módulo 05 · Bitcoin

Sesión 2 / Infraestructura

Bloque 2

# Infraestructura Bitcoin

De la instalación al bloque minado: cómo funciona un nodo Bitcoin por dentro.

Manuel Montenegro Curso de Extensión Universitaria en Tecnologías Blockchain · UMA · 2026

Módulo 05 · Bitcoin

01 · Clientes de nodo

01 · Implementaciones del protocolo

## Varios clientes, un mismo consenso.

C++ · MIT Bitcoin Core ~75% **Implementación de referencia**. v30 (oct. 2025). Descriptor-only wallets, sin BDB, sin límite OP\_RETURN.

C++ · MIT Bitcoin Knots ~22% Fork conservador de **Luke Dashjr**. Mantiene spam filters y el límite de OP\_RETURN.

Go · ISC btcd ~0.5% **Sin wallet** por diseño. Solo nodo + RPC. Muy usado en librerías del ecosistema Go.

C++ · AGPL libbitcoin ~1.3% Arquitectura **modular y limpia**. Poca tracción real en producción.

Node.js bcoin <0.5% Mantenido por Purse/Handshake. **Casi inactivo** hoy.

**¿Descentralización, también en el desarrollo?** Un bug sutil en una implementación minoritaria puede provocar un fork accidental.  
En **marzo de 2013**, la actualización de Bitcoin Core 0.7 a 0.8 cambió la base de datos interna (de BerkeleyDB a LevelDB): un bloque perfectamente válido para los nodos 0.8 fue rechazado por los nodos 0.7 por un límite silencioso de BDB, y la red se bifurcó durante **~6 horas** hasta que los mineros acordaron volver a la cadena compatible con 0.7.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 02/17

Módulo 05 · Bitcoin

02 · Anatomía del nodo

02 · Qué se instala con Bitcoin Core

## Cuatro binarios y un datadir.

bitcoind Daemon en _background_. El nodo propiamente dicho.

bitcoin-qt Mismo binario con GUI en Qt.

bitcoin-cli Cliente CLI que habla **JSON-RPC** con el daemon.

bitcoin-tx Crea y firma tx **offline**, sin nodo.

~/.bitcoin/ \# datadir por defecto ├── blocks/ \# bloques crudos: blk00000.dat, blk00001.dat… ├── chainstate/ \# UTXO set actual (LevelDB) ├── indexes/ \# opcional: txindex, coinstatsindex… ├── wallets/ \# descriptor wallets (SQLite) desde v0.21 ├── mempool.dat \# mempool persistido entre reinicios ├── debug.log \# log principal ├── bitcoin.conf \# configuración ├── testnet4/ \# cada red vive en su subdir ├── signet/ └── regtest/

Cada red (**main · testnet4 · signet · regtest**) aterriza en su propio subdirectorio, aislada del resto.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 03/17

Módulo 05 · Bitcoin

03 · bitcoin.conf

03 · Configuración del nodo

## El 90 % del despliegue vive en bitcoin.conf.

\# ── Red ───────────────────────────── testnet4\=1 \# signet=1 / regtest=1 \# ── Almacenamiento ───────────────── prune\=5000 \# MiB; 0 = archive dbcache\=4000 \# RAM para UTXO cache txindex\=1 \# incompatible con prune coinstatsindex\=1 blockfilterindex\=1 \# ── RPC ──────────────────────────── server\=1 rpcauth\=user:hash... rpcbind\=127.0.0.1 rpcallowip\=127.0.0.1 \# ── ZMQ · push a apps ────────────── zmqpubrawblock\=tcp://127.0.0.1:28332 zmqpubrawtx\=tcp://127.0.0.1:28333 \# ── Privacidad · Tor ─────────────── proxy\=127.0.0.1:9050 listenonion\=1

*   **Flags mutuamente excluyentes**: `testnet`, `testnet4`, `signet`, `regtest`. Sin ninguna = mainnet.
*   **Prune vs. txindex**: elige uno. Prune tira bloques viejos; txindex conserva todo e indexa.
*   **Índices opcionales**: `coinstatsindex` precomputa estadísticas agregadas del UTXO set (supply total, #UTXOs) para responder `gettxoutsetinfo` al instante. `blockfilterindex` construye filtros compactos BIP 157/158 que permiten a light wallets (p.ej. Neutrino) detectar _sus_ tx sin descargar bloques enteros.
*   **rpcauth** (hash salado) > `rpcuser/rpcpassword` en texto plano. _Nunca_ expongas el RPC a internet.
*   **ZMQ** permite que apps externas (explorers, bots) reaccionen al instante a nuevos bloques y tx.
*   **Configuración**: _Bitcoin Core Config Generator:_ [formulario web](https://jlopp.github.io/bitcoin-core-config-generator/) que te devuelve el fichero ya validado.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 04/17

Módulo 05 · Bitcoin

04 · Hardware

04 · Archive vs. pruned

## Dos perfiles de disco, mismo consenso.

Archive · prune=0 Nodo **completo** ~700 GB (abril 2026) · SSD Guarda **toda la historia** de bloques. Útil para: _txindex_, explorers, block-cutters, queries del pasado. **IBD** (_Initial Block Download_ — la sincronización inicial desde el génesis hasta la punta actual): **días a semanas**. **Sirve bloques históricos** a otros peers cuando se sincronizan. _Community service_ de la red.

Pruned · prune≥550 Nodo **completo con poda** 5 – 20 GB · SSD o HDD Verifica **toda la cadena desde el génesis**, pero luego **tira los bloques viejos**. Mantiene solo UTXO set + últimos N MiB. No puede hacer _txindex_ ni servir bloques antiguos. **Misma seguridad** para ti, pero no contribuyes al IBD de otros.

~700GBCadena completa

4GBRAM mínimo

8332Puerto RPC · mainnet

8333Puerto P2P

**Full node** — verifica todo el consenso (archive _o_ pruned).  
**Archive node** — variante de full node que _además_ conserva todos los bloques.  
**SPV / light client** — no verifica: confía en los peers y trabaja solo con cabeceras.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 05/17

Módulo 05 · Bitcoin

05 · Interfaces

05 · Cómo se habla con bitcoind

## Cuatro canales, cuatro propósitos.

Control · pull JSON-RPC :8332 · HTTP + JSON El 95 % del trabajo. Control total del nodo y la wallet desde apps y CLI. **Autenticado**.

Read-only · pull REST :8332 · HTTP GET Solo lectura. Activar con `rest=1`. Útil para explorers que no necesitan escribir.

Notificación · push ZMQ :28332+ · TCP pub/sub El nodo _empuja_ eventos: **bloque nuevo**, **tx nueva**, **hashes**. Sin _polling_, reacción instantánea.

Consenso · pares P2P :8333 · binario propio Protocolo entre nodos para propagar bloques y tx. **BIP 324** añade cifrado entre pares.

Una stack típica: la **app** lanza comandos vía **RPC**, se suscribe a **ZMQ** para notificaciones, y expone datos al navegador por **REST**.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 06/17

Módulo 05 · Bitcoin

06 · bitcoin-cli · cadena

06 · Cheatsheet · estado · bloques · tx

## Los comandos de gestión del nodo.

Todos los comandos de esta lista se invocan como `bitcoin-cli [-regtest|-signet] <comando> [args…]`. El flag de red (por defecto, mainnet) se coloca _antes_ del comando.

Estado del nodo · cadena

*   getblockchaininfo \# altura, IBD, red, softforks
*   getnetworkinfo \# peers, versión, warnings
*   getmempoolinfo \# tx en mempool, minfee
*   getpeerinfo \# detalle de cada peer
*   getblockcount \# altura actual
*   getbestblockhash \# hash del tip
*   uptime \# segundos de vida del nodo

Consultar bloques

*   getblockhash <height>
*   getblock <hash> \[verbosity\]
*   getblockheader <hash>
*   getblockstats <hash|height>
*   getdifficulty \# dificultad actual (×genesis)
*   getchaintxstats \# estadísticas globales

Consultar transacciones

*   getrawtransaction <txid> \[verbose\]
*   decoderawtransaction <hex>
*   gettxout <txid> <vout> # UTXO set
*   sendrawtransaction <hex>
*   testmempoolaccept '\[<hex>\]'

Servicios auxiliares

*   help \[cmd\] # descripción del comando
*   stop \# apaga el nodo limpiamente
*   addnode <host> add|remove|onetry
*   setnetworkactive true|false
*   verifychain \[level\] \[nblocks\]

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 07/17

Módulo 05 · Bitcoin

07 · bitcoin-cli · wallet

07 · Cheatsheet · wallet · PSBT · regtest

## Wallet, firma multi-parte y minería local.

Todos los comandos de esta lista se invocan como `bitcoin-cli [-regtest|-signet] <comando> [args…]`. El flag de red (por defecto, mainnet) se coloca _antes_ del comando.

Wallet · descriptor-only

*   createwallet "name"
*   loadwallet / unloadwallet
*   getnewaddress \["label"\] \[bech32|bech32m\]
*   listunspent \# tus UTXOs
*   getbalance / getbalances \# saldo total / desglose por estado
*   sendtoaddress <addr> <btc> # envía sats a una dirección

PSBT · firmas offline · multisig

*   walletcreatefundedpsbt \# crea PSBT con inputs y cambio
*   walletprocesspsbt \# firma con la wallet local
*   combinepsbt \# junta firmas
*   finalizepsbt \# produce hex broadcastable
*   analyzepsbt \# ¿qué le falta?
*   decodepsbt \# vista humana

Regtest · minería bajo demanda

*   generatetoaddress <n> <addr> # mina n bloques al vuelo
*   generateblock <addr> '\[txs\]' # mina un bloque con txs elegidas
*   invalidateblock <hash> # simula reorg
*   reconsiderblock <hash> # deshace un invalidateblock
*   getmininginfo \# dificultad, tamaño

Mempool · fees · descriptors

*   getrawmempool \[verbose\]
*   bumpfee <txid> # RBF
*   psbtbumpfee <txid>
*   prioritisetransaction \# sube/baja prioridad local
*   estimatesmartfee <confs>
*   getdescriptorinfo \# valida y añade checksum a un descriptor
*   deriveaddresses <desc> # expande un descriptor en direcciones

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 08/17

Módulo 05 · Bitcoin

08 · Redes

08 · Redes de Bitcoin

## Una red para cada propósito.

Red

Consenso

Control

Uso típico

mainnet

PoW · ~10 min

Descentralizado

Producción.

testnet3

PoW, irregular (_timewarp_)

Descentralizado, inestable

Compatibilidad histórica. **En deprecación**.

testnet4

PoW + fix timewarp (**BIP 94**)

Descentralizado

Reemplazo oficial de testnet3 (Core v28+).

signet

Bloques **firmados** (BIP 325)

Clave del signet challenge

Testing predecible y estable.

regtest

Tú mineas con `generatetoaddress`

100 % local

Dev, CI, tests, **prácticas de clase**.

**Timewarp**: vulnerabilidad clásica de testnet3 donde los mineros pueden manipular los _timestamps_ de los bloques para forzar un ajuste de dificultad a la baja y minar cientos de bloques en segundos. BIP 94 (testnet4) lo corrige acotando el margen de los timestamps entre periodos de dificultad.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 09/17

Módulo 05 · Bitcoin

09 · Signet

09 · Signet · la red pública estable

## Misma semántica, otra cadencia.

**Signet** es una red pública de pruebas en la que _no hay competición por minar_: en lugar de _proof-of-work_ abierto, los bloques los produce un conjunto cerrado de firmantes autorizados. Esto elimina los problemas de testnet3 (ataques de timewarp, _stalls_ de días, reorgs enormes) y hace que la red sea **predecible**, **estable** y **compartida** entre desarrolladores de todo el mundo.

Un bloque signet **solo es válido** si su coinbase incluye una firma de las claves autorizadas (_block challenge_). Elimina la volatilidad de testnet3 a cambio de un único punto de control explícito. BIP 325 · propuesto por Karl-Johan Alm en 2020.

Pública · oficial Signet global ~10 min/bloque La instancia por defecto (_Global Signet_). Activas con `-signet`. Faucets, explorers y peers públicos disponibles.

Pública · alternativa MutinyNet bloques cada 30 s Signet custom del equipo **Mutiny Wallet**. Tuvieron que forkear Core para hacer configurable el target. Faucet, esplora API, LSPs.

Privada Custom signet tú defines todo Arrancas con `-signet -signetchallenge=<script>`. **Tu propia red** para laboratorio, CI, talleres.

Signet encaja cuando necesitas **una red pública con otros actores** pero _predecible_. Para trabajo 100 % solo, regtest es mejor.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 10/17

Módulo 05 · Bitcoin

10 · Regtest

10 · Regtest · nuestro laboratorio

## Tu red privada de Bitcoin, en segundos.

01 Arrancar $ bitcoind -regtest -daemon

→

02 Crear wallet + addr $ bitcoin-cli -regtest createwallet "lab" $ A=$(bitcoin-cli -regtest getnewaddress)

→

03 Minar 101 bloques $ bitcoin-cli -regtest \\ generatetoaddress 101 $A

*   **Dificultad mínima**: cada `generatetoaddress` produce un bloque _instantáneo_. Nadie más mina.
*   **Por qué 101** bloques: el coinbase de un bloque no es gastable hasta pasados **100 bloques** (regla COINBASE\_MATURITY).
*   **Red aislada**: puerto p2p `:18444`, RPC `:18443`. Cero riesgo de tocar mainnet.

\# Descargar Bitcoin Core → [bitcoincore.org/en/download](https://bitcoincore.org/en/download/) \# Binarios oficiales firmados por los # mantenedores del proyecto. Incluye # bitcoind, bitcoin-cli, bitcoin-qt y # bitcoin-tx. Disponible para Linux, # macOS y Windows.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 11/17

Módulo 05 · Bitcoin

11 · Simulación

11 · Herramientas de simulación regtest

## Regtest con todo incluido.

GUI · Electron + Docker Polar Interfaz gráfica para levantar **redes Bitcoin + Lightning en regtest** con un clic. Faucet integrado, logs en vivo, visualización de canales. Ideal para: **principiantes**, demos visuales, primeros experimentos. Recomendado · aprendizaje y testing sencillo

CLI · docker-compose Nigiri Un comando: `nigiri start` y tienes **bitcoind regtest + Electrs + Chopsticks** (proxy HTTP con faucet y `/mine`). Ideal para: **CI**, tests automatizados, scripts. Para scripting y tests

Kubernetes · Bitcoin Dev Project Warnet Despliega **redes Bitcoin P2P en un clúster Kubernetes** (o Minikube local). Monitoriza latencia, partición, comportamiento emergente. Usado en _Battle of Galen Erso_ — competición multi-equipo para **atacar nodos**. Avanzado · investigación

Filosofías distintas: **Polar** visualiza, **Nigiri** automatiza, **Warnet** estresa. Para prácticas guiadas en clase, lo más cómodo suele ser empezar con Polar y migrar a Nigiri cuando el ejercicio se automatiza.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 12/17

Módulo 05 · Bitcoin

12 · Infra periférica

12 · Alrededor de bitcoind

## El nodo no va solo.

`bitcoind` valida el consenso, pero por sí solo **no resuelve** preguntas como "¿qué saldo tiene esta dirección?" o "¿qué fees se están pagando ahora mismo?". Alrededor del nodo aparece un **ecosistema de servicios** que transforman esos datos en respuestas útiles para wallets, explorers y pasarelas de pago.

Núcleo bitcoind Valida consenso. Sirve RPC, REST, ZMQ. **No** hace búsqueda por dirección de forma eficiente.

Electrum server · Rust Electrs Indexa por **dirección**. Sync rápido (~1 día). Índice compacto. El más popular.

Electrum server · C++ Fulcrum **~8× más rápido** que ElectrumX para queries. Sync más lento (3-5 días). Recomendado por RaspiBolt.

Electrum server · Python ElectrumX El pionero. **El más lento** sincronizando (una semana). Uso histórico.

Explorer mempool.space El **estándar de facto**. Visualiza mempool, fees, bloques. Auto-hospedable.

Explorer btc-rpc-explorer · Esplora Alternativas más ligeras. Útiles en regtest y CI para inspeccionar.

Pasarela de pago BTCPay Server Auto-hospedado, multi-tienda. Integra bitcoind + Lightning + facturación.

Wallet desktop Sparrow · Specter Conectan a **tu** nodo (directo o vía Electrs). PSBT, multisig, hardware wallets.

**¿Qué es un Electrum server?** Un servicio que se conecta a tu `bitcoind`, lee la blockchain y construye un **índice por dirección y por script**. Expone el _protocolo Electrum_ (TCP/TLS, JSON) para que wallets ligeras (Sparrow, Electrum, Specter) pregunten "dame UTXOs e historial de esta xpub" sin descargar ni indexar toda la cadena. Sin un Electrum server propio, tu wallet acaba hablando con los servidores de terceros.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 13/17

Módulo 05 · Bitcoin

13 · Node-in-a-box

13 · Soberanía sin compilar

## Distros llave en mano.

Distribución

Filosofía

Hardware típico

Umbrel

**Facilidad máxima**. UI tipo iOS, tienda de apps (BTCPay, mempool, electrs…).

Raspberry Pi 4/5 · Umbrel Home · VM Linux.

Start9 · StartOS

**Soberanía y seguridad** ante todo. Tor por defecto, servicios aislados.

Start9 Server (hardware propio) · x86/ARM.

RaspiBlitz

La más longeva. Foco en **Lightning**, pantalla LCD con stats en vivo.

Raspberry Pi + SSD externo.

myNode

Suite completa: BTCPay, JoinMarket, Whirlpool, Specter, Electrs…

**myNode Model Two** (2025): Intel N100, 16 GB, 2 TB.

nix-bitcoin

Config **declarativa y reproducible** en NixOS. Para sysadmins.

Cualquier máquina Linux con NixOS.

**Nota**: todas estas distros permiten ya **cambiar Core por Knots** con un switch en los ajustes — reflejo del cambio de cuota de mercado tras la polémica OP\_RETURN.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 14/17

Módulo 05 · Bitcoin

14 · Minado

14 · Stack de minado · infraestructura

## Cliente, firmware, pool, protocolo.

Cliente · en el minero

*   **CGMiner** C — decano; sigue dominando en ASICs modernos.
*   **BFGMiner** C — fork de CGMiner, hardware específico.
*   **BOSminer** Rust — Braiins; reemplazo moderno, solo Stratum V2.
*   **cpuminer-opt** C — solo aprender o regtest.

Firmware alternativo · ASIC

*   **Braiins OS+** — open source, autotuning.
*   **LuxOS · Vnish · ePIC** — comerciales, optimizan consumo.

Protocolo minero ↔ pool

*   **Stratum V1** (2012, Slush) — TCP + JSON-RPC. _Pool decide_ el template.
*   **Stratum V2** — cifrado, binario, **Job Declaration Protocol**: el minero vuelve a decidir qué txs. Descentraliza la _policy_.
*   **getblocktemplate** BIP22/23 — clásico, para pools descentralizadas.

Software del pool · servidor

*   **CKPool · public-pool** — open source.
*   **SRI** — Stratum V2 reference implementation.
*   **Eloipool** — histórico, apenas mantenido.

Para regtest, `generatetoaddress` sustituye a todo este stack.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 15/17

Módulo 05 · Bitcoin

15 · Policy vs. consensus

15 · La polémica OP\_RETURN / Knots

## Policy no es consensus.

Core v30 (**oct. 2025**) eliminó el límite de 80 bytes en OP\_RETURN. Miles de operadores migraron a **Bitcoin Knots** en protesta. Knots pasó del ~5 % al **~22-25 %** de la red. Es el mejor ejemplo pedagógico actual de que la política de relay _no es lo mismo_ que el consenso. El debate más caliente del ciclo 2024-2026.

Policy · local Lo que decide **cada nodo** **Reglas blandas**, configurables, no rompen la red: qué tx relayas, cuáles aceptas en tu mempool, cuáles minas. Filtros de spam, `datacarriersize`, RBF. Dos nodos honestos pueden **discrepar** en policy sin bifurcar la red. Si una tx "prohibida" llega en un bloque, la **aceptan igual**.

Consensus · red Lo que decide **el protocolo** **Reglas duras**: PoW válida, scripts correctos, firmas ECDSA/Schnorr, cap de 21 M, límites de tamaño de bloque. **Violarlas bifurca la cadena**. Un _soft fork_ endurece consenso; un _hard fork_ lo afloja. El límite de OP\_RETURN **nunca fue consenso** — era policy.

Moraleja para operadores: **eliges tu política** al elegir cliente y configurar flags. Eliges **quién mina por ti** al elegir pool. Consenso lo decide la red entera, no tú.

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 16/17

Módulo 05 · Bitcoin

16 · Recursos y próximos pasos

16 · Cierre · puente a la práctica

## Ahora toca tocarlo.

Libro de referencia Mastering Bitcoin — Antonopoulos & Harding github.com/bitcoinbook/bitcoinbook

Tutoriales Learning Bitcoin from the Command Line github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line

Configuración Bitcoin Core Config Generator · Jameson Lopp jlopp.github.io/bitcoin-core-config-generator/

Docs oficiales bitcoincore.org · RPC API reference bitcoincore.org/en/doc/

Simulación Polar · Nigiri · Warnet lightningpolar.com · nigiri.vulpem.com · warnet.dev

Signet público MutinyNet · faucet · explorer mutinynet.com

Aprendizaje visual Learn Me A Bitcoin — Greg Walker learnmeabitcoin.com

**Curso de Extensión Universitaria en Tecnologías Blockchain** · UMA · 2026 17/17

/\* ======================================================================== SLIDE PRESENTATION · Keyboard nav + progress + dots + IntersectionObserver ======================================================================== \*/ class SlidePresentation { constructor() { this.slides = Array.from(document.querySelectorAll('.slide')); this.total = this.slides.length; this.currentSlide = 0; this.progressBar = document.getElementById('progressBar'); this.navDotsContainer = document.getElementById('navDots'); this.\_buildNavDots(); this.\_observeSlides(); this.\_wireKeys(); this.\_wireScroll(); } \_observeSlides() { const io = new IntersectionObserver((entries) => { entries.forEach((e) => { if (e.isIntersecting) { e.target.classList.add('visible'); const i = this.slides.indexOf(e.target); if (i !== -1) { this.currentSlide = i; this.\_updateNavDots(); } } }); }, { threshold: 0.5 }); this.slides.forEach((s) => io.observe(s)); } \_wireKeys() { document.addEventListener('keydown', (e) => { const t = e.target; const typing = t && t.getAttribute && t.getAttribute('contenteditable') === 'true'; if (typing) return; if (e.key === 'ArrowRight' || e.key === 'PageDown' || e.key === ' ') { e.preventDefault(); this.goTo(this.currentSlide + 1); } else if (e.key === 'ArrowLeft' || e.key === 'PageUp') { e.preventDefault(); this.goTo(this.currentSlide - 1); } else if (e.key === 'Home') { e.preventDefault(); this.goTo(0); } else if (e.key === 'End') { e.preventDefault(); this.goTo(this.total - 1); } }); } \_wireScroll() { window.addEventListener('scroll', () => this.\_updateProgress(), { passive: true }); } \_updateProgress() { const scrollTop = window.scrollY; const total = document.documentElement.scrollHeight - window.innerHeight; const pct = total > 0 ? (scrollTop / total) \* 100 : 0; this.progressBar.style.width = pct + '%'; } \_buildNavDots() { this.navDotsContainer.innerHTML = ''; this.slides.forEach((slide, i) => { const b = document.createElement('button'); b.setAttribute('aria-label', \`Ir a diapositiva ${i + 1}: ${slide.dataset.title || ''}\`); if (i === 0) b.classList.add('active'); b.addEventListener('click', () => this.goTo(i)); this.navDotsContainer.appendChild(b); }); } \_updateNavDots() { this.navDotsContainer.querySelectorAll('button').forEach((b, i) => { b.classList.toggle('active', i === this.currentSlide); }); } goTo(i) { const idx = Math.max(0, Math.min(this.total - 1, i)); this.slides\[idx\].scrollIntoView({ behavior: 'smooth', block: 'start' }); } } // Boot · versión presentación (sin editor inline) window.addEventListener('DOMContentLoaded', () => { new SlidePresentation(); const first = document.querySelector('.slide'); if (first) first.classList.add('visible'); });