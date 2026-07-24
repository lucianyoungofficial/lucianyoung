---
title: "Terminal Simulator"
date: 2026-07-23
summary: "A minimal terminal typing effect in the browser."
draft: false
---

<style>
.terminal {
  background: #1a1a2e;
  border-radius: 8px;
  padding: 20px 24px;
  font-family: "Courier New", Consolas, monospace;
  font-size: 14px;
  line-height: 1.7;
  color: #00ff88;
  max-width: 640px;
  margin: 0 auto;
  box-shadow: 0 4px 24px rgba(0,0,0,0.3);
  min-height: 200px;
}
.terminal .line {
  white-space: pre-wrap;
  word-break: break-all;
}
.terminal .cursor::after {
  content: "█";
  animation: blink 1s step-end infinite;
}
@keyframes blink {
  50% { opacity: 0; }
}
.terminal .dim { color: #555; }
.terminal .prompt { color: #00ccff; }
.terminal .output { color: #aaa; }
.terminal button {
  margin-top: 16px;
  background: #00ff88;
  color: #1a1a2e;
  border: none;
  padding: 6px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-family: inherit;
  font-size: 13px;
}
.terminal button:hover { opacity: 0.85; }
</style>

<div class="terminal" id="term">
  <div class="line dim">[lucianyoung@lab ~]$ <span id="cmd"></span><span class="cursor"></span></div>
  <div id="output"></div>
</div>

<script>
(function() {
  var cmds = [
    { cmd: "whoami", out: "lucianyoung — vehicle engineering student, builder of things" },
    { cmd: "uname -a", out: "Linux lab 6.6.0 #1 SMP x86_64 GNU/Linux" },
    { cmd: "ls projects/", out: "network-infra-lab/  personal-website/" },
    { cmd: "cat ~/.principles", out: "Documentation First\nEngineering Thinking\nBuild Before Polish\nLow Maintenance" },
    { cmd: "uptime", out: "up 24 years, learning since day one" }
  ];
  var i = 0;
  var el = document.getElementById("cmd");
  var out = document.getElementById("output");

  function type(text, cb) {
    var j = 0;
    el.textContent = "";
    var t = setInterval(function() {
      el.textContent += text[j]; j++;
      if (j >= text.length) { clearInterval(t); setTimeout(cb, 400); }
    }, 60);
  }

  function runNext() {
    if (i >= cmds.length) {
      el.textContent = "";
      out.innerHTML += '<div class="line dim">— end of demo —</div>';
      return;
    }
    var c = cmds[i];
    type(c.cmd, function() {
      out.innerHTML += '<div class="line"><span class="prompt">$ ' + c.cmd + '</span></div>';
      out.innerHTML += '<div class="line output">' + c.out.replace(/\n/g, '<br>') + '</div>';
      el.textContent = "";
      i++;
      setTimeout(runNext, 600);
    });
  }

  runNext();
})();
</script>
</br>

Type each command and see the simulated output — a tiny terminal in the browser. Refresh to replay.
