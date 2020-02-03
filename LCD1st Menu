#include <Arduino.h>
#include <Adafruit_ILI9341.h>
#include <TouchScreen.h>

// TFT display and SD card will share the hardware SPI interface.
// For the Adafruit shield, these are the default.
// The display uses hardware SPI, plus #9 & #10
// Mega2560 Wiring: connect TFT_CLK to 52, TFT_MISO to 50, and TFT_MOSI to 51
#define TFT_DC  9
#define TFT_CS 10
#define SD_CS   6

// touch screen pins, obtained from the documentaion
#define YP A2  // must be an analog pin, use "An" notation!
#define XM A3  // must be an analog pin, use "An" notation!
#define YM  5  // can be a digital pin
#define XP  4  // can be a digital pin

// width/height of the display when rotated horizontally
#define TFT_WIDTH  320
#define TFT_HEIGHT 240

// calibration data for the touch screen, obtained from documentation
// the minimum/maximum possible readings from the touch point
#define TS_MINX 150
#define TS_MINY 120
#define TS_MAXX 920
#define TS_MAXY 940

// joystick pins
#define JOY_HORIZ A0
#define JOY_VERT  A1
#define JOY_SEL   2

// neutral position and deadzone of joystick
#define JOY_CENTRE   512
#define JOY_DEADZONE  64

// dimensions of one snake segment/grid box
#define SEG_SIZE 8

// min/max x and y of playable screen (divided into 8x8 grid)
#define GRID_MINX 0
#define GRID_MAXX TFT_WIDTH/SEG_SIZE - 1
#define GRID_MINY 1
#define GRID_MAXY TFT_HEIGHT/SEG_SIZE - 1


Adafruit_ILI9341 tft = Adafruit_ILI9341(TFT_CS, TFT_DC);

// a multimeter reading says there are 300 ohms of resistance across the plate,
// so initialize with this to get more accurate readings
TouchScreen ts = TouchScreen(XP, YP, XM, YM, 300);

// all possible game states - always start with menu
enum stateNames {MENU, INS, SETT, INGAME, GAMEOVER};
stateNames state = MENU;



// score will be reset every game but highScore will be saved until Arduino is
// reset
short int score = 0;
short int highScore = 0;

// 2d array containing position (x,y) of each snake segment in order
// row index 0 stores snake head position and so on
short int snakeSeg[1160][2] = {0};

// initial snake length (number of grid boxes)
short int length = 4;

// 1 is up, 2 is right, 3 is down, 4 is left
// initially direction of snake movement is right
short int direction = 2;

// coordinates of current displayed item
short int itemX, itemY;

// speed of the snake (number of milliseconds delay between reprinting of
// snake), at medium speed by default
short int speed = 100;

uint16_t babyPink = tft.color565(255, 0, 0);
uint16_t white = tft.color565(255, 255, 255);


void menuInit(){
  tft.fillScreen(babyPink);
  tft.setTextColor(white);
   
  tft.setTextSize(4);
  tft.setCursor(40, 25);
  tft.print("MuscleLife");

  tft.setTextSize(2);
  tft.setCursor(136, 100);
  tft.print("Start Workout");

  tft.setCursor(88, 145);
  tft.print("Instructions");
}

void StartWorkoutMenuInit()
{
  tft.fillScreen(babyPink);
  tft.setTextColor(white);

  tft.setTextSize(4);
  tft.setCursor(40, 25);
  tft.print("Enter your Age: ");
}

void Menu()
{
  TSPoint touch = ts.getPoint();

  // get the y coordinate of where the display was touched
  // remember the x-coordinate of touch is really our y-coordinate
  // on the display
  int touchY = map(touch.x, TS_MINX, TS_MAXX, 0, TFT_HEIGHT - 1);

  // need to invert the x-axis, so reverse the
  // range of the display coordinates
  int touchX = map(touch.y, TS_MINY, TS_MAXY, TFT_WIDTH - 1, 0);
  if (touchY > 100 && touchY < 120 && touchX > 112 && touchX < 208) {

    tft.fillScreen(babyPink);
    StartWorkoutMenuInit();

    delay(500);

//    gameInit();

    state = INGAME;
}
}



void setup() {
  tft.begin();
  tft.fillScreen(babyPink);
  tft.setRotation(3);
  menuInit();
  Menu();
}

void loop() {
  // put your main code here, to run repeatedly:

}
