<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Valentine</title>
<style>
  body {
    margin:0;
    height:100vh;
    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
    font-family:sans-serif;
    background: linear-gradient(pink,#ffe6e6);
    overflow:hidden;
    text-align:center;
  }
  button {
    padding:12px 30px;
    margin:10px;
    font-size:1.2em;
    border:none;
    border-radius:30px;
    cursor:pointer;
  }
  #yesBtn { background:#ff4d6d; color:white; }
  #no { background:gray; color:white; position:absolute; }
  canvas { position:fixed; top:0; left:0; width:100vw; height:100vh; pointer-events:none; }
</style>
</head>
<body>
<h1 style="color:#c00;font-size:3em">Salma, Will you be my Valentine? &lt;3</h1>
<button id="yesBtn">YES</button>
<button id="no">NO</button>
<canvas id="canvas"></canvas>

<script>
const y=document.getElementById('yesBtn'),
      n=document.getElementById('no'),
      cv=document.getElementById('canvas'),
      ctx=cv.getContext('2d');

cv.width=innerWidth;
cv.height=innerHeight;

onresize=()=>{ cv.width=innerWidth; cv.height=innerHeight; }

n.onmouseover=()=>{ n.style.left=Math.random()*80+'vw'; n.style.top=Math.random()*80+'vh'; }

r=(a,b)=>Math.random()*(b-a)+a;

function firework(x,y){
  let p=[];
  for(let i=0;i<30;i++) p.push({x,y,vx:r(-5,5),vy:r(-5,5),a:1});
  let t=setInterval(()=>{
    ctx.clearRect(0,0,cv.width,cv.height);
    p.forEach(e=>{
      ctx.fillStyle='rgba(255,'+Math.floor(r(100,255))+',0,'+e.a+')';
      ctx.beginPath();
      ctx.arc(e.x,e.y,3,0,2*Math.PI);
      ctx.fill();
      e.x+=e.vx;
      e.y+=e.vy;
      e.a-=0.02;
    });
    p=p.filter(e=>e.a>0);
    if(!p.length) clearInterval(t);
  },30);
}

y.onclick=()=>{
  alert('Yay!!! <3 <3 <3');
  firework(innerWidth/2,innerHeight/2);
};
</script>
</body>
</html>
