/*
      Obstacle Avoiding Robot Using Ultrasonic Sensor and Ard
      Robot Penghindar Rintangan
*/

const int trigPin = 9;      // pin trigger ultrasonic
const int echoPin = 10;     // pin echo ultrasonic

int revleft4 = 4;     // gerakan mundur motor kiri
int fwdleft5 = 5;     // gerakan maju motor kiri
int revright6 = 6;    // gerakan mundur motor kanan
int fwdright7 = 7;    // gerakan maju motor kanan

int LED = 11;     // lampu LED nyala jika berhenti

void setup() {
  
  pinMode(revleft4, OUTPUT);    // set Motor pins as output
  pinMode(fwdleft5, OUTPUT);
  pinMode(revright6, OUTPUT);
  pinMode(fwdright7, OUTPUT);
  
  pinMode(trigPin, OUTPUT);     // set trig pin as output
  pinMode(echoPin, INPUT);      //set echo pin as input to capture reflected waves

  Serial.begin(9600);

}

void loop() {

  long distance,cm;
  
  digitalWrite(trigPin,LOW);
  delayMicroseconds(2);   
  digitalWrite(trigPin,HIGH);         // send waves for 10 us
  delayMicroseconds(10);
  digitalWrite(trigPin,LOW);
  delayMicroseconds(2);
  
  distance = pulseIn(echoPin,HIGH);   // receive reflected waves

  cm = microtocm(distance);
  
  Serial.print(cm);
  Serial.print(" cm");
  Serial.println();
  delay(100);

  /*
  distance = duration / 58.2;         // convert to distance
  delay(10);
    // If you dont get proper movements of your robot then alter the pin numbers
  */
  
  if (cm >= 50)            
  {
    digitalWrite(fwdright7, HIGH);    // move forward
    digitalWrite(revright6, LOW);
    digitalWrite(fwdleft5, HIGH);                                
    digitalWrite(revleft4, LOW);
    digitalWrite(LED,LOW);
    Serial.print("Berjalan");
    Serial.println();
  }

  else
  {
    digitalWrite(fwdright7, LOW);   //Stop                
    digitalWrite(revright6, LOW);
    digitalWrite(fwdleft5, LOW);                                
    digitalWrite(revleft4, LOW);
    digitalWrite(LED,HIGH);
    delay(500);
    Serial.print("Berhenti");
    Serial.println();
    
    /*
    digitalWrite(fwdright7, LOW);   //movebackword         
    digitalWrite(revright6, HIGH);
    digitalWrite(fwdleft5, LOW);                                
    digitalWrite(revleft4, HIGH);
    delay(500);
    digitalWrite(fwdright7, LOW);   //Stop                
    digitalWrite(revright6, LOW);
    digitalWrite(fwdleft5, LOW);                                
    digitalWrite(revleft4, LOW);  
    delay(100);  
    digitalWrite(fwdright7, HIGH);       
    digitalWrite(revright6, LOW);   
    digitalWrite(revleft4, LOW);                                 
    digitalWrite(fwdleft5, LOW);  
    delay(500);
    */
  }
}
long microtocm(long microseconds)
{
  return microseconds/29/2;
}

/*
        CODE MASIH ERROR. Belum tahu cara penyelesaiannya.
*/
