Please direct your requests to info@arabicspellchecker.com.

You can use this demo token `TqMmyZEGGCEAmDdlfRLCbWnLGWZagACZ` to test the speller. It needs to be sent in the request headers, for example:
```
> POST /get_incorrect_words HTTP/1.1
> Host: api.arabicspellchecker.com
> Content-Type: multipart/form-data; boundary=X-BOUNDARY
> Token: TqMmyZEGGCEAmDdlfRLCbWnLGWZagACZ
> Accept: */*
> Content-Length: 1427
```


# API Endpoints

## POST /get_incorrect_words

Send a text to the server for spell checking.

**Payload:**

~~~~~~~~
text=text
~~~~~~~~~

**Response:**

A list of misspelled words in the text.

~~~~
{
  "outcome": "success",
  "data": [
    "العباسيية",
    "اقوي",
    "والأحمل",
    "الساس",
    "وانهو",
    "بنئها"
  ]
}
~~~~




------------------------------------

## POST /get_suggestions

Get suggestions for a given misspelled word.

**Payload:**

~~~~~~~~
word=missspelled
~~~~~~~~~

**Response:**

An array containing suggestions for the given word:

```
[
  "العباسة",
  "العباسيين",
  "العباسيون",
  "العباسية",
  "للعباسيين",
  "والعباسية",
  "العباية",
  "العباسيات",
  "العباسيي",
  "العباسين",
  "العبسية",
  "والعباسيين",
  "العباسيان",
  "للعباسية",
  "لعباسية",
  "العبسيين"
]
```



----------------------------

## POST /accept_suggestion

Marks a certain suggestion as correct.

**Payload:**

~~~~~~~~
word=ينتسبون
~~~~~~~~~

**Response:**

```
{
  "outcome": "done"
}
```





------------------------------------

## POST /spellcheck

Spell checking in one shot: mark misspelled words and produce suggestions in one request. Can take longer than the two step approach, i.e calling `get_incorrect_words` first and then calling `get_suggestions` for each word individually.

**Payload:**

~~~~~~~~
text=ينتسبون
~~~~~~~~~

**Response:**

A list of misspelled words in the text with their correction suggestions.

```
{
  "العباسيية": [
    "العباسة",
    "العباسيين",
    "العباسيون",
    "العباسية"
  ],
  "اقوي": [
    "أقوى",
    "وقوى",
    "ياقوت",
    "لقوى"
  ],
  "والأحمل": [
    "والأحوال"
  ],
  "الساس": [
    "اليأس",
    "الشاي",
    "إلياس",
    "السوي"
  ],
  "وانهو": [
    "وهو",
    "وأنها"
  ],
  "بنئها": [
    "بها",
    "بينها",
    "ابنها",
    "بنيه"
  ]
}
```




------------------------------------

## POST /add_correction

Adds a new entry to the server to update the dictionary and the error model.

**Payload:**

~~~~~~~~
error=missspelled&crror=misspelled
~~~~~~~~~

**Response:**

```
{
  "outcome": "done"
}
```

