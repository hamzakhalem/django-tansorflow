# Animal Classifier: Django + TensorFlow

A Django web app that recognises animals in photos. Upload a picture and a convolutional neural network trained with TensorFlow tells you if it's a cat, dog, monkey, parrot, elephant or bear.

Built by following the [Academy Omen tensored-django tutorial](https://github.com/Academy-Omen/tensored-django) (MIT licence).

## Features

- Upload a photo on the home page and get the predicted animal
- Six classes: cat, dog, monkey, parrot, elephant, bear
- A CNN built with Keras: three convolution layers and two max-pooling layers, then dense layers, on 50×50 colour images
- Scripts to build the dataset from your own image folders and train the model

## How it works

1. `CNN/load.py` reads the images from `CNN/data/<animal>/`, resizes them to 50×50 and saves them as `animals.npy` and `labels.npy`.
2. `CNN/train.py` trains the CNN on those arrays and saves it as `model.h5`.
3. The Django view resizes the uploaded photo the same way, loads `model.h5` and shows the class with the highest score.

## Built with

- Python 3, Django 4.0
- TensorFlow, Keras
- NumPy, OpenCV, Pillow

## Run it locally

```bash
git clone https://github.com/hamzakhalem/django-tansorflow.git
cd django-tansorflow
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
export DJANGO_SECRET_KEY="any-long-random-string"   # PowerShell: $env:DJANGO_SECRET_KEY="..."
```

The trained model isn't in the repo, so train it first. Put your images in `CNN/data/cat`, `CNN/data/dog`, `CNN/data/monkey`, `CNN/data/parrot`, `CNN/data/elephant` and `CNN/data/bear`, then:

```bash
python CNN/load.py
python CNN/train.py
```

Then start the app:

```bash
python manage.py migrate
python manage.py runserver
```

Open http://127.0.0.1:8000 and upload a photo.

## Project structure

```
CNN/         Dataset loader, training script and a standalone prediction script
core/        Django settings, URLs and the upload/predict view
templates/   Upload page
```
