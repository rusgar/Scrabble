# Scrabble

- Texto de análisis
- Analizar el texto

Primero usaremos nuestra propia herramienta de análisis hecha en casa, luego usaremos una biblioteca de python llamada `TextBlob` para usar algunas herramientas de análisis integradas.


## ¡Scrabble!
<img src="Imagen/Scrabble_game.jpg" width="800" height="380">


Scrabble es un juego popular en el que los jugadores intentan sumar puntos deletreando palabras y colocándolas en el tablero de juego. Usaremos Scrabble para calificar nuestro primer intento de análisis de texto. Esto demostrará los conceptos básicos de cómo funciona el análisis de texto.


## Puntuaremos las palabras o sustantivos

```python
name = "Eduardo"
print("La puntuación de mi nombre es:", scrabble_score(name))

La puntuación de mi nombre es: 9
```
o incluso comparando con otros sustantivos

```python
nombre_mascota = "Lila"
print("La puntuación del nombre de mi mascota es:",scrabble_score(nombre_mascota))

#¡Compara para ver cuál obtiene más puntos!
if scrabble_score(nombre_mascota) > scrabble_score(name):
    print("¡El nombre de mi mascota gana más puntos!")
else:
    print("Mi nombre obtiene más o igual cantidad de puntos que el nombre de mi mascota")
    
La puntuación del nombre de mi mascota es: 4
Mi nombre obtiene más o igual cantidad de puntos que el nombre de mi mascota
```

## Mas de lo sencillo empezaremos cargando bibliotecas

- [&nearr;&nbsp;pandas](https://pandas.pydata.org/)
- [&nearr;&nbsp;textblob](https://textblob.readthedocs.io/en/dev/)
- [&nearr;&nbsp;nltk](https://www.nltk.org/)
- [&nearr;&nbsp;requests](https://docs.python-requests.org/en/latest/)
- [&nearr;&nbsp;matpltolib](https://matplotlib.org/)
- [&nearr;&nbsp;BeautifulSoup](https://beautiful-soup-4.readthedocs.io/en/latest/)


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
## Texto o Coprus

![winnie_diario](https://raw.githubusercontent.com/rusgar/Scrabble/main/Imagen/winnie_diario.png)

Corpus es una forma elegante de decir el texto que vamos a ver. Limpiar un corpus y prepararlo para el análisis es una gran parte del proceso, una vez hecho esto, el resto es fácil. Para nuestro ejemplo, vamos a ver algunas entradas del [&nearr;&nbsp;Diario](https://dr.library.brocku.ca/handle/10464/7282) de Winnie Beam. La siguiente celda cargará este corpus en un marco de datos de Pandas y nos mostrará algunos enteros.

```python
winnie_corpus = pd.read_csv('winnie_corpus.txt', header = None, delimiter="\t")
winnie_corpus.columns = ["Pagina","Dia","Texto"]
winnie_corpus['Dia'] = pd.to_datetime(winnie_corpus['Dia'])
winnie_corpus['Texto'] = winnie_corpus.Texto.astype(str)

#vista previa de nuestras entradas principales
winnie_corpus.head()
```

## Midiendo el Sentimiento

Podemos analizar el `sentimiento`del texto (más [detalles](https://planspace.org/20150607-textblob_sentiment/).), Las frases para ver realmente un buen funcionamiento tienen que estar en Ingles, la siguiente celda demuestra esto:

```python
feliz_sentence = "Python is the best programming language ever!"
triste_sentence = "Python is difficult to use, and very frustrating"


print("Sentimiento de frase feliz ", TextBlob(feliz_sentence).sentiment)
print("Sentimiento de triste frase ", TextBlob(triste_sentence).sentiment)

# polarity oscila entre -1 y 1.
# la subjectvity va de 0 a 1.
Sentimiento de frase feliz  Sentiment(polarity=1.0, subjectivity=0.3)
Sentimiento de triste frase  Sentiment(polarity=-0.51, subjectivity=1.0)
```

Con esto podemos agregar los sentimientos a un texto, corpus, diario...etc, ademas concluimos que en cada sentencia, frase o incluso para las frases por cada palabra

# Generador automático de palabras clave

Un buen uso de la identificación de frases nominales es crear automáticamente palabras clave para una colección de obras en su corpus. La estructura básica es así:

1. Leer cada documento en su corpus

2. Identificar cada frase nominal en sus documentos

3. Las NP que más aparecen son las palabras clave de tu documento

Vamos a ver el libro [&nearr;&nbsp;El Príncipe](https://en.wikipedia.org/wiki/The_Prince) (Puede modificar la línea 4 para descargar un libro diferente, solo elija el texto completo [&nearr;&nbsp;Guttenberg](https://www.gutenberg.org/) URL de la variable.)

```python
keywords = dict()

#Podemos reemplazar con cualquier libro sobre Gutenberg,
BOOK_URL = "https://www.gutenberg.org/ebooks/5201.txt.utf-8"


#Estamos usando una biblioteca llamada `requests` para descargar el libro (https://realpython.com/python-requests/)
print("Descargando libro...")
book = requests.get(BOOK_URL)

#Convertimos el texto del libro en blob de texto
book_blob = TextBlob(book.text)

print("Identificamos las frases nominales y construimos un diccionario de frecuencias...")

#Buscamos todas las frases nominales
for np in book_blob.noun_phrases:
    if np in keywords:
        keywords[np] += 1
    else:
        keywords[np] = 1

        
#Ordenamos el diccionario e imprimimos las 20 entradas principales
print("Nombres o sustantivos más comunes son ...")

for np in sorted(keywords, key=keywords.get, reverse=True)[0:20]:
    print(np, keywords[np])

```

Con esto sacamos la entradas principales de un libro, si a todo esto lo analizamos a nuestro corpus o diario,podemos incluso analizarlo por fechas sea diario o mensual, saber que palabras o sustantivos utilizo cada dia o cada mes.
Si vamos mas alla, lo podemos extrapolar no solo a un libro sino a una direccion de url de cualquier periodico o hacer prediciones de sentimientos de redes sociales
