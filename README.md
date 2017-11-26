# test
test
// Variables
var score = 0;
// Create Sprites
var cake = createSprite(350,200);
cake.setAnimation("cake");

var player = createSprite(200,200);
player.setAnimation("alienWalkRight");

var enemy1 = createSprite(0, randomNumber(150, 250));
enemy1.setAnimation("ladybug");
enemy1.velocityX = 2;

var enemy2 = createSprite(0, randomNumber(150, 250));
enemy2.setAnimation("ladybug");
enemy2.velocityX = 2;
var playerSpeed;
playerSpeed = 2;

function draw() {
  // draw the background
  gameBackground();
  // update the sprites
  playertobug();
  enemiesTouchCake();
  movePlayer();
  displaceEnemies();
  enemiesTouchWater();
  showScore();
  drawSprites();
}

// Functions
function gameBackground() {
  noStroke();
  background(rgb(0,100,255));
  fill(rgb(100,100,100));
  rect(0,150,400,100);
  fill(rgb(80,80,80));
  rect(0,140,400,10);
  rect(0,250,400,10);
}

function enemiesTouchCake(){
  if (enemy1.isTouching(cake)) {
    setEnemy1();
    score = score - 2;
  }
  if (enemy2.isTouching(cake)) {
    setEnemy2();
    score = score - 2;
  }
}

function movePlayer(){
  if (keyDown("left")) {
    player.x = player.x - playerSpeed;
    player.setAnimation("alienWalkRight_copy_1");
  }
  if (keyDown("right")) {
    player.x = player.x + playerSpeed;
    player.setAnimation("alienWalkRight");
  }
  if (keyDown("up")) {
    player.y = player.y - playerSpeed;
  }
  if (keyDown("down")) {
    player.y = player.y + playerSpeed;
  }
}

function displaceEnemies(){
player.displace(enemy1);
player.displace(enemy2);
}

function enemiesTouchWater(){
  if (enemy1.y < 140) {
    score = score + 1;
    setEnemy1();
  }
  if (enemy1.y > 260) {
    score = score + 1;
    setEnemy1();
  }
  if (enemy2.y < 140) {
    score = score + 1;
    setEnemy2();
  }
  if (enemy2.y > 260) {
    score = score + 1;
    setEnemy2();
  }
}

function showScore() {
  fill("white");
  textSize(20);
  text("Score",20,20,200,100);
  text(score,20,40,200,100);
}
function setEnemy1() {
  enemy1.x = 0;
  enemy1.y = randomNumber(150, 250);
  enemy1.velocityX = 2;
}
function setEnemy2() {
  enemy2.x = 0;
  enemy2.y = randomNumber(150, 250);
  enemy2.velocityX = 2;
}
function playertobug() {
  if (player.displace(enemy1)) {
    enemy1.velocityX = 0;
  }
  if (player.displace(enemy2)) {
    enemy2.velocityX = 0;
  }
  if (score == 10) {
    playerSpeed = 1;
  }
  if (score <= -1) {
    enemy1.visible = 0;
    enemy2.visible = 0;
    player.visible = 0;
    cake.setAnimation("sad_cake");
    textSize(50);
    text("Game Over", 50, 200);
  }
}
