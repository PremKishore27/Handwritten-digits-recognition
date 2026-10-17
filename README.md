[README.md](https://github.com/user-attachments/files/33598302/README.md)
# ✍️ Handwritten Digit Recognition + Handwriting Calculator

Draw a digit with your mouse, let a neural network read it, and then use your own handwriting to do math.

This project started as a comparison of machine learning models on the **MNIST** dataset (**SVM**, **MLP** and **CNN**, compared on accuracy and execution time). It then grew into something more fun: a **Tkinter handwriting calculator** powered by a trained **Convolutional Neural Network**.

![Python](https://img.shields.io/badge/Python-3.7%2B-blue)
![Keras](https://img.shields.io/badge/Keras-TensorFlow-red)
![Dataset](https://img.shields.io/badge/Dataset-MNIST-green)
![GUI](https://img.shields.io/badge/GUI-Tkinter-orange)

<!-- Add a screenshot or GIF of the calculator here -->
<!-- ![Demo](docs/demo.gif) -->

---

## 🎯 What it does

- Trains a CNN on the 60,000 MNIST training images when the script starts
- Opens a small window with a canvas where you **draw digits with your mouse**
- Predicts each digit you draw (0–9)
- Lets you chain digits into multi-digit numbers (draw `1`, then `2`, to get `12`)
- Applies **add, subtract, multiply or divide** to two handwritten numbers and shows the answer

---

## 🧠 How it works

The pipeline follows the stages from the project report:

1. **Pre-processing**: MNIST images are reshaped to `28×28×1` and normalised to the `0–1` range.
2. **Feature extraction**: the convolution and pooling layers learn the features automatically.
3. **Classification**: a dense softmax layer outputs one of 10 classes.
4. **GUI**: your drawing is captured from the canvas, resized to 28×28, converted to grayscale and passed to the model.

### CNN architecture

| Layer | Details |
|---|---|
| Conv2D | 32 filters, 3×3 kernel |
| MaxPool2D | 2×2 |
| Activation | ReLU |
| Flatten | |
| Dense | 128 units, ReLU |
| Dense | 10 units, softmax |

**Training setup:** Adam optimizer, categorical cross-entropy loss, batch size 32, 2 epochs, 30% validation split.

---

## 📊 Model comparison (SVM vs MLP vs CNN)

The goal of the research part was to find the best model for digit recognition by comparing:

| Model | Type |
|---|---|
| Support Vector Machine (SVM) | Classical machine learning |
| Multi-Layer Perceptron (MLP) | Neural network |
| Convolutional Neural Network (CNN) | Deep learning |

They were compared on **accuracy** and **execution time**, with plots built in matplotlib. The full write-up is in the project report in this repo.

---

## 🚀 Getting started

### 1. Clone the repo

```bash
git clone https://github.com/<your-username>/Handwritten-digits-recognition.git
cd Handwritten-digits-recognition
```

### 2. Install dependencies

```bash
pip install tensorflow numpy pandas matplotlib pillow
```

Tkinter ships with Python on Windows and macOS. On Debian/Ubuntu install it with:

```bash
sudo apt-get install python3-tk
```

### 3. Run it

```bash
python handwriting_calculator.py
```

The model trains first (it takes a short while), then the calculator window opens.

> 💡 The original code was written in a Jupyter notebook (it uses `%matplotlib inline`). If you run it as a plain `.py` file, delete the two `%` lines.

---

## 🧮 How to use the calculator

1. Draw a digit in the gray square, holding the left mouse button.
2. Click **Save image**. The predicted digit appears below the buttons.
3. Repeat for every digit of the first number (for `23`, draw `2`, save, then `3`, save).
4. Click an operation: **Add**, **Subtract**, **Multiply** or **Divide**.
5. Draw and save the digits of the second number.
6. Click **=** to see the result.

Other buttons:

- **Click here if the number is not correct** removes the last prediction so you can redraw it
- **Reset** clears everything and starts over

**Tips for better results:** draw one digit at a time, make it big and centred in the canvas, and use a thick, clear stroke, similar to MNIST digits.

---

## 🗂️ Project structure

```
.
├── README.md
├── handwriting_calculator.py        # CNN training + Tkinter GUI
└── handwritten_digit_recognition.docx   # Full project report
```

---

## 🛠️ Tech stack

- **Python**
- **TensorFlow / Keras**: CNN model
- **NumPy, Pandas**: data handling
- **Matplotlib**: visualisation of model comparison
- **Pillow (PIL)**: turning the canvas drawing into a 28×28 image
- **Tkinter**: GUI
- **MNIST**: dataset

---

## ⚠️ Known limitations

- The calculator handles **one operation on two numbers** at a time.
- Division by zero is not handled yet.
- Accuracy depends on your drawing style. Real handwriting on a mouse canvas looks different from MNIST samples.
- The model is retrained on every launch. Saving it with `model.save()` and loading it next time would make startup much faster.

---

## 🔧 Troubleshooting

**`ModuleNotFoundError: keras.utils.np_utils`**
Newer Keras versions moved this. Replace

```python
from keras.utils.np_utils import to_categorical
```

with

```python
from tensorflow.keras.utils import to_categorical
```

If other `keras` imports fail, switch them to `tensorflow.keras` in the same way.

---

## 🔮 Future improvements

- Save and load the trained model
- Support more than two numbers and chained operations
- Handle multiple digits drawn on one canvas using segmentation
- Add data augmentation for more robust recognition
- Try deeper architectures such as LeNet-5 or ResNet-style CNNs
- Evaluate on harder handwriting datasets

---

## 👥 Authors

**Ramprasad D** and **Prem Kishore V**
B.Tech Information Technology, St. Joseph's College of Engineering (Anna University, Chennai), 2022

Supervised by **Dr. G. Manikandan**.

---

## 📚 References

- Dixit, Kushwah, Pashine: *Handwritten Digit Recognition using Machine and Deep Learning Algorithms*, 2021
- Shamim et al.: *Handwritten Digit Recognition using Machine Learning Algorithms*, GJCST, 2018
- Abu Ghosh, Maghari: *A Comparative Study on Handwriting Digit Recognition Using Neural Networks*, ICPET, 2017
- Li et al.: *Handwritten Digit Recognition System Based on Convolutional Neural Network*, AEECA, 2020

The full list is in the project report.

---

⭐ If you had fun with this, drop a star on the repo!
