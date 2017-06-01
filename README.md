// # Bucketbot
int goPin = 11;
int rightTurnPin = 10;
int leftTurnPin = 12;
int redPin = 13;
int bluePin = 5;
int greenPin = 6;
int maxZoomZoom = 165; // 125 = threshhold
int zoomZoom = 80;
int vroomVroom = 5;
int maxDriveTimeBeforeTurn = 800;
int loopsSoFar = 0;
int loopsBeforeRightTurn = 4;
int loopsBeforeLeftTurn = 8;
int loopsBeforeReset = 9;
int resetsSoFar = 0;
int resetsBeforeStop = 4;

void setup()
{
  // put your setup code here, to run once:
  pinMode (goPin, OUTPUT) ;
  pinMode (rightTurnPin, OUTPUT) ;
  pinMode (leftTurnPin, OUTPUT) ;
  pinMode (redPin, OUTPUT);
  pinMode (bluePin, OUTPUT) ;
  pinMode (greenPin, OUTPUT) ;

   // ramp up and level out
 while (zoomZoom < maxZoomZoom) {
  analogWrite( goPin, zoomZoom) ;
 
  zoomZoom = zoomZoom + vroomVroom;
  
 } // END: ramp up while

  while (zoomZoom > 155) {
    analogWrite (goPin, zoomZoom) ;
    zoomZoom = zoomZoom - vroomVroom ;
    delay(100) ;
  } //END : level off

  
    
} // END: setup() function

void loop() {
  // put your main code here, to run repeatedly:
  digitalWrite( greenPin,HIGH) ;
  // drive for a while
 delay (maxDriveTimeBeforeTurn);
  
  //slowdown and stop
  /*
   while (zoomZoom > 0) {
    (zoomZoom = zoomZoom - vroomVroom) ;
  }
  */
  
  digitalWrite ( redPin, HIGH) ;
  digitalWrite( rightTurnPin,HIGH) ;
  delay (2000);
  digitalWrite( rightTurnPin, LOW) ;
  digitalWrite( redPin, LOW) ;

  delay (2000);

  // Turn left for 2000 ms
  digitalWrite (bluePin, HIGH) ;
  digitalWrite( leftTurnPin, HIGH) ;
  delay (2000);
  digitalWrite( leftTurnPin, LOW) ;
  digitalWrite( bluePin, LOW) ;

 loopsSoFar = loopsSoFar + 1;

 if (loopsSoFar == loopsBeforeReset) { // @brian: use == for comparison
  loopsSoFar = 0;
  resetsSoFar = resetsSoFar + 1;
 }

 if (resetsSoFar == resetsBeforeStop) {
    // Slow back down to zero
    while (zoomZoom > 0) {
      analogWrite (goPin, zoomZoom) ;
      zoomZoom = zoomZoom - vroomVroom;
      digitalWrite( greenPin, LOW) ;
    }
    // Empty while to simulate "turning off"
    while (1==1) {
    } // END: empty while
 }

 }  // END: loop() function
