---
title: Memristor
date: 2018-06-20 20:53:03
tags: memristor
categories: paper
---
什么是忆阻器，它是一种新型的元器件，本质上是一个变化的电阻。变化的电阻有光敏电阻，压控电阻等等，这些变化的电阻和忆阻器有什么区别呢？光敏电阻的阻值是随光的强度不同而不同，但是当光撤掉之后，光敏电阻的阻值会呈高阻态，而忆阻器的特点在于当忆阻器的发生变化时，比如从高阻态变化到低组态，撤掉电路中的电源，忆阻器的阻值不会发生变化，这意味着当再次接通电源时，忆阻器的阻值还是处于低组态。举个例子来说明：忆阻器和电解电容相似，是存在极性的，当正向电流通过时，忆阻器的阻值会从高组态变化到低组态，基于这个知识点，我们假设一个忆阻器的阻值正处于高组态，将其和一个发光二极管串联，并在电路中施加电压，因为初始组态忆阻器是高组态，发光二极管是处于熄灭状态，随后忆阻器的阻值发生变化，从高组态变化到低组态，发光二极管点亮。如果此时将电源撤掉，再重新接入，忆阻器的阻值会保持断电前的状态不变，二极管依然会点亮，如果是光敏电阻的话，其电阻会初始化为高组态，二极管是不会点亮的。这个特性可被用作存储数据，断电后数据保持不变。
忆阻器的特点有：非易失性（nonvolatile），高密度（dense），快（fast），高效的内存（power efficient memort)