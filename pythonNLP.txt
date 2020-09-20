
# coding: utf-8

# NLP Task




# Common imports
from bs4 import BeautifulSoup
import lxml
import requests
import pandas as pd
import numpy as np
import html as ihtml
import re
import urllib.request

from textblob import TextBlob



# Using TextBlob to tokenise Arabic text from:
# 1. Modern Standard Arabic: https://ar.wikipedia.org/wiki/%D9%84%D9%87%D8%AC%D8%A9_%D9%85%D8%B5%D8%B1%D9%8A%D8%A9)
# 2. Dialect Egyptian Arabic: https://arz.wikipedia.org/wiki/%D8%A7%D9%84%D9%84%D8%BA%D9%87_%D8%A7%D9%84%D9%85%D8%B5%D8%B1%D9%8A%D9%87_%D8%A7%D9%84%D8%AD%D8%AF%D9%8A%D8%AB%D9%87)




standard_arabic = "https://ar.wikipedia.org/wiki/%D9%84%D9%87%D8%AC%D8%A9_%D9%85%D8%B5%D8%B1%D9%8A%D8%A9"
egyptian_dialect = "https://arz.wikipedia.org/wiki/%D8%A7%D9%84%D9%84%D8%BA%D9%87_%D8%A7%D9%84%D9%85%D8%B5%D8%B1%D9%8A%D9%87_%D8%A7%D9%84%D8%AD%D8%AF%D9%8A%D8%AB%D9%87"
base_url = requests.get('https://ar.wikipedia.org/wiki/%D9%84%D9%87%D8%AC%D8%A9_%D9%85%D8%B5%D8%B1%D9%8A%D8%A9', timeout=5)

standard_arabic_text = requests.get(standard_arabic).text
egyptian_dialect_text = requests.get(egyptian_dialect).text





# Tokenising
standard_arabic_blob = TextBlob(standard_arabic_text)
standard_arabic_words = standard_arabic_blob.words
standard_arabic_sentences = standard_arabic_blob.sentences

egyptian_dialect_blob = TextBlob(egyptian_dialect_text)
egyptian_dialect_words = egyptian_dialect_blob.words
egyptian_dialect_sentences = egyptian_dialect_blob.sentences

print("Standard Arabic words:\n**********************\n", standard_arabic_words)





print("Standard Arabic sentences:\n**************************\n", standard_arabic_sentences)




# Removing HTML tags
def clean_text(text):
    text = BeautifulSoup(ihtml.unescape(text)).text
    text = re.sub(r"http[s]?://\S+", "", text)
    text = re.sub(r"\s+", " ", text)   
    return text




cleaned_standard_arabic_text = clean_text(standard_arabic_text)
print(cleaned_standard_arabic_text)

cleaned_egyptian_dialect_text = clean_text(egyptian_dialect_text)
print(cleaned_egyptian_dialect_text)



# Tokenising cleaned text
cleaned_standard_arabic_blob = TextBlob(cleaned_standard_arabic_text)
cleaned_standard_arabic_words = cleaned_standard_arabic_blob.words
cleaned_standard_arabic_sentences = cleaned_standard_arabic_blob.sentences

cleaned_egyptian_dialect_blob = TextBlob(cleaned_egyptian_dialect_text)
cleaned_egyptian_dialect_words = cleaned_egyptian_dialect_blob.words
cleaned_egyptian_dialect_sentences = cleaned_egyptian_dialect_blob.sentences

print("Standard Arabic words:\n**********************\n", cleaned_standard_arabic_words)




from nltk.corpus import stopwords
cleaned_standard_arabic_words_list = [word for word in cleaned_standard_arabic_blob.words if word not in stopwords.words('arabic')]
cleaned_standard_arabic_words_list_joined = ' '.join(cleaned_standard_arabic_words_list)
cleaned_standard_arabic_blob_no_stop_word = TextBlob(cleaned_standard_arabic_words_list_joined)
print(cleaned_standard_arabic_blob_no_stop_word)




blob.detect_language()


# Add part of speech tags and Named Entity Recognition tags to the extracted text (make sure the taggers work with Arabic language, don’t worry if they are not suitable for Egyptian they’ll still run).




cleaned_standard_arabic_with_tags = cleaned_standard_arabic_blob_no_stop_word.tags
print(cleaned_standard_arabic_with_tags)
