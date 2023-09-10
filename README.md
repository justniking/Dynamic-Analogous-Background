# Dynamic-Analogous-Background
let t;
let lines = 50;
let freqMultiplier = 0.1;
let amplitudeMultiplier = 5;
let speed = 0.01; // Faster speed for more dynamic movement

function setup() {
  createCanvas(800, 600);
  t = 0;
  stroke(0);
  strokeWeight(0.5);
}

function draw() {
  // Colorful, dynamic background
  let bg1 = color(128 + sin(t) * 128, 128 + cos(t) * 128, 128 + sin(t + PI / 2) * 128);
  let bg2 = color(128 - sin(t) * 128, 128 - cos(t) * 128, 128 - sin(t + PI / 2) * 128);
  for (let i = 0; i <= width; i++) {
    let inter = map(i, 0, width, 0, 1);
    let c = lerpColor(bg1, bg2, inter);
    stroke(c);
    line(i, 0, i, height);
  }
  
  for (let i = 0; i < lines; i++) {
    let freq = (i + 1) * freqMultiplier + sin(t) * 0.05; // Vary frequency over time
    let amplitude = (i + 1) * amplitudeMultiplier + cos(t) * 5; // Vary amplitude over time
    let offset = map(i, 0, lines, height, 0); // Moving from bottom to top
    
    beginShape();
    for (let x = 0; x <= width; x++) {
      let y1 = sin(freq * x + t) * amplitude;
      let y2 = sin((freq + 0.1) * x + t) * amplitude; // Second wave for interference
      let y = offset + y1 + y2; // Combine waves and add offset
      vertex(x, y);
    }
    endShape();
  }

  t += speed;
}



