---
layout: post
title: Word Master
subtitle: Finding more about a word via a Python script
show-avatar: false
bigimg: /img/wordmaster.png
share-img: /img/wordmaster.png
gh-repo: bidyutchanda/WordMaster
gh-badge: [star, fork, follow]
tags: [python,word,nlp,nltk,textblob,etymology]
---

## Story behind this project

First things first, for quite a long time now, my girlfriend and I have been obsessing over languages, words, their histories and roots.

And we found ourselves neck-deep in the search for the meanings of unknown and strange words, reading blogs about the most beautiful words from diverse languages, racking our brains over the mind-boggling stories each of these trace back to (we found the word _komorebi_ exceptionally beautiful, the meaning of which is for you to find out). We would spend hours on Google looking these up and translating them to English and back to their original languages and finding the roots of those words (A subject called etymology, which was an interesting find for me). Now, I will admit that doing these things in 2018 is so much easier than before, say 10 years ago. Translation is not such a pain now thanks to Google Translate and finding its meaning or its etymological roots has never been quicker and easier. But soon I became tired of these long searches for each word and devised something that would make my task easier, the description of which starts below. 

## Project Details

You can find the code for this project at GitHub [here](https://github.com/bidyutchanda/WordMaster) and can fork or star it from the buttons above. 

## Packages used  

All the packages used in this project are open-source and are available at PyPi.
* [NLTK](http://nltk.org) - Statistical natural language processing for English.
* [TextBlob](https://textblob.readthedocs.io/en/dev/) - For processing textual data.
* [ety](https://github.com/jmsv/ety-python) - To analyse etymologies of text written by various historical authors.

## Working of the script

The code opens with the import statements to import all the packages which I have used for this. 

```javascript
from textblob import TextBlob
from datetime import datetime
from nltk.corpus import wordnet
import ety
```

A dictionary of language code, language name pair is hard-coded for reference and a word and a choice integer (for displaying the meaning or translating it) is asked from the user.

I, now, use TextBlob to feed the word into it and detect the language from it. 

```javascript
toTB="" 
toTB=TextBlob(word)
toTB_lang=toTB.detect_language()
```

Wordnet from NLTK is used to tell the meaning of the word, which is first translated to English, if a word in some other language was entered in the first place. 

```javascript
syns = wordnet.synsets(word)
print(syns[0].definition()) 
```

Now comes the translation part. The challenge here I faced is an user won't know the ISO code of a language and while asking the name of a language into which to translate in, I get a language name whereas TextBlob needs a language code for translation. So, I wrote a function explicitly for this into which the dictionary which I had previously hardcoded was fed and any language name inputted returns the language code for it. 

```javascript
def langCode_to_lang(list,langName):
	return [langCode for langCode,toLang in list.iteritems() if toLang 
        == langName]
```

The word is translated to the desired language via :

```javascript
langCode=langCode_to_lang(langcodes,toLang) 
toTB.translate(to=langCode[0])
```

At the end, whatever the choice of the user be, the etymological roots of a word is displayed anyway. 

```javascript
ety.tree(word)
```

The GitHub page for this code, which I had linked earlier to this post, remains a better parallel explanation for this code. I will leave an embedded video for this project here, which shows the working of the whole thing live.


<p align="center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/ZZyOHoSNteY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>








