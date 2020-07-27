---
title: Creazione di un aspetto personalizzato nei moduli HTML5
seo-title: Creazione di un aspetto personalizzato nei moduli HTML5
description: È possibile collegare widget personalizzati a moduli mobili. Potete estendere i widget jQuery esistenti o sviluppare widget personalizzati.
seo-description: È possibile collegare widget personalizzati a moduli mobili. Potete estendere i widget jQuery esistenti o sviluppare widget personalizzati.
uuid: a9013c3d-20c7-45c9-be24-8e9d4525eff8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 17a86543-30d3-4e16-a373-67b46d551da9
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---


# Creazione di un aspetto personalizzato nei moduli HTML5{#create-custom-appearances-in-html-forms}

È possibile collegare widget personalizzati a moduli mobili. Potete estendere i widget jQuery esistenti o sviluppare widget personalizzati utilizzando il framework di aspetto. Il motore XFA utilizza vari widget. Per informazioni dettagliate, vedere Framework [Aspetto per i moduli](/help/forms/using/introduction-widgets.md) adattivi e HTML5.

![Un esempio di widget predefinito e personalizzato](assets/custom-widgets.jpg)

Un esempio di widget predefinito e personalizzato

## Integrazione di widget personalizzati con moduli HTML5 {#integrating-custom-widgets-with-html-forms}

### Creazione di un profilo  {#create-a-profile-nbsp}

Puoi creare un profilo o scegliere un profilo esistente per aggiungere un widget personalizzato. Per ulteriori informazioni sulla creazione dei profili, consultate [Creazione di un profilo](/help/forms/using/custom-profile.md)personalizzato.

### Creare un widget {#create-a-widget}

I moduli HTML5 forniscono un&#39;implementazione del framework di widget che può essere esteso per creare nuovi widget. L’implementazione è un widget jQuery *abstractWidget* che può essere esteso per scrivere un nuovo widget. Il nuovo widget può essere reso funzionale solo estendendo/sostituendo le funzioni elencate di seguito.

<table>
 <tbody>
  <tr>
   <td>Funzione/Classe</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td>rendering</td>
   <td>La funzione di rendering restituisce l'oggetto jQuery per l'elemento HTML predefinito del widget. L'elemento HTML predefinito deve essere di tipo attivabile. Ad esempio, &lt;a&gt;, &lt;input&gt; e &lt;li&gt;. L'elemento restituito viene utilizzato come $userControl. Se $userControl specifica il vincolo di cui sopra, le funzioni della classe AbstractWidget funzionano come previsto, altrimenti alcune delle API comuni (focus, click) richiedono delle modifiche. </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>Restituisce una mappa per convertire gli eventi HTML in eventi XFA. <br /> {<br /> sfocatura: XFA_EXIT_EVENT,<br /><br /> } In questo esempio viene mostrato che la sfocatura è un evento HTML e che XFA_EXIT_EVENT è un evento XFA corrispondente. </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>Restituisce una mappa che fornisce informazioni dettagliate sulle azioni da eseguire in caso di modifica di un'opzione. Le chiavi sono le opzioni fornite al widget e i valori sono le funzioni che vengono chiamate ogni volta che viene rilevata una modifica in tale opzione. Il widget fornisce handler per tutte le opzioni comuni (tranne valore e displayValue)</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>Il framework Widget carica la funzione ogni volta che il valore del widget viene salvato nel modello XFAM (ad esempio, in corrispondenza dell'evento exit di un oggetto textField). L’implementazione deve restituire il valore salvato nel widget. Al gestore viene fornito il nuovo valore per l'opzione.</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>Per impostazione predefinita, in XFA all'evento enter, viene visualizzato il valore rawValue del campo. Questa funzione viene chiamata per mostrare il valore rawValue all'utente. </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>Per impostazione predefinita, in XFA all'uscita, viene visualizzato il valore formattedValue del campo. Questa funzione viene chiamata per mostrare l'oggetto formattedValue all'utente. </td>
  </tr>
 </tbody>
</table>

Per creare un widget personalizzato, nel profilo creato sopra, includete i riferimenti del file JavaScript che contiene funzioni sostituite e funzioni aggiunte di recente. Ad esempio, *sliderNumericFieldWidget* è un widget per i campi numerici. Per utilizzare il widget nel profilo nella sezione di intestazione, includi la seguente riga:

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### Registrazione di un widget personalizzato con il motore di script XFA  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

Quando il codice widget personalizzato è pronto, registrate il widget con il motore di script utilizzando `registerConfig`API per [Form Bridge](/help/forms/using/form-bridge-apis.md). È necessario widgetConfigObject come input.

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

La configurazione del widget è fornita come oggetto JSON (una raccolta di coppie di valori chiave) in cui la chiave identifica i campi e il valore rappresenta il widget da utilizzare con tali campi. Esempio di configurazione:

*{*

*&quot;identifier1&quot; : &quot;customwidgetname&quot;,&quot;identifier2&quot; : &quot;customwidgetname2&quot;,..
}*

dove &quot;identifier&quot; è un selettore CSS jQuery che rappresenta un particolare campo, un set di campi di un particolare tipo o tutti i campi. Di seguito è riportato il valore dell’identificatore in diversi casi:

| Tipo di identificatore | modulo | Descrizione |
|---|---|---|
| Campo particolare con nome campo | Identificatore:&quot;div.fieldname&quot; | Viene eseguito il rendering di tutti i campi con il nome &quot;nome campo&quot; utilizzando il widget. |
| Tutti i campi di tipo &quot;type&quot;(dove type è NumericField, DateField e così via): | Identificatore: &quot;div.type&quot; | Per Timefield e DateTimeField, il tipo è textfield in quanto questi campi non sono supportati. |
| Tutti i campi | Identificatore: &quot;div.field&quot; |  |
