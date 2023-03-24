# Gesture-Recognition-with-Arduino-Nano-33-BLE-Sense-for-Remote-Physiotherapy

![1](https://user-images.githubusercontent.com/102630199/227560566-71e4ce17-d34a-4a2b-91f9-737d4bdef638.PNG)

This project aims to provide a low-cost solution for remote physiotherapy sessions using an Arduino Nano 33 BLE Sense board to recognize gestures made by the user.
The board's onboard sensors, including the accelerometer, gyroscope, magnetometer, and proximity sensor, are used to capture the user's gestures, which are then processed by a machine learning algorithm to determine the corresponding action.

The project requires basic knowledge of Arduino programming and machine learning algorithms. The user needs to train the machine learning model using their own gestures, and the model will then recognize these gestures in real-time and provide the corresponding feedback.

The Arduino Nano 33 BLE Sense has a variety of onboard sensors meaning potential for some cool TinyML applications:

•	Voice – digital microphone

•	Motion – 9-axis IMU (accelerometer, gyroscope, magnetometer)

•	Environmental – temperature, humidity and pressure

•	Light – brightness, color and object proximity


Here's how to use the Gesture Recognition with Arduino Nano 33 BLE Sense for Remote Physiotherapy project:

## Requirements:

    Arduino Nano 33 BLE Sense board
    USB cable
    Arduino IDE
    Python environment with scikit-learn, numpy, and pandas libraries
    Gesture dataset (images and labels) for training the model
    Computer or laptop with Bluetooth capability

## Installation:

    Clone the project repository to your local machine.
    Install the Arduino IDE and Python environment on your computer.
    Connect the Arduino Nano 33 BLE Sense board to your computer via the USB cable.
    Open the Arduino IDE and load the GestureRecognition.ino sketch from the Arduino directory.
    Upload the sketch to the board.
    Open the gesture_recognition.py script from the Python directory in your Python environment.
    Train the machine learning model using the gesture dataset by running the train_model() function.
    Connect the Arduino Nano 33 BLE Sense board to your computer via Bluetooth.
    Run the gesture_recognition() function to start recognizing gestures.
    
## Procedure

## Streaming Sensor Data From the Arduino Board

First, we needed to capture some training data. We captured sensor data logs from the Arduino board over the same USB cable you use to program the board with the laptop or PC.

Arduino boards run small applications (also called sketches) which are compiled from .ino format Arduino source code, and programmed onto the board using the Arduino IDE or Arduino Create. 


With the sketch we created we did the following:

•	Monitor the board’s accelerometer and gyroscope 

•	Trigger a sample window on detecting significant linear acceleration of the board 

•	Sample for one second at 119Hz, outputting CSV format data over USB 

•	Loop back and monitor for the next gesture


## Visualizing Live Sensor Data Log From the Arduino Board

With that done we can now visualize the data coming off the board. We’re not capturing data yet this is just to give you a feel for how the sensor data capture is triggered and how long a sample window is. This will help when it comes to collecting training samples.

•	In the Arduino IDE, open the Serial Plotter Tools > Serial Plotter 

•	Pick up the board and practice your punch ,flex, slash, stab and upper gestures.

•	You’ll see it only sample for a one second window, then wait for the next gesture

•	You should see a live graph of the sensor data capture (see Image below)

![22](https://user-images.githubusercontent.com/102630199/227561275-ab002b38-5769-4020-90f1-c2c0b2431e51.PNG)


## Capturing Gesture Training Data

To capture data as a CSV log to upload to TensorFlow, we used Arduino IDE > Tools > Serial Monitor to view the data and export it to your desktop machine:

•	Reset the board by pressing the small white button on the top

•	Pick up the board in one hand (picking it up later will trigger sampling)

•	In the Arduino IDE, open the Serial Monitor Tools > Serial Monitor

•	If you get an error that the board is not available, reselect the port:

•	Tools > Port > portname (Arduino Nano 33 BLE) [This issue was encountered previously hence was easily detected and fixed]!

•	Make a punch gesture with the board in your hand (Be careful whilst doing this!)

•	Make the outward punch quickly enough to trigger the capture

•	Return to a neutral position slowly so as not to trigger the capture again 

•	Repeat the gesture capture step 10 or more times to gather more data

•	Copy and paste the data from the Serial Console to new text file called punch.csv 

•	Clear the console window output and repeat all the steps above, this time with a flex gesture in a file called flex.csv 

•	Make the inward flex fast enough to trigger capture returning slowly each time

Note: the first line of your two csv files should contain the fields aX,aY,aZ,gX,gY,gZ.

![trainingData](https://user-images.githubusercontent.com/102630199/227561652-43025d0a-8d19-4ba8-b24e-e2d522fbbcd7.png)


## Training in TensorFlow
We employed Google Colab to train our machine learning model using the data we collected from the Arduino board in the previous section. Colab provides a Jupyter notebook that allows us to run our TensorFlow training in a web browser.

            Step 1: Set up the Python Environment
            Step 2: Upload the Data
            Step 3: Graph Data (Optional)

![image](https://user-images.githubusercontent.com/102630199/227561987-4fff1d9e-8be4-4cb6-8ec2-1afbc676dc5d.png)


![image](https://user-images.githubusercontent.com/102630199/227562083-d2479692-3818-441a-b581-c9b795f80257.png)


![image](https://user-images.githubusercontent.com/102630199/227562281-3d08a9eb-2dc2-4d32-bd9d-451876388024.png)

            Step 4: Build and Train the neural Network
            Step 5: Parse and prepare the data
            Step 6: Randomize and split the input and output pairs for training
            Step 7: Build & Train the Model
            Step 8: Verify
            Step 9: Convert the Trained Model to Tensor Flow Lite
            Step 10: Encode the Model in an Arduino Header File
            Step 11: Classifying IMU Data
            Step 12: Classifying IMU Data
            
            

## Errors

![image](https://user-images.githubusercontent.com/102630199/227565976-32f42421-ae9b-4ddc-a237-8382c7dde9f6.png)


•	The error was due to the absence of the in-built Arduino_TensorFlowLite library. Using any of the alternative libraries such as Adafruit_TensorFlow_Lite, tensorflow_lite, TensorFlowLite_ESP32, EloquentTinyML. gave the Compilation error: TensorFlowLite.h: No such file or directory.
•	Also using Arduino_TensorFlowLite-2.4.0-ALPHA-precompiled library worked for other machine learning projects such as the magic wand but failed for the gesture recognition due to undefined reference to DebugLog error


## Possible Solutions

Through vigorous searches and research, we finally found a library that gives no errors whatsoever and fully supports the Arduino Nano 33 	BLE Sense: Ameba_TensorFlowLite

Given in the link below:

https://github.com/ambiot/ambd_arduino/blob/master/Arduino_zip_libraries/Ameba_TensorFlowLite.zip

Addition of Emoji Buttons

Errors
After attempting to run the code we were unduly faced with several different errors including void setup and loop errors due to numerous conflictions between the IMU_Classifier and Emoji_Button code and hence another method/OS had to be employed.


NOTE
After running several tests and compiling different codes, we concluded that there were no issues whatsoever with the precompiled library (Ameba TensorFlow lite). Hence this meant that the issue(s) faced were solely from the Operating Systems used (MAC and Linux).


Errors and Project Setbacks for Linux OS
After hours of debugging, research and generally working with Ubuntu on a virtual machine platform, we came to an abrupt conclusion that using such methods were not feasible for the said project!

Possible Solutions
•	Using the Windows OS, we managed to “manually” insert various emojis using the in-built emojis in Windows by inserting them at the appropriate places within the code.


The final results are shown below!

![image](https://user-images.githubusercontent.com/102630199/227567302-2d2aedb8-85df-4cb3-8413-88f0756dd1b5.png)


## EXPORTING DATA FROM ARDUINO SERIAL MONITOR TO A CSV OR TXT FILE

Data Streamer is a two-way data transfer for Excel that streams live data from a microcontroller into Excel, and sends data from Excel back to the microcontroller.
To get data from a sensor into an Excel workbook, connect the sensor to a microcontroller that is connected to a Windows 10 PC or Windows 11 PC. Excel’s Data Streamer add-in also needs to be enabled, and a workbook needs to be opened.  
Classrooms can be modernized with live data to transform how students model modern scientific and engineering practices.  
Excel’s Data Streamer add-in supports capturing, visualizing, and analyzing real-time sensor data in Excel.   
Data Streamer empowers students with a simple way to move data from the physical world in-and-out of Excel’s powerful digital canvas. With a sensor, a microcontroller (Arduino), and Excel, Data Streamer introduces students to the worlds of data science and the internet of things (IoT).   

Note:

There are several mechanisms and applications that can be used to extract data from Arduino’s serial monitor to excel (as a csv file format). The simplest way is using a software that acts as a serial monitor and can save the data. The most commonly used is PuTTY.


Using PuTTY
Procedure
1.	Install putty:
sudo apt-get install putty putty-tools

2.	Run Putty.

![image](https://user-images.githubusercontent.com/102630199/227568114-e480b265-b42a-4d4f-8e86-449f86bf6d01.png)

3.	in Putty select serial and specify the right port:

4.	then on the left under session go to the logging. select the printable output. and then specify the right address and file name for the output file:

![image](https://user-images.githubusercontent.com/102630199/227568235-e511afde-f595-432a-84a6-3ec7e0691106.png)


5.Then everything in the terminal will be recorded to the file in a csv format.

![image](https://user-images.githubusercontent.com/102630199/227568406-b8903be7-adfb-454b-b066-80383dd7688f.png)


After extracting and saving the data using PuTTY, Excel can then be used to for several different applications

## Project Setbacks

• Directly connecting the Arduino Nano 33 Ble Sense to Excel via the Microsoft Data Streamer was not feasible as it does not support Nano boards mostly. The board is easily detected by the Excel data streamer but unfortunately does not obtain the data from the serial monitor. 

## Possible Solutions

Via a third-party apps such as PuTTY, we managed to both extract and save the data from the Arduino serial monitor to a csv file format that can be accessed by Excel for processing

## Result

![image](https://user-images.githubusercontent.com/102630199/227568634-a220a5b7-7fb0-44e5-80d7-bef0b916a1ae.png)


![image](https://user-images.githubusercontent.com/102630199/227568758-9c6b203d-95fc-44a4-88d8-21ecb24f766f.png)


## Usage:

    Put the Arduino Nano 33 BLE Sense board on your wrist or attach it to your body.
    Perform the gestures that you want to train the model with and record them using the board's sensors.
    Load the recorded gesture dataset into the train_model() function and run it to train the model.
    Connect the board to your computer via Bluetooth.
    Run the gesture_recognition() function to start recognizing your gestures in real-time.
    Use the recognized gestures to provide feedback during remote physiotherapy sessions.

## Troubleshooting:

    If the board fails to connect to your computer via Bluetooth, make sure that the Bluetooth connection is enabled on both devices and that the board is in pairing       mode.
    If the board is not recognizing your gestures, try adjusting the sensitivity of the sensors in the GestureRecognition.ino sketch.
    If the machine learning model is not accurately recognizing your gestures, try recording more training data and re-training the model.
    
## Project Setbacks

•	The gesture recognition project requires the use of two major libraries: Arduino_LSM9DS1 and Arduino_TensorFlowLite.

•	The first library had no known issues whatsoever. Unfortunately, the Arduino_TensorFlowLite library is no more available in any version of Arduino and hence we resulted to the use of Arduino Nano 33 BLE Sense board since Arduino Nano RP2040 is relatively new in the system, it still has some unresolved issues one of which is machine learning applications especially involving TensorFlow lite.

•	Hence Arduino Nano 33 BLE Sense board was employed in this project instead.


## Conclusion

Further development using tech gloves and other means of technology, one’s gestures can be accurately recognized and applied in areas like gyms and fitness as well as remote physiotherapy. 


## Credits:

This project was inspired by the Arduino Gesture Control Robot project by Dejan Nedelkovski. The machine learning model was trained using the scikit-learn library.

## References

[1] https://github.com/arduino/ArduinoTensorFlowLiteTutorials/

[2] https://docs.arduino.cc/tutorials/nano-33-ble-sense/get-started-with-machine-learning

[3]https://colab.research.google.com/github/arduino/ArduinoTensorFlowLiteTutorials/blob/master/GestureToEmoji/arduino_tinyml_workshop.ipynb#scrollTo=9J33uwpNtAku

[4] https://www.ardu-badge.com/Arduino_TensorFlowLite/zip

[5]https://github.com/ambiot/ambd_arduino/blob/master/Arduino_zip_libraries/Ameba_TensorFlowLite.zip

[6]https://github.com/arduino/ArduinoTensorFlowLiteTutorials/blob/master/GestureToEmoji/ArduinoSketches/Emoji_Button/Emoji_Button.ino

[7] https://blog.tensorflow.org/2019/11/how-to-get-started-with-machine.html

[8] https://thesecmaster.com/install-ubuntu-linux-on-vmware-workstation/

[9] https://github.com/don/tinyml-workshop/blob/master/exercises/exercise8.md

[10] https://github.com/don/tinyml-workshop/blob/master/exercises/exercise9.md

[11] https://forum.arduino.cc/t/how-to-export-data-from-arduino-serial-monitor-to-a-csv-or-txt-file/354651

[12] https://forum.arduino.cc/t/cant-get-arduino-nano-33-ble-senses-data-on-excel-data-streamer/886081/8

[13] https://forum.arduino.cc/t/cant-get-arduino-nano-33-ble-senses-data-on-excel-data-streamer/886081/17
 
[14] https://www.hackster.io/HackingSTEM/stream-data-from-arduino-into-excel-f1bede
 
[15] https://learn.microsoft.com/en-us/microsoft-365/education/data-streamer/connecting-serial-devices

[16] https://www.electromaker.io/project/view/export-data-from-arduino-to-excel-sheet

[17] https://nerdytechy.com/how-to-export-data-from-arduino-to-excel/


