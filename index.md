---
title       : Cables in Electrical Power Transmission
subtitle    : Coursera Developing Data Products
author      : ME
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Outline

1. Context
2. Cable Parameters
3. Charging Current

--- .class #id 

## Context

- The cables that are used in today's electric power systems consist of a concentric conductor (generally copper or aluminium), the dielectric isolating material (e.g. PVC) and a metallic shield which is grounded normally on both sides. Hence, a cables typically behaves like a capacitor.
- When operated with alternating current (which is the case except some particular point-to-point-connections), this capacity is charged and decharged with the system frequency.
- The power that can be transmitted over a cable is limited by the current, or more precisely: the current determines the losses inside the conductor which are transformed into heat. And it is mainly the isolating material which is irreversibly damaged in case of over-temperature.
- Hence, the current rating is defined by the material and it applies to both active and reactive current. While the active current is able to transmit power, the reactive current is necessary for the described charging process without being useful.
- The so-called charging current increases with the cables length. The maximum cable length is reached when the charging current equals the contiuous current carrying capacity and, thus, no active power can be transmitted any more.
- However, only half of this maximum cable length is considered as useful cable length.

---

## Cable Parameters

- The following technical cable data is given as an example

```r
f <- 50      # system frequency in Hertz
Um <- 24     # highest voltage for equipment Um in kV
X1 <- 0.122  # positive sequence reactance in ohm per km
C1 <- 0.254  # positive sequence capacitance in microfarad per km
Id <- 366    # continuous current carrying capacity in Ampere
```

- The following characteristic parameters for a lossless cable are calculated


```r
ZW1 <- sqrt(X1/(2*pi*f*C1*1e-6))            # characteristic impedance in Ohms
beta1 <- sqrt(X1*2*pi*f*C1*1e-6)*180/pi*100 # propagation constant in degrees per 100km
Pnat <- Um^2/ZW1                            # natural loading in Megawatts 
c(ZW1, beta1, Pnat)
```

```
## [1] 39.10 17.88 14.73
```

---

## Charging Current

- Next, the charging current for an unloaded cable (no consumer connected at the end) is calculated for a given cable length. 


```r
l <- 100     # length in km
Ic <- 1/ZW1*tan(beta1/180*pi/100*l)*Um*1000/sqrt(3) # charging current in Ampere
```

- The graph gives an idea what portion of the current carrying capacity of the cable is used for the charging current or if already only the charging current would exceed the maximum permissible current.

![plot of chunk chart](assets/fig/chart.png) 


