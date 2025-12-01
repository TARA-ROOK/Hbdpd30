<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8" />
<title>Happy 30th Birthday</title>
<style>
body{
  margin:0;
  font-family:'Prompt',sans-serif;
  background:linear-gradient(135deg,#ff7eb3,#ff758c);
  text-align:center;
  color:white;
  overflow:hidden;
}
#start-screen{
  position:fixed;top:0;left:0;width:100%;height:100%;
  background:linear-gradient(135deg,#ff9a9e,#fad0c4);
  display:flex;flex-direction:column;justify-content:center;align-items:center;
  animation:fadeIn 1.5s;
}
.start-btn{
  padding:20px 40px;font-size:1.8rem;border:none;border-radius:40px;
  background:white;color:#ff6f91;cursor:pointer;
  box-shadow:0 5px 20px rgba(0,0,0,0.25);transition:0.3s;
}
.start-btn:hover{transform:scale(1.1);} 
#main-content{display:none;}

h1{font-size:3rem;margin-top:40px;animation:fadeDown 1.5s;}
.sub{font-size:1.5rem;margin-bottom:20px;opacity:0;animation:fadeIn 2s forwards 1s;}
.gif-box img{
  width:320px;border-radius:20px;box-shadow:0 0 20px rgba(255,255,255,0.7);
  animation:float 3s infinite ease-in-out;margin-top:20px;
}
.marquee{width:100%;white-space:nowrap;overflow:hidden;margin-top:20px;}
.marquee span{display:inline-block;padding-left:100%;font-size:1.6rem;animation:marquee 12s linear infinite;color:#fff7b2;text-shadow:0 0 8px rgba(0,0,0,0.4);} 
@keyframes marquee{0%{transform:translateX(0);}100%{transform:translateX(-100%);} }
.glow{position:fixed;top:0;left:0;width:100%;height:100%;background:radial-gradient(circle,#ffffff44,#ffffff00);animation:glow 4s infinite ease-in-out;pointer-events:none;}
@keyframes glow{0%{opacity:0.2;}50%{opacity:0.7;}100%{opacity:0.2;}}
@keyframes fadeDown{from{opacity:0;transform:translateY(-40px);}to{opacity:1;transform:translateY(0);} }
@keyframes fadeIn{from{opacity:0;}to{opacity:1;}}
@keyframes float{0%{transform:translateY(0);}50%{transform:translateY(-20px);}100%{transform:translateY(0);} }
.confetti{position:fixed;top:0;left:0;width:100%;height:100%;pointer-events:none;}
</style>
</head>
<body>
<div class="glow"></div>

<div id="start-screen">
  <h1 style="margin-bottom:25px;">🎁 ของขวัญสำหรับพี่สาว</h1>
  <button class="start-btn" onclick="openGift()">เปิดของขวัญ</button>
</div>

<div id="main-content">
<canvas id="confetti" class="confetti"></canvas>
<h1>สุขสันต์วันเกิดพี่สาว 🎉 อายุครบ 30!</h1>
<div class="sub">ขอให้พี่มีความสุขมาก ๆ สวยขึ้น เก่งขึ้น และสมหวังในทุกเรื่อง ❤️</div>
<div class="marquee"><span>🎉 สุขสันต์วันเกิดนะพี่สาว! ขอให้ปีนี้เป็นปีที่ดีที่สุดของพี่ 🎂 รักที่สุด! 💖 — From น้องผู้แสนดี 😎</span></div>
<div class="gif-box"><img id="giftGif" src="" style="opacity:0;transition:1s;"></div>
</div>

<!-- เพลง -->
<audio id="bgMusic" src="music.mp3"></audio>

<script>
function openGift(){
  document.getElementById("start-screen").style.display = "none";
  document.getElementById("main-content").style.display = "block";

  // เล่นเพลง
  const music = document.getElementById("bgMusic");
  music.volume = 1.0;
  music.play().catch(err => console.log("Autoplay blocked:", err));

  const gif = document.getElementById("giftGif");
  gif.src = "https://uppic.cloud/ib/gKGFOMBH53lqiKz_1764539867.gif";
  setTimeout(()=>{gif.style.opacity=1;},200);
}

// confetti
const canvas=document.getElementById("confetti");
const ctx=canvas.getContext("2d");
canvas.width=window.innerWidth;
canvas.height=window.innerHeight;
let pieces=[];
for(let i=0;i<150;i++){
  pieces.push({
    x:Math.random()*canvas.width,
    y:Math.random()*canvas.height,
    s:5+Math.random()*5,
    v:1+Math.random()*3,
    c:`hsl(${Math.random()*360},100%,70%)`
  });
}
function update(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  for(let p of pieces){
    p.y+=p.v;
    if(p.y>canvas.height)p.y=-10;
    ctx.fillStyle=p.c;
    ctx.beginPath();ctx.arc(p.x,p.y,p.s,0,Math.PI*2);ctx.fill();
  }
  requestAnimationFrame(update);
}
update();
</script>
</body>
</html>
