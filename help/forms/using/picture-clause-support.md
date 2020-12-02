---
title: Supporto della clausola illustrazione per i moduli HTML5
seo-title: Supporto della clausola illustrazione per i moduli HTML5
description: I moduli HTML5 supportano la clausola XFA Picture per la visualizzazione di valori e valori formattati per data, testo e simboli numerici.
seo-description: I moduli HTML5 supportano la clausola XFA Picture per la visualizzazione di valori e valori formattati per data, testo e simboli numerici.
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 5%

---


# Supporto della clausola illustrazione per i moduli HTML5 {#picture-clause-support-for-html-forms}

I moduli HTML5 supportano la clausola XFA Picture per la visualizzazione di valori e valori formattati per data, testo e simboli numerici. Sono supportate le seguenti espressioni della clausola illustrazione:

* category(locale){clausola-immagine} | category(locale){clausola illustrazione} | category(locale){clausola illustrazione}
* category.subcategory{}

>[!NOTE]
>
>Attualmente, Mobile Forms non supporta la clausola Edit Picture. Inoltre, i simboli delle clausole DateTime e Time Picture non sono supportati.

## Simboli dei campi data supportati {#supported-date-field-symbols}

Espressione supportata per la clausola Date Picture:

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture Clausole}

>[!NOTE]
>
>Il pattern predefinito della clausola illustrazione è {MMM G, YYYY} pattern. Se non viene applicato alcun pattern, viene utilizzato il pattern predefinito.

<table>
 <tbody>
  <tr>
   <th><strong>Simbolo</strong></th>
   <th>Interpretazione</th>
  </tr>
  <tr>
   <td>D</td>
   <td>Giorno del mese di 1 o 2 cifre (1-31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>Giorno del mese di due cifre completato con zero (01-31).<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>Mese dell'anno di 1 o 2 cifre (1-12).<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>Mese dell'anno di due cifre completato con zero (01-12).<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>Nome del mese abbreviato dell'impostazione internazionale corrente<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>Nome completo del mese delle impostazioni internazionali correnti<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>Nome abbreviato del giorno della settimana delle impostazioni internazionali correnti<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>Nome completo del giorno della settimana della lingua corrente<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>Anno di 2 cifre, dove 00 = 2000, 29 = 2029, 30 = 1930, e 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>Anno di 4 cifre<br /> </td>
  </tr>
 </tbody>
</table>

## Clausola illustrazione numerica {#numeric-picture-clause}

I moduli HTML5 supportano i simboli illustrazione numerica. Tuttavia, esiste una differenza nel supporto tra PDF forms e Forms HTML.

In **PDF forms**, viene formattato un numero indipendentemente dal numero di simboli nella clausola Picture

In **HTML Forms**, un numero è formattato solo se il numero ha cifre inferiori al numero di simboli nella clausola Immagine.

**Esempio**: Considerare una clausola Picture: num{zzz,zzz,zz9}.

Il numero **10000** è formattato come **10.000** sia in HTML che in PDF forms.

Il numero 1000000 è formattato come 10000000 in PDF forms. Tuttavia, in HTML Forms il numero rimane non formattato come 1000000.

Le espressioni supportate per la clausola Numeric Picture in **HTML Forms** sono:

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Simboli di clausola illustrazione numerica}

<table>
 <tbody>
  <tr>
   <th><strong>Simbolo</strong></th>
   <th><strong>Interpretazione</strong></th>
   <th>Analisi input</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>Formattazione</strong> output: una cifra singola. Oppure per la cifra zero se i dati di input sono vuoti o uno spazio nella posizione corrispondente.<br /> </td>
   <td>Singola cifra</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>Formattazione</strong> output: una cifra singola. Oppure per uno spazio se i dati di input sono vuoti, uno spazio o la cifra zero nella posizione corrispondente.<br /> </td>
   <td>Singola cifra o spazio</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>Formattazione</strong> output: una cifra singola. Oppure nulla se i dati di input sono vuoti, uno spazio o la cifra zero nella posizione corrispondente.<br /> </td>
   <td>Singola cifra o niente</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>Formattazione</strong> output: la parte esponenziale di un numero a virgola mobile costituita dal simbolo esponenziale (E). Seguito dal segno più o meno facoltativo. Seguito dal valore esponenziale.<br /> </td>
   <td>Come per la formattazione dell'output</td>
  </tr>
  <tr>
   <td>CR o cr<br /> </td>
   <td>Simbolo di credito (CR) se il numero è negativo. Niente altro.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S o s<br /> </td>
   <td>Formattazione output: un segno meno se il numero è negativo. Altro spazio.<br /> </td>
   <td>Segno meno se il numero è negativo. Segno più se il numero è positivo</td>
  </tr>
  <tr>
   <td>V</td>
   <td>Radice decimale delle impostazioni internazionali prevalenti. Consentire la radice decimale di essere implicita durante l'analisi dell'input.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>Radice decimale delle impostazioni internazionali prevalenti. Consentire la radice decimale di essere implicita durante l'analisi dell'input e la formattazione dell'output.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>Radice decimale delle impostazioni internazionali prevalenti.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>Separatore di raggruppamento delle impostazioni internazionali prevalenti</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>Simbolo della valuta dell'impostazione internazionale prevalente.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>Simbolo percentuale delle impostazioni internazionali prevalenti.</td>
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
   <td>Carattere di tabulazione</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Text Picture Clausola {#text-picture-clause}

I moduli HTML5 supportano le seguenti espressioni della clausola Text Picture:

* testo{simboli della clausola illustrazione}

| **Simbolo** | **Interpretazione** |
|---|---|
| A | Singolo carattere alfabetico. |
| X | Singolo carattere. |
| O | Singolo carattere alfanumerico. |
| 0 (zero) | Singolo carattere alfanumerico. |
| 9 | Singola cifra. |
