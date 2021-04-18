# clock
30 day JS Projects challenge

This project creates a simple clock.

This project helped me to learn and understand better:
1) transform-origin
2) Use case of creating unique cubic-bezier() 
3) DOM manipulation
4) Javascript coding

This project is not slated for any improvements and has 1 known bug in need of fixing. 
The bug is that upon the hands reaching 12 O'Clock there will be a transform event as the transform rotate reaches 90 and so resets itself.

A simple walkthrough and explanation of the code is below:

The three hand divs are stacked on top of one another. They will be rotated according to the time. By default, these div elements will rotate around their center. In order to move this center of rotation to the right side, like on a wall-clock, the transform-origin: 100% property is used. This transforms the origin of rotation according to the specifications (100% in this case which moves it completely from the center to the far right end).

Due to divs being block elements from left to right the divs will not start at the 12 O'Clock position. To fix this a transform: rotate(90deg) is used. At this point the three divs are still stacked on one another but they are each in the 12 O'Clock position and each rotating around their bottom ends because of transform origin. 

Lastly, to give the hands that familiar 'tick' where the hand moves slightly forward and then back on each movement, the transition timing function is used and a custom bezier function applied.
```CSS
    .hand {
      width: 50%;
      height: 6px;
      background: black;
      position: absolute;
      top: 50%;
      transform-origin: 100%;
      transform: rotate(90deg);
      transition: all .05s;
      transition-timing-function: cubic-bezier(0, 2.33, 1, 1)
      
      
    }
```

Now that the clock and hands are ready to go the JavaScript needs to be written. A function is created to find the current date and then parse it into seconds, minutes and hours. Then to use those values in order to calculate their equivalent degree out of a 360 degree circle. Once the degrees have been calculated they can be used to adjust the transform rotate property using a template literal.
```JavaScript
const secondHand = document.querySelector('.second-hand'); 
const minuteHand = document.querySelector('.min-hand');
const hourHand = document.querySelector('.hour-hand');
const hand = document.querySelector('.hand');
    
 function setDate(){
  const now = new Date();
  const seconds = now.getSeconds();
  const secondsDegrees = ((seconds / 60) * 360) + 90;

    secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
    

    const minutes = now.getMinutes();
    const minutesDegrees = ((minutes / 60) * 360) + 90;
    minuteHand.style.transform = `rotate(${minutesDegrees}deg)`;
    

    const hours = now.getHours();
    const hoursDegrees = ((hours / 12) * 360) + 90;
    hourHand.style.transform = `rotate(${hoursDegrees}deg)`;
  }
```

***End walkthrough
