# GravityGame
Gravity Game

<!DOCTYPE html>
<html>
<head>
  <title>Lunar Lander</title>
  <style>
    body {
      background-color: black;
      font-family: sans-serif;
    }

    canvas {
      width: 500px;
      height: 500px;
    }
  </style>
</head>
<body>
  <canvas id="game-canvas"></canvas>
</body>
</html>

#CSS
body {
  background-color: black;
  font-family: sans-serif;
}

canvas {
  width: 500px;
  height: 500px;
}

// Get the canvas element
const canvas = document.getElementById("game-canvas");

// Set the canvas context
const ctx = canvas.getContext("2d");

// Create the game object
const game = new Game(ctx);

// Start the game loop
game.start();

// Game class
class Game {
  constructor(ctx) {
    this.ctx = ctx;

    // Create the lunar lander
    this.lander = new Lander();

    // Create the landing pad
    this.landingPad = new LandingPad();

    // Create the background
    this.background = new Background();
  }

  start() {
    // Update the game state
    this.update();

    // Render the game
    this.render();

    // Request the next animation frame
    requestAnimationFrame(() => this.start());
  }

  update() {
    // Update the lander's position and velocity
    this.lander.update();

    // Check if the lander has collided with the landing pad
    if (this.lander.hasCollided(this.landingPad)) {
      // The player has won!
      alert("You win!");
    }
  }

  render() {
    // Clear the canvas
    this.ctx.clearRect(0, 0, canvas.width, canvas.height);

    // Render the background
    this.background.render(this.ctx);

    // Render the lander
    this.lander.render(this.ctx);

    // Render the landing pad
    this.landingPad.render(this.ctx);
  }
}

// Lander class
class Lander {
  constructor() {
    this.position = { x: 100, y: 100 };
    this.velocity = { x: 0, y: 0 };
  }

  update() {
    // Update the lander's position based on its velocity
    this.position.x += this.velocity.x;
    this.position.y += this.velocity.y;
  }

  render(ctx) {
    // Draw a triangle to represent the lander
    ctx.fillStyle = "white";
    ctx.beginPath();
    ctx.moveTo(this.position.x, this.position.y);
    ctx.lineTo(this.position.x + 10, this.position.y + 10);
    ctx.lineTo(this.position.x - 10, this.position.y + 10);
    ctx.closePath();
    ctx.fill();
  }

  hasCollided(landingPad) {
    // Check if the lander's position is within the landing pad's bounds
    return this.position.x >= landingPad.position.x &&
      this.position.x <= landingPad.position.x + landingPad.width &&
      this.position.y >= landingPad.position.y &&
      this.position.y <= landingPad.position.y + landingPad.height;
  }
}

// LandingPad class
class LandingPad {
  constructor() {
    this.position = { x: 200, y: 400 };
    this.width = 50;
    this.height = 50;
  }

  render(ctx) {
    // Draw a rectangle to represent the landing pad
    ctx.fillStyle = "
