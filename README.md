## Running Inference
- Install all the required Python dependencies:
```
pip install -r requirements.txt
```
- Download the weights file from [**here**](https://drive.google.com/file/d/1O2zmGIIHLX8SGs24W7mjRyFKvE_CSY8n/view?usp=sharing) and place it in the 'yolo' folder.

```
python run.py
```
***1. Real-Time alert:***
- If selected, we send an email alert in real-time. Use case: If the total number of violations (say 10 or 30) exceeded in a store/building, we simply alert the staff.
- You can set the max. violations limit in config (```Threshold = 15```).
- This is pretty useful considering the COVID-19 scenario.

> Note: To setup the sender email, please refer the instructions inside 'mylib/mailer.py'. Setup receiver email in the config.

***2. Threading:***
- Multi-Threading is implemented in 'mylib/thread.py'. If you ever see a lag/delay in your real-time stream, consider using it.
- Threading removes OpenCV's internal buffer (which basically stores the new frames yet to be processed until your system processes the old frames) and thus reduces the lag/increases fps.
- If your system is not capable of simultaneously processing and outputting the result, you might see a delay in the stream. This is where threading comes into action.
- It is most suitable for solid performance on complex real-time applications. To use threading:

set ```Thread = True``` in the config.

***3. People counter:***
- If enabled, we simply count the total number of people: set ```People_Counter = True``` in the config.

***4. Desired violations limits:***
- You can also set your desired minimum and maximum violations limits. For example, ```MAX_DISTANCE = 80``` implies the maximum distance 2 people can be closer together is 80 pixels. If they fell under 80, we treat it as an 'abnormal' violation (yellow).
- Similarly ```MIN_DISTANCE = 50``` implies the minimum distance between 2 people. If they fell under 50 px (which is closer than 80), we treat it as a more 'serious' violation (red).
- Anything above 80 px is considered as a safe distance and thus, 'no' violation (green).
