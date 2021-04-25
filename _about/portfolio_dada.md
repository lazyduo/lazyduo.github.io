---
title: "Dada's Portfolio"
date: 2021-04-08 23:02:00 +0800
---
This is Dada

```python
from universe import human
import datetime

class Dada:
  def __init__(self, **kwargs):
    self.name, self.year, self.sex = human.birth('Dada Ahn', 1992, 'M')
    self.weight = 4.2 # kg
    self.place = 'Seoul, Korea'
    self.talent = kwargs.get('parent's DNA', None)
    self.skill = ['cry']
    return
    
  def aging(self, year): 
    age = time.year - self.year
    
    if age < 8 :
      return
    elif age < 20 :
      self.learn('chemistry')
      
      
    


if __name__ == '__main__':
  dada = Dada()
  time = datetime.datetime.now()
  while (1):
    dada.aging(time.year)

```
