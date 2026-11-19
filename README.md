# Hand Gesture Recognition Interface

**🇬🇧 [English](#-english) | 🇸🇦 [العربية](#-العربية)**

---

## 🇬🇧 English

### Overview

A real-time computer vision system that recognizes hand signs and finger gestures from a webcam feed, using **Google MediaPipe** for hand landmark detection combined with lightweight neural network classifiers (MLP) for sign and gesture recognition.

This project adapts and localizes the open-source [hand-gesture-recognition-using-mediapipe](https://github.com/Kazuhito00/hand-gesture-recognition-using-mediapipe) project by Kazuhito Takahashi: the full codebase, comments, and training notebooks were translated to English, and the hand-sign and finger-gesture classification models were retrained.

![demo](https://user-images.githubusercontent.com/37477845/102222442-c452cd00-3f26-11eb-93ec-c387c98231be.gif)

### How It Works

1. MediaPipe detects 21 hand landmarks (key points) per hand from the webcam feed.
2. The landmark coordinates are preprocessed (normalized relative to the wrist and flattened).
3. A **hand sign classifier** (MLP, TFLite) predicts the static hand sign (e.g., open hand, closed fist, pointing) from the current frame's landmarks.
4. A **finger gesture classifier** (MLP, TFLite) predicts the dynamic gesture (e.g., stationary, clockwise, counter-clockwise, moving) from a short history of the index fingertip's position over time.
5. Both models can be retrained with new classes using the included Jupyter notebooks.

### Tech Stack

| Component | Technology |
|---|---|
| Hand Landmark Detection | Google MediaPipe |
| Classification Models | TensorFlow / Keras → TFLite (MLP) |
| Computer Vision | OpenCV |
| Language | Python |

### Getting Started

#### Requirements
- mediapipe 0.8.1
- OpenCV 3.4.2 or later
- TensorFlow 2.3.0 or later (tf-nightly 2.5.0.dev or later only if creating a TFLite LSTM model)
- scikit-learn 0.23.2 or later (only to display the confusion matrix)
- matplotlib 3.3.2 or later (only to display the confusion matrix)

#### Run the Demo

```bash
python app.py
```

Options:
- `--device` — camera device number (default: 0)
- `--width` / `--height` — camera capture resolution (defaults: 960 / 540)
- `--use_static_image_mode` — use MediaPipe's static image mode
- `--min_detection_confidence` — detection confidence threshold (default: 0.5)
- `--min_tracking_confidence` — tracking confidence threshold (default: 0.5)

### Project Structure

```
app.py                                 Inference demo + training-data collection
keypoint_classification.ipynb           Hand sign model training notebook
point_history_classification.ipynb      Finger gesture model training notebook
model/keypoint_classifier/              Hand sign training data, model, labels, inference module
model/point_history_classifier/         Finger gesture training data, model, labels, inference module
utils/cvfpscalc.py                      FPS measurement utility
```

### Training Your Own Gestures

Both the hand sign classifier and the finger gesture classifier can be retrained with new classes. The detailed step-by-step training guide (data collection, labeling, notebook training, model structure) is included in the **Technical Reference** section at the bottom of this file.

### Credits

- Based on [hand-gesture-recognition-using-mediapipe](https://github.com/Kazuhito00/hand-gesture-recognition-using-mediapipe) by Kazuhito Takahashi.
- [MediaPipe](https://mediapipe.dev/)

### Author

**Mohammad Molazem** — [GitHub](https://github.com/eng-molazem) · [LinkedIn](https://www.linkedin.com/in/mohammad-molazem/)

---

## 🇸🇦 العربية

### نظرة عامة

نظام رؤية حاسوبية يعمل في الزمن الحقيقي للتعرّف على إشارات اليد وحركات الأصابع من كاميرا الويب، باستخدام **Google MediaPipe** لكشف نقاط اليد المميّزة، مع مصنّفات شبكة عصبية خفيفة (MLP) للتعرّف على الإشارات والحركات.

هذا المشروع يُكيّف ويُعرّب مشروع [hand-gesture-recognition-using-mediapipe](https://github.com/Kazuhito00/hand-gesture-recognition-using-mediapipe) مفتوح المصدر لـKazuhito Takahashi: تُرجمت الشيفرة البرمجية الكاملة والتعليقات ودفاتر التدريب إلى الإنكليزية، وأُعيد تدريب نماذج تصنيف إشارات اليد وحركات الأصابع.

### آلية العمل

1. يكشف MediaPipe عن 21 نقطة مميّزة (Landmarks) لكل يد من تغذية الكاميرا.
2. تُعالَج إحداثيات النقاط مسبقاً (تطبيع نسبةً للمعصم وتحويلها لمتجه مسطّح).
3. **مصنّف إشارة اليد** (MLP, TFLite) يتنبأ بالإشارة الثابتة (يد مفتوحة، قبضة مغلقة، إشارة تأشير...) من نقاط الإطار الحالي.
4. **مصنّف حركة الأصابع** (MLP, TFLite) يتنبأ بالحركة الديناميكية (ثابت، باتجاه عقارب الساعة، عكس عقارب الساعة، متحرك) من تاريخ قصير لموقع طرف السبّابة عبر الزمن.
5. يمكن إعادة تدريب كلا النموذجين بفئات جديدة باستخدام دفاتر Jupyter المرفقة.

### البنية التقنية

| المكوّن | التقنية |
|---|---|
| كشف نقاط اليد | Google MediaPipe |
| نماذج التصنيف | TensorFlow / Keras → TFLite (MLP) |
| الرؤية الحاسوبية | OpenCV |
| اللغة | Python |

### التشغيل محلياً

#### المتطلبات
- mediapipe 0.8.1
- OpenCV 3.4.2 أو أحدث
- TensorFlow 2.3.0 أو أحدث (tf-nightly 2.5.0.dev أو أحدث فقط عند إنشاء نموذج LSTM بصيغة TFLite)
- scikit-learn 0.23.2 أو أحدث (فقط لعرض مصفوفة الالتباس)
- matplotlib 3.3.2 أو أحدث (فقط لعرض مصفوفة الالتباس)

#### تشغيل العرض التوضيحي

```bash
python app.py
```

الخيارات المتاحة:
- `--device` — رقم جهاز الكاميرا (افتراضي: 0)
- `--width` / `--height` — دقة التقاط الكاميرا (افتراضي: 960 / 540)
- `--use_static_image_mode` — استخدام وضع الصورة الثابتة في MediaPipe
- `--min_detection_confidence` — عتبة ثقة الكشف (افتراضي: 0.5)
- `--min_tracking_confidence` — عتبة ثقة التتبّع (افتراضي: 0.5)

### بنية المشروع

```
app.py                                 عرض الاستدلال التوضيحي + جمع بيانات التدريب
keypoint_classification.ipynb           دفتر تدريب نموذج إشارة اليد
point_history_classification.ipynb      دفتر تدريب نموذج حركة الأصابع
model/keypoint_classifier/              بيانات تدريب إشارة اليد، النموذج، التصنيفات، وحدة الاستدلال
model/point_history_classifier/         بيانات تدريب حركة الأصابع، النموذج، التصنيفات، وحدة الاستدلال
utils/cvfpscalc.py                      أداة قياس معدل الإطارات (FPS)
```

### تدريب إشارات جديدة

يمكن إعادة تدريب كل من مصنّف إشارة اليد ومصنّف حركة الأصابع بفئات جديدة. الدليل التفصيلي خطوة بخطوة للتدريب (جمع البيانات، التصنيف، التدريب عبر الدفاتر، بنية النموذج) موجود في قسم **المرجع التقني** أسفل هذا الملف.

### الإشادة والمصدر

- مبني على مشروع [hand-gesture-recognition-using-mediapipe](https://github.com/Kazuhito00/hand-gesture-recognition-using-mediapipe) لـKazuhito Takahashi.
- [MediaPipe](https://mediapipe.dev/)

### المطوّر

**محمد ملازم** — [GitHub](https://github.com/eng-molazem) · [LinkedIn](https://www.linkedin.com/in/mohammad-molazem/)

---

## 📖 Technical Reference (Detailed Training Guide, English)

# Requirements
* mediapipe 0.8.1
* OpenCV 3.4.2 or Later
* Tensorflow 2.3.0 or Later<br>tf-nightly 2.5.0.dev or later (Only when creating a TFLite for an LSTM model)
* scikit-learn 0.23.2 or Later (Only if you want to display the confusion matrix) 
* matplotlib 3.3.2 or Later (Only if you want to display the confusion matrix)

# Demo
Here's how to run the demo using your webcam.
```bash
python app.py
```

The following options can be specified when running the demo.
* --device<br>Specifying the camera device number (Default：0)
* --width<br>Width at the time of camera capture (Default：960)
* --height<br>Height at the time of camera capture (Default：540)
* --use_static_image_mode<br>Whether to use static_image_mode option for MediaPipe inference (Default：Unspecified)
* --min_detection_confidence<br>
Detection confidence threshold (Default：0.5)
* --min_tracking_confidence<br>
Tracking confidence threshold (Default：0.5)

# Directory
<pre>
│  app.py
│  keypoint_classification.ipynb
│  point_history_classification.ipynb
│  
├─model
│  ├─keypoint_classifier
│  │  │  keypoint.csv
│  │  │  keypoint_classifier.hdf5
│  │  │  keypoint_classifier.py
│  │  │  keypoint_classifier.tflite
│  │  └─ keypoint_classifier_label.csv
│  │          
│  └─point_history_classifier
│      │  point_history.csv
│      │  point_history_classifier.hdf5
│      │  point_history_classifier.py
│      │  point_history_classifier.tflite
│      └─ point_history_classifier_label.csv
│          
└─utils
    └─cvfpscalc.py
</pre>
### app.py
This is a sample program for inference.<br>
In addition, learning data (key points) for hand sign recognition,<br>
You can also collect training data (index finger coordinate history) for finger gesture recognition.

### keypoint_classification.ipynb
This is a model training script for hand sign recognition.

### point_history_classification.ipynb
This is a model training script for finger gesture recognition.

### model/keypoint_classifier
This directory stores files related to hand sign recognition.<br>
The following files are stored.
* Training data(keypoint.csv)
* Trained model(keypoint_classifier.tflite)
* Label data(keypoint_classifier_label.csv)
* Inference module(keypoint_classifier.py)

### model/point_history_classifier
This directory stores files related to finger gesture recognition.<br>
The following files are stored.
* Training data(point_history.csv)
* Trained model(point_history_classifier.tflite)
* Label data(point_history_classifier_label.csv)
* Inference module(point_history_classifier.py)

### utils/cvfpscalc.py
This is a module for FPS measurement.

# Training
Hand sign recognition and finger gesture recognition can add and change training data and retrain the model.

### Hand sign recognition training
#### 1.Learning data collection
Press "k" to enter the mode to save key points（displayed as 「MODE:Logging Key Point」）<br>
<img src="https://user-images.githubusercontent.com/37477845/102235423-aa6cb680-3f35-11eb-8ebd-5d823e211447.jpg" width="60%"><br><br>
If you press "0" to "9", the key points will be added to "model/keypoint_classifier/keypoint.csv" as shown below.<br>
1st column: Pressed number (used as class ID), 2nd and subsequent columns: Key point coordinates<br>
<img src="https://user-images.githubusercontent.com/37477845/102345725-28d26280-3fe1-11eb-9eeb-8c938e3f625b.png" width="80%"><br><br>
The key point coordinates are the ones that have undergone the following preprocessing up to ④.<br>
<img src="https://user-images.githubusercontent.com/37477845/102242918-ed328c80-3f3d-11eb-907c-61ba05678d54.png" width="80%">
<img src="https://user-images.githubusercontent.com/37477845/102244114-418a3c00-3f3f-11eb-8eef-f658e5aa2d0d.png" width="80%"><br><br>
In the initial state, three types of learning data are included: open hand (class ID: 0), close hand (class ID: 1), and pointing (class ID: 2).<br>
If necessary, add 3 or later, or delete the existing data of csv to prepare the training data.<br>
<img src="https://user-images.githubusercontent.com/37477845/102348846-d0519400-3fe5-11eb-8789-2e7daec65751.jpg" width="25%">　<img src="https://user-images.githubusercontent.com/37477845/102348855-d2b3ee00-3fe5-11eb-9c6d-b8924092a6d8.jpg" width="25%">　<img src="https://user-images.githubusercontent.com/37477845/102348861-d3e51b00-3fe5-11eb-8b07-adc08a48a760.jpg" width="25%">

#### 2.Model training
Open "[keypoint_classification.ipynb](keypoint_classification.ipynb)" in Jupyter Notebook and execute from top to bottom.<br>
To change the number of training data classes, change the value of "NUM_CLASSES = 3" <br>and modify the label of "model/keypoint_classifier/keypoint_classifier_label.csv" as appropriate.<br><br>

#### X.Model structure
The image of the model prepared in "[keypoint_classification.ipynb](keypoint_classification.ipynb)" is as follows.
<img src="https://user-images.githubusercontent.com/37477845/102246723-69c76a00-3f42-11eb-8a4b-7c6b032b7e71.png" width="50%"><br><br>

### Finger gesture recognition training
#### 1.Learning data collection
Press "h" to enter the mode to save the history of fingertip coordinates (displayed as "MODE:Logging Point History").<br>
<img src="https://user-images.githubusercontent.com/37477845/102249074-4d78fc80-3f45-11eb-9c1b-3eb975798871.jpg" width="60%"><br><br>
If you press "0" to "9", the key points will be added to "model/point_history_classifier/point_history.csv" as shown below.<br>
1st column: Pressed number (used as class ID), 2nd and subsequent columns: Coordinate history<br>
<img src="https://user-images.githubusercontent.com/37477845/102345850-54ede380-3fe1-11eb-8d04-88e351445898.png" width="80%"><br><br>
The key point coordinates are the ones that have undergone the following preprocessing up to ④.<br>
<img src="https://user-images.githubusercontent.com/37477845/102244148-49e27700-3f3f-11eb-82e2-fc7de42b30fc.png" width="80%"><br><br>
In the initial state, 4 types of learning data are included: stationary (class ID: 0), clockwise (class ID: 1), counterclockwise (class ID: 2), and moving (class ID: 4). <br>
If necessary, add 5 or later, or delete the existing data of csv to prepare the training data.<br>
<img src="https://user-images.githubusercontent.com/37477845/102350939-02b0c080-3fe9-11eb-94d8-54a3decdeebc.jpg" width="20%">　<img src="https://user-images.githubusercontent.com/37477845/102350945-05131a80-3fe9-11eb-904c-a1ec573a5c7d.jpg" width="20%">　<img src="https://user-images.githubusercontent.com/37477845/102350951-06444780-3fe9-11eb-98cc-91e352edc23c.jpg" width="20%">　<img src="https://user-images.githubusercontent.com/37477845/102350942-047a8400-3fe9-11eb-9103-dbf383e67bf5.jpg" width="20%">

#### 2.Model training
Open "[point_history_classification.ipynb](point_history_classification.ipynb)" in Jupyter Notebook and execute from top to bottom.<br>
To change the number of training data classes, change the value of "NUM_CLASSES = 4" and <br>modify the label of "model/point_history_classifier/point_history_classifier_label.csv" as appropriate. <br><br>

#### X.Model structure
The image of the model prepared in "[point_history_classification.ipynb](point_history_classification.ipynb)" is as follows.
<img src="https://user-images.githubusercontent.com/37477845/102246771-7481ff00-3f42-11eb-8ddf-9e3cc30c5816.png" width="50%"><br>
The model using "LSTM" is as follows. <br>Please change "use_lstm = False" to "True" when using (tf-nightly required (as of 2020/12/16))<br>
<img src="https://user-images.githubusercontent.com/37477845/102246817-8368b180-3f42-11eb-9851-23a7b12467aa.png" width="60%">

# Reference
* [MediaPipe](https://mediapipe.dev/)
