---
title: "Python 3 Text Encoding"
date: 2022-09-12T17:53:46+05:00
draft: false
categories: ["Python"]
---

## Why do we need text encoding?
Humans understand text, computers understand binary. Encoding is the process of converting human readable text into sequences of bytes and decoding is the reverse of that.

## Schemes to map characters to numbers (character codes)
To store, transmit and process characters digitally, the characters are mapped to integers, called code points. `ASCII` is one such scheme. In ASCII, each character is represented by a number from `0` to `127`. To represent that number in binary, only `7` bits are needed, but the downside is that we can only work with `128` characters/symbols at max.

`A` in ASCII:
`A <==> 65 (decimal) <==> 41 (hex) <==> 1000001`

`Unicode` scheme uses a much larger range of numbers from `0` to `1,114,111` for mapping, which means around `1.1` million characters can be represented using this scheme! 
The binary equivalent of a unicode character has variable length bits and not fixed 7 bits as ASCII does.

## Encodings

`UTF-8` is the defacto unicode to bytes conversion mechanism. It uses one to four bytes to represent unicode code points. To maintain backward compatability with ASCII, the first 128 characters has same bits representation as ASCII. 

Offcourse there are a lot more other encodings also e.g., `latin-1`, `UTF-16` etc

## Python 3 unicode and bytes
In Python 3, strings or text is a sequence of unicode code points and `utf-8` is the default source code encoding. 
```python
>>> city = 'São Paulo'
>>> city.encode('utf_8')  
b'S\xc3\xa3o Paulo'
>>> city.encode('utf_16')
b'\xff\xfeS\x00\xe3\x00o\x00 \x00P\x00a\x00u\x00l\x00o\x00'
>>> city.encode('iso8859_1')  
b'S\xe3o Paulo'
```

