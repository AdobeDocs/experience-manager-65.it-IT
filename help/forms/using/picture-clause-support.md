---
title: Supporto delle clausole di immagine per i moduli HTML5
description: HTML5 Forms supporta la clausola immagine XFA per il valore di visualizzazione e il valore formattato per i simboli di data, testo e numerici.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# Supporto delle clausole di immagine per i moduli HTML5 {#picture-clause-support-for-html-forms}

HTML5 Forms supporta la clausola immagine XFA per il valore di visualizzazione e il valore formattato per i simboli di data, testo e numerici. Sono supportate le seguenti espressioni della clausola Picture:

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>Al momento, Mobile Forms non supporta la clausola Edit Picture. Inoltre, i simboli delle clausole DateTime e Time Picture non sono supportati.

## Simboli di campo data supportati {#supported-date-field-symbols}

Espressione supportata per la clausola Date Picture:

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date} Simboli della clausola immagine}

>[!NOTE]
>
>Il pattern predefinito della clausola immagine è {MMM D, YYYY}. Se non viene applicato alcun pattern, viene utilizzato quello di default.

<table>
 <tbody>
  <tr>
   <th><strong>Simbolo</strong></th>
   <th>Interpretazione</th>
  </tr>
  <tr>
   <td>D</td>
   <td>1 o 2 cifre (1-31) del giorno del mese</td>
  </tr>
  <tr>
   <td>GG</td>
   <td>Giorno del mese a due cifre (01-31) senza riempimento.<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>1 o 2 cifre (1-12) del mese dell’anno.<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>Mese dell’anno a due cifre (01-12) imbottite a zero.<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>Nome del mese abbreviato della lingua corrente<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>Nome mese completo della lingua corrente<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>Nome abbreviato del giorno feriale della lingua corrente<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>Nome completo del giorno feriale della lingua corrente<br /> </td>
  </tr>
  <tr>
   <td>AA</td>
   <td>Anno a 2 cifre, dove 00 = 2000, 29 = 2029, 30 = 1930 e 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>AAAA</td>
   <td>Anno a 4 cifre<br /> </td>
  </tr>
 </tbody>
</table>

## Clausola immagine numerica {#numeric-picture-clause}

I moduli HTML5 supportano i simboli di immagine numerica. Tuttavia, esiste una differenza nel supporto tra PDF forms e HTML Forms.

In entrata **PDF forms**, un numero viene formattato indipendentemente dal numero di simboli nella clausola Picture

In entrata **HTML Forms**, un numero viene formattato solo se il numero contiene cifre inferiori al numero di simboli nella clausola Picture.

**Esempio**: considerare una clausola Picture: num{zzz,zzz,zz9}.

Il numero **10000** è formattato come **10.000** sia in HTML che in PDF forms.

Il numero 1000000 è formattato come 1.000.000 in PDF forms. Tuttavia, in HTML Forms il numero rimane non formattato come 1000000.

Espressioni supportate per la clausola Numeric Picture in **HTML Forms** sono:

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Simboli clausola immagine numerica}

<table>
 <tbody>
  <tr>
   <th><strong>Simbolo</strong></th>
   <th><strong>Interpretazione</strong></th>
   <th>Analisi input</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>Formattazione di output</strong>: una cifra singola. Oppure per la cifra zero se i dati di input sono vuoti o uno spazio nella posizione corrispondente.<br /> </td>
   <td>Cifra singola</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>Formattazione di output</strong>: una cifra singola. Oppure per uno spazio se i dati di input sono vuoti, uno spazio o la cifra zero nella posizione corrispondente.<br /> </td>
   <td>Cifra singola o spazio</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>Formattazione di output</strong>: una cifra singola. Oppure nulla se i dati di input sono vuoti, uno spazio o la cifra zero nella posizione corrispondente.<br /> </td>
   <td>Cifra singola o nulla</td>
  </tr>
  <tr>
   <td>Err.</td>
   <td><strong>Formattazione di output</strong>: la parte esponente di un numero a virgola mobile costituito dal simbolo esponenziale (E). Seguito da un segno più o meno facoltativo. Seguito dal valore esponente.<br /> </td>
   <td>Come per la formattazione di output</td>
  </tr>
  <tr>
   <td>CR o cr<br /> </td>
   <td>Simbolo di credito (CR) se il numero è negativo. Altrimenti niente.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S o s<br /> </td>
   <td>Formattazione output: un segno meno se il numero è negativo. Altro spazio.<br /> </td>
   <td>Segno meno se il numero è negativo. Segno più se il numero è positivo</td>
  </tr>
  <tr>
   <td>V</td>
   <td>Raggio decimale della lingua prevalente. Consente di implicare il raggio decimale durante l'analisi dell'input.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>Raggio decimale della lingua prevalente. Consente di implicare il raggio decimale durante l'analisi di input e la formattazione di output.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>Raggio decimale della lingua prevalente.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>Separatore di raggruppamento delle impostazioni internazionali prevalenti</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>Simbolo di valuta della lingua prevalente.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>Simbolo di percentuale della lingua prevalente.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>Parentesi sinistra se il numero è negativo. Altro spazio.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>Parentesi destra se il numero è negativo. Altro spazio.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>Carattere scheda</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Clausola immagine di testo {#text-picture-clause}

I moduli HTML5 supportano le seguenti espressioni della clausola Text Picture:

* text{text Simboli della clausola Picture}

| **Simbolo** | **Interpretazione** |
|---|---|
| A | Carattere alfabetico singolo. |
| X | Singolo carattere. |
| O | Singolo carattere alfanumerico. |
| 0 (zero) | Singolo carattere alfanumerico. |
| 9 | Una cifra. |
