# This is a heading

Replace

``import turtle

t = turtle.Turtle()
t.forward(100)``
with your own code below. You can also add text above or below but don't modify the code.


<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js" type="text/javascript"></script> 
<script src="https://cdn.jsdelivr.net/npm/skulpt@1.2.0/dist/skulpt.min.js" type="text/javascript"></script> 
<script src="https://cdn.jsdelivr.net/npm/skulpt@1.2.0/dist/skulpt-stdlib.js" type="text/javascript"></script> 

<script type="text/javascript"> 
function outf(text) { 
    var mypre = document.getElementById("output"); 
    mypre.innerHTML = mypre.innerHTML + text; 
} 
function builtinRead(x) {
    if (Sk.builtinFiles === undefined || Sk.builtinFiles["files"][x] === undefined)
            throw "File not found: '" + x + "'";
    return Sk.builtinFiles["files"][x];
}

function runit() { 
   var prog = document.getElementById("yourcode").value; 
   var mypre = document.getElementById("output"); 
   mypre.innerHTML = ''; 
   Sk.pre = "output";
   Sk.configure({output:outf, read:builtinRead}); 
   (Sk.TurtleGraphics || (Sk.TurtleGraphics = {})).target = 'mycanvas';
   var myPromise = Sk.misceval.asyncToPromise(function() {
       return Sk.importMainWithBody("<stdin>", false, prog, true);
   });
   myPromise.then(function(mod) {
       console.log('success');
   },
       function(err) {
       console.log(err.toString());
   });
} 
</script> 

<h3>Try This</h3> 
<form> 
<textarea id="yourcode" cols="40" rows="10">
import turtle

# We will need the edges of our box, so we set them
# Note that the screen is centred on zero, so the edges are at:
# -width / 2 and width / 2
# and -height / 2 and height / 2
width = 800
height = 800
floor=400
wall=400
window = turtle.Screen()
window.setup(width, height)
window.tracer(0)

ball = turtle.Turtle()
ball.penup()
ball.color("red")
ball.shape("circle")

tur = turtle.Turtle()

tleft=(-200,200)
tright=(200,200)
bleft=(-200,-200)
bright=(200,-200)
tur.penup()
tur.goto(tleft)
tur.pendown()
tur.goto(tright)
tur.goto(bright)
tur.goto(bleft)
tur.goto(tleft)
tur.hideturtle()




# Free fall acceleration -g
g = -9.81

# Timestep size
t = 0.0016

# Starting velocity
u = 0

ball.sety(200)


while True:
	v=(u+(g*t))
	s=(v*t)
	u=v	
	ball.sety(ball.ycor()+s)
	if ball.ycor()<-(floor/2):
		u=-v	
		v=(u+(g*t))
		s=(v*t)
		ball.sety(ball.ycor()+s)
	window.update()


</textarea><br /> 
<button type="button" onclick="runit()">Run</button> 
</form> 
<pre id="output" ></pre> 
<!-- If you want turtle graphics include a canvas -->
<div id="mycanvas"></div> 
