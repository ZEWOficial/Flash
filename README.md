<!doctype html><html><head><meta charset=utf8><meta name=viewport content="width=device-width,initial-scale=1,viewport-fit=cover"><style>:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}html{scroll-padding-top:env(safe-area-inset-top,0px)}body{margin:0;padding:0;font:14px -apple-system,BlinkMacSystemFont,sans-serif;background:#fff;color:#000}img{max-width:100%}[hidden]:not([hidden=until-found i]){display:none!important}</style></head><body>
<title>Flashlight Pro</title>
<meta name="claude:viewport-fit-sides" content="cover">
<style>
/* Layout: one iPhone-style device centred on a quiet stage; the app inside has 3 states (dark, lit, paywall). */
:root {
  --bg: #e8eaef;
  --fg: #14161c;
  --muted: #5d6272;
  --pill-bg: #d5d8e0;
  --pill-fg: #3a3e4b;
  --bezel: #0b0b0f;
  --yellow: #f6e414;
  --yellow-deep: #e8b800;
  --ink: #0a0a0f;
  --font: -apple-system, BlinkMacSystemFont, "SF Pro Display", "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) { --bg: #0d0e13; --fg: #ecedf2; --muted: #9a9fb0; --pill-bg: #23252e; --pill-fg: #c5c8d4; color-scheme: dark; }
}
:root[data-theme="dark"] { --bg: #0d0e13; --fg: #ecedf2; --muted: #9a9fb0; --pill-bg: #23252e; --pill-fg: #c5c8d4; color-scheme: dark; }

html, body { min-height: 100%; }
body {
  background: var(--bg); color: var(--fg); font-family: var(--font);
  padding-block: 24px;
  padding-left: max(16px, env(safe-area-inset-left, 0px));
  padding-right: max(16px, env(safe-area-inset-right, 0px));
  display: flex; flex-direction: column; align-items: center; gap: 16px;
}

.phone {
  container-type: inline-size;
  width: min(340px, 100%); aspect-ratio: 9 / 19.2;
  border-radius: 14cqw; background: var(--bezel);
  padding: 2.4cqw; position: relative;
  box-shadow: 0 0 0 1px rgba(255,255,255,.08), 0 30px 60px -20px rgba(0,0,0,.45);
}
.screen {
  position: relative; width: 100%; height: 100%; overflow: hidden;
  border-radius: 12cqw; isolation: isolate;
  font-size: 4cqw; user-select: none; -webkit-user-select: none;
}

/* backgrounds crossfade between dark and lit */
.bg { position: absolute; inset: 0; transition: opacity .55s ease; z-index: -2; }
.bg-dark { background: linear-gradient(180deg, #0e0e15 0%, #15152a 55%, #1d1c3a 100%); }
.bg-lit { background: linear-gradient(180deg, #f2ec86 0%, #fbf8cf 28%, #ffffff 70%); opacity: 0; }
.screen[data-power="on"] .bg-lit { opacity: 1; }

.island { position: absolute; top: 2.6cqw; left: 50%; transform: translateX(-50%); width: 27cqw; height: 8cqw; background: #000; border-radius: 99px; z-index: 5; }
.status { position: absolute; top: 4.5cqw; left: 8cqw; right: 8cqw; display: flex; justify-content: space-between; align-items: center; font-weight: 600; font-size: 3.6cqw; color: #fff; z-index: 4; transition: color .55s; }
.screen[data-power="on"] .status { color: #1a1a1a; }
.status svg { width: 11cqw; height: 4cqw; }

.title { position: absolute; top: 20cqw; width: 100%; text-align: center; z-index: 2; }
.title h1 { margin: 0; font-size: 2.9cqw; letter-spacing: .42em; font-weight: 800; color: #fff; padding-left: .42em; transition: color .55s; }
.title p { margin: 1.2cqw 0 0; font-size: 2.6cqw; font-weight: 600; color: #8d8ca8; transition: color .55s; }
.screen[data-power="on"] .title h1 { color: #2b2a1c; }
.screen[data-power="on"] .title p { color: #8a8458; }

.dial { position: absolute; left: 50%; top: 48%; width: 46cqw; height: 46cqw; transform: translate(-50%, -50%); z-index: 1; }
.ring { position: absolute; inset: -9cqw; border-radius: 50%; background: rgba(255,255,255,.07); transition: opacity .55s; }
.disc { position: absolute; inset: 0; border-radius: 50%; background: #c7c7cd; display: grid; place-items: center; transition: opacity .55s, transform .55s; }
.disc svg { width: 17cqw; height: 28cqw; }
.glow { position: absolute; inset: -26cqw; border-radius: 50%; opacity: 0; transition: opacity .6s ease;
  background: radial-gradient(circle, rgba(255,230,0,.95) 0%, rgba(255,222,0,.7) 22%, rgba(255,230,60,.28) 48%, rgba(255,255,255,0) 70%); filter: blur(2cqw); }
.screen[data-power="on"] .glow { opacity: 1; animation: pulse 3.2s ease-in-out .6s infinite; }
.screen[data-power="on"] .disc { opacity: .08; transform: scale(.9); }
.screen[data-power="on"] .ring { opacity: 0; }
@keyframes pulse { 0%,100% { transform: scale(1); filter: blur(2cqw) hue-rotate(0deg); } 50% { transform: scale(1.12); filter: blur(2cqw) hue-rotate(-8deg); } }

.controls { position: absolute; left: 7cqw; right: 7cqw; bottom: 7cqw; display: flex; gap: 3.5cqw; z-index: 2; }
.btn { flex: 1; height: 13cqw; border-radius: 99px; border: 0; font: inherit; font-weight: 800; font-size: 3.6cqw; letter-spacing: .06em; cursor: pointer; display: flex; align-items: center; justify-content: center; gap: 1.6cqw; transition: background .5s, color .5s, opacity .5s, transform .12s; }
.btn:active { transform: scale(.97); }
.btn svg { width: 3.6cqw; height: 3.6cqw; display: none; }
.btn-on { background: var(--yellow); color: #111; }
.btn-off { background: rgba(255,255,255,.14); color: #b9b8cd; border: 1px solid rgba(255,255,255,.14); }
.screen[data-power="on"] .btn-on { background: #eef07a; color: rgba(40,40,10,.25); }
.screen[data-power="on"] .btn-off { background: #0b0b0b; color: #fff; border-color: #0b0b0b; }
.screen[data-power="on"] .btn-off svg { display: block; }
.btn:focus-visible { outline: 2px solid #fff; outline-offset: 2px; box-shadow: 0 0 0 4px #7a6cff; }

/* paywall sheet */
.sheet { position: absolute; left: 0; right: 0; bottom: 0; top: 13cqw; z-index: 6; border-radius: 9cqw 9cqw 0 0;
  background: linear-gradient(180deg, #14141b 0%, #1a1810 46%, #3b3004 78%, #8a7300 100%);
  transform: translateY(104%); transition: transform .45s cubic-bezier(.22,.9,.28,1);
  display: flex; flex-direction: column; align-items: center; padding: 8cqw 7cqw 5cqw; color: #fff; }
.screen[data-paywall="true"] .sheet { transform: translateY(0); }
.close { position: absolute; top: 4.5cqw; right: 5cqw; width: 7cqw; height: 7cqw; border: 0; background: transparent; color: #d8d8e0; cursor: pointer; display: grid; place-items: center; border-radius: 50%; }
.close svg { width: 3.6cqw; height: 3.6cqw; }
.pro { display: flex; align-items: center; gap: 1.2cqw; font-weight: 800; font-size: 3.7cqw; margin-top: 4cqw; }
.pro svg { width: 3cqw; height: 3cqw; color: var(--yellow); }
.price { margin: 4cqw 0 0; font-size: 21cqw; font-weight: 900; line-height: 1; letter-spacing: -.02em; color: #ffd60a; text-shadow: 0 0 5cqw rgba(255,214,10,.45); font-variant-numeric: tabular-nums; }
.kicker { margin: 5.5cqw 0 0; font-size: 2.5cqw; letter-spacing: .14em; font-weight: 800; color: #e8e6dc; text-align: center; }
.sub { margin: 3.5cqw 0 0; font-size: 3.1cqw; line-height: 1.45; color: #dedbd0; text-align: center; font-weight: 500; }
.perks { list-style: none; margin: 8cqw 0 0; padding: 5cqw 4.5cqw; width: 100%; border-radius: 4cqw; background: rgba(120,110,85,.45); display: flex; flex-direction: column; gap: 4.2cqw; }
.perks li { display: flex; align-items: center; gap: 3.5cqw; font-size: 3.1cqw; font-weight: 700; color: #f1efe6; }
.perks svg { width: 4.4cqw; height: 4.4cqw; flex: none; color: var(--yellow); }
.cta { margin-top: auto; width: 100%; height: 12.5cqw; border: 0; border-radius: 99px; background: var(--yellow); color: #111; font: inherit; font-weight: 800; font-size: 3.5cqw; cursor: pointer; transition: transform .12s; box-shadow: 0 2cqw 6cqw rgba(246,228,20,.25); }
.cta:active { transform: scale(.98); }
.cta.nudge { animation: nudge .4s; }
@keyframes nudge { 25% { transform: translateX(-1.4cqw); } 75% { transform: translateX(1.4cqw); } }
.restore { margin-top: 3.2cqw; border: 0; background: transparent; color: #cfcbb8; font: inherit; font-size: 2.7cqw; font-weight: 600; cursor: pointer; }
.fine { margin: 2cqw 0 0; font-size: 2.1cqw; color: #bdb58a; text-align: center; line-height: 1.4; }

.toast { position: absolute; left: 50%; top: 17cqw; transform: translate(-50%, -8cqw); z-index: 8; background: rgba(0,0,0,.82); color: #fff; font-size: 3cqw; font-weight: 600; padding: 2.2cqw 4cqw; border-radius: 99px; white-space: nowrap; opacity: 0; transition: opacity .25s, transform .25s; pointer-events: none; }
.toast.show { opacity: 1; transform: translate(-50%, 0); }

.rail { display: flex; gap: 10px; }
.chip { font-size: 12px; font-weight: 600; padding: 6px 12px; border-radius: 99px; background: var(--pill-bg); color: var(--pill-fg); display: inline-flex; align-items: center; gap: 6px; }
.chip svg { width: 13px; height: 13px; }
.hint { margin: 0; font-size: 13px; color: var(--muted); text-align: center; max-width: 34ch; }

@media (prefers-reduced-motion: reduce) {
  .bg, .sheet, .glow, .disc, .btn, .toast { transition-duration: .01s; }
  .screen[data-power="on"] .glow, .cta.nudge { animation: none; }
}
</style>

<main class="phone" aria-label="Flashlight Pro app">
  <div class="screen" id="screen" data-power="off" data-paywall="false">
    <div class="bg bg-dark"></div>
    <div class="bg bg-lit"></div>
    <div class="island"></div>
    <div class="status" aria-hidden="true">
      <span>4:17</span>
      <svg viewBox="0 0 44 16" fill="currentColor"><path d="M2 12a1.5 1.5 0 013 0 1.5 1.5 0 01-3 0zM9 9a1.5 1.5 0 013 0v3a1.5 1.5 0 01-3 0zM16 6a1.5 1.5 0 013 0v6a1.5 1.5 0 01-3 0z" opacity="0"/><path d="M8 5.2a8.5 8.5 0 0112 0l-1.4 1.4a6.5 6.5 0 00-9.2 0zM11 8.2a4.2 4.2 0 016 0l-1.4 1.4a2.2 2.2 0 00-3.2 0zM13.2 11.2a1.2 1.2 0 011.6 0L14 12.4z"/><rect x="26" y="3" width="16" height="9" rx="2.6"/></svg>
    </div>
    <div class="title"><h1>FLASHLIGHT</h1><p id="state-label">Off</p></div>

    <div class="dial" aria-hidden="true">
      <div class="glow"></div>
      <div class="ring"></div>
      <div class="disc">
        <svg viewBox="0 0 34 56" fill="none"><path d="M5 2h24l-3 12v4a6 6 0 01-18 0z" fill="#1a1a1f" opacity="0"/><path d="M4 2h26l-2 11H6z" fill="#17171b"/><path d="M8 13h18v6a9 9 0 01-3 6.7V50a6 6 0 01-12 0V25.700A9 9 0 018 19z" fill="#17171b"/><rect x="14.500" y="29" width="5" height="10" rx="2.500" fill="#c7c7cd"/></svg>
      </div>
    </div>

    <div class="controls">
      <button class="btn btn-on" id="btn-on" type="button">ON</button>
      <button class="btn btn-off" id="btn-off" type="button">
        <svg viewBox="0 0 16 16" fill="currentColor" aria-hidden="true"><path d="M8 1a3.500 3.500 0 00-3.500 3.500V6H4a1.500 1.500 0 00-1.500 1.500v6A1.500 1.500 0 004 15h8a1.500 1.500 0 001.500-1.500v-6A1.500 1.500 0 0012 6h-.5V4.500A3.500 3.500 0 008 1zm2 5H6V4.500a2 2 0 114 0z"/></svg>
        OFF
      </button>
    </div>

    <section class="sheet" id="sheet" aria-label="Flashlight Pro upgrade" aria-hidden="true">
      <button class="close" id="btn-close" type="button" aria-label="Close"><svg viewBox="0 0 12 12" stroke="currentColor" stroke-width="2" stroke-linecap="round" fill="none"><path d="M1.500 1.500l9 9M10.500 1.500l-9 9"/></svg></button>
      <div class="pro"><svg viewBox="0 0 16 16" fill="currentColor" aria-hidden="true"><path d="M8 1a3.500 3.500 0 00-3.500 3.500V6H4a1.500 1.500 0 00-1.500 1.500v6A1.500 1.500 0 004 15h8a1.500 1.500 0 001.500-1.500v-6A1.500 1.500 0 0012 6h-.5V4.500A3.500 3.500 0 008 1zm2 5H6V4.500a2 2 0 114 0z"/></svg>Flashlight Pro™</div>
      <p class="price">$499</p>
      <p class="kicker">ONE-TIME PAYMENT TO TURN IT OFF</p>
      <p class="sub">Turning it on was free.<br>Turning it off is a premium experience.</p>
      <ul class="perks">
        <li><svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><path d="M10 2v8M5.500 5.200a7 7 0 109 0"/></svg>Unlock the legendary OFF button</li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.200" stroke-linecap="round" aria-hidden="true"><path d="M12 12c-2-3-3.500-4.500-5.500-4.500a4.500 4.500 0 000 9C8.500 16.500 10 15 12 12zm0 0c2 3 3.500 4.500 5.500 4.500a4.500 4.500 0 000-9C15.500 7.500 14 9 12 12z"/></svg>Unlimited off presses, forever</li>
        <li><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><rect x="1.500" y="7" width="18" height="10" rx="2.500"/><rect x="21" y="10" width="2" height="4" rx="1"/></svg>Save your battery (eventually)</li>
        <li><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M20 14.500A8.500 8.500 0 119.500 4a7 7 0 0010.500 10.500z"/></svg>Priority access to darkness</li>
      </ul>
      <button class="cta" id="btn-unlock" type="button">Unlock OFF — $499.00</button>
      <button class="restore" id="btn-restore" type="button">Restore Purchases</button>
      <p class="fine">Demo app. No payment is taken.</p>
    </section>

    <div class="toast" id="toast" role="status" aria-live="polite"></div>
  </div>
</main>

<div class="rail" aria-hidden="true">
  <span class="chip"><svg viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.500"><rect x="2" y="4" width="12" height="9" rx="2"/><circle cx="8" cy="8.500" r="2"/></svg>Screenshot</span>
  <span class="chip"><svg viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.500"><rect x="1.500" y="4" width="9" height="8" rx="2"/><path d="M10.500 7l4-2v6l-4-2"/></svg>Record</span>
</div>
<p class="hint">Bấm ON, rồi thử bấm OFF.</p>

<script>
(function () {
  var screen = document.getElementById('screen');
  var sheet = document.getElementById('sheet');
  var label = document.getElementById('state-label');
  var toast = document.getElementById('toast');
  var cta = document.getElementById('btn-unlock');
  var state = { power: 'off', paywall: false };
  var toastTimer = null;

  function render() {
    screen.dataset.power = state.power;
    screen.dataset.paywall = String(state.paywall);
    label.textContent = state.power === 'on' ? 'On' : 'Off';
    sheet.setAttribute('aria-hidden', state.paywall ? 'false' : 'true');
    sheet.inert = !state.paywall;
  }
  function say(msg) {
    toast.textContent = msg;
    toast.classList.add('show');
    clearTimeout(toastTimer);
    toastTimer = setTimeout(function () { toast.classList.remove('show'); }, 2200);
  }

  // Turning it on is free.
  document.getElementById('btn-on').addEventListener('click', function () {
    state.power = 'on'; state.paywall = false; render();
  });
  // Turning it off opens the paywall. The light never goes out.
  document.getElementById('btn-off').addEventListener('click', function () {
    if (state.power === 'on') { state.paywall = true; render(); }
    else say('Already off. For now.');
  });
  document.getElementById('btn-close').addEventListener('click', function () {
    state.paywall = false; render();
  });
  cta.addEventListener('click', function () {
    cta.classList.remove('nudge'); void cta.offsetWidth; cta.classList.add('nudge');
    say('Demo only. The light stays on.');
  });
  document.getElementById('btn-restore').addEventListener('click', function () {
    say('No purchases to restore.');
  });
  document.addEventListener('keydown', function (e) {
    if (e.key === 'Escape' && state.paywall) { state.paywall = false; render(); }
  });
  render();
})();
</script>

</body></html>
