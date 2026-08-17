import processing.serial.*;

Serial myPort;
float respValue = 0;
float smoothedDiameter = 100;

void setup() {
  size(800, 600);
  frameRate(30);
  
  // Replace with your active serial port name
  String portName = "COM16"; 
  
  println("Connecting to: " + portName);
  myPort = new Serial(this, portName, 115200);
  myPort.bufferUntil('\n');
}

void draw() {
  background(20);
  
  // Map respiration range (-15.0 to +15.0) to circle diameter (100 to 500 px)
  float targetDiameter = map(respValue, -15.0, 15.0, 100, 500);
  
  // ADD THIS LINE: Force the diameter to never grow larger than 600px or smaller than 50px
  targetDiameter = constrain(targetDiameter, 50, 600);
  
  // Exponential easing for smooth visual transition
  smoothedDiameter = lerp(smoothedDiameter, targetDiameter, 0.1);
  
  noStroke();
  fill(0, 150, 255, 150); // Translucent blue
  ellipse(width/2, height/2, smoothedDiameter, smoothedDiameter);
  
  fill(255);
  text("Respiration Value: " + respValue, 20, 30);
}

void serialEvent(Serial p) {
  try {
    String inString = p.readStringUntil('\n');
    if (inString != null) {
      inString = trim(inString);
      respValue = float(inString);
    }
  } catch (Exception e) {
    // Ignore packet corruption
  }
}
