int trigPin = 3;     // Sensor Pin 
int echoPin = 4;     // Input Pin 

int in1 = 11;  //Motor A 
int in2 = 10;   //Motor A 
int in3 = 9;  // Motor B
int in4 = 8;    //Motor B 
int ena = 6; // pwm Motor A 
int enb = 5;  // pwm Motor B
int sensor_out = 13;
long duration;
float distance,x, area , circle_area;
void setup() {
  // put your setup code here, to run once:
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);
pinMode(sensor_out,OUTPUT);
 pinMode(in1, OUTPUT);
 pinMode(in2, OUTPUT);
 pinMode(in3, OUTPUT);
 pinMode(in4, OUTPUT);
pinMode(ena, OUTPUT);
pinMode(enb, OUTPUT);
  Serial.begin(9600);
}

void loop() {

    int dist=calculateDistance();
    delay(100);
    Serial.println(distance);
    
 
    if (dist <= 25 ){
       digitalWrite(sensor_out,HIGH);
analogWrite(ena, 200);
analogWrite(enb, 200);
  digitalWrite(in1,HIGH);
  digitalWrite(in2,LOW); 
  // left /right 
  digitalWrite(in3,LOW);
 digitalWrite(in4,LOW);
   //digitalWrite(in1,HIGH);// forward
  //digitalWrite(in2,LOW);
 Serial.println("Objects");
    }
    else{
  analogWrite(ena, 150);
analogWrite(enb, 150);    
 digitalWrite(in1,LOW); // forward
digitalWrite(in2,HIGH);
digitalWrite(in3,LOW);
digitalWrite(in4,HIGH);
digitalWrite(sensor_out,LOW); 
Serial.println("no objects");
    }
}
int calculateDistance()
{
  digitalWrite(trigPin,LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin,HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin,LOW);
  duration=pulseIn(echoPin,HIGH);
  distance=duration*0.034/2;
 // Serial.print(distance);
 // Serial.println(" ");
  return distance;
}
