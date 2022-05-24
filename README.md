# Practica-4.2-Tasques-i-Leds-Rafael-Moncayo-Palate

## Codi de la pràctica

```cpp

#include <Arduino.h>
 
// This TaskHandle will allow
TaskHandle_t task1Handle = NULL;
 
const int led1 = 17; // Pin of the LED
const int led2 = 21; // Pin of the LED
 
 
 
void toggleLED(void * parameter){
for(;;){
 
vTaskDelay(500 / portTICK_PERIOD_MS);
// Turn the LED on
Serial.print("Turn the LED 1 on \n");
digitalWrite(led1, HIGH);
// Pause the task for 500m
vTaskDelay(500 / portTICK_PERIOD_MS);
Serial.print(" Pause the task for 500ms\n");
// Turn the LED off
digitalWrite(led1, LOW);
Serial.print("Turn the LED 1 off\n");
 
// Kill task1 if it's running
   if(task1Handle != NULL) {
   vTaskDelete(task1Handle);
   }
 
}
// vTaskDelete( NULL );
 
 
}
 
void toggleLED2(void * parameter){
  for(;;){ // infinite loop
  // Turn the LED on
  digitalWrite(led2, HIGH);
  Serial.print("Turn the LED 2 on\n");
  // Pause the task for 500ms
  Serial.print(" Pause the task for 500ms\n");
  vTaskDelay(500 / portTICK_PERIOD_MS);
  // Turn the LED off
  digitalWrite(led2, LOW);
  Serial.print("Turn the LED 2 off\n");
  // Pause the task again for 500ms
  vTaskDelay(500 / portTICK_PERIOD_MS);
  }
  vTaskDelete( NULL );
}
 
 
 
void setup()
{
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  Serial.begin(112500);
  
  /* we create a new task here */
  xTaskCreate(
    toggleLED, /* Task function. */
    "toggleLED", /* name of task. */
    10000, /* Stack size of task */
    NULL, /* parameter of the task */
    1, /* priority of the task */
    NULL); /* Task handle to keep track of created task */
  
  xTaskCreate(
    toggleLED2, /* Task function. */
    "toggleLED2", /* name of task. */
    10000, /* Stack size of task */
    NULL, /* parameter of the task */
    1, /* priority of the task */
    NULL);
  
}
 
 
 
/* the forever loop() function is invoked by Arduino ESP32 loopTask */
void loop()
{
}
```
