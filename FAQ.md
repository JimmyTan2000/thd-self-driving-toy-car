# jetson-self-driving-toy-car

# Known Issues
1. Firefox does not seem to recognise the controller.
-   fixed by using Edge instead.  

2. Setting up pytorch on Jupyter brings "num_workers" Runtime Error.
- fixed by editing code in "Create data loaders to load data in batches" and changing "num_workers" from "4" to "0"  

3. Original notebooks "train_model" converts .pth file as zip instead.  
- fixed by editing code in "train_model" notebook under "Train Regression" last if-statement and adding a kawg at torch.save "torch.save(model.state_dict(), BEST_MODEL_PATH, _use_new_zipfile_serialization=False)"   

4. What is steeringkd?
- The KD value is the "derivative" value.
- Proportional gain ("steering gain" in notebook): Increases proportionally with how far away we are from our target
- Derivative gain ("steering kd" in notebook): Increases proportionally with how fast we're moving towards or away from our target. For example, if currently facing our target, but we know from the last sample that we're quickly turning right, KD would still tell us to turn left.  

KD is typically used to dampen the response, which might help with wobbliness. The issue is, that at certain frame rates, or because of "noise", KD can actually cause sharp jitters.  

5. Camera delays a lot alongside neural network processing.
- Change resolution and make camera fps LOWER. 
- First, check what resolution settings are allowed by typing in terminal "gst-launch-1.0 nvarguscamerasrc". 
- See "GST_ARGUS: Available Sensor modes :" 
- cd back to as Problem 6 (cd usr/local/lib/python3.6/dist-packages/jetbot-0.3.0-py3.6.egg/jetbot/camera) 
- edit camera.py using "sudo vim camera,py" 
- edit line from "# config" and set fps to 4, along with "self.value = np.empty((self.height, self.width, 4), dtype=np.uint8)" in __init__ function and save. 

6. Module not found error: qwiic in motor.py.
- You have installed the system from the wrong repository. Please refer to https://www.waveshare.com/wiki/JetBot_AI_Kit?Amazon and https://github.com/waveshare/jetbot  
- qwiic is a library that was installed on the Nvidia's repository, unfortunately not made available on Waveshare's jetbot model.  

7. Camera keeps crashing kernel. 
Possibility 1: Camera could be trying to initiate from wrong allowed settings. Check what settings are recommended for your sensor. (LEAST LIKELY)
    - First, check what resolution settings are allowed by typing in terminal "gst-launch-1.0 nvarguscamerasrc".
    - See "GST_ARGUS: Available Sensor modes :"
    - cd back to as Problem 6 (cd usr/local/lib/python3.6/dist-packages/jetbot-0.3.0-py3.6.egg/jetbot)
    - edit camera.py using "sudo vim camera,py"
    - change some parameters to the recommended. We will use width:1920 height:1080 fps:29 
    - edit line from "# config" and save  

Possibility 2: WRONG JETBOT VERSION. Jetbot directory needs to be downloaded from Waveshare and waveshare only! (MOST LIKELY)
    - follow link https://www.waveshare.com/wiki/JetBot_AI_Kit?Amazon step 5 to reconfigure the jetbot libraries. Skip the installation of rsync and notebook sync creation however if you are not starting from a reformated robot.  

8. Could not initialize camera.  Please see error trace.
- "sudo systemctl restart nvargus-daemon"
- test if camera is free by using "gst-launch-1.0 nvarguscamerasrc ! nvoverlaysink"  

9. Illegal instruction (core dumped)
- Numpy version problem. Type in terminal "pip3 install numpy==1.19.4"  