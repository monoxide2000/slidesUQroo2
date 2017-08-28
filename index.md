---
title       : Introducción a R
subtitle    : Subindexado
author      : Julio César Ramírez Pacheco
job         : Universidad de Quintana Roo
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax,quiz, bootstrap, interactive] # {mathjax, quiz, bootstrap}
#ext_widgets : {rCharts: [libraries/nvd3, libraries/leaflet, libraries/dygraphs]}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
#logo        : unicaribelogo.jpeg
#biglogo     : unicaribelogo.jpeg
logo        : uqroo.png
biglogo     : uqroo.png
assets      : {assets: ../../assets}
---

<style type="text/css">
body {background:grey transparent;
}
</style>



## Subindexado en R
> - Los operadores de subindexado en `R` son rápidos y poderosos.
> - Conocer los diferentes operadores permite manipular los datos de manera precisa y eficiente.
> - En ocasiones es dificil de aprender porque se tiene que conocer a profundidad las estructuras de datos en `R`.
> - En esta lección aprenderemos
   > * Los tres operadores de subindexado.
   > * Los 6 tipos de subindexado.
   > * Los diferentes comportamientos de estos operadores en (vectores atómicos, listas, marices y `data.frames`).
   > * El uso del subindexado junto al de asignación.

--- .segue bg:grey

## Subindexado de vectores atómicos

---


## Subindexado de vectores atómicos

+ La mejor manera de aprender el **subindexado** es mediante los vectores atómicos y el operador `[`, el cual es el operador de subindexado más común.
+ Los vectores atómicos se pueden subindexar mediante:
 * Enteros positivos.
 * Enteros negativos.
 * Vectores lógicos.
 * Un elemento vacío.
 * Cero.
 * Vectores de carácteres.

--- .class #id 


## Subindexado (continuación): enteros positivos


```r
x <- c(2.1, 4.2, 3.3, 5.4)
x[1]
```

```
## [1] 2.1
```

```r
x[c(1,1,3)]
```

```
## [1] 2.1 2.1 3.3
```

```r
x[c(1.1,2.9,3.8)]
```

```
## [1] 2.1 4.2 3.3
```

--- .class #id 



## Subindexado (continuación): enteros negativos


```r
x <- c("uno","cuatro","veinte","treinta", "cero")
x[-3]
```

```
## [1] "uno"     "cuatro"  "treinta" "cero"
```

```r
x[-(1:3)]
```

```
## [1] "treinta" "cero"
```

```r
x[-1:3]
```

```
## Error in x[-1:3]: only 0's may be mixed with negative subscripts
```

--- .class #id 


## Subindexado (continuación): vectores lògicos


```r
x <- c("uno","cuatro","veinte","treinta", "cero")
x[T]
```

```
## [1] "uno"     "cuatro"  "veinte"  "treinta" "cero"
```

```r
x[c(T,T,F,F,F)]
```

```
## [1] "uno"    "cuatro"
```

```r
x[x=="uno"]
```

```
## [1] "uno"
```

--- .class #id 


## Subindexado (continuación): nada, cero, nombres


```r
x <- 1:4
x[]
```

```
## [1] 1 2 3 4
```

```r
x[0]
```

```
## integer(0)
```

```r
names(x) <-LETTERS[1:4]
x[c("A","B")]
```

```
## A B 
## 1 2
```

--- .segue bg:grey

## Subindexado de listas

---

## Subindexado de listas
- Las listas se pueden subindexar mediante los operadores `[`, `[[` y `$`.
- Las listas subindexadas mediante `[` siempre retornan una lista.
- Las listas subindexadas mediante `[[` permiten obtener los elementos de la lista.
- Las listas se pueden subindexar mediante el operador `$` siempre y cuando éstas tengan asociados nombres.
- A continuación veamos algunos ejemplos.

--- .class #id


## Subindexado de listas


```r
lista1 <- list(a=1:4, b=letters[1:9], list(a=1,b=TRUE,c="alpha"))
# Subindexado mediante `[`
str(lista1[2])
```

```
## List of 1
##  $ b: chr [1:9] "a" "b" "c" "d" ...
```

```r
# Subindexado mediante `[[`
str(lista1[[2]])
```

```
##  chr [1:9] "a" "b" "c" "d" "e" "f" "g" "h" "i"
```

```r
# Subindexado mediante `$`
str(lista1$b)
```

```
##  chr [1:9] "a" "b" "c" "d" "e" "f" "g" "h" "i"
```

--- .segue bg:grey


## Subindexado de matrices

---


## Subindexado de matrices
- Existen diversas maneras de subindexar una matriz en `R`.
- La manera más simple es proporcionar dos vectores, una por cada dimensión. Por ejemplo:

```r
a <- matrix(1:9, nrow = 3)
colnames(a) <- c("A", "B", "C")
a[c(TRUE, FALSE, TRUE), c("B", "A")]
```

```
##      B A
## [1,] 4 1
## [2,] 6 3
```

```r
a[1:2, ]
```

```
##      A B C
## [1,] 1 4 7
## [2,] 2 5 8
```


--- .classs #id



## Subindexado de matrices (continuación)
- Una matriz se puede subindexar como un vector, ya que la matriz es una generalización de éstos.
- En este caso se utiliza `[`  e indexar de la siguiente manera $a[i,j]$ quiere decir tomar la fila $i$ y la columna $j$.


```r
a <- matrix(1:9, nrow = 3)
colnames(a) <- c("A", "B", "C")
a[0,]
```

```
##      A B C
```

```r
a[0, -2]
```

```
##      A C
```

```r
a[1,3]
```

```
## C 
## 7
```


--- .segue bg:grey


## Subindexado de data frames

---



## Subindexado de data frames
- Los `data.frame` se comportan como las listas y las matrices, por lo tanto se pueden subindexar de la misma manera. 
- Si subindexamos con un vector se comportan como listas mientras que si lo hacemos con dos vectores se comportan como matrices.


```r
df <- data.frame(x = 1:3, y = 3:1, z = letters[1:3])
df[df$x == 2, ]
```

```
##   x y z
## 2 2 2 b
```

```r
df[c(1, 3), ]
```

```
##   x y z
## 1 1 3 a
## 3 3 1 c
```

--- .class #id



## Subindexado de data frames (continuación)



```r
df <- data.frame(x = 1:3, y = 3:1, z = letters[1:3])
df[c("x", "z")]   # Seleccionamos como una lista
```

```
##   x z
## 1 1 a
## 2 2 b
## 3 3 c
```

```r
df[, c("x", "z")] # Seleccionamos como una matriz
```

```
##   x z
## 1 1 a
## 2 2 b
## 3 3 c
```

--- .class #id


## Preguntas

¡Gracias!

---

