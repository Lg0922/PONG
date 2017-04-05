#include <U8glib.h>
#include <Microduino_Key.h>
#include <Adafruit_NeoPixel.h>
#define PIN 0  
#define PIN_NUM 2 
#define buzzer_pin 6 
#define buzzer_fre 600
#define INTERVAL_LCD 10  
#define A 0x1FE807F     
#define B 0x1FE40BF  
#define r1 0
#define r2 1
#define l1 2
#define l2 3
#define u1 4
#define u2 5
#define d1 6
#define d2 7 
Adafruit_NeoPixel strip = Adafruit_NeoPixel(PIN_NUM, PIN, NEO_GRB + NEO_KHZ800);               
unsigned long lcd_time = millis();  
U8GLIB_SSD1306_128X64 u8g(U8G_I2C_OPT_NONE); 
Key UP(A0, INPUT);
Key DOWN(A0, INPUT);
Key UP1(A2, INPUT);
Key DOWN1(A2, INPUT);
Key CHOOSE(A0, INPUT);
int y1=8;
int y2=8;
int xb=64;
int yb=32;
int le=1;
int ri=0;
int direction;
int balldir;
int score1=0;
int score2=0;
int a;
void start(){
    y1=8;
    y2=8;
    xb=64;
    yb=32;
    score1=0;
    score2=0;
}
void load(){
  u8g.firstPage();
  do {
  u8g.setFont(u8g_font_9x18Br);
  u8g.setPrintPos(47,28);
  u8g.print("PONG!");
  u8g.setFont(u8g_font_fixed_v0r);
  u8g.setPrintPos(75,60);
  u8g.print("BY DEDSEC");
  }while(u8g.nextPage());
  delay(5000);
}
void menu(){
 u8g.firstPage();
  do
  { 
  u8g.setFont(u8g_font_7x13);
  u8g.setPrintPos(20,25);
  u8g.print("UP TO PVE");
  u8g.setPrintPos(20,40);
  u8g.print("DOWN TO PVP");
  }while(u8g.nextPage());
}
void table(){
  u8g.drawFrame(4,4,120,56) ;
  u8g.drawBox(62,0,4,64);
  u8g.setFont(u8g_font_fixed_v0r);
  u8g.setPrintPos(50, 14);
  u8g.print(score1);
  u8g.setPrintPos(68, 14);
  u8g.print(score2);
 }
 void backet(){
  u8g.drawBox(4,y1,4,16) ;
  u8g.drawBox(120,y2,4,16) ;
 }
 void key(){
  if(UP.read(680, 720)){
    if(y1==4){
      y1=y1;
    }
    else{
    y1=y1-4;
    }
    delay(10);
  }
  if(DOWN.read(310,350)) {
    if(y1==44){
      y1=y1;
    }
    else{
    y1=y1+4;
    }
    delay(10);
  }
  if(UP1.read(680, 720)){
    if(y2==4){
      y2=y2;
    }
    else{
    y2=y2-4;
    }
    delay(10);
  }
  if(DOWN1.read(310,350)) {
    if(y2==44){
      y2=y2;
    }
    else{
    y2=y2+4;
    }
  }
  delay(10);
 }
void ball(){
  u8g.drawDisc(xb,yb,2);
}
void hit(){
  if(xb<=6){
    if(y1<yb&&yb-y1<=8){
      balldir=r1;
      direction=ri;
      boom();
    }
    else if(y1<yb&&yb-y1>8&&yb-y1<+16){
      balldir=r2;
      direction=ri;
      boom();
    }
    else{
      scorer();
    }
  }
  if(xb>=118){
    if(y2<yb&&yb-y2<=8){
      balldir=l1;
      direction=le;
      boom();
    }
    else if(y2<yb&&yb-y2>8&&yb-y2<+16){
      balldir=l2;
      direction=le;
      boom();
    }
    else{
      scorel();
    }
  }
 if(yb<=6){
  if(direction==0){
      balldir=u1;
  }
  else{
    balldir=u2;
  }
 }
 if(yb>=58){
  if(direction==0){
    balldir=d1;
  }
  else{
    balldir=d2;
  }
 }
}
void ballgame(){
  switch(balldir){
    case r1:
    xb=xb+2;
    yb=yb-1;
    break;
    case r2:
    xb=xb+2;
    yb=yb+2;
    break;
    case l1:
    xb=xb-1;
    yb=yb-1;
    break;
    case l2:
    xb=xb-2;
    yb=yb+2;
    break;
    case u1:
    xb=xb+1;
    yb=yb+2;
    break;
    case u2:
    xb=xb-2;
    yb=yb+1;
    break;
    case d1:
    xb=xb+2;
    yb=yb-1;
    break;
    case d2:
    xb=xb-1;
    yb=yb-2;
    break;
  }
  hit();
}
void scorel(){
  xb=32;
  yb=32;
  score1=score1+1;
  direction=ri;
  balldir=r1;
  delay(500);
}
void scorer(){
  xb=96;
  yb=32;
  score2=score2+1;
  direction=le;
  balldir=l1;
  delay(500);
}
void win(){
  if(score1==11){
    u8g.firstPage();
  do {
  u8g.setFont(u8g_font_7x13);
  u8g.setPrintPos(24,28);
  u8g.print("PLAYER1 WIN!");
  u8g.setFont(u8g_font_fixed_v0r);
  u8g.setPrintPos(75,60);
  u8g.print("BY DEDSEC");
  }while(u8g.nextPage());
  delay(5000);
  xb=32;
  yb=32;
  score1=0;
  score2=0;
  direction=ri;
  balldir=r1;
  }
  if(score2==11){
    u8g.firstPage();
  do {
  u8g.setFont(u8g_font_7x13);
  u8g.setPrintPos(24,28);
  u8g.print("PLAYER2 WIN!");
  u8g.setFont(u8g_font_fixed_v0r);
  u8g.setPrintPos(75,60);
  u8g.print("BY DEDSEC");
  }while(u8g.nextPage());
  delay(5000);
  xb=96;
  yb=32;
  score1=0;
  score2=0;
  direction=le;
  balldir=l1;
  }
}
void npc(){
  if(xb>=64){
  a=random(0,7);
  y2=yb+a;
  if(y2<=4){
    y2=4;
  }
  if(y2>=44){
    y2=44;
  }
  }
}
void boom(){
    tone(buzzer_pin,buzzer_fre);  
    delay(50);
    noTone(buzzer_pin);
    strip.setPixelColor(0, strip.Color(255, 0, 0));
    strip.show();   
    delay(100); 
    strip.setPixelColor(0, strip.Color(0, 0, 0));
    strip.show();
}
void pvemode(){
  u8g.firstPage();
  do {
  table();
  backet();
  ball();
 }while(u8g.nextPage());
 key();
 ballgame();
 npc();
 win();
 delay(10);
}
void pvpmode(){
  u8g.firstPage();
  do {
  table();
  backet();
  ball();
 }while(u8g.nextPage());
 key();
 ballgame();
 win();
 delay(10);
}
void setup() {
   strip.begin();
   strip.show();
   load();
}
void loop(){
if(UP.read(680, 720)){
  for(;;){
    pvemode();
    if(CHOOSE.read(0,20))
    break;
  }
}
else if(DOWN.read(310,350)){
  for(;;){
    pvpmode();
    if(CHOOSE.read(0,20))
    break;
  }
}
else{
  menu();
  start();
}
}
