# Test Design Scripts for Higher-Order Human Behavior Data Collection

This repository contains MATLAB scripts designed for creating and managing test designs used in the collection of higher-order human behavior data. These scripts are particularly useful for designing and implementing interactive tests and experiments that require precise control and monitoring of user inputs and behaviors.

## Project Overview

The scripts provided in this repository facilitate the creation of interactive test elements, such as sliders and response interfaces, using Psychtoolbox. They are intended for researchers and practitioners who need to collect and analyze complex behavioral data in laboratory settings or controlled experiments.

## Requirements

- **MATLAB**: Ensure you have MATLAB installed.
- **Psychtoolbox**: Download and install Psychtoolbox. For installation instructions, visit [Psychtoolbox](https://psychtoolbox.org/).

##  File Contents

- **`slider_bar_example.m`**: MATLAB script for creating an interactive slider bar that responds to mouse input.

##  How to Use

1. **Install Psychtoolbox**: Follow the [installation instructions](https://psychtoolbox.org/download) to set up Psychtoolbox in MATLAB.

2. **Run the Script**:
   - Open MATLAB.
   - Navigate to the directory containing the script files.
   - Run the desired script by typing its name in the MATLAB command window.

3. **Interact with the Test Elements**:
   - Use the mouse to interact with the test elements, such as adjusting sliders or responding to prompts.
   - Follow any additional instructions provided within the scripts for specific interactions.

##  Example Script: Slider Bar

### Description

The `slider_bar_example.m` script creates a simple interactive slider bar where users can adjust a value by dragging a handle with the mouse.

### Script Overview

1. **Initialize Psychtoolbox**: Opens a Psychtoolbox window for displaying the interactive elements.
2. **Draw Interactive Elements**: Creates and displays the slider bar and handle.
3. **Main Loop**: Listens for mouse input and updates the handle's position based on user interaction.
4. **Exit Condition**: Allows exiting the script with the 'ESCAPE' key.
5. **Cleanup**: Closes the Psychtoolbox window and performs cleanup.

### Example Code

Here’s a snippet from the `slider_bar_example.m` script:

```matlab
% Initialize Psychtoolbox
Screen('Preference', 'SkipSyncTests', 1);
[window, windowRect] = Screen('OpenWindow', 0, [255 255 255]);

% Slider parameters
sliderWidth = 400;
sliderHeight = 20;
sliderX = 100;
sliderY = 300;
sliderColor = [0 0 0];
handleColor = [255 0 0];
handleWidth = 30;

% Draw slider bar
rectSlider = [sliderX, sliderY - sliderHeight/2, sliderX + sliderWidth, sliderY + sliderHeight/2];
Screen('FillRect', window, sliderColor, rectSlider);
handleX = sliderX;
rectHandle = [handleX - handleWidth/2, sliderY - sliderHeight/2, handleX + handleWidth/2, sliderY + sliderHeight/2];
Screen('FillRect', window, handleColor, rectHandle);
Screen('Flip', window);

% Main loop
while true
    [mouseX, mouseY, buttons] = GetMouse(window);
    if buttons(1)
        if mouseY >= sliderY - sliderHeight/2 && mouseY <= sliderY + sliderHeight/2
            handleX = mouseX;
            handleX = max(sliderX, min(handleX, sliderX + sliderWidth));
            sliderValue = (handleX - sliderX) / sliderWidth;
            rectHandle = [handleX - handleWidth/2, sliderY - sliderHeight/2, handleX + handleWidth/2, sliderY + sliderHeight/2];
            Screen('FillRect', window, sliderColor, rectSlider);
            Screen('FillRect', window, handleColor, rectHandle);
            Screen('Flip', window);
        end
    end
    [keyIsDown, ~, keyCode] = KbCheck;
    if keyIsDown && keyCode(KbName('ESCAPE'))
        break;
    end
end

% Cleanup
Screen('CloseAll');
