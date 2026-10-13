---
title: Supporto delle clausole di immagine per i moduli HTML5
description: HTML5 Forms supporta la clausola immagine XFA per il valore di visualizzazione e il valore formattato per i simboli di data, testo e numerici.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: HTML5 Forms,Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 3%
---
# Supporto delle clausole di immagine per i moduli HTML5 {#picture-clause-support-for-html-forms}

HTML5 Forms supporta la clausola immagine XFA per il valore di visualizzazione e il valore formattato per i simboli di data, testo e numerici. Sono supportate le seguenti espressioni della clausola Picture:

* category(locale){picture-clause} | categoria(impostazioni locali){picture-clause} | category(locale){picture-clause}
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
* data{date Picture Clause symbols}

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
   <td>Giorno del mese a due cifre (01-31) imbottite a zero.<br /> </td>
  </tr>
  <tr>
   <td>L</td>
   <td>Mese dell'anno a 1 o 2 cifre (1-12).<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>Mese dell'anno a due cifre (01-12) imbottite a zero.<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>Nome del mese abbreviato delle impostazioni locali correnti<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>Nome mese completo delle impostazioni locali correnti<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>Abbreviazione del nome del giorno feriale delle impostazioni locali correnti<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>Nome completo del giorno della settimana delle impostazioni locali correnti<br /> </td>
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

>[!NOTE]
>
> In base alla progettazione, il campo Data in HTML5 Forms non supporta il pattern `MM-YYYY` in formato di modifica. Tuttavia, il modello è supportato nel formato di visualizzazione.

## Clausola immagine numerica {#numeric-picture-clause}

I moduli HTML5 supportano i simboli di immagine numerica. Tuttavia, esiste una differenza nel supporto tra PDF forms e HTML Forms.

In **PDF forms** un numero viene formattato indipendentemente dal numero di simboli nella clausola Picture

In **HTML Forms** un numero viene formattato solo se il numero contiene cifre inferiori al numero di simboli nella clausola Picture.

**Esempio**: considerare una clausola Picture: num{zzz,zzz,zz9}.

Il numero **10000** è formattato come **10.000** in HTML e PDF forms.

In PDF forms, il numero 1000000 è formattato come 1.000.000. Tuttavia, in HTML Forms il numero rimane non formattato come 1000000.

Le espressioni supportate per la clausola Numeric Picture in **HTML Forms** sono:

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Numeric Picture Clause Symbols}

<table>
 <tbody>
  <tr>
   <th><strong>Simbolo</strong></th>
   <th><strong>Interpretazione</strong></th>
   <th>Analisi input</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>Formattazione output</strong>: una sola cifra. Oppure per la cifra zero se i dati di input sono vuoti o uno spazio nella posizione corrispondente.<br /> </td>
   <td>Cifra singola</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>Formattazione output</strong>: una sola cifra. Oppure per uno spazio se i dati di input sono vuoti, uno spazio o la cifra zero nella posizione corrispondente.<br /> </td>
   <td>Cifra singola o spazio</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>Formattazione output</strong>: una sola cifra. Oppure nulla se i dati di input sono vuoti, uno spazio o la cifra zero nella posizione corrispondente.<br /> </td>
   <td>Cifra singola o nulla</td>
  </tr>
  <tr>
   <td>Err.</td>
   <td><strong>Formattazione output</strong>: parte esponente di un numero a virgola mobile costituito dal simbolo esponenziale (E). Seguito da un segno più o meno facoltativo. Seguito dal valore dell'esponente.<br /> </td>
   <td>Come per la formattazione di output</td>
  </tr>
  <tr>
   <td>CR o cr<br /> </td>
   <td>Simbolo di credito (CR) se il numero è negativo. Altrimenti niente.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S o s<br /> </td>
   <td>Formattazione output: un segno meno se il numero è negativo. Spazio alternativo.<br /> </td>
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

* text{text Picture clause symbols}

| **Simbolo** | **Interpretazione** |
|---|---|
| A | Carattere alfabetico singolo. |
| X | Singolo carattere. |
| O | Singolo carattere alfanumerico. |
| 0 (zero) | Singolo carattere alfanumerico. |
| 9 | Una cifra. |
