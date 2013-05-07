Game01
======
level 1:-
---------
<!DOCTYPE HTML>
<html>
<head>
  <title>yomna&riham</title>
	<style>
		body {
			margin: 0;
			padding: 0;
			background-color: #000000;

		}

		.textHolder{
			width: 300px;
		}
	</style>

	<script src="pixi.js"></script>
</head>
<body>
<audio src="clip.wav" autoplay="autoplay" repeat='all'  id='clip' >
 <canvas id="myCanvas" height="2048" width="600">
 <button id="as" type="button" onmouseover='startMove()' onmouseout='stopMove()'>Left</button></body>

 </canvas>


	<script>
	
	//BackgroundCreation
	// create an new instance of a pixi stage
	var stage = new PIXI.Stage(0x97c56e, true);
	
	//Global variables
	var innerWidth=500;
	var innerHeight=900;
	var count_background = 0;
	var down=0;
	var counter = 0;
	var i = 0;
	var bullets=[];//array of bullets
	var jeet=[];//array of jeets1
	var jeet2=[];//array of jeet2
	var jeet3=[];//array of jeet3
	var enemy01=[];//array of enemy

	// create a renderer instance
	var renderer = PIXI.autoDetectRenderer(window.innerWidth, window.innerHeight, null);

	// add the renderer view element to the DOM
	document.body.appendChild(renderer.view);
	renderer.view.style.position = "absolute";
	renderer.view.style.top = "0px";
	
	//calling animation function
	requestAnimFrame( animate );


	// create a Background texture 
	var texture = PIXI.Texture.fromImage("background.jpg");
	// create a plane texture 
	var plan = PIXI.Texture.fromImage("plan.png");
	//create a gun texture
	var gun = PIXI.Texture.fromImage("gun.png");
	//create enemy texture
	var texture1 = PIXI.Texture.fromImage("enemy.png");
	//create 2nd kind of enemy
	var enemy = PIXI.Texture.fromImage("enemy2.png");

	var Background = new PIXI.TilingSprite(texture, window.innerWidth, window.innerHeight)

	stage.addChild(Background);
	
	//function to create plane
	createPlane(Math.random() * 500, Math.random() *900);
	
	//checkCollesion(){}



	for (i=0;i<1000;i++){
	jeet[i]= new PIXI.Sprite(texture1);
	jeet[i].anchor.x = 0.5;
	jeet[i].anchor.y = 0.5;
	jeet[i].position.x=Math.random()*300;
	jeet[i].position.y-=200*i;
	stage.addChild(jeet[i]);	
			}
			
	for (i=0;i<1000;i++){
	jeet2[i]= new PIXI.Sprite(texture1);
	jeet2[i].anchor.x = 0.5;
	jeet2[i].anchor.y = 0.5;
	jeet2[i].position.x=Math.random()*500;
	jeet2[i].position.y-=Math.random()*900*i;
	stage.addChild(jeet2[i]);	
			}
			

	for (i=0;i<1000;i++){
	jeet3[i]= new PIXI.Sprite(texture1);
	jeet3[i].anchor.x = 0.5;
	jeet3[i].anchor.y = 0.5;
	jeet3[i].position.x=Math.random() *500;
	jeet3[i].position.y-=Math.random()*900*i;
	stage.addChild(jeet3[i]);
			}
	
	


	for (i=1;i<1000;i++){
	bullets[i]= new PIXI.Sprite(gun);
	bullets[i].anchor.x = 0.5;
	bullets[i].anchor.y = 0.5;
	bullets[i].position.x=500;
	bullets[i].position.y-=2;
	//stage.addChild(bullets[i]);		
				}


	for (i=0;i<1000;i++){
	enemy01[i]= new PIXI.Sprite(enemy);
	enemy01[i].anchor.x = 0.5;
	enemy01[i].anchor.y = 0.5;
	enemy01[i].position.x=Math.random()*700;
	enemy01[i].position.y-=Math.random()*125*i;
	stage.addChild(enemy01[i]);	
					}

	
function createPlane(x, y)
{
	// create plane
	var plane = new PIXI.Sprite(plan);
	//plane.width = 300;
	//plane.hight=300;
	
	// enable the plane to be interactive.. this will allow it to respond to mouse and touch events
	plane.setInteractive(true);
	
	// center the plane anchor point
	plane.anchor.x = 0.5;
	plane.anchor.y = 0.5;
	
	// use the mousedown and touchstart
	plane.mousemove = plane.touchstart = function(data)
		{
	// store a refference to the data
	//the reason for this is because of multitouch
	// we want to track the movement of this particular touch
	this.data = data;
	this.alpha = 0.9;
	this.dragging = true;
		};

	plane.mousedown = plane.touchstart =function(data){
	this.data = data;
	this.isdown = true;	
	newx=this.position.x;
	newy=this.position.y;

		for(i =1 ; i <9 ; i++){
			bullets[i] = new PIXI.Sprite(gun);
			bullets[i].anchor.x = 0.5;
			bullets[i].anchor.y = 0.5;	
			bullets[i].scale.x=bullets[i].scale.y=1;
			bullets[i].position.x = newx ;
			bullets[i].position.y = newy -75*i;
				stage.addChild(bullets[i]);
			}	
				this.alpha = 1;
	}

			plane.mousemove = function(event){
			this.position.x = event.global.x;
			this.position.y = event.global.y;
				}
				
			plane.ontouchmove = function(event){
			this.position.x = event.global.x;
			this.position.y = event.global.y;	
				}
		// add it to the stage
		stage.addChild(plane);
	}




function animate() {
requestAnimFrame( animate );
		//moving of background
	//	Background.tilePosition.x += 1;
		Background.tilePosition.y += 4;
	    renderer.render(stage);

	for(var i = 0; i<100;i++){
	jeet[i].position.y+=1;
	}
	for(var i = 0; i<100;i++){
	jeet2[i].position.y+=2;
	}

	for(var i = 0; i<100;i++){
	jeet3[i].position.y+=3;	
	}
	for(var i = 1; i<99;i++){
	bullets[i].position.y-=20;
	}

	for(var i = 0; i<1000;i++){
	enemy01[i].position.y+=2.5;
	}
	renderer.render(stage);
	
}


myclip=document.getElementById("clip");
    myclip.loop=true;
	
</script>
	

	

	
	

	</body>
</html>


================================================
//level 2:-
----------------
<!DOCTYPE HTML>
<html>
<head>
  <title>yomna&riham</title>
	<style>
		body {
			margin: 0;
			padding: 0;
			background-color: #000000;

		}

		.textHolder{
			width: 300px;
		}
	</style>

	<script src="pixi.js"></script>
</head>
<body>
<audio src="clip.wav" autoplay="autoplay" repeat='all'  id='clip' >
 <canvas id="myCanvas" height="2048" width="600">
 <button id="as" type="button" onmouseover='startMove()' onmouseout='stopMove()'>Left</button></body>

 </canvas>


	<script>
	
	//BackgroundCreation
	// create an new instance of a pixi stage
	var stage = new PIXI.Stage(0x97c56e, true);
	
	//Global variables
	var innerWidth=500;
	var innerHeight=900;
	var count_background = 0;
	var down=0;
	var counter = 0;
	var i = 0;
	var bullets=[];//array of bullets
	var jeet=[];//array of jeets1
	var jeet2=[];//array of jeet2
	var jeet3=[];//array of jeet3
	var enemy01=[];//array of enemy
	var enemy02=[];//array of enemy
	
	// create a renderer instance
	var renderer = PIXI.autoDetectRenderer(window.innerWidth, window.innerHeight, null);

	// add the renderer view element to the DOM
	document.body.appendChild(renderer.view);
	renderer.view.style.position = "absolute";
	renderer.view.style.top = "0px";
	
	//calling animation function
	requestAnimFrame( animate );


	// create a Background texture 
	var texture = PIXI.Texture.fromImage("background.jpg");
	// create a plane texture 
	var plan = PIXI.Texture.fromImage("plan.png");
	//create a gun texture
	var gun = PIXI.Texture.fromImage("gun.png");
	//create enemy texture
	var texture1 = PIXI.Texture.fromImage("enemy.png");
	//create 2nd kind of enemy
	var enemy = PIXI.Texture.fromImage("enemy2.png");

	var enemy2 = PIXI.Texture.fromImage("enemy3.png");
	var Background = new PIXI.TilingSprite(texture, window.innerWidth, window.innerHeight)

	stage.addChild(Background);
	
	//function to create plane
	createPlane(Math.random() * 500, Math.random() *900);
	
	//checkCollesion(){}



	for (i=0;i<1000;i++){
	jeet[i]= new PIXI.Sprite(texture1);
	jeet[i].anchor.x = 0.5;
	jeet[i].anchor.y = 0.5;
	jeet[i].position.x=Math.random()*300;
	jeet[i].position.y-=200*i;
	stage.addChild(jeet[i]);	
			}
			
	for (i=0;i<1000;i++){
	jeet2[i]= new PIXI.Sprite(texture1);
	jeet2[i].anchor.x = 0.5;
	jeet2[i].anchor.y = 0.5;
	jeet2[i].position.x=Math.random()*500;
	jeet2[i].position.y-=Math.random()*900*i;
	stage.addChild(jeet2[i]);	
			}
			

	for (i=0;i<1000;i++){
	jeet3[i]= new PIXI.Sprite(texture1);
	jeet3[i].anchor.x = 0.5;
	jeet3[i].anchor.y = 0.5;
	jeet3[i].position.x=Math.random() *500;
	jeet3[i].position.y-=Math.random()*900*i;
	stage.addChild(jeet3[i]);
			}
	
	


	for (i=1;i<1000;i++){
	bullets[i]= new PIXI.Sprite(gun);
	bullets[i].anchor.x = 0.5;
	bullets[i].anchor.y = 0.5;
	bullets[i].position.x=500;
	bullets[i].position.y-=2;
	//stage.addChild(bullets[i]);		
				}


	for (i=0;i<1000;i++){
	enemy01[i]= new PIXI.Sprite(enemy);
	enemy01[i].anchor.x = 0.5;
	enemy01[i].anchor.y = 0.5;
	enemy01[i].position.x=Math.random()*700;
	enemy01[i].position.y-=Math.random()*125*i;
	stage.addChild(enemy01[i]);	
					}

					
		for (i=0;i<1000;i++){
	enemy02[i]= new PIXI.Sprite(enemy2);
	enemy02[i].anchor.x = 0.5;
	enemy02[i].anchor.y = 0.5;
	enemy02[i].position.x=Math.random()*700;
	enemy02[i].position.y-=Math.random()*125*i;
	stage.addChild(enemy02[i]);	
					}
				
	
function createPlane(x, y)
{
	// create plane
	var plane = new PIXI.Sprite(plan);
	//plane.width = 300;
	//plane.hight=300;
	
	// enable the plane to be interactive.. this will allow it to respond to mouse and touch events
	plane.setInteractive(true);
	
	// center the plane anchor point
	plane.anchor.x = 0.5;
	plane.anchor.y = 0.5;
	
	// use the mousedown and touchstart
	plane.mousemove = plane.touchstart = function(data)
		{
	// store a refference to the data
	//the reason for this is because of multitouch
	// we want to track the movement of this particular touch
	this.data = data;
	this.alpha = 0.9;
	this.dragging = true;
		};

	plane.mousedown = plane.touchstart =function(data){
	this.data = data;
	this.isdown = true;	
	newx=this.position.x;
	newy=this.position.y;

		for(i =1 ; i <9 ; i++){
			bullets[i] = new PIXI.Sprite(gun);
			bullets[i].anchor.x = 0.5;
			bullets[i].anchor.y = 0.5;	
			bullets[i].scale.x=bullets[i].scale.y=1;
			bullets[i].position.x = newx ;
			bullets[i].position.y = newy -75*i;
				stage.addChild(bullets[i]);
			}	
				this.alpha = 1;
	}

			plane.mousemove = function(event){
			this.position.x = event.global.x;
			this.position.y = event.global.y;
				}
				
			plane.ontouchmove = function(event){
			this.position.x = event.global.x;
			this.position.y = event.global.y;	
				}
		// add it to the stage
		stage.addChild(plane);
	}




function animate() {
requestAnimFrame( animate );
		//moving of background
	//	Background.tilePosition.x += 1;
		Background.tilePosition.y += 4;
	    renderer.render(stage);

	for(var i = 0; i<100;i++){
	jeet[i].position.y+=1;
	}
	for(var i = 0; i<100;i++){
	jeet2[i].position.y+=2;
	}

	for(var i = 0; i<100;i++){
	jeet3[i].position.y+=3;	
	}
	for(var i = 1; i<99;i++){
	bullets[i].position.y-=20;
	}

	for(var i = 0; i<1000;i++){
	enemy01[i].position.y+=2.5;
	}
	
	for(var i = 0; i<1000;i++){
	enemy02[i].position.y+=2.5;
	}
	renderer.render(stage);
	
}


myclip=document.getElementById("clip");
    myclip.loop=true;
	
</script>
	

	</body>
</html>
