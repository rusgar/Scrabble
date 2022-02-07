# Scrabble

- texto de análisis
- analizar el texto

Primero usaremos nuestra propia herramienta de análisis hecha en casa, luego usaremos una biblioteca de python llamada `TextBlob` para usar algunas herramientas de análisis integradas.

## ¡Scrabble!

![]("https://github.com/rusgar/Scrabble/blob/main/Imagen/Scrabble_game.jpg",width="350")

Scrabble es un juego popular en el que los jugadores intentan sumar puntos deletreando palabras y colocándolas en el tablero de juego. Usaremos Scrabble para calificar nuestro primer intento de análisis de texto. Esto demostrará los conceptos básicos de cómo funciona el análisis de texto.


## Puntuaremos las palabras o sustantivos

```python
name = "Eduardo"
print("La puntuación de mi nombre es:", scrabble_score(name))

La puntuación de mi nombre es: 9
```
o incluso comparando con otros sustantivos

## Mas de lo sencillo empezaremos cargando bibliotecas

```python
pip install textblob


from textblob import TextBlob

import pandas as pd
import nltk
from nltk.corpus import stopwords
import requests
import matplotlib.pyplot as plt
from bs4 import BeautifulSoup

nltk.download('stopwords')
nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')
nltk.download('brown')
nltk.download('wordnet')

```
