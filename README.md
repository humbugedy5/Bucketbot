int goPin = 8; //changed from 11
int reversePin = 9;
int rightTurnPin = 12; //changed from 10
int leftTurnPin = 13; //changed from 12
int enablerPin1 = 10;
int enablerPin2 = 11;
int echoPinLeft = 4; //old TriggerPin, CHANGE CODE
int echoPinRight = 5; //old EchoPin, CHANGE GCODE
long duration, distance, cm;
//CREATE function (pointTurn)
//CREATE function (sense)
int redPin = 1;
; //changed from 13, not tested
int bluePin = 5;
int greenPin = 6;
//Pins Defined above
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
int doSomethingNow = 60; //start turning when object detected at 60 cm
int turnTime = 2000; //turn for 2000 milliseconds
int tooLate = 45;
int distance1 = 0;
int fullStop = 500;
int reverseTime = 1000;
int lastTurn = 0; //0 for left, 1 for right
//NEED TO ADD A PIN (or more) for the WIFI SIGNAL
void setup()
{
  // put your setup code here, to run once:
  pinMode (goPin, OUTPUT) ;
  pinMode (reversePin, OUTPUT) ;
  pinMode (rightTurnPin, OUTPUT) ;
  pinMode (leftTurnPin, OUTPUT) ;
  pinMode (enablerPin1, OUTPUT) ;
  pinMode (enablerPin2, OUTPUT) ;
  Serial.begin (9600);
  pinMode (triggerPin, OUTPUT) ;
  pinMode (echoPin, INPUT) ;
  pinMode (redPin, OUTPUT);
  pinMode (bluePin, OUTPUT) ;
  pinMode (greenPin, OUTPUT) ;
  //now define the functions pointTurn and sense
  void sense() {
/*  digitalWrite( triggerPin, LOW) ; //low pulse to give clean HIGH
  delayMicroseconds(5);
  digitalWrite (triggerPin, HIGH) ;
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW) ; */
  // the above code pulses ultrasonic sensor. It is not wanted because
the Shovel needs to recieve the pulse from the Bucket.

  duration = pulseIn(echoPin, HIGH); //check for a signal

  distance = duration/58.2; //in centimeters
  }
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
/* this is the original code. it is commented out and will eventually be deleted
  digitalWrite( greenPin,LOW) ; //high changed to low because of
signal inversion
  digitalWrite( triggerPin, LOW) ; //low pulse to give clean HIGH
  delayMicroseconds(5);
  digitalWrite (triggerPin, HIGH) ;
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW) ;

  duration = pulseIn(echoPin, HIGH);

  distance = duration/58.2; //in centimeters
  distance1 = distance;
  if (distance <= tooLate) {
    digitalWrite( goPin, LOW);
    delay (fullStop);
    digitalWrite( reversePin, HIGH);
    delay(reverseTime);
    digitalWrite(reversePin, LOW);
  }
  else {
  if (distance <= doSomethingNow) {
 digitalWrite( rightTurnPin, HIGH); //turn
 digitalWrite( redPin, HIGH);
 digitalWrite( triggerPin, LOW) ; //low pulse to give clean HIGH
  delayMicroseconds(5);
  digitalWrite (triggerPin, HIGH) ;
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW) ;

  duration = pulseIn(echoPin, HIGH);

  distance = duration/58.2; //in centimeters
  if (distance < distance1) {
    digitalWrite( rightTurnPin, LOW);
    digitalWrite( redPin, LOW);
    digitalWrite( goPin, LOW);
    digitalWrite( reversePin, HIGH);
    delay(reverseTime);    //reverse
    digitalWrite( leftTurnPin, HIGH);
    digitalWrite( bluePin, HIGH);
    delay(turnTime);
    digitalWrite( leftTurnPin, LOW);
    digitalWrite( bluePin, LOW);
    int lastTurn = 0; //left
  }
  else {
 delay (turnTime);
 digitalWrite( rightTurnPin, LOW);
 digitalWrite( redPin, LOW);
 int lastTurn = 1; //right
  }
  } //end turn right
  else {} //nothing - not less than do something now NEED TO ADD A DRIVE TIME
  } // end of the not too late code
  //ADD LOOP COUNTER AND WHILE INTERRUPT HERE
} //end loop */
