<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0, viewport-fit=cover">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black">
  <meta name="format-detection" content="telephone=no">
  <meta name="wechat-enable-text-zoom-em" content="true">
  <meta name="x5-fullscreen" content="true">
  <meta name="x5-page-mode" content="app">
  <meta name="github-pages-no-banner" content="true">
  <title>AI调酒师</title>
  <style>
    /* 隐藏GitHub Pages顶部横幅 */
    .github-pages-banner,
    header[role="banner"],
    .header {
      display: none !important;
      visibility: hidden !important;
      height: 0 !important;
      opacity: 0 !important;
      pointer-events: none !important;
    }
    
    body {
      margin: 0;
      padding: 0;
      font-family: 'Press Start 2P', 'Microsoft YaHei', 'PingFang SC', sans-serif;
      background-color: #0a0a1f;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      position: relative;
    }
    
    .floating-text {
      position: fixed;
      color: rgba(255, 255, 255, 0.9);
      font-size: 1.2rem;
      font-weight: normal;
      font-family: 'Press Start 2P', monospace;
      text-shadow: 2px 2px 0 rgba(52, 152, 219, 0.9);
      animation: float 15s steps(30) infinite;
      white-space: nowrap;
      opacity: 0;
      z-index: 10;
      letter-spacing: 1px;
      left: 0;
      pointer-events: none;
    }
    
    @keyframes float {
      0% {
        transform: translateX(-100%);
        opacity: 0;
      }
      10% {
        opacity: 1;
      }
      90% {
        opacity: 1;
      }
      100% {
        transform: translateX(100%);
        opacity: 0;
      }
    }
    
    .floating-text.line-1 {
      top: 25vh;
    }
    
    .floating-text.line-2 {
      top: 50vh;
    }
    
    .floating-text.line-3 {
      top: 75vh;
    }
    
    .mobile-container {
      width: 100%;
      min-height: 100vh;
      max-width: 390px;
      background: linear-gradient(135deg, #0f0f2d 0%, #1a1a4f 50%, #2d1a4f 100%);
      box-shadow: 0 0 30px rgba(81, 255, 246, 0.3);
      position: relative;
      z-index: 5;
      padding-bottom: 30px;
    }
    
    .app-header {
      text-align: center;
      padding: 30px 0 15px;
      margin-bottom: 10px;
      position: relative;
      z-index: 10;
    }
    
    .app-title {
      background: linear-gradient(90deg, #ff00ff 0%, #00ffff 100%);
      color: #ffffff;
      font-size: 2rem;
      font-weight: normal;
      padding: 12px 30px;
      border: 2px solid #00ffff;
      display: inline-block;
      box-shadow: 4px 4px 0 rgba(255, 0, 255, 0.5),
                  -4px -4px 0 rgba(0, 255, 255, 0.5);
      margin-bottom: 15px;
      font-family: 'Press Start 2P', monospace;
      text-transform: uppercase;
      position: relative;
      text-shadow: 2px 2px #ff00ff, -2px -2px #00ffff;
      animation: glitch 5s infinite;
    }
    
    @keyframes glitch {
      0%, 100% { transform: none; }
      20% { transform: skewX(-15deg); }
      40% { transform: skewX(15deg); }
      60% { transform: skewX(-10deg); }
      80% { transform: skewX(10deg); }
    }
    
    .app-subtitle {
      display: flex;
      justify-content: center;
      margin-top: 10px;
      flex-wrap: wrap; /* 允许换行 */
    }
    
    .subtitle-pill {
      background: linear-gradient(45deg, #ff00ff 0%, #00ffff 100%);
      color: white;
      font-size: 0.8rem;
      font-weight: normal;
      padding: 6px 12px;
      margin: 3px;
      box-shadow: 2px 2px 0 rgba(255, 0, 255, 0.4),
                  -2px -2px 0 rgba(0, 255, 255, 0.4);
      font-family: 'Press Start 2P', monospace;
      border: 1px solid #00ffff;
      text-shadow: 1px 1px #ff00ff;
    }
    
    .cocktail-image {
      width: 130px;
      height: 160px;
      margin: 20px auto 40px;
      background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%23FFFFFF"><path d="M7.5,7L5.5,5H18.5L16.5,7M11,13V19H6V21H18V19H13V13L21,5V3H3V5L11,13Z"/></svg>');
      background-size: contain;
      background-repeat: no-repeat;
      background-position: center;
      position: relative;
      image-rendering: pixelated;
    }
    
    .cocktail-glass {
      width: 100%;
      height: 100%;
      background: linear-gradient(to bottom, 
        rgba(0, 255, 255, 0.8) 0%, 
        rgba(255, 0, 255, 0.8) 50%, 
        rgba(255, 255, 0, 0.8) 100%);
      -webkit-mask-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M7.5,7L5.5,5H18.5L16.5,7M11,13V19H6V21H18V19H13V13L21,5V3H3V5L11,13Z"/></svg>');
      mask-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M7.5,7L5.5,5H18.5L16.5,7M11,13V19H6V21H18V19H13V13L21,5V3H3V5L11,13Z"/></svg>');
      -webkit-mask-size: contain;
      -webkit-mask-repeat: no-repeat;
      -webkit-mask-position: center;
      mask-size: contain;
      mask-repeat: no-repeat;
      mask-position: center;
      image-rendering: pixelated;
    }
    
    .lime-slice {
      width: 32px;
      height: 32px;
      background-color: #00ff00;
      border-radius: 50%;
      position: absolute;
      top: 13px;
      right: 33px;
      transform: rotate(-20deg);
      box-shadow: 0 0 10px rgba(0, 255, 0, 0.7);
      image-rendering: pixelated;
    }
    
    .bubbles {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 4;
      pointer-events: none;
    }
    
    .bubble {
      position: fixed;
      background-color: rgba(255, 255, 255, 0.1);
      border-radius: 0;
      animation: bubble-rise steps(20) infinite;
      border: 1px solid rgba(255, 255, 255, 0.2);
      image-rendering: pixelated;
    }
    
    @keyframes bubble-rise {
      0% {
        transform: translateY(100vh) translateX(0);
        opacity: 0;
      }
      10% {
        opacity: 0.8;
      }
      90% {
        opacity: 0.4;
      }
      100% {
        transform: translateY(-100vh) translateX(20px);
        opacity: 0;
      }
    }
    
    .input-container {
      width: 85%;
      margin: 0 auto;
      background-color: rgba(15, 15, 45, 0.9);
      padding: 10px;
      box-shadow: 4px 4px 0 rgba(255, 0, 255, 0.2),
                  -4px -4px 0 rgba(0, 255, 255, 0.2);
      border: 2px solid #00ffff;
      margin-bottom: 30px;
    }
    
    textarea {
      width: 100%;
      height: 60px;
      padding: 8px;
      border: 1px solid #00ffff;
      color: #ffffff;
      font-size: 12px;
      background: transparent;
      font-family: 'Press Start 2P', monospace;
    }
    
    textarea::placeholder {
      color: rgba(0, 255, 255, 0.5);
    }
    
    .action-button {
      background: linear-gradient(45deg, #ff00ff, #00ffff);
      color: white;
      padding: 12px 30px;
      border: 2px solid #00ffff;
      cursor: pointer;
      font-size: 16px;
      font-weight: normal;
      font-family: 'Press Start 2P', monospace;
      transition: all 0.3s ease;
      box-shadow: 4px 4px 0 rgba(255, 0, 255, 0.5);
      text-shadow: 2px 2px #ff00ff;
      display: block;
      margin: 0 auto 30px;
      width: auto;
      min-width: 200px;
    }
    
    .action-button:hover {
      transform: translate(2px, 2px);
      box-shadow: 2px 2px 0 rgba(255, 0, 255, 0.5);
    }
    
    .loading {
      display: none;
      text-align: center;
      margin: 15px 0;
      opacity: 0.8;
    }
    
    .loading-spinner {
      width: 40px;
      height: 40px;
      border: 3px solid rgba(0, 255, 255, 0.3);
      border-top: 3px solid #ff00ff;
      border-right: 3px solid #00ffff;
      border-radius: 0;
      animation: cyberspin 1s steps(8) infinite;
      margin: 10px auto;
    }
    
    @keyframes cyberspin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
    
    .loading p {
      color: #00ffff;
      font-size: 0.8rem;
      opacity: 0.8;
      text-shadow: 1px 1px #ff00ff;
    }
    
    .response-content {
      background: rgba(15, 15, 45, 0.9);
      padding: 15px;
      margin: 15px auto;
      width: 85%;
      display: flex;
      flex-direction: column;
      align-items: center;
      box-shadow: 4px 4px 0 rgba(255, 0, 255, 0.2),
                  -4px -4px 0 rgba(0, 255, 255, 0.2);
      border: 2px solid #00ffff;
    }
    
    .result-cocktail-image {
      width: 100%;
      max-width: 280px;
      border-radius: 0;
      margin: 0 auto 10px;
      box-shadow: 4px 4px 0 rgba(0, 0, 0, 0.2);
      border: 2px solid #000;
      object-fit: contain;
      image-rendering: pixelated;
      cursor: default; /* 移除点击效果 */
    }
    
    .download-button {
      background: linear-gradient(45deg, #ff00ff, #00ffff);
      color: white;
      padding: 12px 25px;
      border: 2px solid #00ffff;
      text-decoration: none;
      font-weight: normal;
      font-family: 'Press Start 2P', monospace;
      transition: all 0.2s ease;
      margin-top: 12px;
      box-shadow: 4px 4px 0 rgba(255, 0, 255, 0.5);
      font-size: 14px;
      width: 80%;
      text-align: center;
      text-shadow: 2px 2px #ff00ff;
    }
    
    .download-button:hover {
      transform: translate(2px, 2px);
      box-shadow: 2px 2px 0 rgba(255, 0, 255, 0.5);
    }
    
    @media (max-width: 390px) {
      .app-title {
        font-size: 1rem;
        padding: 6px 15px;
      }
      
      .subtitle-pill {
        font-size: 0.6rem;
        padding: 4px 8px;
      }
      
      .cocktail-image {
        width: 130px;
        height: 160px;
      }
      
      .lime-slice {
        width: 32px;
        height: 32px;
      }
      
      .mobile-container {
        min-height: 100vh;
        padding-bottom: 50px;
      }
    }
    
    @media (max-height: 844px) {
      .mobile-container {
        min-height: 100vh;
      }
    }
    
    /* 微信浏览器特定样式 */
    .wx-save-tip {
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    
    .wx-save-tip::before {
      content: "";
      display: inline-block;
      width: 16px;
      height: 16px;
      margin-right: 8px;
      background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%23FFFFFF"><path d="M12,2C6.477,2,2,6.477,2,12c0,5.523,4.477,10,10,10s10-4.477,10-10C22,6.477,17.523,2,12,2z M12,17.5c-0.828,0-1.5-0.672-1.5-1.5s0.672-1.5,1.5-1.5s1.5,0.672,1.5,1.5S12.828,17.5,12,17.5z M13,12h-2V7h2V12z"/></svg>');
      background-size: contain;
      background-repeat: no-repeat;
    }
    
    /* 修复微信浏览器中的滚动问题 */
    body.wechat {
      -webkit-overflow-scrolling: touch;
    }
    
    body.wechat .mobile-container {
      -webkit-overflow-scrolling: touch;
    }
    
    body.wechat #main-content {
      -webkit-overflow-scrolling: touch;
    }
    
    /* 修复微信中的字体显示 */
    body.wechat * {
      -webkit-text-size-adjust: 100% !important;
    }
    
    #main-content {
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 20px 0;
      position: relative;
      z-index: 10;
    }
    
    /* 添加背景动画效果 */
    .cyberpunk-bg {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(45deg, 
        rgba(255, 0, 255, 0.1) 0%, 
        rgba(0, 255, 255, 0.1) 100%);
      pointer-events: none;
      z-index: -1;
    }
    
    /* 移除所有可能影响整页滑动的overflow设置 */
    html, body {
      overflow-x: hidden;
      overflow-y: auto;
      -webkit-overflow-scrolling: touch;
    }
    
    /* 确保内容可以正常滚动 */
    .mobile-container {
      overflow: visible;
    }
    
    #main-content {
      overflow: visible;
    }
  </style>
</head>
<body>
  <div class="cyberpunk-bg"></div>
  <div class="mobile-container">
    <div class="app-header">
      <div class="app-title">AI调酒师</div>
      <div class="app-subtitle">
        <div class="subtitle-pill">私人</div>
        <div class="subtitle-pill">定制</div>
        <div class="subtitle-pill">鸡尾酒</div>
        <div class="subtitle-pill">推荐</div>
      </div>
    </div>
    
    <div class="cocktail-image">
      <div class="cocktail-glass"></div>
      <div class="lime-slice"></div>
    </div>
    
    <div id="main-content">
      <div class="input-container">
        <textarea id="input" placeholder="告诉我你的心情，或者描述你想要的鸡尾酒..."></textarea>
      </div>
      <button class="action-button" onclick="callCozeAPI()">开始调酒</button>
      
      <div class="loading" id="loading">
        <div class="loading-spinner"></div>
        <p style="color: white;">正在为您调制专属定制噢！...</p>
      </div>
      
      <div id="response"></div>
    </div>
    
    <div class="bubbles" id="bubbles"></div>
  </div>
  
  <script src="https://lf-cdn.coze.cn/obj/unpkg/flow-platform/chat-app-sdk/1.2.0-beta.10/libs/cn/index.js"></script>
  <script src="https://res.wx.qq.com/open/js/jweixin-1.6.0.js"></script>
  <script>
    // 检测是否在微信浏览器中
    function isWechat() {
      const ua = navigator.userAgent.toLowerCase();
      return ua.indexOf('micromessenger') !== -1;
    }
    
    // 微信浏览器适配
    function setupWechatCompat() {
      if (isWechat()) {
        // 添加微信浏览器特定的类名
        document.body.classList.add('wechat');
        
        // 禁用微信内置的字体缩放
        document.addEventListener('WeixinJSBridgeReady', function onBridgeReady() {
          WeixinJSBridge.invoke('setFontSizeCallback', { 'fontSize': 0 });
          WeixinJSBridge.on('menu:setfont', function() {
            WeixinJSBridge.invoke('setFontSizeCallback', { 'fontSize': 0 });
          });
        });
        
        // 修复微信浏览器中的点击延迟
        document.addEventListener('touchstart', function(){}, {passive: true});
        
        // 修复微信浏览器中的图片保存
        document.querySelectorAll('.download-button').forEach(btn => {
          btn.addEventListener('click', function(e) {
            if (isWechat()) {
              e.preventDefault();
              const imgUrl = this.getAttribute('href');
              // 显示提示，引导用户长按图片保存
              alert('请长按图片，选择"保存图片"');
              return false;
            }
          });
        });
        
        // 禁用微信右上角菜单
        if (typeof WeixinJSBridge !== 'undefined') {
          WeixinJSBridge.call('hideOptionMenu');
        }
      }
    }
    
    document.addEventListener('DOMContentLoaded', function() {
      // 检测并设置微信浏览器兼容
      setupWechatCompat();
      
      // 酒文化语录和网络热梗
      const wineQuotes = [
        "早 C 晚 A，不如早啤晚白",
        "微醺，才是生活顶配",
        "敬过往，干了这杯酒",
        "酒是生活的调味剂",
        "以酒为墨，写人生稿",
        "酒精，当代快乐开关",
        "酒杯一端，故事开讲",
        "小酌怡情，大酌也灵",
        "今夜，与酒坦诚相见",
        "用酒，敬生活的难",
        "醉翁之意，全在酒里",
        "把心事，泡进酒杯里",
        "喝酒，是灵魂的 SPA",
        "酒逢知己，千杯不腻",
        "有酒，平凡也有诗意",
        "举杯，敬这滚烫人间",
        "酒桌风云，情谊先行",
        "借酒，与自己和解",
        "美酒下肚，烦恼让路",
        "让酒，治愈疲惫日常"
      ];
      
      // 创建飘屏文字
      let currentLine = 1;
      const lineDelay = 2000; // 每行文字之间的延迟时间
      
      function createFloatingText() {
        const text = document.createElement('div');
        text.className = `floating-text line-${currentLine}`;
        text.textContent = wineQuotes[Math.floor(Math.random() * wineQuotes.length)];
        
        // 随机位置和动画时间
        const startX = Math.random() * window.innerWidth;
        text.style.left = `${startX}px`;
        text.style.animationDuration = `8s`;
        
        // 随机颜色
        const hue = Math.floor(Math.random() * 360);
        text.style.color = `hsla(${hue}, 100%, 80%, 0.9)`;
        text.style.textShadow = `0 0 10px hsla(${hue}, 100%, 60%, 0.8), 0 0 20px hsla(${hue}, 100%, 40%, 0.6)`;
        
        document.body.appendChild(text);
        
        // 3秒后开始淡出
        setTimeout(() => {
          text.style.opacity = '0';
          text.style.transition = 'opacity 1s ease-out';
        }, 3000);
        
        // 动画结束后移除元素
        setTimeout(() => {
          document.body.removeChild(text);
        }, 8000);

        // 更新行号
        currentLine = currentLine >= 3 ? 1 : currentLine + 1;
      }
      
      // 每隔一段时间创建新的飘屏文字
      setInterval(createFloatingText, lineDelay);
      
      // 初始创建几个飘屏文字，确保每行都有一个
      for (let i = 0; i < 3; i++) {
        setTimeout(createFloatingText, i * (lineDelay / 3));
      }
      
      // 创建气泡效果
      function createBubbles() {
        const bubblesContainer = document.getElementById('bubbles');
        
        for (let i = 0; i < 40; i++) {
          const bubble = document.createElement('div');
          bubble.className = 'bubble';
          
          // 随机大小和位置
          const size = 5 + Math.random() * 25;
          const left = Math.random() * 100;
          const duration = 8 + Math.random() * 12;
          const delay = Math.random() * 15;
          
          bubble.style.width = `${size}px`;
          bubble.style.height = `${size}px`;
          bubble.style.left = `${left}%`;
          bubble.style.animationDuration = `${duration}s`;
          bubble.style.animationDelay = `${delay}s`;
          
          // 随机透明度和颜色
          const opacity = 0.1 + Math.random() * 0.2;
          const hue = Math.floor(Math.random() * 360);
          bubble.style.backgroundColor = `hsla(${hue}, 100%, 70%, ${opacity})`;
          
          bubblesContainer.appendChild(bubble);
        }
      }
      
      // 创建气泡效果
      createBubbles();
    });
    
    async function callCozeAPI() {
      const input = document.getElementById('input').value;
      const loading = document.getElementById('loading');
      const response = document.getElementById('response');

      if (!input) {
          alert('请告诉我你想要什么样的鸡尾酒！');
          return;
      }

      loading.style.display = 'block';
      response.innerHTML = '';
      
      // 添加延迟提示
      const loadingText = document.querySelector('.loading p');
      setTimeout(() => {
        if (loading.style.display === 'block') {
          loadingText.innerHTML = '正在为您调制专属定制噢！<br><span style="font-size: 0.6rem; opacity: 0.6;">个性化调配需要一点时间，请稍候...</span>';
        }
      }, 3000);

      try {
          const apiResponse = await fetch('https://api.coze.cn/v1/workflow/run', {
              method: 'POST',
              headers: {
                  'Authorization': 'Bearer pat_K6QPZiAxDVh2CJHYxatf0RDzNt14VGC6886r71lO8cbK3jEN1XTtUZ8f6qkvanJF',
                  'Content-Type': 'application/json'
              },
              body: JSON.stringify({
                  parameters: {
                      input: input
                  },
                  workflow_id: "7500239957405073420"
              })
          });

          const data = await apiResponse.json();
          
          let imgUrl = null;
          try {
              let inner = data.data;
              if (typeof inner === 'string') {
                  inner = JSON.parse(inner);
              }
              if (inner && inner.data) {
                  const urlMatch = inner.data.match(/https?:\/\/[^\s"']+/);
                  if (urlMatch) {
                      imgUrl = urlMatch[0];
                  }
              }
          } catch (e) {}
          
          if (imgUrl) {
              const isWx = isWechat();
              const downloadBtnText = isWx ? '长按图片保存' : '下载图片';
              const downloadBtnClass = isWx ? 'download-button wx-save-tip' : 'download-button';
              
              document.getElementById('response').innerHTML = `
                  <div class="response-content">
                      <img src="${imgUrl}" class="result-cocktail-image" alt="AI 调酒图片" ${isWx ? 'data-long-press-save="true"' : ''}>
                      <a href="${imgUrl}" download="专属调酒.png" class="${downloadBtnClass}">${downloadBtnText}</a>
                  </div>
              `;
              
              // 在微信中重新绑定长按保存事件
              if (isWx) {
                setTimeout(() => {
                  document.querySelectorAll('.wx-save-tip').forEach(btn => {
                    btn.addEventListener('click', function(e) {
                      e.preventDefault();
                      alert('请长按图片，选择"保存图片"');
                      return false;
                    });
                  });
                }, 100);
              }
          } else {
              document.getElementById('response').innerHTML = `<div class="response-content" style="color:#00ffff;">未获取到图片链接</div>`;
          }
      } catch (error) {
          document.getElementById('response').innerHTML = `<div class="response-content" style="color:#00ffff;">错误: ${error.message}</div>`;
      } finally {
          loading.style.display = 'none';
      }
    }
  </script>
</body>
</html> 
