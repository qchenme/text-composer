# Text-Composer
MIDI Sonification of text message (implemented based on MAX/MSP)

## Work flows and detailed design explaination
### 3 main sub-patchers
* Transfer: Take text input and transfer to ASCII numbers that within the range(0-127). Save all numbers to a message and then send it.
* Play: Receive the transferred numbers and play it. Has a sub-patcher Scale that takes the current note number and play the accompniment chosen based on that number.
* Drumbeat: It implemented 3 built-in beat styles. And it's independent from text message.
* There're 2 extra patchers that used to define some parameters:
** defscale: Load data into 3 built-in accompaniment scales.
** appendmsg: Append beat program number selection menu.

### Patcher-transfer
* Route: Textedit object sends text in front of whatever users typed. In order not to include it, using route to get rid of "text".
* atoi: Convert characters to ASCII numbers.
* select(32): Filter the space.
* If out of bound then subtract it by 127.
* send: Integrate to message and send it.

### Patcher-play
* Receive notes.
* zl slice(1): Slice notes into single number one by one.
* delay: Send the sliced single number after delaying a time that specified. The velocity of outputting the notes depends on delay time.
* If pitch shift is too high, then output 127.
* Pass current note to patcher scale(where liner accompaniment proceed).

### Patcher-drumbeat
* metro: Send bang regularly.
* gate: to open/close which beat style implementation.
* eceive corresponding beat program number to play.

## Possible improvement
* Randomization: Program number, Velocity, Pitch

* Link drumbeat to message, i.e., make it depends on the melody played and been able to automatically play the beat style and velocity that are harmonic with the melody.

* Key word system: *Weather: For example, key words like "windy, wind" will trigger wind sound. While "rain, rainy" will trigger rain sound.* *Emotion: Emotional words like "happy" will trigger a more dynamic beatstyle and corresponding suitable velocity. While "sad" will trigger more heavy sound.*
