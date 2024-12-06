# IOT_project
Fire Sensor and Extinguisher     
#code          
//C++ code     
     
     #include <LiquidCrystal.h>     
     #define D4 7     
     #define D5 6     
     #define D6 5     
     #define D7 4     
     #define E 8     
     #define RS 9     
     #include <Adafruit_NeoPixel.h>     
     #define PIN 2     
     #define N_LEDS 7     
     LiquidCrystal LCD(9,8,7,6,5,4);     
          
     int piezo =3;     
     int pump = 10;      
     int temp = 0;     
     int light = 0;     
     Adafruit_NeoPixel strip = Adafruit_NeoPixel(N_LEDS, PIN, NEO_GRB + NEO_KHZ800);     
     
     void setup()
     {
          Serial.begin(9600);
          pinMode(A0, INPUT); // temp sensor
          pinMode(A1,INPUT);// gas sensor
          pinMode(A2,INPUT);// phototransistor
          pinMode(piezo,OUTPUT);
          pinMode(pump,OUTPUT);
          LCD.begin(16,2); 
          strip.begin();
     }
     
     void loop()
     {	
          int temp=analogRead(A0);
          Serial.print("The Temperature is : ");
          Serial.println(temp);
       
          int light= analogRead(A2);
          Serial.print("The value of Phototransistor :");
          Serial.println(light);
       
          int a= analogRead(A1);
          int b= map(a,0,1023,0,255);
          Serial.print("The gas intensity is : ");
          Serial.println(b);
          delay(2000);
         
     if ((b>70 && light>5 ) || (temp>80 && light>5) || (b>70 && temp>80))
     { 
         digitalWrite(piezo,HIGH);
         digitalWrite(pump,HIGH);
         LCD.clear();                
         LCD.setCursor(0,0);
         LCD.print("ALERT");     
         delay(1000);              
         LCD.clear();             
         LCD.setCursor(0,1); 
         LCD.print("EVACUATE");  
         delay(1000);
         chase(strip.Color(255, 0, 0)); //Red
         delay(100);
     }
     
     else
     {
         digitalWrite(piezo,LOW);
         digitalWrite(pump,LOW);
         LCD.clear();           
         LCD.setCursor(0,0);
         LCD.print("SAFE");        
         delay(1000);             
         LCD.clear();           
         LCD.setCursor(0,1);
         LCD.print("ALL CLEAR"); 
         delay(1000);
         chase(strip.Color(0, 255, 0)); //green
         delay(100);
     }
     }
     
     static void chase(uint32_t c)//Loop of the NeoPixel Strip
     {
       for(uint8_t i=0; i<strip.numPixels()+8; i++)
       {
           strip.setPixelColor(i  , c);
           strip.setPixelColor(i-8, 0);
           strip.show();
           delay(50);
       }
     }
