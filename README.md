# Digital-Electronics-2 | Radim Dvořák 186800

[![university](https://img.shields.io/badge/university-Brno%20University%20of%20Technology-red.svg)](https://www.vutbr.cz/en/)
[![faculty](https://img.shields.io/badge/faculty-Faculty%20of%20Electrical%20Engineering%20and%20Communication-blue.svg)](https://www.fekt.vutbr.cz/)


# Semestrální projekt

## Zadání projektu
Parkovací senzory s využitím Multi function shieldu a ultrazvukového(ých) senzoru(ů) HC-SR04. Frekvence pípání podle vzdálenosti, zobrazení vzdálenosti na 7segmentovém displeji v centimetrech, indikace vzdálenosti na LED (daleko žádná, blízko všechny LED, apod.). Uvažovat nastavení limitů vzdálenosti pomoci interaktivní konzole přes UART.

## Použité komponenty
| **Součástka** | **Popis** |
| ------------- | --------- |
| ATMEGA328P | Arduino Nano 
| 3x 8bitový posuvný registr | 74HC595N 
| 1x 4 Sedmisegmentový display | Common Cathode 
| Bzučák | 
| Senzor vzdálenosti | HC-SR04 
| 8x LED | 3x zelená, 3x žlutá, 2x červená 
| Tranzistor MOSFET | 
| Propojky | Různé velikosti a barvy 

## Schéma zapojení

## Realizace
HW : 
Pro komunikaci se senzorem využíváme 2 piny portu B.

| **Pin senzoru** | **Pin mikrokontroléru** | **Pin na desce (Arduinu)** |
| --------------- | ----------------------- | -------------------------- |
| Trigger | PORTB1 | D9
| Echo | PORTB0 | D8

Pro aktivování senzoru je nutné přivést na Trigger pin 10 mikrosekundový pulz. Senzor potom odpovídá na pinu Echo zvednutím napěťové úrovně do logické úrovně HIGH, kterou poté udržuje po dobu odpovídající vzdálenosti, kterou změřil. Změříme-li tuto dobu, můžeme vzdálenost vypočítat podle stanovené rovnice v datasheetu senzoru.
Doporučená hranice pro buzení senzoru je dle datasheetu minimálně 60 mikrosekund.

V našem projektu jsme využili 3 posuvné registry pro adresaci sedmisegmentových displejů a také na ovládání indikačních LED diod.
Pro komunikaci s posuvnými registry využíváme port D

| **Pin registru** | **Pin mikrokontroléru** | **Pin na desce (Arduinu)** |
| ---------------- | ------------------------| -------------------------- |
| Data Pin | PORTD4 | D4
| Clock Pin | PORTD5 | D5
| Latch Pin | PORTD6 | D6
