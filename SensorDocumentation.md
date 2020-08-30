# OCR Sensor Documentation for Android 
## How I contributed
The initial theme of my project was drone related, but after a discussion with my mentor we decided to derived from the original theme to something simpler and more achievable over the course of the 3 months, but still camera related. The choice was to implement the OCR (optical character recognition) sensors to the Catroid, the Android version of [Pocket Code](https://play.google.com/store/apps/details?id=org.catrobat.catroid&hl=ro).
The choice was to use Google’s machine learning API [ML Kit](https://developers.google.com/ml-kit) as it has an ability to recognize and extract text from images.

As for the ending of the last coding period, I implemented 5 sensors:
-	“text from camera” sensor
-	“text block x from camera( block_number )” sensor
-	“text block y from camera( block_number )” sensor
-	“text block size from camera( block_number )” sensor
-	“number of text blocks” sensor

The “text block x from camera”, “text block y from camera, “text block size from camera” sensors are implemented as functions as they take an argument. The “block_number” parameter is used for choosing the text block and it takes values greater or equal than 1. Default is 1.

You can check out the pull request here: https://github.com/Catrobat/Catroid/pull/3734/files

When one of the sensors is used and a text appears in the image captured by the selected camera, it is detected and the text sensors take the values of the recognized text.

The text sensors are under the “Visual sensors” category. The previous "Face detection" category is renamed to the “Visual sensors” category. The place in the list of sensors stays the same. The text sensors are placed below the face detection sensors.
The text is detected in blocks which are grouped by the similarities (e.g., size). The text block consists of lines of text. Zero or more text blocks can be detected at once.

#### 1. “text from camera” sensor
The “text from camera” returns the complete detected text. The text is returned as the string value. This sensor is the first one in the Carotid app to return string, so to implement it I had to do such changes as overloading of the constructors and much more.
#### 2. “text block x from camera” sensor
The “text block x from camera” returns the x coordinate of center of the text block. The text block points coordinates are usually the coordinates of the point of the smallest square or rectangle that can be drawn around the text. So, my task with this sensor was to calculate the center coordinates of the text block using its point coordinates. My main problem this this was to change from the default screen coordinate system where (0, 0) point is in the upper left corner of the screen to the Pockset Code system where the (0, 0) point is in the center of the screen.
#### 3. “text block y from camera” sensor
The “text block y from camera” returns the y coordinate of center of the text block. The implementation is pretty much the same as for the X coordinate sensor.
#### 4. “text block size from camera” sensor
The “text block size from camera” returns the size of the text block. It takes values from 0 to 100 where 0 is when text block is far away, 100 is when the text block is directly in front of the camera, and covers the whole camera image (this is not precisely defined, but more or less so). 
#### 5. “number of text blocks” sensor
The "number of text blocks" is how many text blocks are currently seen. If no text is seen, the value is zero.
The sensors work with the front and rear camera, depending which one is selected. Default is the front camera (screen-side of the phone).

The behavior of the sensors is described in the user stories below:
-	When the camera moves over text, all the sensors change values.
-	When the camera moves towards or from text, the block size sensor value increases or decreases respectively and all the other sensors can change values if the text is wide and/or long.
-	When the camera turns away from text and no text is seen anymore, all the sensors change values to zero or the empty string. 
-	When there is no text to be seen from the camera, all the sensors set values to zero or the empty string.
## Other things I did
My first task was to create the CLT (Catrobat Language Test) for the “Send web request” brick. I wrote the ticket for it and created a Pocket Code script. My CLT didn’t end up merged as the whole part with all the CLT tests got relocated and changed, so this task lost its priority, but still it was very interesting to work on this task.  Also, I did code reviews and wrote couple of Jira tickets for the different tasks. 
## What I’ll do next
As I'm planning to continue contributing to the Pocket Code after the end of the GSOC 2020 my next step will be to add another 2 OCR sensors using the ML Kit: the sensors for getting the text and language of the specified text block. Also, I’ll be additionally implementing the [Huawei API for the text recognition](https://developer.huawei.com/consumer/en/codelab/HiAIGeneralTextRecognition/index.html#0).
## What I learnt
-	To work with Git (pull requests, merge conflicts, rebasing)
-	Wo write tickets and create user stories
-	What doing the code review together is very cool!
-	Test Driven Development (TDD)
