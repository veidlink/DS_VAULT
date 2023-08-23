## 📚 References 
- Tags :  [[Self-attention]]
- Links: те же, что в Self-attention

## ❓ Questions
- $W$ - что за матрица весов?

## 🔗 Related material

# Multi-head attention

В сети может быть много Self-attention'ов, никак не связанных между собой. Так в [[Bert]]. Это делается для того, чтобы каждый self-attention улавивал закономерности разного характера между словами.

К примеру: зависимость по лицу, по роду, по числу и т.д.

$Multi$-$head$ $atten = concat(at1, at2, ...at_{n})*W$
