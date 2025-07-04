<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ashish Mac OS</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    html, body { height: 100%; font-family: sans-serif; overflow: hidden; }
    #bootScreen, #loginScreen, #desktop { position: absolute; width: 100%; height: 100%; }
    #bootScreen {
      background: black;
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      font-size: 1.5em;
      z-index: 999;
    }
    .loader {
      margin-top: 20px;
      width: 40px;
      height: 40px;
      border: 5px solid white;
      border-top: 5px solid transparent;
      border-radius: 50%;
      animation: spin 1s linear infinite;
    }
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
    #loginScreen {
      background: linear-gradient(to top right, #222, #555);
      display: none;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      color: white;
    }
    #loginScreen input {
      padding: 10px;
      margin: 10px;
      border-radius: 5px;
      border: none;
    }
    #desktop {
      display: none;
      background-image: url('https://wallpapercave.com/wp/wp2757874.jpg');
      background-size: cover;
    }
    .icon {
      position: absolute;
      color: white;
      text-align: center;
      cursor: pointer;
      width: 80px;
    }
    .icon img { width: 64px; height: 64px; }
    .window {
      position: absolute;
      top: 120px;
      left: 120px;
      width: 600px;
      height: 400px;
      background: white;
      border: 1px solid #ccc;
      box-shadow: 0 0 10px rgba(0,0,0,0.5);
      display: flex;
      flex-direction: column;
      z-index: 100;
      resize: both;
      overflow: auto;
    }
    .window-header {
      background: #333;
      color: white;
      padding: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      cursor: move;
    }
    .window-body { flex: 1; padding: 0; overflow: auto; }
    .taskbar {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      height: 40px;
      background: rgba(0,0,0,0.7);
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0 10px;
      color: white;
    }
    .start-btn { cursor: pointer; font-weight: bold; }
    .clock { font-size: 14px; }
    .start-menu {
      position: absolute;
      bottom: 40px;
      left: 10px;
      background: #222;
      color: white;
      padding: 10px;
      display: none;
      flex-direction: column;
      width: 200px;
      border: 1px solid #444;
    }
    .start-menu button {
      background: transparent;
      color: white;
      border: none;
      text-align: left;
      padding: 5px;
      cursor: pointer;
    }
    .start-menu button:hover {
      background: #444;
    }
  </style>
</head>
<body>
  <div id="bootScreen">
    <div>Ashish Mac OS Booting...</div>
    <div class="loader"></div>
  </div>
  <div id="loginScreen">
    <h1>Welcome, Ashish</h1>
    <input type="password" placeholder="Enter Password" id="password">
    <button onclick="login()">Login</button>
  </div>
  <div id="desktop">
    <!-- Icons -->
    <div class="icon" onclick="openApp('vscode')" style="top:40px;left:40px">
      <img src="https://upload.wikimedia.org/wikipedia/commons/9/9a/Visual_Studio_Code_1.35_icon.svg"><div>VS Code</div>
    </div>
    <div class="icon" onclick="openApp('notepad')" style="top:40px;left:140px">
      <img src="https://icons.iconarchive.com/icons/custom-icon-design/mono-general-4/512/notepad-icon.png"><div>Notepad</div>
    </div>
    <div class="icon" onclick="openApp('calculator')" style="top:40px;left:240px">
      <img src="https://icons.iconarchive.com/icons/paomedia/small-n-flat/1024/calculator-icon.png"><div>Calculator</div>
    </div>
    <div class="icon" onclick="openApp('paint')" style="top:140px;left:40px">
      <img src="https://icons.iconarchive.com/icons/microsoft/fluentui-emoji-flat/512/Paintbrush-Flat.png"><div>Paint</div>
    </div>
    <div class="icon" onclick="openApp('terminal')" style="top:140px;left:140px">
      <img src="https://icons.iconarchive.com/icons/papirus-team/papirus-apps/512/terminal-icon.png"><div>Terminal</div>
    </div>
    <div class="icon" onclick="openApp('media')" style="top:140px;left:240px">
      <img src="https://icons.iconarchive.com/icons/dakirby309/windows-8-metro/256/Apps-Windows-Media-Player-Metro-icon.png"><div>Media</div>
    </div>
    <div class="icon" onclick="openApp('browser')" style="top:240px;left:40px">
      <img src="https://icons.iconarchive.com/icons/google/chrome/512/Google-Chrome-icon.png"><div>Browser</div>
    </div><!-- Start Menu -->
<div class="start-menu" id="startMenu">
  <button onclick="openApp('notepad')">📝 Notepad</button>
  <button onclick="openApp('calculator')">🧮 Calculator</button>
  <button onclick="openApp('vscode')">🧑‍💻 VS Code</button>
  <button onclick="openApp('paint')">🎨 Paint</button>
  <button onclick="openApp('media')">🎬 Media Player</button>
  <button onclick="openApp('terminal')">💻 Terminal</button>
  <button onclick="openApp('browser')">🌐 Browser</button>
</div>

<!-- Taskbar -->
<div class="taskbar">
  <div class="start-btn" onclick="toggleStartMenu()">Start</div>
  <div class="clock" id="clock"></div>
</div>

  </div>  <script>
    setTimeout(() => {
      document.getElementById('bootScreen').style.display = 'none';
      document.getElementById('loginScreen').style.display = 'flex';
    }, 2500);

    function login() {
      const pw = document.getElementById('password').value;
      if (pw === "1234") {
        document.getElementById('loginScreen').style.display = 'none';
        document.getElementById('desktop').style.display = 'block';
        updateClock();
        setInterval(updateClock, 1000);
      } else {
        alert("Incorrect password");
      }
    }

    function updateClock() {
      const clock = document.getElementById('clock');
      const now = new Date();
      clock.textContent = now.toLocaleTimeString();
    }

    function toggleStartMenu() {
      const menu = document.getElementById('startMenu');
      menu.style.display = menu.style.display === 'flex' ? 'none' : 'flex';
    }

    function openApp(app) {
      const win = document.createElement('div');
      win.classList.add('window');
      let content = '';
      if (app === 'vscode') {
        content = `<iframe src='https://vscode.dev' style='width:100%;height:100%;border:none;'></iframe>`;
      } else if (app === 'notepad') {
        content = `<textarea style='width:100%;height:100%;border:none;padding:10px;font-size:16px;'></textarea>`;} else if (app === 'calculator') {
    content = `<iframe src='https://www.online-calculator.com/full-screen-calculator/' style='width:100%;height:100%;border:none;'></iframe>`;
  } else if (app === 'media') {
    content = `<video controls autoplay style='width:100%;height:100%;'><source src='https://www.w3schools.com/html/mov_bbb.mp4' type='video/mp4'></video>`;
  } else if (app === 'browser') {
    window.open('https://www.google.com', '_blank'); return;
  } else if (app === 'terminal') {
    content = `<div style='padding:10px;font-family:monospace;color:green;background:black;height:100%;overflow:auto;'>
      <div>> help</div>
      <div>Available commands: help, dir, echo [text]</div>
      <input onkeydown="if(event.key==='Enter'){this.insertAdjacentHTML('beforebegin','> '+this.value+'<br>');this.value=''}" style='width:100%;color:white;background:black;border:none;'>
    </div>`;
  } else if (app === 'paint') {
    content = `<canvas id='paintCanvas' width='600' height='350' style='border:1px solid #ccc;'></canvas>
    <script>
      const c = document.getElementById('paintCanvas');
      const ctx = c.getContext('2d');
      let painting = false;
      c.onmousedown = () => painting = true;
      c.onmouseup = () => painting = false;
      c.onmousemove = e => {
        if (!painting) return;
        ctx.fillStyle = 'black';
        ctx.fillRect(e.offsetX, e.offsetY, 2, 2);
      };
    </script>`;
  }

  win.innerHTML = `
    <div class="window-header">
      <span>${app.toUpperCase()}</span>
      <button onclick="this.closest('.window').remove()">X</button>
    </div>
    <div class="window-body">${content}</div>
  `;
  document.getElementById('desktop').appendChild(win);
}

  </script>
</body>
</html>
