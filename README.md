# elezen.crash
detect crashes using accelerometer and arduino

*
This code is for Arduino crash sensor by Armin Nehzat
v.1
*/

int delayval = 600; // time to pump air

//set values for accelometer
int x, y, z;
int px, py, pz;
int tolerance = 300; //impact of fall
int led = 13;

void setup()
{
  Serial.begin(9600);      // sets the serial port to 9600
  // initialize the digital pin as an output.
  pinMode(led, OUTPUT); 
}

void loop()
{
  
  px = x;
  py = y;
  pz = z;

  x = analogRead(0);       // read analog input pin 0
  y = analogRead(1);       // read analog input pin 1
  z = analogRead(2);       // read analog input pin 1

  float cx = abs(x-px);
  float cy = abs(y-py);
  float cz = abs(z-pz);
  
  Serial.println (cx);
  Serial.println (cy);
  Serial.println (cz); 


   if (cz > tolerance) {
      LightFunction (cz);     
    } else if (cz < tolerance) {
      LightFunction (0);
    }


}

int LightFunction(int state){
   
  if (state == 0) {
    digitalWrite(13, LOW);
  } else {
   digitalWrite(13, HIGH);
    delay(delayval); // Delay for a period of time (in milliseconds).   
  }
     
}

