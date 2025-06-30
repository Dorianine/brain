---
hide:
#   - navigation # 显示右
#   - toc #显示左
  - footer
  - feedback
comments: false
---
# Welcome to Dorianine's home!
<center><font  color= #757575 size=6 class="ml3">“因为小狗在摇尾巴”</font></center>
<script src="https://cdn.statically.io/libs/animejs/2.0.2/anime.min.js"></script>
<div id="rcorners2">
  <div id="rcorners1">
    <body>
      <font color="#4351AF">
        <p class="p1"></p>
        <script defer>
          function format(newDate) {
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
          var timerId = setInterval(function () {
            var newDate = new Date();
            var p1 = document.querySelector(".p1");
            if (p1) {
              p1.textContent = format(newDate);
            }
          }, 1000);
        </script>
      </font>
    </body>
  </div>
</div>

-   :octicons-bookmark-16:{ .lg .middle } __推荐的文章__

    ---

    - [C语言](Tutorial/C.md)
</div>
    



