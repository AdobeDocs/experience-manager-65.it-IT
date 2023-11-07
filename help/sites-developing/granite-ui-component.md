---
title: Creazione di un nuovo componente campo dell’interfaccia utente Granite
description: L’interfaccia utente Granite offre una serie di componenti progettati per essere utilizzati nei moduli, denominati campi
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Creazione di un nuovo componente campo dell’interfaccia utente Granite{#creating-a-new-granite-ui-field-component}

L’interfaccia utente Granite offre una serie di componenti progettati per essere utilizzati nei moduli, denominati *campi* nel vocabolario dell’interfaccia utente Granite. I componenti del modulo Granite standard sono disponibili in:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Questi campi modulo dell’interfaccia utente Granite sono di particolare interesse in quanto vengono utilizzati per [finestre di dialogo dei componenti](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Per informazioni complete sui campi, vedi [Documentazione dell’interfaccia utente Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Utilizza il framework Granite UI Foundation per sviluppare e/o estendere i componenti Granite. Ciò si basa su due elementi:

* lato server:

   * una raccolta di componenti di base

      * foundation: modulare, componibile, a più livelli, riutilizzabile
      * componenti: componenti Sling

   * assistenti per lo sviluppo delle applicazioni

* lato client:

   * una raccolta di clientlibs che fornisce un vocabolario (ovvero un’estensione del linguaggio HTML) per ottenere modelli di interazione generici tramite un’interfaccia utente guidata da Hypermedia.

Il componente generico dell’interfaccia utente Granite `field` è composto da due file di interesse:

* `init.jsp`: gestisce l’elaborazione generica; l’etichettatura, la descrizione e fornisce il valore del modulo necessario per il rendering del campo.
* `render.jsp`: questo è il punto in cui viene eseguito il rendering effettivo del campo e deve essere sostituito per il campo personalizzato; è incluso da `init.jsp`.

Consulta [Documentazione dell’interfaccia utente Granite - Campo](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) per i dettagli.

Per esempi, consulta:

* `cqgems/customizingfield/components/colorpicker`

   * fornite da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Poiché questo meccanismo utilizza JSP, i18n e XSS non sono forniti come preconfigurati. Questo significa che devi internazionalizzare ed evitare le tue Stringhe. La directory seguente contiene i campi generici di un’istanza standard, che puoi utilizzare come riferimento:
>
>`/libs/granite/ui/components/foundation/form` directory

## Creazione dello script lato server per il componente {#creating-the-server-side-script-for-the-component}

Il campo personalizzato deve sostituire solo il `render.jsp` script, in cui viene fornito il markup per il componente. Puoi considerare JSP (ovvero lo script di rendering) come un wrapper per il markup.

1. Creare un componente che utilizza `sling:resourceSuperType` proprietà da cui ereditare:

   `/libs/granite/ui/components/foundation/form/field`

1. Ignora lo script:

   `render.jsp`

   In questo script, genera il markup hypermedia (ovvero, il markup arricchito, contenente l’affordance hypermedia) in modo che il client sappia come interagire con l’elemento generato. Questo dovrebbe seguire lo stile di codifica lato server dell’interfaccia utente Granite.

   Durante la personalizzazione, l’unico contratto che *deve* adempiere significa leggere il valore del modulo (inizializzato in `init.jsp`) dalla richiesta utilizzando:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Per ulteriori dettagli, consulta l’implementazione dei campi predefiniti dell’interfaccia utente Granite; ad esempio, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >Al momento, JSP è il metodo di scripting preferito, in quanto la trasmissione di informazioni da un componente all’altro (frequente nel contesto di moduli/campi) non è facilmente raggiungibile in HTL.

## Creazione della libreria client per il componente {#creating-the-client-library-for-the-component}

Per aggiungere al componente un comportamento specifico lato client:

1. Creare una libreria client di categoria `cq.authoring.dialog`.
1. Creare una libreria client di categoria `cq.authoring.dialog` e definisci `JS`/ `CSS` dentro.

   Definisci le `JS`/ `CSS` dentro clientlib.

   >[!NOTE]
   >
   >Al momento, l’interfaccia utente Granite non fornisce alcun listener o hook predefinito che puoi utilizzare direttamente per aggiungere il comportamento JS. Per aggiungere un ulteriore comportamento JS al componente, devi implementare un hook JS a una classe personalizzata che viene quindi assegnata al componente durante la generazione del markup.
