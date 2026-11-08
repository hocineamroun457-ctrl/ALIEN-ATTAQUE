<!doctype html>
<html lang="fr">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1"/>
  <title>Attrape l’Étoile ✨ (Mini Jeu)</title>
  <style>
    body{
      margin:0; background:#070A12; color:#EAF2FF;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      display:flex; align-items:center; justify-content:center; min-height:100vh;
    }
    .wrap{
      width:min(980px, 96vw);
      background: rgba(20, 30, 55, .55);
      border: 1px solid rgba(255,255,255,.08);
      border-radius:16px;
      padding:14px 14px 18px;
      box-shadow: 0 20px 60px rgba(0,0,0,.45);
    }
    header{
      display:flex; gap:12px; align-items:flex-start; justify-content:space-between;
      flex-wrap:wrap;
      padding:6px 4px 12px;
    }
    h1{ font-size:18px; margin:0; letter-spacing:.2px; }
    .sub{ opacity:.85; font-size:13px; margin-top:4px; }
    .hud{
      display:flex; gap:10px; align-items:center; flex-wrap:wrap;
      font-size:13px;
    }
    .pill{
      background: rgba(255,255,255,.08);
      border: 1px solid rgba(255,255,255,.10);
      padding:6px 10px; border-radius:999px;
    }
    canvas{
      width:100%;
      height:auto;
      aspect-ratio: 16 / 9;
      display:block;
      background:
        radial-gradient(1200px 700px at 50% 20%, rgba(90,120,255,.25), transparent 60%),
        linear-gradient(#0A1020, #070A12);
      border-radius:12px;
      border:1px solid rgba(255,255,255,.08);
    }
    .controls{
      display:flex; gap:10px; flex-wrap:wrap; align-items:center; justify-content:space-between;
      margin-top:12px;
      padding:0 4px;
      color:rgba(234,242,255,.92);
      font-size:13px;
    }
    button{
      cursor:pointer;
      background: rgba(110, 160, 255, .18);
      border: 1px solid rgba(110,160,255,.35);
      color:#EAF2FF;
      padding:10px 14px;
      border-radius:12px;
      font-weight:700;
    }
    button:hover{ background: rgba(110, 160, 255, .25); }
    .kbd{
      display:inline-block;
      padding:2px 8px;
      border-radius:8px;
      border:1px solid rgba(255,255,255,.18);
      background: rgba(255,255,255,.06);
      font-weight:700;
      letter-spacing:.2px;
    }
  </style>
</head>

<body>
  <div class="wrap">
    <header>
      <div>
        <h1>Attrape l’Étoile ✨</h1>
        <div class="sub">
          Bouge le vaisseau avec <span class="kbd">←</span>/<span class="kbd">→</span> (ou touche l’écran).
          Attrape les étoiles (+points), évite les bombes.
        </div>
      </div>
      <div class="hud">
        <div class="pill">Score: <b id="score">0</b></div>
        <div class="pill">Vies: <b id="lives">3</b></div>
        <div class="pill">Niveau: <b id="level">1</b></div>
      </div>
    </header>

    <canvas id="game" width="960" height="540" aria-label="Jeu Attrape l'Étoile"></canvas>

    <div class="controls">
      <div>
        <b>Astuce :</b> 4 étoiles = +1 niveau.
      </div>
      <button id="btn">Démarrer / Reprendre</button>
    </div>
  </div>

<script>
(() => {
  const canvas = document.getElementById('game');
  const ctx = canvas.getContext('2d');

  const scoreEl = document.getElementById('score');
  const livesEl = document.getElementById('lives');
  const levelEl = document.getElementById('level');
  const btn = document.getElementById('btn');

  const W = canvas.width, H = canvas.height;
  const clamp = (v, a, b) => Math.max(a, Math.min(b, v));
  const rand = (a, b) => a + Math.random() * (b - a);

  let running = false;
  let lastT = 0;

  const keys = new Set();
  window.addEventListener('keydown', (e) => {
    if (['ArrowLeft','ArrowRight',' '].includes(e.key)) e.preventDefault();
    keys.add(e.key);
    if (e.key === ' ' && !state.gameOver && !running) start();
  }, {passive:false});
  window.addEventListener('keyup', (e) => keys.delete(e.key));

  // Pointer (mobile)
  const pointer = { active:false, x: W/2 };
  canvas.addEventListener('pointerdown', (e) => {
    pointer.active = true;
    const rect = canvas.getBoundingClientRect();
    pointer.x = (e.clientX - rect.left) / rect.width * W;
    canvas.setPointerCapture(e.pointerId);
  });
  canvas.addEventListener('pointermove', (e) => {
    if (!pointer.active) return;
    const rect = canvas.getBoundingClientRect();
    pointer.x = (e.clientX - rect.left) / rect.width * W;
  });
  canvas.addEventListener('pointerup', () => pointer.active = false);

  btn.addEventListener('click', () => {
    if (state.gameOver) reset();
    start();
  });

  function reset() {
    running = false;
    lastT = 0;

    state = {
      score: 0,
      lives: 3,
      level: 1,
      starsCaught: 0,
      gameOver: false,

      ship: { x: W/2, y: H - 70, w: 70, h: 18, speed: 520 },
      items: [], // {x,y,vy,type,r}
      spawnTimer: 0,
      spawnInterval: 750
    };

    scoreEl.textContent = state.score;
    livesEl.textContent = state.lives;
    levelEl.textContent = state.level;
  }

  reset();

  function start(){
    if (state.gameOver) return;
    running = true;
    lastT = performance.now();
  }

  function spawnItem() {
    const bombChance = clamp(0.18 + (state.level-1)*0.05, 0.18, 0.55);
    const type = (Math.random() < bombChance) ? 'bomb' : 'star';

    const r = (type === 'star') ? 16 : 14;
    const x = rand(30, W - 30);
    const y = -30;
    const baseSpeed = 120 + state.level*30;
    const vy = baseSpeed + rand(0, 90);

    state.items.push({ x, y, vy, type, r });
  }

  function circleRectCollide(cx, cy, r, rx, ry, rw, rh) {
    const closestX = clamp(cx, rx, rx + rw);
    const closestY = clamp(cy, ry, ry + rh);
    const dx = cx - closestX;
    const dy = cy - closestY;
    return (dx*dx + dy*dy) <= r*r;
  }

  // Polyfill roundRect if needed
  if (!CanvasRenderingContext2D.prototype.roundRect) {
    CanvasRenderingContext2D.prototype.roundRect = function(x,y,w,h,r){
      r = Math.min(r, w/2, h/2);
      this.beginPath();
      this.moveTo(x+r,y);
      this.arcTo(x+w,y,x+w,y+h,r);
      this.arcTo(x+w,y+h,x,y+h,r);
      this.arcTo(x,y+h,x,y,r);
      this.arcTo(x,y,x+w,y,r);
      this.closePath();
      return this;
    };
  }

  function drawBgStars(t){
    const n = 60;
    for (let i=0; i<n; i++){
      const px = (i * 97) % W;
      const py = ((i * 263) % H) * 0.65 + (t*0.02*(i%3+1)) % 20;
      const a = 0.15 + (i%7)*0.03;
      ctx.fillStyle = `rgba(185, 215, 255, ${a})`;
      ctx.fillRect(px, py, 2, 2);
    }
  }

  function drawStar(x, y, r){
    ctx.save();
    ctx.translate(x, y);
    ctx.fillStyle = 'rgba(160, 210, 255, .95)';
    ctx.strokeStyle = 'rgba(255,255,255,.45)';
    ctx.lineWidth = 2;

    const spikes = 5;
    const outer = r;
    const inner = r * 0.45;

    ctx.beginPath();
    for (let i=0; i<spikes*2; i++){
      const ang = i * Math.PI / spikes;
      const rr = (i%2===0) ? outer : inner;
      ctx.lineTo(Math.cos(ang)*rr, Math.sin(ang)*rr);
    }
    ctx.closePath();
    ctx.fill();
    ctx.stroke();

    // glow
    ctx.globalAlpha = 0.25;
    ctx.beginPath();
    ctx.arc(0,0,r*2.1,0,Math.PI*2);
    ctx.fillStyle = 'rgba(120,180,255,.35)';
    ctx.fill();
    ctx.restore();
  }

  function drawBomb(x, y, r){
    ctx.save();
    ctx.translate(x, y);

    ctx.fillStyle = 'rgba(255, 90, 90, .95)';
    ctx.strokeStyle = 'rgba(255,255,255,.35)';
    ctx.lineWidth = 2;

    ctx.beginPath();
    ctx.arc(0,0,r,0,Math.PI*2);
    ctx.fill();
    ctx.stroke();

    // fuse
    ctx.strokeStyle = 'rgba(255, 200, 120, .95)';
    ctx.lineWidth = 3;
    ctx.beginPath();
    ctx.moveTo(-r*0.15, -r);
    ctx.lineTo(-r*0.15, -r*1.55);
    ctx.stroke();

    ctx.fillStyle = 'rgba(255, 200, 120, .95)';
    ctx.beginPath();
    ctx.arc(0, -r*1.7, r*0.18, 0, Math.PI*2);
    ctx.fill();

    // highlight
    ctx.globalAlpha = 0.35;
    ctx.beginPath();
    ctx.ellipse(-r*0.25, -r*0.25, r*0.35, r*0.55, -0.3, 0, Math.PI*2);
    ctx.fillStyle = 'rgba(255,255,255,.85)';
    ctx.fill();

    ctx.restore();
  }

  function drawShip(){
    const s = state.ship;
    ctx.save();
    ctx.translate(s.x, s.y);

    // glow
    ctx.globalAlpha = 0.25;
    ctx.fillStyle = 'rgba(120, 200, 255, .55)';
    ctx.beginPath();
    ctx.ellipse(0, 8, s.w*0.55, s.h*2.2, 0, 0, Math.PI*2);
    ctx.fill();

    // hull
    ctx.globalAlpha = 1;
    ctx.fillStyle = 'rgba(120, 200, 255, .95)';
    ctx.strokeStyle = 'rgba(255,255,255,.35)';
    ctx.lineWidth = 2;

    ctx.beginPath();
    ctx.roundRect(-s.w/2, -s.h/2, s.w, s.h, 9);
    ctx.fill();
    ctx.stroke();

    // cockpit
    ctx.fillStyle = 'rgba(25, 40, 80, .8)';
    ctx.beginPath();
    ctx.arc(0, -2, s.h*0.35, 0, Math.PI*2);
    ctx.fill();

    // wings
    ctx.fillStyle = 'rgba(180, 230, 255, .7)';
    ctx.beginPath();
    ctx.moveTo(-s.w/2 - 10, 0);
    ctx.quadraticCurveTo(-s.w/2 + 10, -s.h/1.8, -s.w/2 + 8, -s.h/2);
    ctx.lineTo(-s.w/2 + 14, -s.h/8);
    ctx.closePath();
    ctx.fill();

    ctx.beginPath();
    ctx.moveTo(s.w/2 + 10, 0);
    ctx.quadraticCurveTo(s.w/2 - 10, -s.h/1.8, s.w/2 - 8, -s.h/2);
    ctx.lineTo(s.w/2 - 14, -s.h/8);
    ctx.closePath();
    ctx.fill();

    ctx.restore();
  }

  function update(dt){
    const s = state.ship;

    // ship movement
    if (pointer.active){
      s.x += (pointer.x - s.x) * clamp(dt * 10, 0, 1);
    } else {
      let targetX = s.x;
      if (keys.has('ArrowLeft')) targetX = s.x - s.speed * dt;
      if (keys.has('ArrowRight')) targetX = s.x + s.speed * dt;
      s.x = targetX;
    }
    s.x = clamp(s.x, s.w/2 + 10, W - s.w/2 - 10);

    // spawn
    state.spawnTimer += dt * 1000;
    const interval = clamp(state.spawnInterval - (state.level-1)*55, 360, 900);
    while (state.spawnTimer >= interval){
      state.spawnTimer -= interval;
      spawnItem();
    }

    // items update + collisions
    for (let i = state.items.length - 1; i >= 0; i--){
      const it = state.items[i];
      it.y += it.vy * dt;

      const hit = circleRectCollide(
        it.x, it.y, it.r,
        s.x - s.w/2, s.y - s.h/2, s.w, s.h
      );

      if (hit){
        if (it.type === 'star'){
          state.score += 5;
          state.starsCaught += 1;
          if (state.starsCaught >= 4){
            state.starsCaught = 0;
            state.level += 1;
          }
        } else {
          state.lives -= 1;
          // remove a couple of nearby items for less frustration
          state.items.splice(Math.max(0, i-2), 2);
        }
        state.items.splice(i, 1);
      } else if (it.y - it.r > H + 10){
        if (it.type === 'star') state.lives -= 0.15; // small penalty
        state.items.splice(i, 1);
      }
    }

    state.lives = Math.max(0, state.lives);

    scoreEl.textContent = Math.floor(state.score);
    livesEl.textContent = Math.ceil(state.lives);
    levelEl.textContent = state.level;

    if (!state.gameOver && state.lives <= 0){
      state.gameOver = true;
      running = false;
    }
  }

  function draw(t){
    ctx.clearRect(0,0,W,H);
    drawBgStars(t);

    // items
    for (const it of state.items){
      if (it.type === 'star') drawStar(it.x, it.y, it.r);
      else drawBomb(it.x, it.y, it.r);

      // tiny trail
      ctx.save();
      ctx.globalAlpha = 0.08;
      ctx.fillStyle = it.type === 'star' ? 'rgba(160, 210, 255, 1)' : 'rgba(255, 90, 90, 1)';
      ctx.fillRect(it.x - 1, it.y - 12, 2, 24);
      ctx.restore();
    }

    // ship
    drawShip();

    // ground glow line
    ctx.save();
    ctx.globalAlpha = 0.35;
    ctx.strokeStyle = 'rgba(120, 200, 255, .6)';
    ctx.lineWidth = 3;
    ctx.beginPath();
    ctx.moveTo(0, state.ship.y + 18);
    ctx.lineTo(W, state.ship.y + 18);
    ctx.stroke();
    ctx.restore();

    // overlay
    if (state.gameOver){
      ctx.save();
      ctx.fillStyle = 'rgba(0,0,0,.45)';
      ctx.fillRect(0,0,W,H);
      ctx.fillStyle = 'rgba(255,255,255,.95)';
      ctx.textAlign = 'center';
      ctx.font = '700 44px system-ui, -apple-system, Segoe UI, Roboto, Arial';
      ctx.fillText('GAME OVER', W/2, H/2 - 20);

      ctx.font = '500 20px system-ui, -apple-system, Segoe UI, Roboto, Arial';
      ctx.fillStyle = 'rgba(234,242,255,.92)';
      ctx.fillText(`Score: ${Math.floor(state.score)} | Niveau: ${state.level}`, W/2, H/2 + 25);
      ctx.fillText('Clique sur "Démarrer / Reprendre"', W/2, H/2 + 55);
      ctx.restore();
    }
  }

  function loop(now){
    const dt = Math.min(0.033, (now - lastT) / 1000);
    lastT = now;

    if (running && !state.gameOver) update(dt);
    draw(now);

    requestAnimationFrame(loop);
  }

  requestAnimationFrame((now) => { lastT = now; draw(now); requestAnimationFrame(loop); });
})();
</script>
</body>
</html>
