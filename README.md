# RTK-Code
Having issues in code at Keypad data entry following is the code
// Adding Library
#include<LiquidCrystal.h>
#include<Keypad.h>

/*** Define LCD ***/
const int rs = 24, en = 26, d4 = 28, d5 = 30, d6 =32, d7 = 34;
LiquidCrystal lcd(rs,en,d4,d5,d6,d7);

/*** Define Keypad ***/
const byte ROWS = 4; 
const byte COLS = 4;

char keys[ROWS][COLS] = 
                        {
                          {'1','2','3','A'},
                          {'4','5','6','B'},
                          {'7','8','9','C'},
                          {'*','0','#','D'},                    
                        };

byte rowPins[ROWS] = {25,27,29,31};
byte colPins[COLS] = {33,35,37,39};

Keypad customKeypad = Keypad (makeKeymap(keys), rowPins, colPins, ROWS, COLS);
char key;

/**** Variables *****/

byte var[] = {12,11,10,4,22,36};
/*** var arry is use for O/P
 * relay 1 = 12, Relay 4 = 4
 * Relay 2 = 11, Relay 5 = 22
 * Relay 3 = 10, Buzzer  = 36
 */

 int ip[] = {A15,A14,A13,A12,A11,A10};

/**** ip array is used for Analog I/P Signals
* A15 = charging Current, A14 = Discharging Current
* 
* A13 = Mean Well voltage, A12 = Aux U-cap voltage.
* A11 = EUT I/P voltage, A10 = EUT O/P Voltage.
*/

/*** Volatge divder 
 *  R1 = 33 k-ohm ,R2 = 5.6 k-ohm ,Rt = R1+R2
 *  Formula :
 *            Vout= (Vin X R2)/ Rt
 *         calcultation for I/P Voltage
 *         Vin = (Vout X Rt)/R2
 *       eq = Rt/R2
 */
const float  eq = 6.9;


void setup() 
{
Serial.begin(9600);
lcd.begin(20,4);
//pinMode(v1,INPUT);
for(int i = 0 ; i<6;i++)
{
pinMode(var[i], OUTPUT);

pinMode(ip[i],INPUT);
}

digitalWrite(var[0],HIGH);
lcd.print("Welcome To Test Kit");
lcd.setCursor(6,1);
lcd.print("V.2.0.0");
lcd.setCursor(6,2);
lcd.print("AARTECH");
lcd.setCursor(3,3);
lcd.print("Solonics Ltd.");
for(int i=0; i <=10 ; i++)
    {
      digitalWrite(var[5], HIGH);
      delay(100);
      digitalWrite(var[5], LOW);
      delay(100);
      Serial.print(i);
    }

 delay(2000);
    lcd.clear();
    lcd.setCursor(2,0);
    lcd.print("Select Your Test");
    lcd.setCursor(0,1);
    lcd.print("A Charging Test");
    lcd.setCursor(0,2);
    lcd.print("B Discharging Test");
    lcd.setCursor(0,3);
    lcd.print("C Performanch Test");
}

void loop()
{
   char customKey = customKeypad.getKey();
   Serial.println(customKey);   
   menu();

}

/*** Menu ***/
void menu()
{

  char customKey = customKeypad.getKey();
  char key = customKey;
  switch(customKey)
  {
    case 'A':
    digitalWrite(var[5], HIGH);
    delay(100);
    digitalWrite(var[5], LOW);
    delay(100);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Power Supply:     V");
    lcd.setCursor(0,1);
    lcd.print("Set Voltage:      V");
    lcd.setCursor(0,2);
    lcd.print("EUT IP=     OP=    V");
    lcd.setCursor(0,3);
    lcd.print("Current:         Amp");
    break;
    
    case'B':
    digitalWrite(var[5], HIGH);
    delay(100);
    digitalWrite(var[5], LOW);
    delay(100);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Power Supply:     V");
    lcd.setCursor(0,1);
    lcd.setCursor(0,2);
    lcd.print("EUT IP=     OP=    V");
    lcd.setCursor(0,3);
    lcd.print("Current:         Amp");
    break;

    case'C':
    digitalWrite(var[5], HIGH);
    delay(100);
    digitalWrite(var[5], LOW);
    delay(100);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Power Supply:     V");
    lcd.setCursor(0,1);
    
    lcd.setCursor(0,2);
    lcd.print("EUT IP=     OP=    V");
    lcd.setCursor(0,3);
    lcd.print("Current:         Amp");
    break;
    case'D':
    lcd.clear();
    digitalWrite(var[5], HIGH);
    delay(100);
    digitalWrite(var[5], LOW);
    delay(100);
    lcd.setCursor(0,0);
    lcd.print("Select Your Test");
    lcd.setCursor(0,1);
    lcd.print("A Charging Test");
    lcd.setCursor(0,2);
    lcd.print("B Discharging Test");
    lcd.setCursor(0,3);
    lcd.print("C Performanch Test");
      break;
  }
}


 

