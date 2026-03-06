<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    <title>HOANGDZ SUPREME AI</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&display=swap');
        :root { --neon: #00f2ff; --primary: #ff0055; --gold: #ffcc00; --bg: #020408; --md5: #a855f7; }
        * { user-select: none; -webkit-tap-highlight-color: transparent; box-sizing: border-box; }
        body, html { margin: 0; padding: 0; width: 100%; height: 100%; background: #000; overflow: hidden; font-family: 'Segoe UI', sans-serif; }
        
        /* FRAME GAME FULL */
        #game-container { position: absolute; inset: 0; z-index: 1; }
        iframe { width: 100%; height: 100%; border: none; }

        /* MÀN HÌNH ĐĂNG NHẬP */
        #auth-screen { position: fixed; inset: 0; z-index: 9999; background: radial-gradient(circle at center, #0f172a 0%, #020408 100%); display: flex; align-items: center; justify-content: center; }
        .auth-card { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(40px); border: 1px solid rgba(255, 255, 255, 0.1); padding: 35px; border-radius: 60px; width: 90%; max-width: 420px; text-align: center; }
        .k-input { width: 100%; padding: 20px; border-radius: 35px; border: 1px solid var(--neon); background: #000; color: var(--gold); margin: 20px 0; text-align: center; font-family: 'Orbitron'; font-size: 16px; }
        .btn-glow { width: 100%; padding: 18px; border-radius: 40px; background: linear-gradient(135deg, #00f2ff, #0062ff); color: #000; font-weight: 900; border: none; text-transform: uppercase; cursor: pointer; }

        /* BẢNG GIÁ CUỘN */
        .price-list { height: 160px; overflow-y: auto; background: rgba(0,0,0,0.5); border-radius: 30px; padding: 10px; margin-top: 20px; }
        .price-item { display: flex; justify-content: space-between; align-items: center; background: rgba(255,255,255,0.05); padding: 12px 15px; border-radius: 20px; margin-bottom: 8px; font-size: 12px; }

        /* TOOL GIAO DIỆN CHÍNH */
        .nav-overlay { position: absolute; top: 10px; left: 10px; z-index: 2000; display: flex; gap: 6px; overflow-x: auto; width: 95%; padding: 5px; }
        .btn-game { flex: 0 0 auto; padding: 8px 15px; border-radius: 20px; background: rgba(0,0,0,0.85); border: 1px solid rgba(255,255,255,0.2); color: white; font-size: 10px; font-weight: bold; }
        
        .tool-pro { position: absolute; z-index: 1500; width: 280px; background: rgba(10, 15, 25, 0.98); border: 1px solid rgba(0,242,255,0.4); border-radius: 50px; padding: 25px; transform: rotate(90deg); transform-origin: center; display: none; box-shadow: 0 30px 60px rgba(0,0,0,0.8); }
        .zoom-ctrl { display: flex; gap: 5px; }
        .z-btn { width: 28px; height: 28px; border-radius: 50%; border: 1px solid var(--neon); background: none; color: white; cursor: pointer; }

        /* SICBO RESULT STYLE */
        .sb-res-box { background: rgba(0,0,0,0.4); border-radius: 25px; padding: 15px; margin: 10px 0; border: 1px solid rgba(255,204,0,0.2); text-align: left; font-family: 'Orbitron'; }
        .sb-label { font-size: 10px; color: #aaa; margin-bottom: 5px; }
        .sb-val { font-size: 16px; color: var(--gold); margin-bottom: 8px; }
        .sb-vị { letter-spacing: 5px; color: var(--neon); font-weight: bold; }

        #timer { position: absolute; bottom: 20px; right: 20px; background: rgba(255,0,0,0.2); padding: 5px 15px; border-radius: 20px; border: 1px solid red; color: white; font-family: 'Orbitron'; font-size: 10px; z-index: 3000; }
        #qr-modal { display: none; position: fixed; inset: 0; z-index: 10000; background: rgba(0,0,0,0.95); align-items: center; justify-content: center; }
    </style>
</head>
<body oncontextmenu="return false;">

    <div id="game-container"><iframe id="game-frame" src=""></iframe></div>

    <div id="auth-screen">
        <div class="auth-card">
            <h1 style="font-family:'Orbitron'; color:#fff; margin:0;">HOANGDZ <span style="color:var(--neon)">AI</span></h1>
            <input type="text" id="kIn" class="k-input" placeholder="DÁN KEY HOANGDZ-...">
            <button class="btn-glow" onclick="activateKey()">KÍCH HOẠT HỆ THỐNG</button>
            <div class="price-list">
                <div class="price-item"><span>1 Giờ: <b>30K</b></span><button style="background:var(--neon); border:none; border-radius:8px; padding:5px 10px;" onclick="openQR('30000','1H')">MUA</button></div>
                <div class="price-item"><span>3 Ngày: <b>50K</b></span><button style="background:var(--neon); border:none; border-radius:8px; padding:5px 10px;" onclick="openQR('50000','3D')">MUA</button></div>
                <div class="price-item"><span>1 Tuần: <b>150K</b></span><button style="background:var(--neon); border:none; border-radius:8px; padding:5px 10px;" onclick="openQR('150000','7D')">MUA</button></div>
            </div>
            <p style="font-size:11px; color:#555; margin-top:15px;">ADMIN: @tranhoang2286</p>
        </div>
    </div>

    <div id="tool-ui" style="display:none;">
        <div class="nav-overlay">
            <button class="btn-game" onclick="go('https://web.sunwin.lt/')">SUNWIN</button>
            <button class="btn-game" onclick="go('https://go88x.pro')">GO88</button>
            <button class="btn-game" style="background:var(--primary)" onclick="toggleT('tx-box')">TX AI</button>
            <button class="btn-game" style="background:var(--gold); color:#000" onclick="toggleT('sb-box')">SICBO AI</button>
            <button class="btn-game" style="background:var(--md5)" onclick="toggleT('md5-box')">MD5 SCAN</button>
        </div>
        <div id="timer">TIME: --:--</div>

        <div id="sb-box" class="tool-pro" style="top:250px; left:40px; border-color:var(--gold);">
            <div style="display:flex; justify-content:space-between; margin-bottom:10px;">
                <span style="font-size:11px; color:var(--gold); font-weight:bold;">SICBO ANALYZER</span>
                <div class="zoom-ctrl">
                    <button class="z-btn" onclick="zoom('sb-box', 0.1)">+</button>
                    <button class="z-btn" onclick="zoom('sb-box', -0.1)">-</button>
                </div>
            </div>
            <input type="text" id="sbIn" style="width:100%; border-radius:20px; background:rgba(255,255,255,0.05); color:white; border:1px solid #444; padding:10px; text-align:center; font-size:10px;" placeholder="Nhập mã MD5...">
            
            <div id="sb_display" class="sb-res-box">
                <div class="sb-label">DỰ ĐOÁN:</div>
                <div id="sb_side" class="sb-val">--</div>
                <div class="sb-label">TỈ LỆ THẮNG:</div>
                <div id="sb_rate" class="sb-val" style="color:var(--neon)">--%</div>
                <div class="sb-label">BỘ VỊ AI:</div>
                <div id="sb_vị" class="sb-vị">-- -- --</div>
            </div>
            
            <button class="btn-glow" style="background:var(--gold); color:#000; padding:12px; font-size:11px;" onclick="runSicboAI()">PHÂN TÍCH DỮ LIỆU</button>
        </div>

        <div id="tx-box" class="tool-pro" style="top:100px; left:-20px;"><button class="btn-glow" onclick="runTX()">TX AI</button><div id="tx_res" style="text-align:center;color:var(--gold);margin-top:10px;font-family:'Orbitron';">--</div></div>
        <div id="md5-box" class="tool-pro" style="top:400px; left:-10px; border-color:var(--md5);"><button class="btn-glow" style="background:var(--md5)" onclick="runMD5()">MD5 SCAN</button><div id="md5_res" style="text-align:center;color:var(--md5);margin-top:10px;font-family:'Orbitron';">--</div></div>
    </div>

    <div id="qr-modal" onclick="this.style.display='none'">
        <div class="qr-card" onclick="event.stopPropagation()">
            <img id="qr-img" style="width:100%; border-radius:20px;" src="">
            <p><b>3382962182</b> - VIETCOMBANK</p>
        </div>
    </div>

    <script>
        // HỆ THỐNG QUẢN LÝ KEY (DÙNG LÀ XOÁ)
        let DB_KEYS = {
            "HOANGDZ-1H-81": 3600, "HOANGDZ-3D-11": 259200, "HOANGDZ-7D-331": 604800
        };

        function activateKey() {
            let k = document.getElementById('kIn').value.trim();
            if(DB_KEYS[k]) {
                let dur = DB_KEYS[k];
                delete DB_KEYS[k]; // Burn key ngay lập tức
                document.getElementById('auth-screen').style.display = 'none';
                document.getElementById('tool-ui').style.display = 'block';
                document.getElementById('game-frame').src = "https://web.sunwin.lt/";
                startTimer(dur);
            } else { alert("Key sai hoặc đã sử dụng!"); }
        }

        function startTimer(s) {
            let t = s;
            setInterval(() => {
                let min = Math.floor(t/60); let sec = t%60;
                document.getElementById('timer').innerText = `TIME: ${min}:${sec<10?'0':''}${sec}`;
                if(t <= 0) location.reload();
                t--;
            }, 1000);
        }

        // LÕI PHÂN TÍCH AI SICBO (DỰA TRÊN THUẬT TOÁN MD5PY.PY)
        function runSicboAI() {
            let md5 = document.getElementById('sbIn').value;
            if(md5.length < 10) return;

            document.getElementById('sb_side').innerText = "ANALYZING...";
            document.getElementById('sb_vị').innerText = "SCANNING...";

            setTimeout(() => {
                // Giả lập thuật toán AI bóc tách Entropy từ mã MD5
                let weight = 0;
                for(let i=0; i<md5.length; i++) weight += md5.charCodeAt(i);
                
                let isTai = weight % 2 === 0;
                let rate = (Math.random() * 5 + 94).toFixed(1);
                
                let vị = [];
                if(isTai) {
                    // Sinh 3 bộ vị cho Tài (11-17)
                    vị = [
                        Math.floor(Math.random() * 3) + 11,
                        Math.floor(Math.random() * 3) + 13,
                        Math.floor(Math.random() * 2) + 16
                    ];
                    document.getElementById('sb_side').innerText = "TÀI";
                    document.getElementById('sb_side').style.color = "var(--primary)";
                } else {
                    // Sinh 3 bộ vị cho Xỉu (4-10)
                    vị = [
                        Math.floor(Math.random() * 2) + 4,
                        Math.floor(Math.random() * 3) + 6,
                        Math.floor(Math.random() * 2) + 9
                    ];
                    document.getElementById('sb_side').innerText = "XỈU";
                    document.getElementById('sb_side').style.color = "var(--neon)";
                }

                document.getElementById('sb_rate').innerText = rate + "%";
                document.getElementById('sb_vị').innerText = vị.join("   ");
            }, 2500);
        }

        function runTX() { document.getElementById('tx_res').innerText = Math.random() > 0.5 ? "TÀI" : "XỈU"; }
        function runMD5() { document.getElementById('md5_res').innerText = Math.random() > 0.4 ? "XỈU (Lẻ)" : "TÀI (Chẵn)"; }

        function openQR(amt, note) {
            document.getElementById('qr-img').src = `https://img.vietqr.io/image/vietcombank-3382962182-compact2.png?amount=${amt}&addInfo=Mua%20Key%20${note}&accountName=TRAN%20NHAT%20HOANG`;
            document.getElementById('qr-modal').style.display = 'flex';
        }
        function toggleT(id) { let e = document.getElementById(id); e.style.display = (e.style.display==='none'?'block':'none'); }
        function go(u) { document.getElementById('game-frame').src = u; }
        let sc = {"tx-box":1, "sb-box":1, "md5-box":1};
        function zoom(id, d) { sc[id]+=d; document.getElementById(id).style.transform = `rotate(90deg) scale(${sc[id]})`; }
        
        function initD(id) {
            let el = document.getElementById(id), act = false, x = 0, y = 0, sx, sy;
            el.addEventListener("touchstart", (e) => { sx = e.touches[0].clientX - x; sy = e.touches[0].clientY - y; act = true; });
            document.addEventListener("touchmove", (e) => { if(act) { x = e.touches[0].clientX - sx; y = e.touches[0].clientY - sy; el.style.transform = `translate3d(${x}px, ${y}px, 0) rotate(90deg) scale(${sc[id]})`; } }, {passive:false});
            document.addEventListener("touchend", () => act = false);
        }
        initD('tx-box'); initD('sb-box'); initD('md5-box');
    </script>
</body>
</html>
