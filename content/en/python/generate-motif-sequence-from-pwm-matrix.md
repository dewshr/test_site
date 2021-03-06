---
title: "Generate Motif Sequence From Pwm Matrix"
date: 2020-05-12T23:24:14-05:00
description: generate motif sequence using position weight matrix from meme
author: Dewan Shrestha
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: inner
tocLevels: ["h2", "h3", "h4"]
tags:
- motif
- DNA
- sequence
series:
-
categories:
- python
image: images/feature3/code-file.png
---

<br/>

I am using PWM (Position Weight Matrix) file in meme format downloaded from [JASPAR database](http://jaspar.genereg.net/) as the input file. I am using random.choices from python to randomly generate the nucleotide motif sequence using the probability value for each position as weights.

```
import random


def generate_nucleotide(probability):
    if sum(probability) ==1:
        return random.choices(['A','C','G','T'], weights=probability)
    elif sum(probability) < 1:
        diff = 1 - sum(probability)
        index = probability.index(max(probability))
        probability[index] = probability[index] + diff
        return random.choices(['A','C','G','T'], weights=probability)
    else:
        diff = 1 - sum(probability)
        index = probability.index(max(probability))
        probability[index] = probability[index] - diff
        return random.choices(['A','C','G','T'], weights=probability)

pwm = open('tf_selected_pwm.txt','r').read().split('letter-')[1].split('\n')
pwm = list(filter(None, pwm))


motif = ''
for i in range(1, len(pwm)-1):
    p = [np.round(float(x),2) for x in pwm[i].split()]
    #print(p)
    motif = motif + generate_nucleotide(p)[0]
        
print(motif)
```

After running this, you will get something like this `TTGCCACCAGAGGGAGCTA`.






