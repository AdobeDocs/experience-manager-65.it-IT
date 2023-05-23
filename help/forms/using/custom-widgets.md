---
title: Creare aspetti personalizzati nei moduli di HTML5
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

# Creare aspetti personalizzati nei moduli di HTML5{#create-custom-appearances-in-html-forms}

Puoi collegare widget personalizzati a un Forms mobile. È possibile estendere i widget jQuery esistenti o sviluppare widget personalizzati utilizzando il framework di aspetti. Il motore XFA utilizza vari widget, vedi [Framework di aspetto per moduli adattivi e HTML5](/help/forms/using/introduction-widgets.md) per informazioni dettagliate.

![Un esempio di widget predefinito e personalizzato](assets/custom-widgets.jpg)

Un esempio di widget predefinito e personalizzato

## Integrazione di widget personalizzati con moduli HTML5 {#integrating-custom-widgets-with-html-forms}

### Creare un profilo  {#create-a-profile-nbsp}

Puoi creare un profilo o sceglierne uno esistente per aggiungere un widget personalizzato. Per ulteriori informazioni sulla creazione di profili, consulta [Creazione di un profilo personalizzato](/help/forms/using/custom-profile.md).

### Creare un widget {#create-a-widget}

I moduli HTML5 forniscono un’implementazione del framework dei widget che può essere estesa per creare nuovi widget. L’implementazione è un widget jQuery *abstractWidget* che può essere esteso per scrivere un nuovo widget. Il nuovo widget può essere reso funzionale solo estendendo/sovrascrivendo le seguenti funzioni.

<table>
 <tbody>
  <tr>
   <td>Funzione/Classe</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td>rendering</td>
   <td>La funzione render restituisce l’oggetto jQuery per l’elemento HTML predefinito del widget. L’elemento HTML predefinito deve essere di tipo attivabile. Ad esempio: &lt;a&gt;, &lt;input&gt;, e &lt;li&gt;. L'elemento restituito viene utilizzato come $userControl. Se $userControl specifica il vincolo riportato sopra, le funzioni della classe AbstractWidget funzioneranno come previsto. In caso contrario, alcune delle API comuni (attivazione, clic) richiederanno modifiche. </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>Restituisce una mappa per convertire gli eventi HTML in eventi XFA. <br /> {<br /> sfocatura: XFA_EXIT_EVENT,<br /> }<br /> Questo esempio mostra che la sfocatura è un evento HTML e XFA_EXIT_EVENT è un evento XFA corrispondente. </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>Restituisce una mappa che fornisce dettagli sull’azione da eseguire in caso di modifica di un’opzione. Le chiavi sono le opzioni fornite al widget e i valori sono le funzioni che vengono richiamate ogni volta che viene rilevata una modifica in tale opzione. Il widget fornisce gestori per tutte le opzioni comuni (ad eccezione di value e displayValue)</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>Il framework Widget carica la funzione ogni volta che il valore del widget viene salvato nel XFAModel (ad esempio all'evento di uscita di un textField). L’implementazione deve restituire il valore salvato nel widget. Al gestore viene fornito il nuovo valore per l’opzione.</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>Per impostazione predefinita, in XFA all’evento Invio viene visualizzato il valore rawValue del campo. Questa funzione viene chiamata per mostrare il valore raw all’utente. </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>Per impostazione predefinita, in XFA all’evento di uscita viene visualizzato il formattedValue del campo. Questa funzione viene chiamata per mostrare formattedValue all’utente. </td>
  </tr>
 </tbody>
</table>

Per creare un widget personalizzato, nel profilo creato in precedenza, includi i riferimenti del file JavaScript che contiene funzioni sovrascritte e funzioni appena aggiunte. Ad esempio, il *sliderNumericFieldWidget* è un widget per campi numerici. Per utilizzare il widget nel profilo nella sezione di intestazione, includi la seguente riga:

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### Registrare un widget personalizzato con il motore di script XFA  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

Quando il codice widget personalizzato è pronto, registralo con il motore di script utilizzando `registerConfig`API per [Bridge modulo](/help/forms/using/form-bridge-apis.md). Prende widgetConfigObject come input.

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

La configurazione del widget viene fornita come oggetto JSON (un insieme di coppie chiave-valore) in cui la chiave identifica i campi e il valore rappresenta il widget da utilizzare con tali campi. Esempio di configurazione:

```
*{*

*"identifier1" : "customwidgetname",
"identifier2" : "customwidgetname2",
..
}*
```

dove &quot;identifier&quot; è un selettore CSS jQuery che rappresenta un particolare campo, un insieme di campi di un particolare tipo o tutti i campi. Di seguito viene elencato il valore dell’identificatore in casi diversi:

| Tipo di identificatore | Identificatore | Descrizione |
|---|---|---|
| Campo particolare con nome nomecampo | Identificatore:&quot;div.fieldname&quot; | Tutti i campi denominati &quot;fieldname&quot; vengono riprodotti utilizzando il widget. |
| Tutti i campi di tipo &quot;type&quot; (dove type è NumericField, DateField e così via).: | Identificatore: &quot;div.type&quot; | Per Timefield e DateTimeField, il tipo è textfield in quanto questi campi non sono supportati. |
| Tutti i campi | Identificatore: &quot;div.field&quot; |  |
