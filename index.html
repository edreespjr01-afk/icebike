<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>دوچرخه سواری روی یخ - نسخه نهایی</title>
    <style>
        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        body {
            margin: 0; padding: 0;
            background-color: #0b1a2a; color: #fff;
            font-family: Tahoma, Arial, sans-serif;
            display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            height: 100vh; overflow: hidden;
            touch-action: none;
        }
        #gameContainer {
            position: relative; width: 100%; max-width: 800px;
            display: flex; flex-direction: column; align-items: center;
            height: 100%;
            justify-content: center;
        }
        canvas {
            display: block; background-color: #1a2a3a;
            width: 100%; height: auto; max-height: 70vh;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 255, 255, 0.4);
        }
        #uiLayer {
            position: absolute; top: 10px; left: 10px; right: 10px;
            display: flex; justify-content: space-between;
            pointer-events: none; font-size: 0.8rem; font-weight: bold;
        }
        .ui-box {
            background: rgba(0, 0, 0, 0.7); padding: 4px 8px;
            border-radius: 5px; border: 1px solid #00ffff;
        }
        #dangerTimer { color: #ff4d4d; }
        #crackOverlay {
            position: absolute; top: 50%; left: 50%;
            transform: translate(-50%, -50%);
            font-size: 1.5rem; color: #ff0000;
            font-weight: bold; text-shadow: 0 0 10px #000;
            display: none; pointer-events: none; text-align: center; width: 100%;
        }
        
        #mobileControls {
            display: flex; justify-content: space-between;
            width: 100%; max-width: 800px;
            margin-top: 15px; padding: 0 20px;
            position: relative; z-index: 100;
        }
        .touch-btn {
            background: rgba(255, 255, 255, 0.15);
            border: 2px solid #00ffff; color: #00ffff;
            font-size: 1.5rem; font-weight: bold;
            width: 70px; height: 70px;
            border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            user-select: none; cursor: pointer;
        }
        .touch-btn:active { background: rgba(0, 255, 255, 0.4); transform: scale(0.95); }
        #btnJump { width: 90px; height: 90px; border-color: #ffff00; color: #ffff00; }
        
        #gameOverScreen, #winScreen, #startScreen {
            position: absolute; top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(0, 0, 0, 0.95);
            display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            text-align: center; z-index: 1000; padding: 20px;
        }
        h1 { font-size: 1.3rem; color: #00ffff; margin: 10px 0; }
        p { font-size: 0.85rem; margin: 5px 0; line-height: 1.5; }
        button {
            margin-top: 15px; padding: 10px 25px;
            font-size: 1rem; background-color: #00ffff;
            color: #000; border: none; border-radius: 5px;
            font-weight: bold; cursor: pointer;
        }
        .hidden { display: none !important; }
    </style>
</head>
<body>

<div id="gameContainer">
    <canvas id="gameCanvas" width="800" height="500"></canvas>
    
    <div id="uiLayer" class="hidden">
        <div class="ui-box">مرحله: <span id="levelDisplay">1</span>/10</div>
        <div class="ui-box">زمان: <span id="timeDisplay">00:20</span></div>
        <div class="ui-box">یخ: <span id="dangerTimer">10.0</span>s</div>
    </div>
    
    <div id="crackOverlay">⚠️ یخ داره می‌شکنه! ⚠️</div>

    <div id="mobileControls" class="hidden">
        <div class="touch-btn" id="btnLeft">◀</div>
        <div style="display:flex; gap: 10px;">
            <div class="touch-btn" id="btnRight">▶</div>
            <div class="touch-btn" id="btnJump">پرش</div>
        </div>
    </div>

    <div id="startScreen">
        <h1>🚲 دوچرخه سواری روی یخ 🧊</h1>
        <p>با دکمه <b>▶</b> گاز بده و با <b>پرش</b> از روی شکاف‌ها بپر!</p>
        <p>هر مرحله فقط <b>۲۰ ثانیه</b> وقت داری!</p>
        <p>مدام در حرکت باش تا یخ زیر پات نشکنه.</p>
        <button onclick="startGame()">شروع بازی</button>
    </div>

    <div id="gameOverScreen" class="hidden">
        <h1 style="color: #ff4d4d;">بازی تموم شد!</h1>
        <p id="gameOverReason">شما افتادید!</p>
        <button onclick="resetGame()">تلاش دوباره</button>
    </div>

    <div id="winScreen" class="hidden">
        <h1 style="color: #4dff4d;">🎉 تبریک! برنده شدی! 🎉</h1>
        <p>تو با موفقیت تمام ۱۰ مرحله رو رد کردی.</p>
        <button onclick="resetGame()">بازی مجدد</button>
    </div>
</div>

<script>
    // ====== باگ‌گیری: متغیرها رو اول تعریف می‌کنیم ======
    let keys = {};
    
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');
    
    let gameState = 'start';
    let level = 1;
    let timeLeft = 20; // ⏱️ ۲۰ ثانیه برای هر مرحله
    let lastTime = 0;
    
    const GRAVITY = 0.6;
    const JUMP_FORCE = -13;
    const FRICTION = 0.95;
    const ACCELERATION = 0.5;
    
    let player = {
        x: 100, y: 300, vx: 0, vy: 0,
        width: 40, height: 35,
        onGround: false, maxSpeed: 8, speed: 0
    };
    
    let cameraX = 0;
    let platforms = [];
    let trees = [];
    let snowflakes = [];
    let particles = [];
    let standStillTimer = 10;

    // ====== تابع نمایش خطا (برای دیباگ) ======
    window.onerror = function(msg, url, line, col, error) {
        alert("خطا در کد: " + msg + "\nخط: " + line);
    };
    
    function applyDifficultyAlgorithm() {
        player.maxSpeed = 6 + (level * 0.5);
        generateLevel();
        standStillTimer = 10;
        player.x = 100;
        player.y = 300;
        player.vx = 0;
        player.vy = 0;
        cameraX = 0;
        particles = [];
    }

    function generateLevel() {
        platforms = [];
        trees = [];
        let currentX = 0;
        
        platforms.push({ x: 0, y: 400, width: 400, height: 100, type: 'flat' });
        currentX = 400;
        
        for (let i = 0; i < 15; i++) { 
            let gap = 80 + (level * 20) + Math.random() * 80;
            let platWidth = 250 - (level * 10) + Math.random() * 100;
            if (platWidth < 120) platWidth = 120;
            
            currentX += gap;
            
            let rand = Math.random();
            let type = 'flat';
            let platHeight = 100;
            
            if (level > 1 && rand > 0.7) {
                type = 'ramp';
            } else if (level > 2 && rand > 0.5 && rand <= 0.7) {
                type = 'pad';
            }
            
            platforms.push({ 
                x: currentX, 
                y: 400, 
                width: platWidth, 
                height: platHeight, 
                type: type 
            });
            
            if (Math.random() > 0.4) {
                trees.push({ x: currentX + Math.random() * platWidth, y: 400, size: 30 + Math.random() * 20 });
            }
            
            currentX += platWidth;
        }
    }

    function startGame() {
        document.getElementById('startScreen').classList.add('hidden');
        document.getElementById('uiLayer').classList.remove('hidden');
        document.getElementById('mobileControls').classList.remove('hidden');
        resetGame();
    }

    function resetGame() {
        document.getElementById('gameOverScreen').classList.add('hidden');
        document.getElementById('winScreen').classList.add('hidden');
        document.getElementById('uiLayer').classList.remove('hidden');
        document.getElementById('mobileControls').classList.remove('hidden');
        
        gameState = 'playing';
        level = 1;
        timeLeft = 20; 
        applyDifficultyAlgorithm();
        
        snowflakes = [];
        for (let i = 0; i < 60; i++) {
            snowflakes.push({ x: Math.random() * 800, y: Math.random() * 500, r: Math.random() * 3, speed: Math.random() * 2 + 1 });
        }
        
        lastTime = performance.now();
        requestAnimationFrame(gameLoop);
   (let }

    // ====== اصلاح دکمه‌های لمسی i با passive: false =======
    function setupTouchControls()0 {
        const bindTouch = (id, keyName); => {
            const el = document.getElementById(id);
            el.addEventListener('touchstart', (e) => { 
                e.preventDefault(); 
                keys[keyName] = true; 
            }, { passive: false });
            
            el.addEventListener('touchend', (e) => { 
                e.preventDefault(); 
                keys[keyName] = false; 
            }, { passive: false });
            
            // برای تست با موس در کامپیوتر
            el.addEventListener('mousedown', (e) => { e.preventDefault(); keys[keyName] = true; });
            el.addEventListener('mouseup', (e) => { e.preventDefault(); keys[keyName] = false; });
            el.addEventListener('mouseleave', (e) => { keys[keyName] = false; });
        };
        bindTouch('btnLeft', 'ArrowLeft');
        bindTouch('btnRight', 'ArrowRight');
        bindTouch('btnJump', 'ArrowUp');
    }
    
    // فراخوانی بعد از بارگذاری کامل صفحه
    window.addEventListener('load', setupTouchControls);

    window.addEventListener('keydown', (e) => {
        keys[e.code] = true;
        if(['ArrowUp', 'ArrowDown', 'ArrowLeft', 'ArrowRight', 'Space'].includes(e.code)) e.preventDefault();
    });
    window.addEventListener('keyup', (e) => { keys[e.code] = false; });

    function gameLoop(timestamp) {
        if (gameState !== 'playing') return;
        const deltaTime = (timestamp - lastTime) / 1000;
        lastTime = timestamp;
        update(deltaTime);
        draw();
        requestAnimationFrame(gameLoop);
    }

    function update(dt) {
        timeLeft -= dt;
        if (timeLeft <= 0) {
            timeLeft = 0;
            level++;
            if (level > 10) {
                gameState = 'win';
                document.getElementById('winScreen').classList.remove('hidden');
                document.getElementById('uiLayer').classList.add('hidden');
                document.getElementById('mobileControls').classList.add('hidden');
                return;
            } else {
                timeLeft = 20; 
                applyDifficultyAlgorithm();
            }
        }

        if (keys['ArrowRight']) {
            player.vx += ACCELERATION;
            if (player.vx > player.maxSpeed) player.vx = player.maxSpeed;
        } else if (keys['ArrowLeft']) {
            player.vx -= ACCELERATION * 1.5;
        } else {
            player.vx *= FRICTION;
        }

        if (keys['ArrowUp'] && player.onGround) {
            player.vy = JUMP_FORCE;
            player.onGround = false;
            for i<5; i++) particles.push({x: player.x + 20, y: player.y + 35, vx: (Math.random()-0.5)*4, vy: Math.random()*-2, life: 1, color: '#ffffff'});
        }

        player.vy += GRAVITY;
        player.x += player.vx;
        player.y += player.vy;
        
        if (player.x > cameraX + 300) cameraX = player.x - 300;

        player.onGround = false;
        for (let plat of platforms) {
            if (player.x + player.width > plat.x && player.x < plat.x + plat.width) {
                
                if (plat.type === 'flat') {
                    if (player.vy >= 0 && player.y + player.height <= plat.y + 20 && player.y + player.height + player.vy >= plat.y) {
                        player.y = plat.y - player.height;
                        player.vy = 0;
                        player.onGround = true;
                    }
                }
                else if (plat.type === 'ramp') {
                    let slopeY = plat.y + plat.height - ((player.x + player.width - plat.x) / plat.width) * plat.height;
                    if (player.vy >= 0 && player.y + player.height <= slopeY + 15 && player.y + player.height + player.vy >= slopeY) {
                        player.y = slopeY - player.height;
                        player.vy = -2;
                        player.onGround = true;
                    }
                }
                else if (plat.type === 'pad') {
                    let padCenterX = plat.x + plat.width / 2;
                    let padCenterY = plat.y;
                    let distToPad = Math.sqrt(Math.pow((player.x + 20) - padCenterX, 2) + Math.pow((player.y + 35) - padCenterY, 2));
                    
                    if (distToPad < 40 && player.vy >= 0) {
                        player.y = plat.y - player.height;
                        player.vy = -18; 
                        player.onGround = true;
                        for(let i=0; i<10; i++) particles.push({x: padCenterX, y: padCenterY, vx: (Math.random()-0.5)*6, vy: Math.random()*-5, life: 1, color: '#00ffff'});
                    }
                }
            }
        }

        if (Math.abs(player.vx) < 1 && player.onGround) {
            standStillTimer -= dt;
            document.getElementById('crackOverlay').style.display = 'block';
            if (standStillTimer <= 0) {
                endGame("یخ زیر پات شکست! باید مدام گاز بدی.");
                return;
            }
        } else {
            standStillTimer = 10;
            document.getElementById('crackOverlay').style.display = 'none';
        }

        if (player.y > 600) {
            endGame("توی شکاف یخ افتادی!");
            return;
        }

        for (let i = particles.length - 1; i >= 0; i--) {
            particles[i].x += particles[i].vx;
            particles[i].y += particles[i].vy;
            particles[i].life -= dt * 2;
            if (particles[i].life <= 0) particles.splice(i, 1);
        }

        updateUI();
    }

    function updateUI() {
        document.getElementById('levelDisplay').innerText = level;
        let minutes = Math.floor(timeLeft / 60);
        let seconds = Math.floor(timeLeft % 60);
        document.getElementById('timeDisplay').innerText = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        let dangerEl = document.getElementById('dangerTimer');
        dangerEl.innerText = Math.max(0, standStillTimer).toFixed(1);
        dangerEl.style.color = standStillTimer < 4 ? '#ff0000' : '#ff4d4d';
    }

    function drawTree(ctx, x, y, size) {
        ctx.fillStyle = '#5c4033';
        ctx.fillRect(x - 5, y - size/2, 10, size/2);
        ctx.fillStyle = '#2e8b57';
        ctx.beginPath();
        ctx.moveTo(x, y - size * 1.5);
        ctx.lineTo(x - size/2, y - size/2);
        ctx.lineTo(x + size/2, y - size/2);
        ctx.fill();
        ctx.beginPath();
        ctx.moveTo(x, y - size * 1.2);
        ctx.lineTo(x - size/1.5, y - size/3);
        ctx.lineTo(x + size/1.5, y - size/3);
        ctx.fill();
        ctx.beginPath();
        ctx.moveTo(x, y - size);
        ctx.lineTo(x - size, y - size/6);
        ctx.lineTo(x + size, y - size/6);
        ctx.fill();
        ctx.fillStyle = '#ffffff';
        ctx.beginPath();
        ctx.moveTo(x, y - size * 1.5);
        ctx.lineTo(x - size/4, y - size);
        ctx.lineTo(x + size/4, y - size);
        ctx.fill();
    }

    function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        let skyGradient = ctx.createLinearGradient(0, 0, 0, 500);
        skyGradient.addColorStop(0, '#0f1a2a');
        skyGradient.addColorStop(1, '#2a4a6a');
        ctx.fillStyle = skyGradient;
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        ctx.fillStyle = '#1a3a5a';
        ctx.beginPath();
        ctx.moveTo(0 - cameraX * 0.1, 400);
        ctx.lineTo(200 - cameraX * 0.1, 100);
        ctx.lineTo(400 - cameraX * 0.1, 400);
        ctx.fill();
        ctx.beginPath();
        ctx.moveTo(300 - cameraX * 0.15, 400);
        ctx.lineTo(550 - cameraX * 0.15, 80);
        ctx.lineTo(800 - cameraX * 0.15, 400);
        ctx.fill();
        
        ctx.fillStyle = '#ffffff';
        ctx.beginPath();
        ctx.moveTo(200 - cameraX * 0.1, 100);
        ctx.lineTo(170 - cameraX * 0.1, 150);
        ctx.lineTo(230 - cameraX * 0.1, 150);
        ctx.fill();

        ctx.fillStyle = 'rgba(255, 255, 255, 0.7)';
        for (let sf of snowflakes) {
            ctx.beginPath();
            ctx.arc(sf.x - (cameraX * 0.3) % 800, sf.y, sf.r, 0, Math.PI * 2);
            ctx.fill();
            sf.y += sf.speed;
            if (sf.y > 500) sf.y = -10;
        }

        ctx.save();
        ctx.translate(-cameraX, 0);

        for (let tree of trees) {
            drawTree(ctx, tree.x, tree.y, tree.size);
        }

        for (let plat of platforms) {
            if (plat.type === 'flat') {
                let iceGradient = ctx.createLinearGradient(plat.x, plat.y, plat.x, plat.y + plat.height);
                iceGradient.addColorStop(0, '#a0e6ff');
                iceGradient.addColorStop(1, '#4a90e2');
                ctx.fillStyle = iceGradient;
                ctx.fillRect(plat.x, plat.y, plat.width, plat.height);
                ctx.fillStyle = '#ffffff';
                ctx.fillRect(plat.x, plat.y, plat.width, 8);
                ctx.strokeStyle = 'rgba(255, 255, 255, 0.3)';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.moveTo(plat.x + 30, plat.y + 20);
                ctx.lineTo(plat.x + 60, plat.y + 60);
                ctx.moveTo(plat.x + plat.width - 40, plat.y + 30);
                ctx.lineTo(plat.x + plat.width - 80, plat.y + 80);
                ctx.stroke();
            } else if (plat.type === 'ramp') {
                ctx.beginPath();
                ctx.moveTo(plat.x, plat.y + plat.height);
                ctx.lineTo(plat.x + plat.width, plat.y);
                ctx.lineTo(plat.x + plat.width, plat.y + plat.height);
                ctx.closePath();
                let rampGradient = ctx.createLinearGradient(plat.x, plat.y, plat.x + plat.width, plat.y + plat.height);
                rampGradient.addColorStop(0, '#4a90e2');
                rampGradient.addColorStop(1, '#a0e6ff');
                ctx.fillStyle = rampGradient;
                ctx.fill();
                ctx.beginPath();
                ctx.moveTo(plat.x, plat.y + plat.height);
                ctx.lineTo(plat.x + plat.width, plat.y);
                ctx.strokeStyle = '#ffffff';
                ctx.lineWidth = 4;
                ctx.stroke();
            } else if (plat.type === 'pad') {
                ctx.fillStyle = '#a0e6ff';
                ctx.fillRect(plat.x, plat.y + 20, plat.width, plat.height - 20);
                ctx.beginPath();
                ctx.arc(plat.x + plat.width / 2, plat.y + 20, 30, Math.PI, 0);
                ctx.fillStyle = '#00ffff';
                ctx.fill();
                ctx.strokeStyle = '#ffffff';
                ctx.lineWidth = 3;
                ctx.stroke();
                ctx.beginPath();
                ctx.arc(plat.x + plat.width / 2, plat.y + 20, 40, Math.PI, 0);
                ctx.strokeStyle = 'rgba(0, 255, 255, 0.3)';
                ctx.lineWidth = 5;
                ctx.stroke();
            }
        }

        ctx.save();
        ctx.translate(player.x + 20, player.y + 17);
        
        ctx.beginPath();
        ctx.arc(-10, 18, 10, 0, Math.PI * 2);
        ctx.fillStyle = '#222'; ctx.fill();
        ctx.strokeStyle = '#ccc'; ctx.lineWidth = 2; ctx.stroke();
        for(let i=0; i<4; i++) {
            ctx.beginPath(); ctx.moveTo(-10, 18); 
            let angle = (Date.now() / 100) + (i * Math.PI/2);
            ctx.lineTo(-10 + Math.cos(angle)*8, 18 + Math.sin(angle)*8);
            ctx.strokeStyle = '#666'; ctx.lineWidth = 1; ctx.stroke();
        }

        ctx.beginPath();
        ctx.arc(15, 18, 10, 0, Math.PI * 2);
        ctx.fillStyle = '#222'; ctx.fill();
        ctx.strokeStyle = '#ccc'; ctx.lineWidth = 2; ctx.stroke();
        for(let i=0; i<4; i++) {
            ctx.beginPath(); ctx.moveTo(15, 18); 
            let angle = (Date.now() / 100) + (i * Math.PI/2);
            ctx.lineTo(15 + Math.cos(angle)*8, 18 + Math.sin(angle)*8);
            ctx.strokeStyle = '#666'; ctx.lineWidth = 1; ctx.stroke();
        }

        ctx.beginPath();
        ctx.moveTo(-10, 18);
        ctx.lineTo(0, 5);
        ctx.lineTo(15, 18);
        ctx.lineTo(0, 5);
        ctx.lineTo(5, -5);
        ctx.strokeStyle = '#00ffff';
        ctx.lineWidth = 3;
        ctx.stroke();

        ctx.fillStyle = '#ff4500';
        ctx.beginPath();
        ctx.ellipse(5, -8, 8, 12, 0.2, 0, Math.PI * 2);
        ctx.fill();
        
        ctx.beginPath();
        ctx.arc(8, -22, 7, 0, Math.PI * 2);
        ctx.fillStyle = '#ffcc00';
        ctx.fill();
        ctx.beginPath();
        ctx.arc(8, -25, 8, Math.PI, 0);
        ctx.fillStyle = '#ffffff';
        ctx.fill();

        ctx.beginPath();
        ctx.moveTo(0, -15);
        ctx.quadraticCurveTo(-15, -15 + Math.sin(Date.now()/100)*5, -25, -10 + Math.sin(Date.now()/100)*8);
        ctx.strokeStyle = '#ff0000';
        ctx.lineWidth = 4;
        ctx.stroke();

        ctx.restore();

        for (let p of particles) {
            ctx.globalAlpha = p.life;
            ctx.fillStyle = p.color;
            ctx.beginPath();
            ctx.arc(p.x, p.y, 3, 0, Math.PI * 2);
            ctx.fill();
        }
        ctx.globalAlpha = 1.0;

        if (standStillTimer < 10 && player.onGround) {
            ctx.strokeStyle = 'rgba(255, 0, 0, ' + (1 - standStillTimer/10) + ')';
            ctx.lineWidth = 3;
            for (let i = 0; i < 5; i++) {
                ctx.beginPath();
                ctx.moveTo(player.x + 20, player.y + 35);
                ctx.lineTo(player.x + 20 + (Math.random() * 40 - 20), player.y + 35 + Math.random() * 20);
                ctx.stroke();
            }
        }

        ctx.restore();
    }

    function endGame(reason) {
        gameState = 'gameover';
        document.getElementById('gameOverReason').innerText = reason;
        document.getElementById('gameOverScreen').classList.remove('hidden');
        document.getElementById('uiLayer').classList.add('hidden');
        document.getElementById('mobileControls').classList.add('hidden');
        document.getElementById('crackOverlay').style.display = 'none';
    }
</script>
</body>
</html>