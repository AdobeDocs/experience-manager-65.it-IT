---
title: Creazione di un nuovo componente Campo interfaccia Granite
seo-title: Creazione di un nuovo componente Campo interfaccia Granite
description: L'interfaccia utente Granite offre una serie di componenti progettati per essere utilizzati nei moduli, denominati campi
seo-description: L'interfaccia utente Granite offre una serie di componenti progettati per essere utilizzati nei moduli, denominati campi
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Creazione di un nuovo componente campo di interfaccia Granite{#creating-a-new-granite-ui-field-component}

L&#39;interfaccia utente Granite offre una serie di componenti progettati per essere utilizzati nei moduli; questi sono denominati *fields* nel vocabolario dell&#39;interfaccia utente Granite. I componenti per modulo Granite standard sono disponibili in:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Questi campi modulo Granite UI sono particolarmente interessanti in quanto sono utilizzati per le finestre di dialogo dei componenti [](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Per informazioni dettagliate sui campi, consultare la [documentazione Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Utilizzate il framework Granite UI Foundation per sviluppare e/o estendere i componenti Granite. Sono disponibili due elementi:

* lato server:

   * una raccolta di componenti di base

      * fondazione - modulare, componibile, leggibile, riutilizzabile
      * componenti - Sling components
   * aiutanti per lo sviluppo delle applicazioni


* lato client:

   * una raccolta di clientlibs che forniscono un vocabolario (ad esempio l&#39;estensione del linguaggio HTML) per ottenere pattern di interazione generici tramite un&#39;interfaccia utente ipermedia

Il componente generico dell&#39;interfaccia utente Granite `field` è composto da due file di interesse:

* `init.jsp`: gestisce la trasformazione generica; l&#39;etichettatura, la descrizione e il valore del modulo saranno necessari per il rendering del campo.
* `render.jsp`: in questo punto viene eseguito il rendering effettivo del campo e deve essere ignorato per il campo personalizzato; è incluso da  `init.jsp`.

Per ulteriori informazioni, fare riferimento alla [documentazione Granite UI - Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html).

Per esempi, vedete:

* `cqgems/customizingfield/components/colorpicker`

   * fornito da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Poiché questo meccanismo utilizza JSP, i18n e XSS non sono forniti out-of-the-box. Ciò significa che sarà necessario internazionalizzare ed evitare le Stringhe. La seguente directory contiene i campi generici di un’istanza standard, che potete utilizzare come riferimento:
>
>`/libs/granite/ui/components/foundation/form` directory

## Creazione dello script sul lato server per il componente {#creating-the-server-side-script-for-the-component}

Il campo personalizzato deve sostituire solo lo script `render.jsp`, in cui è possibile fornire la marcatura per il componente. È possibile considerare JSP (ovvero lo script di rendering) come un wrapper per la marcatura.

1. Create un nuovo componente da cui ereditare la proprietà `sling:resourceSuperType`:

   `/libs/granite/ui/components/foundation/form/field`

1. Ignora script:

   `render.jsp`

   In questo script, è necessario generare il markup ipermedia (ad es. il markup arricchito, contenente il costo contenuto dell&#39;ipermedia) in modo che il client sappia come interagire con l&#39;elemento generato. Questo dovrebbe seguire lo stile di codifica lato server dell’interfaccia utente Granite.

   Durante la personalizzazione, l&#39;unico contratto che *è necessario eseguire* consiste nel leggere il valore del modulo (inizializzato in `init.jsp`) dalla richiesta utilizzando:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Per ulteriori dettagli, consultare l&#39;implementazione dei campi predefiniti dell&#39;interfaccia utente Granite; ad esempio, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >Al momento, JSP è il metodo di script preferito, in quanto il passaggio di informazioni da un componente all’altro (che è abbastanza frequente nel contesto di modulo/campi) non è facilmente raggiungibile in HTL.

## Creazione della libreria client per il componente {#creating-the-client-library-for-the-component}

Per aggiungere al componente un comportamento lato client specifico:

1. Creare una clientlib di categoria `cq.authoring.dialog`.
1. Create una clientlib della categoria `cq.authoring.dialog` e definite il `JS`/ `CSS` al suo interno.

   Definite la `JS`/ `CSS` all&#39;interno della clientlib.

   >[!NOTE]
   >
   >Al momento, l&#39;interfaccia utente Granite non fornisce alcun listener o ganci out-of-the-box che è possibile utilizzare direttamente per aggiungere il comportamento JS. Pertanto, per aggiungere un comportamento JS aggiuntivo al componente, è necessario implementare un gancio JS a una classe personalizzata che poi si assegna al componente durante la generazione del markup.

