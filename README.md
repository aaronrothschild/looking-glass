# looking-glass
Hardware project for displaying Reef-pi data and some simple button based controls, so you don't need to use your phone to check the temperature/PH of your reef tank

This is intended to use with a Reef-pi controller, and will use it's API to retrieve basic data and to trigger actions such as a Macro on the Reef-pi

Use Cases:
- I'm walking by my tank and want to know the temp or if anything is awry
- Every morning or so I add some frozen food, but want to disable the pumps while the food is floating around. 
- Adjusting lighting Turn On/Off/Lower reef-pi controlled lights


Concept:
- At A glance - "Is Everything Ok?" ---> LCD Display will be backlit Blue/Yellow/Red if temp/Ph is outside of set limits
- Display some simple textual data on an LCD Screen by the Tank
    - Temperature
    - PH
- Navigation Buttons: Move from temp to PH to error screen, etc.
- Buttons to control:
    - Feed Mode (enabling - turns off return pump and wavemaker so fish can eat in peace for 15mins)
    - Programmable Macro Control Button
        - Specify a Macro that will be triggered when the button is pushed
        - OR Specify multiple Macros to execute, then allow the user to choose from a list.  
