# Gesture-Recognition-with-Arduino-Nano-33-BLE-Sense-for-Remote-Physiotherapy

This project aims to provide a low-cost solution for remote physiotherapy sessions using an Arduino Nano 33 BLE Sense board to recognize gestures made by the user.
The board's onboard sensors, including the accelerometer, gyroscope, magnetometer, and proximity sensor, are used to capture the user's gestures, which are then processed by a machine learning algorithm to determine the corresponding action.

The project requires basic knowledge of Arduino programming and machine learning algorithms. The user needs to train the machine learning model using their own gestures, and the model will then recognize these gestures in real-time and provide the corresponding feedback.

Here's how to use the Gesture Recognition with Arduino Nano 33 BLE Sense for Remote Physiotherapy project:
Requirements:

    Arduino Nano 33 BLE Sense board
    USB cable
    Arduino IDE
    Python environment with scikit-learn, numpy, and pandas libraries
    Gesture dataset (images and labels) for training the model
    Computer or laptop with Bluetooth capability

Installation:

    Clone the project repository to your local machine.
    Install the Arduino IDE and Python environment on your computer.
    Connect the Arduino Nano 33 BLE Sense board to your computer via the USB cable.
    Open the Arduino IDE and load the GestureRecognition.ino sketch from the Arduino directory.
    Upload the sketch to the board.
    Open the gesture_recognition.py script from the Python directory in your Python environment.
    Train the machine learning model using the gesture dataset by running the train_model() function.
    Connect the Arduino Nano 33 BLE Sense board to your computer via Bluetooth.
    Run the gesture_recognition() function to start recognizing gestures.

Usage:

    Put the Arduino Nano 33 BLE Sense board on your wrist or attach it to your body.
    Perform the gestures that you want to train the model with and record them using the board's sensors.
    Load the recorded gesture dataset into the train_model() function and run it to train the model.
    Connect the board to your computer via Bluetooth.
    Run the gesture_recognition() function to start recognizing your gestures in real-time.
    Use the recognized gestures to provide feedback during remote physiotherapy sessions.

Troubleshooting:

    If the board fails to connect to your computer via Bluetooth, make sure that the Bluetooth connection is enabled on both devices and that the board is in pairing mode.
    If the board is not recognizing your gestures, try adjusting the sensitivity of the sensors in the GestureRecognition.ino sketch.
    If the machine learning model is not accurately recognizing your gestures, try recording more training data and re-training the model.

License:

This project is licensed under the MIT License. See the LICENSE file for more information.
Credits:

This project was inspired by the Arduino Gesture Control Robot project by Dejan Nedelkovski. The machine learning model was trained using the scikit-learn library.
