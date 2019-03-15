---
layout: post
title:  "tennis game"
date:   2019-03-15 17:51:31 +0800
categories: jekyll update
---
<html>
	<canvas id="gameCanvas" width="800" height="600"></canvas>
	<script>
	var canvas;
	var canvasContext;
	var ballX = 50;
	var ballY = 50;
	var ballSpeedX = 10;
	var ballSpeedY = 4;
	
	var playerScore = 0;
	var comScore = 0;
	const WINNING_SCORE = 3;
	
	var showingWinScreen = false;
	
	var paddle1Y = 250;
	var paddle2Y = 250;
	
	const PADDLE_HEIGHT = 100;
	const PADDLE_WIDTH = 10;
	
	function calculateMousePos(evt) {
		var rect = canvas.getBoundingClientRect();
		var root = document.documentElement;
		var mouseX = evt.clientX - rect.left - root.scrollLeft;
		var mouseY = evt.clientY - rect.top - root.scrollTop;
		return {
			x:mouseX,
			y:mouseY
		};
	}
	
	function handleMouseClick(evt) {
		if(showingWinScreen) {
			playerScore = 0;
			comScore = 0;
			showingWinScreen = false;
		}
	}
	
	window.onload = function() {
		canvas = document.getElementById('gameCanvas');
		canvasContext = canvas.getContext('2d');
		
		var framesPerSecond = 30;
		setInterval(function(){
			moveEverything();
			drawEverything();
		}, 1000/framesPerSecond);
	
		canvas.addEventListener('mousedown', handleMouseClick);	
	
		canvas.addEventListener('mousemove',
			function(evt) {
				var mousePos = calculateMousePos(evt);
				paddle1Y = mousePos.y - (PADDLE_HEIGHT/2);
			});
	}
	
	function ballReset() {
		if(playerScore >= WINNING_SCORE ||
		   comScore >= WINNING_SCORE) {
			showingWinScreen = true;
		}
	
		ballSpeedX = -ballSpeedX;
		ballX = canvas.width/2;
		ballY = canvas.height/2;
	}
	
	function computerMovement() {
		var paddlewYCenter = paddle2Y + (PADDLE_HEIGHT/2);
		if(paddlewYCenter < ballY-35) {
			paddle2Y += 6;
		} else if (paddlewYCenter > ballY+35) {
			paddle2Y -= 6;
		}
	}
	
	function moveEverything() {
		if(showingWinScreen) {
			return;
		}
	
		computerMovement();
		
		ballX += ballSpeedX;
		ballY += ballSpeedY;
		
		if(ballX > canvas.width){
			if(ballY > paddle2Y &&
			   ballY < paddle2Y+PADDLE_HEIGHT) {
				ballSpeedX = -ballSpeedX;
				
				var deltaY = ballY - (paddle2Y+PADDLE_HEIGHT/2);
				ballSpeedY = deltaY * 0.35;
			} else {
				playerScore++;
				ballReset();
			}
		}
		if(ballX < 0){
			if(ballY > paddle1Y &&
			   ballY < paddle1Y+PADDLE_HEIGHT) {
				ballSpeedX = -ballSpeedX;
				
				var deltaY = ballY - (paddle1Y+PADDLE_HEIGHT/2);
				ballSpeedY = deltaY * 0.35;
			} else {
				comScore++;
				ballReset();
			}
		}
		if(ballY < 0){
			ballSpeedY = -ballSpeedY;
		}
		if(ballY > canvas.height){
			ballSpeedY = -ballSpeedY;
		}
	}
	
	function drawNet() {
		for(var i=0;i<canvas.height;i+=40) {
			colorRect(canvas.width/2 - 1, i, 2, 20, 'white');
		}
	}
	
	function drawEverything() {
		//background
		colorRect(0, 0, canvas.width, canvas.height, 'black');
	
		if(showingWinScreen) {
			canvasContext.fillStyle = 'white';
			
			if(playerScore >= WINNING_SCORE) {
				canvasContext.fillText("Player win.", 350, 200);
			} else if(comScore >= WINNING_SCORE) {
				canvasContext.fillText("Computer win.", 350, 200);
			}
	
			canvasContext.fillText("Click to continue.", 350, 500);
	
			return;
		}
	
		drawNet();
	
		//player paddle
		colorRect(0, paddle1Y, PADDLE_WIDTH, PADDLE_HEIGHT, 'white');
	
		//com paddle
		colorRect(canvas.width-PADDLE_WIDTH, paddle2Y, PADDLE_WIDTH, PADDLE_HEIGHT, 'white');
	
		//ball
		colorCircle(ballX, ballY, 10, 'white');
	
		//score
		canvasContext.fillText(playerScore, 100, 100);
		canvasContext.fillText(comScore, canvas.width-100, 100);
	}
	
	function colorCircle(centerX, centerY, radius, drawColor) {
		canvasContext.fillStyle = drawColor;
		canvasContext.beginPath();
		canvasContext.arc(centerX, centerY, radius, 0, Math.PI*2, true);
		canvasContext.fill();
	}
	
	function colorRect(leftX, topY, width, height, drawColor) {
		canvasContext.fillStyle = drawColor;
		canvasContext.fillRect(leftX , topY, width, height);
	}
	
	</script>
</html>

使用JavaScript製作的簡單小遊戲，簡單的AI。<br>
玩家利用「滑鼠」控制「左方」檔板。<br>
「三分」為勝負判定。