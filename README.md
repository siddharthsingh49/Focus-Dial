/* ============================================
   Focus Dial — token system
   Color:  #1B2430 charcoal (bg) · #232E3D panel
           #EDE6D6 bone (text) · #C9A227 brass (primary)
           #B33A3A rust (stop) · #3E6E64 teal (success)
   Type:   Fraunces (display/numerals) · IBM Plex Sans (ui)
           IBM Plex Mono (data / timestamps)
   ============================================ */

:root {
  --bg: #1B2430;
  --panel: #232E3D;
  --panel-raised: #2A3648;
  --bone: #EDE6D6;
  --bone-dim: #A9A79C;
  --brass: #C9A227;
  --brass-bright: #E0BC4C;
  --rust: #B33A3A;
  --teal: #3E6E64;
  --line: rgba(237, 230, 214, 0.12);

  --font-display: 'Fraunces', serif;
  --font-ui: 'IBM Plex Sans', sans-serif;
  --font-mono: 'IBM Plex Mono', monospace;

  color-scheme: dark;
}

* { box-sizing: border-box; }

html, body {
  margin: 0;
  padding: 0;
  background: var(--bg);
  color: var(--bone);
  font-family: var(--font-ui);
}

body {
  min-height: 100vh;
  background-image:
    radial-gradient(circle at 50% -10%, rgba(201,162,39,0.08), transparent 60%);
  display: flex;
  justify-content: center;
  padding: 48px 20px 80px;
}

@media (prefers-reduced-motion: reduce) {
  * { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
}

.workshop {
  width: 100%;
  max-width: 480px;
}

/* ---------- Masthead ---------- */

.masthead {
  text-align: center;
  margin-bottom: 40px;
}

.eyebrow {
  font-family: var(--font-mono);
  font-size: 12px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--brass);
  margin: 0 0 10px;
}

.masthead h1 {
  font-family: var(--font-display);
  font-optical-sizing: auto;
  font-weight: 600;
  font-size: clamp(34px, 8vw, 46px);
  margin: 0 0 8px;
  letter-spacing: -0.01em;
}

.tagline {
  margin: 0;
  color: var(--bone-dim);
  font-size: 15px;
}

/* ---------- Instrument (dial) ---------- */

.instrument {
  background: linear-gradient(180deg, var(--panel-raised), var(--panel));
  border: 1px solid var(--line);
  border-radius: 20px;
  padding: 40px 28px 32px;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-shadow: 0 20px 50px -20px rgba(0,0,0,0.6), inset 0 1px 0 rgba(255,255,255,0.03);
}

.dial-wrap {
  position: relative;
  width: min(320px, 78vw);
  height: min(320px, 78vw);
  touch-action: none;
}

.dial-ticks {
  width: 100%;
  height: 100%;
  overflow: visible;
}

.dial-track {
  fill: none;
  stroke: var(--line);
  stroke-width: 2;
}

.dial-progress {
  stroke: var(--brass);
  stroke-width: 3;
  stroke-linecap: round;
  transition: d 0.15s ease-out;
}

.tick {
  stroke: var(--bone-dim);
  stroke-width: 1.5;
  opacity: 0.45;
}
.tick.major {
  stroke: var(--bone);
  stroke-width: 2.5;
  opacity: 0.8;
}

.knob {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 58%;
  height: 58%;
  transform: translate(-50%, -50%);
  border-radius: 50%;
  border: none;
  cursor: grab;
  background:
    radial-gradient(circle at 35% 28%, #E4C765, #C9A227 45%, #8f7015 100%);
  box-shadow:
    0 10px 24px -8px rgba(0,0,0,0.65),
    inset 0 2px 3px rgba(255,255,255,0.4),
    inset 0 -6px 10px rgba(0,0,0,0.35);
  display: flex;
  align-items: center;
  justify-content: center;
}

.knob:active { cursor: grabbing; }

.knob:focus-visible {
  outline: 3px solid var(--bone);
  outline-offset: 4px;
}

.knob-notch {
  position: absolute;
  top: 10%;
  left: 50%;
  width: 4px;
  height: 16%;
  background: var(--bg);
  border-radius: 2px;
  transform-origin: 50% 250%;
  transform: translateX(-50%);
}

.readout {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  pointer-events: none;
}

.readout-time {
  font-family: var(--font-display);
  font-weight: 500;
  font-size: clamp(30px, 8vw, 38px);
  color: var(--bg);
  letter-spacing: -0.01em;
}

.readout-label {
  font-family: var(--font-mono);
  font-size: 10px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: rgba(27, 36, 48, 0.65);
  margin-top: 2px;
}

/* running state */
.instrument.running .knob {
  cursor: default;
}
.instrument.running .dial-progress {
  stroke: var(--teal);
}
.instrument.running .readout-label {
  color: rgba(27, 36, 48, 0.65);
}
.instrument.done .dial-progress { stroke: var(--rust); }

/* ---------- Controls ---------- */

.controls {
  display: flex;
  gap: 12px;
  margin-top: 32px;
  width: 100%;
  justify-content: center;
}

.btn {
  font-family: var(--font-ui);
  font-weight: 600;
  font-size: 14px;
  border-radius: 10px;
  padding: 13px 22px;
  border: 1px solid transparent;
  cursor: pointer;
  transition: transform 0.12s ease, background 0.15s ease, border-color 0.15s ease;
}
.btn:active { transform: scale(0.97); }
.btn:focus-visible { outline: 2px solid var(--brass); outline-offset: 2px; }

.btn-primary {
  background: var(--brass);
  color: #1B2430;
}
.btn-primary:hover { background: var(--brass-bright); }
.btn-primary.is-active {
  background: var(--rust);
  color: var(--bone);
}
.btn-primary.is-active:hover { background: #c94747; }

.btn-ghost {
  background: transparent;
  color: var(--bone-dim);
  border-color: var(--line);
}
.btn-ghost:hover { color: var(--bone); border-color: var(--bone-dim); }

.btn-text {
  background: transparent;
  color: var(--bone-dim);
  font-size: 12px;
  font-weight: 500;
  padding: 6px 4px;
  align-self: flex-start;
  text-decoration: underline;
  text-underline-offset: 3px;
  text-decoration-color: transparent;
}
.btn-text:hover { text-decoration-color: var(--bone-dim); }

.hint {
  margin: 18px 0 0;
  font-size: 12px;
  color: var(--bone-dim);
  text-align: center;
}

/* ---------- Session log ---------- */

.log {
  margin-top: 28px;
  background: var(--panel);
  border: 1px solid var(--line);
  border-radius: 20px;
  padding: 24px 24px 16px;
}

.log-head {
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  margin-bottom: 12px;
}

.log-head h2 {
  font-family: var(--font-display);
  font-size: 18px;
  font-weight: 600;
  margin: 0;
}

.log-total {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--brass);
}

.log-list {
  list-style: none;
  margin: 0;
  padding: 0;
  border-top: 1px solid var(--line);
}

.log-list li {
  display: flex;
  justify-content: space-between;
  gap: 12px;
  padding: 12px 0;
  border-bottom: 1px solid var(--line);
  font-size: 14px;
}

.log-empty {
  color: var(--bone-dim);
  font-size: 13px !important;
  justify-content: flex-start !important;
}

.log-entry-time {
  font-family: var(--font-mono);
  color: var(--bone-dim);
  font-size: 12px;
}

.log-entry-dur {
  font-family: var(--font-mono);
  color: var(--teal);
  font-weight: 500;
}

/* ---------- Colophon ---------- */

.colophon {
  text-align: center;
  margin-top: 24px;
  font-size: 12px;
  color: var(--bone-dim);
}

.colophon a { color: var(--bone-dim); }
.colophon a:hover { color: var(--brass); }
.dot { opacity: 0.5; margin: 0 4px; }
