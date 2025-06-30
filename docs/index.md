---
hide:
  - navigation
  - toc
  - feedback
comments: false
---

<style>
  :root {
    --tesla-red: #e82127;
    --tesla-dark: #000000;
    --tesla-light: #ffffff;
  }
  
  .tesla-header {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    background-color: var(--tesla-dark);
    color: var(--tesla-light);
    padding: 2rem;
  }
  
  .tesla-clock {
    font-family: 'Roboto', sans-serif;
    font-size: 1.5rem;
    color: var(--tesla-red);
    margin-bottom: 2rem;
  }
  
  .tesla-title {
    font-size: 3.5rem;
    font-weight: bold;
    margin-bottom: 1rem;
    color: var(--tesla-red);
  }
  
  .tesla-subtitle {
    font-size: 1.5rem;
    margin-bottom: 3rem;
    color: var(--tesla-light);
  }
  
  .tesla-footer {
    position: fixed;
    bottom: 0;
    width: 100%;
    text-align: center;
    padding: 1rem;
    background-color: var(--tesla-dark);
    color: var(--tesla-light);
    border-top: 1px solid var(--tesla-red);
  }
  
  @media (max-width: 768px) {
    .tesla-title {
      font-size: 2.5rem;
    }
    .tesla-subtitle {
      font-size: 1.2rem;
    }
  }
</style>

<div class="tesla-header">
  <div class="tesla-clock">
    <script>
      function formatDate(newDate) {
        var day = newDate.getDay();
        var y = newDate.getFullYear();
        var m = newDate.getMonth() + 1 < 10 ? "0" + (newDate.getMonth() + 1) : newDate.getMonth() + 1;
        var d = newDate.getDate() < 10 ? "0" + newDate.getDate() : newDate.getDate();
        var h = newDate.getHours() < 10 ? "0" + newDate.getHours() : newDate.getHours();
        var min = newDate.getMinutes() < 10 ? "0" + newDate.getMinutes() : newDate.getMinutes();
        var s = newDate.getSeconds() < 10 ? "0" + newDate.getSeconds() : newDate.getSeconds();
        var dict = { 1: "一", 2: "二", 3: "三", 4: "四", 5: "五", 6: "六", 0: "天" };
        return y + "年" + m + "月" + d + "日" + " " + h + ":" + min + ":" + s + " 星期" + dict[day];
      }
      
      document.write('<div id="tesla-time">' + formatDate(new Date()) + '</div>');
      
      setInterval(function() {
        document.getElementById('tesla-time').textContent = formatDate(new Date());
      }, 1000);
    </script>
  </div>
  
  <h1 class="tesla-title">DORIANINE</h1>
  <p class="tesla-subtitle">“暮色垂睫 月泊眉梢”</p>
  
  <div class="grid cards" markdown>
    - __推荐的文章__
      ---
      - [C语言](Tutorial/C.md)
  </div>
</div>

<div class="tesla-footer">
  因为小狗在摇尾巴
</div>

<script src="https://cdn.statically.io/libs/animejs/2.0.2/anime.min.js"></script>
<script>
  // Animation for the title
  anime.timeline({loop: false})
    .add({
      targets: '.tesla-title',
      opacity: [0,1],
      easing: "easeInOutQuad",
      duration: 1000,
    });
</script>