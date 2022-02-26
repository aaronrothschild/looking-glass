# looking-glass
Hardware project for displaying Reef-pi data and some simple button based controls, so you don't need to use your phone to check the temperature/PH of your reef tank

This is intended to use with a Reef-pi controller, and will use it's API to retrieve basic data and to trigger actions such as a Macro on the Reef-pi

### Use Cases:
- I'm walking by my tank and want to know the temp or if anything is awry
- Every morning or so I add some frozen food, but want to disable the pumps while the food is floating around. 
- Adjusting lighting Turn On/Off/Lower reef-pi controlled lights


### Concept:
- At A glance - "Is Everything Ok?" ---> LCD Display will be backlit Blue/Yellow/Red if temp/Ph is outside of set limits
- Display some simple textual data on an LCD Screen by the Tank
    - Always show: Current Temperature + PH
    - If error conditions come up - then change display color and display the problems:
        -  RO Top Off Reservoir level (Low = Yellow, Empty=Red Light, needs filling)
        - Skimmer Overflowed tripped switch (Needs cleaning) 
- Single Press Buttons to control:
    - Feed Mode (enabling - turns off return pump and wavemaker so fish can eat in peace for 15mins)
    - Macros - Programmable Macro Control Button
        - Specify a Macro that will be triggered when the button is pushed
        - OR Specify multiple Macros to execute, then allow the user to choose from a list. 
    - Take a Pic!
        - Tell reef-pi to take a photo with it's camera because something cool is happening
- Configuration:
    - Initial WIFI config is done via Flash step?
    - Configuration of Macros/Buttons/Display options is done by logging into a basic Web Interface
- Installation: 
    - Allow a User to flash the [ESP32 via a website](https://esphome.github.io/esp-web-tools/)


Buttons:
- Status (Main Screen)
- Feed button (Feed Screen)
- Macro Button (Macro Screen)
- LEFT/RIGHT Buttons to Navigate
- ? "Photo" button (triggers taking a picture in Reef-pi)





Parts of App:
- LCD: Status Screen
    - Display key Stats: Temperature and PH Level
    - Set Backlight of LCD to GREEN if Temp/Ph levels are between X/Y
    - Display time of the last logged error and text "scrolling")
    Push button 1 -> Status Scren: More Info
        - Temp: "78.4 Now, was 78.2 1 hr ago"
        - pH: "7.8 now, was 8.1 1 hr ago"
    Push Button 1 -> Status Screen: Error Info
        - Show the last error message(s)
- LCD: Feed Mode
    - Starts after pushing "Feed" button
    - Show "Feeding Time!" and a Countdown timer ("13:22 remaining...or until you push the button").
    - Set Backlight to Yellow while ON, back to Green (if in range) when done
    - After countdown, flash BLUE, then return to status screen.
    - If just running a Macro, display the text message "Running XYZ Macro"
- LCD: Macro Button Mode
    - If only 1 Macro ID specified in Config, then run that Macro and show the text specified in the config (ie:"Yo dawg, adding mysis shrimp, cause i heard you like shrimp") for 3 secs, then return to Status Mode.
    - If multiple Macros specified, show list.
        - User can select macro from list with LEFT/RIGHT buttons
        - Press "Macro" button again to select and run.
        - Run that Macro and show the text specified in the config (ie:"Yo dawg, adding copepods, cause i heard you like pods") for 3 secs, then return to Status Mode.
- LCD: Photo Taken
    - If the Camera isn't setup on reef-pi, return an error "Setup your camera!" 
    - Send "Take Pic" request via API to reef-pi,  Random Witty comment: "I saw that too! Crazy!", "I can't believe the gall of that Tang" or something small. 
    - Display for 1 second, then back to Main screen


- WEB Page: Configuration Area:
    - Set Wifi
    - Set Temperature
        - Set preference for C/F? or auto?
        - Which Thermometer probe to use and display
    - Set PH 
        - Set PH Probe to Use
    - Set Reef-Pi login info
        - Set polling time for API queries
    - Set Feed Button:  
        - feeding time in minutes
        - Set a Macro to run after feeding time
            - Alternatively - override "Feed" button to just run a Macro and display text "XYZ" 
    - Set Macro Button:
        - Allow user to add a Macro ID (or select from a list retrieved via API)
            - Allow user to specify the text to be displayed on the LCD when running the macro 
    - LCD Display Type: 
        - Configure: OLED Display via I2C
        - Configure: RGB LCD 20x4 or 16x2 display size



### Intended Hardware:
- RGB Backlit LCD Screen (see Adafruit) 
    - Alernative: OLED display (~$8)
- ESP32 Controller
- Some Push-Buttons
- A 3d Printed Enclosure of some sort
