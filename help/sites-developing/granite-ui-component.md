---
title: Creazione di un nuovo componente campo dell’interfaccia Granite
seo-title: Creating a New Granite UI Field Component
description: L’interfaccia utente Granite offre una serie di componenti progettati per essere utilizzati nei moduli, denominati campi
seo-description: Granite UI provides a range of components designed to be used in forms, called fields
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# Creazione di un nuovo componente campo dell’interfaccia Granite{#creating-a-new-granite-ui-field-component}

L’interfaccia utente Granite offre una serie di componenti progettati per essere utilizzati nei moduli; si chiamano *field* nel vocabolario dell’interfaccia Granite. I componenti standard per moduli Granite sono disponibili in:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Questi campi modulo Granite UI sono di particolare interesse in quanto vengono utilizzati per [finestre di dialogo dei componenti](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Per maggiori dettagli sui campi, consulta la sezione [Documentazione dell’interfaccia utente Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Utilizza il framework Granite UI Foundation per sviluppare e/o estendere i componenti Granite. Sono disponibili due elementi:

* lato server:

   * una raccolta di componenti di base

      * base - modulare, compositore, leggibile, riutilizzabile
      * componenti - Componenti Sling
   * aiutanti per lo sviluppo delle applicazioni


* lato client:

   * una raccolta di clientlibs che forniscono un certo vocabolario (cioè l&#39;estensione del linguaggio HTML) per ottenere modelli di interazione generici tramite un&#39;interfaccia utente guidata da Hypermedia

Componente generico dell’interfaccia utente Granite `field` è composto da due file di interesse:

* `init.jsp`: gestisce la trasformazione generica; l’etichettatura, la descrizione e fornisce il valore del modulo che sarà necessario per eseguire il rendering del campo.
* `render.jsp`: in questo punto viene eseguito il rendering effettivo del campo e deve essere sostituito per il campo personalizzato; è incluso da `init.jsp`.

Fai riferimento alla [Documentazione dell’interfaccia utente Granite - Campo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) se vuoi maggiori dettagli.

Per esempi, consulta:

* `cqgems/customizingfield/components/colorpicker`

   * di cui [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Poiché questo meccanismo utilizza JSP, i18n e XSS non sono preconfigurati. Ciò significa che sarà necessario internazionalizzare e sfuggire alle vostre Strings. La seguente directory contiene i campi generici di un’istanza standard, che puoi utilizzare come riferimento:
>
>`/libs/granite/ui/components/foundation/form` directory

## Creazione dello script lato server per il componente {#creating-the-server-side-script-for-the-component}

Il campo personalizzato deve solo sostituire `render.jsp` script, in cui fornisci il markup per il componente. È possibile considerare il JSP (cioè lo script di rendering) come wrapper per il markup.

1. Crea un nuovo componente che utilizza il `sling:resourceSuperType` da cui ereditare:

   `/libs/granite/ui/components/foundation/form/field`

1. Ignora script:

   `render.jsp`

   In questo script, è necessario generare il markup ipermedia (ad esempio il markup arricchito, contenente il prezzo dell’ipermedia) in modo che il cliente sappia come interagire con l’elemento generato. Questo dovrebbe seguire lo stile di codifica lato server dell&#39;interfaccia utente Granite.

   Quando si personalizza, l&#39;unico contratto che si *deve* eseguire è leggere il valore del modulo (inizializzato in `init.jsp`) dalla richiesta utilizzando:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Per ulteriori dettagli, consulta l’implementazione dei campi predefiniti dell’interfaccia utente Granite; ad esempio, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >Al momento, JSP è il metodo di script preferito, in quanto non è facile passare informazioni da un componente all’altro (che è abbastanza frequente nel contesto di moduli/campi) in HTL.

## Creazione della libreria-client per il componente {#creating-the-client-library-for-the-component}

Per aggiungere al componente un comportamento specifico lato client:

1. Creare una clientlib di una categoria `cq.authoring.dialog`.
1. Creare una clientlib di una categoria `cq.authoring.dialog` e definire le `JS`/ `CSS` dentro.

   Definisci i `JS`/ `CSS` all’interno di clientlib.

   >[!NOTE]
   >
   >Al momento, l’interfaccia utente Granite non fornisce alcun listener o hook preconfigurati che è possibile utilizzare direttamente per aggiungere il comportamento JS. Quindi, per aggiungere ulteriori comportamenti JS al componente, devi implementare un hook JS a una classe personalizzata che poi assegni al componente durante la generazione del markup.
