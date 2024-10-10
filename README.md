<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""></a></p>

Thats my code for the pong game that i created


let ball;
let playerPaddle;
let computerPaddle;
let ballSpeedX = 4;
let ballSpeedY = 4;
let playerScore = 0;
let computerScore = 0;
let paddleSpeed = 5;

function setup() {
  createCanvas(600, 400);
  ball = {
    x: width / 2,
    y: height / 2,
    diameter: 20
  };
  playerPaddle = {
    x: 20,
    y: height / 2,
    width: 10,
    height: 100
  };
  computerPaddle = {
    x: width - 30,
    y: height / 2,
    width: 10,
    height: 100
  };
}

function draw() {
  background(80);
  
  // Draw the ball
  ellipse(ball.x, ball.y, ball.diameter, ball.diameter);
  
  // Draw the paddles
  rect(playerPaddle.x, playerPaddle.y, playerPaddle.width, playerPaddle.height);
  rect(computerPaddle.x, computerPaddle.y, computerPaddle.width, computerPaddle.height);
  
  // Update the ball position
  ball.x += ballSpeedX;
  ball.y += ballSpeedY;
  
  // Collision with the edges
  if (ball.y < 0 || ball.y > height) {
    ballSpeedY *= -1;
  }
  
  // Collision with the paddles
  if (ball.x < playerPaddle.x + playerPaddle.width && ball.y > playerPaddle.y && ball.y < playerPaddle.y + playerPaddle.height) {
    ballSpeedX *= -1;
  } else if (ball.x > computerPaddle.x && ball.y > computerPaddle.y && ball.y < computerPaddle.y + computerPaddle.height) {
    ballSpeedX *= -1;
  }
  
  // Scoring
  if (ball.x < 0) {
    computerScore++;
    ball.x = width / 2;
    ball.y = height / 2;
  } else if (ball.x > width) {
    playerScore++;
    ball.x = width / 2;
    ball.y = height / 2;
  }
  
  // Computer AI
  if (ball.x > width / 2) {
    if (ball.y < computerPaddle.y) {
      computerPaddle.y -= 4;
    } else if (ball.y > computerPaddle.y + computerPaddle.height) {
      computerPaddle.y += 4;
    }
  }
  
  // Update the player's paddle position
  if (keyIsDown(UP_ARROW)) {
    playerPaddle.y -= paddleSpeed;
  } else if (keyIsDown(DOWN_ARROW)) {
    playerPaddle.y += paddleSpeed;
  }
  
  // Keep the paddle within the boundaries
  playerPaddle.y = constrain(playerPaddle.y, 0, height - playerPaddle.height);
  
  // Display the scores
  textSize(32);
  text(playerScore, width / 4, 40);
  text(computerScore, width * 3 / 4, 40);
}

function keyPressed() {
  // No need for keyPressed function anymore
}
