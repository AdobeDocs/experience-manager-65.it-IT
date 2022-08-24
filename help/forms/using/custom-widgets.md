---
title: Creare un aspetto personalizzato nei moduli di HTML5
seo-title: Create custom appearances in HTML5 forms
description: Puoi collegare widget personalizzati a un Forms mobile. Puoi estendere i widget jQuery esistenti o sviluppare widget personalizzati.
seo-description: You can plug in custom widgets to a Mobile Forms. You can extend existing jQuery Widgets or develop your own custom widgets.
uuid: a9013c3d-20c7-45c9-be24-8e9d4525eff8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 17a86543-30d3-4e16-a373-67b46d551da9
docset: aem65
feature: Mobile Forms
exl-id: 76bd1e2d-9e65-452c-8cef-123d28886a62
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Creare un aspetto personalizzato nei moduli di HTML5{#create-custom-appearances-in-html-forms}

Puoi collegare widget personalizzati a un Forms mobile. È possibile estendere i widget jQuery esistenti o sviluppare widget personalizzati utilizzando il framework appearances. Il motore XFA utilizza vari widget, vedi [Framework di aspetto per i moduli adattivi e HTML5](/help/forms/using/introduction-widgets.md) per informazioni dettagliate.

![Esempio di widget predefiniti e personalizzati](assets/custom-widgets.jpg)

Esempio di widget predefiniti e personalizzati

## Integrazione di widget personalizzati con i moduli HTML5 {#integrating-custom-widgets-with-html-forms}

### Creare un profilo  {#create-a-profile-nbsp}

Puoi creare un profilo o scegliere un profilo esistente per aggiungere un widget personalizzato. Per ulteriori informazioni sulla creazione dei profili, consulta [Creazione di un profilo personalizzato](/help/forms/using/custom-profile.md).

### Creare un widget {#create-a-widget}

I moduli di HTML5 forniscono un’implementazione del framework di widget che può essere esteso per creare nuovi widget. L’implementazione è un widget jQuery *abstractWidget* che può essere esteso per scrivere un nuovo widget. Il nuovo widget può essere reso funzionale solo estendendo/ignorando le funzioni di seguito menzionate.

<table>
 <tbody>
  <tr>
   <td>Funzione/Classe</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td>rendering</td>
   <td>La funzione di rendering restituisce l'oggetto jQuery per l'elemento HTML predefinito del widget. L’elemento HTML predefinito deve essere di tipo focalizzabile. Ad esempio: &lt;a&gt;, &lt;input&gt;e &lt;li&gt;. L'elemento restituito viene utilizzato come $userControl. Se $userControl specifica il vincolo di cui sopra, le funzioni della classe AbstractWidget funzionano come previsto, altrimenti alcune delle API comuni (attivazione, clic) richiedono modifiche. </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>Restituisce una mappa per convertire gli eventi HTML in eventi XFA. <br /> {<br /> sfocatura: XFA_EXIT_EVENT,<br /> }<br /> Questo esempio mostra che la sfocatura è un evento HTML e che XFA_EXIT_EVENT è l’evento XFA corrispondente. </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>Restituisce una mappa che fornisce dettagli sull'azione da eseguire in caso di modifica di un'opzione. Le chiavi sono le opzioni fornite al widget e i valori sono le funzioni che vengono chiamate ogni volta che viene rilevata una modifica in tale opzione. Il widget fornisce gestori per tutte le opzioni comuni (ad eccezione di value e displayValue)</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>Il framework Widget carica la funzione ogni volta che il valore del widget viene salvato nel modello XFAM (ad esempio, in caso di uscita da un evento textField). L'implementazione deve restituire il valore salvato nel widget. Al gestore viene fornito il nuovo valore per l’opzione .</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>Per impostazione predefinita, in XFA all’evento enter viene visualizzato il valore rawValue del campo. Questa funzione viene chiamata per mostrare il rawValue all'utente. </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>Per impostazione predefinita, in XFA all'evento di uscita viene visualizzato il valore formattedValue del campo. Questa funzione viene chiamata per mostrare l'oggetto formattedValue all'utente. </td>
  </tr>
 </tbody>
</table>

Per creare un widget personalizzato, nel profilo creato sopra, includi i riferimenti del file JavaScript che contiene funzioni ignorate e funzioni appena aggiunte. Ad esempio, il *sliderNumericFieldWidget* è un widget per campi numerici. Per utilizzare il widget nel tuo profilo nella sezione intestazione, includi la seguente riga:

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### Registra widget personalizzato con motore di scripting XFA  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

Quando il codice del widget personalizzato è pronto, registra il widget con il motore di scripting utilizzando `registerConfig`API per [Form Bridge](/help/forms/using/form-bridge-apis.md). Richiede widgetConfigObject come input.

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

La configurazione del widget viene fornita come un oggetto JSON (una raccolta di coppie di valori chiave) in cui la chiave identifica i campi e il valore rappresenta il widget da utilizzare con tali campi. Esempio di configurazione:

```
*{*

*"identifier1" : "customwidgetname",
"identifier2" : "customwidgetname2",
..
}*
```

dove &quot;identifier&quot; è un selettore CSS jQuery che rappresenta un particolare campo, un insieme di campi di un particolare tipo o tutti i campi. Di seguito è riportato un elenco del valore dell’identificatore in diversi casi:

| Tipo di identificatore | modulo | Descrizione |
|---|---|---|
| Campo particolare con nome campo | Identificatore:&quot;div.fieldname&quot; | Viene eseguito il rendering di tutti i campi con il nome &quot;nome campo&quot; utilizzando il widget. |
| Tutti i campi di tipo &quot;type&quot; (in cui il tipo è NumericField, DateField e così via).: | Identificatore: &quot;div.type&quot; | Per Timefield e DateTimeField, il tipo è textfield perché questi campi non sono supportati. |
| Tutti i campi | Identificatore: &quot;div.field&quot; |  |
