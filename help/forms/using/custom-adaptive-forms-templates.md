---
title: Creazione di un modello di modulo adattivo personalizzato
description: Questo articolo descrive come creare modelli di moduli adattivi personalizzati.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# Creazione di un modello di modulo adattivo personalizzato{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms ha introdotto modelli dinamici. Puoi utilizzare l’editor di modelli di AEM Sites per [creare o modificare modelli dinamici](../../forms/using/template-editor.md). I modelli menzionati nell’articolo seguente sono modelli statici. Non sono disponibili in un&#39;installazione predefinita. [Installare il pacchetto di compatibilità](../../forms/using/compatibility-package.md) per ottenere questi modelli nel tuo ambiente.

## Prerequisiti {#prerequisites}

* Comprensione dell’AEM [Modello pagina](/help/sites-authoring/templates.md) e [Authoring di moduli adattivi](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* Comprensione dell’AEM [Librerie lato client](/help/sites-developing/clientlibs.md)

## Modello di modulo adattivo {#adaptive-form-template}

Un modello di modulo adattivo è un modello di pagina AEM specializzato, con determinate proprietà e struttura di contenuto utilizzate per creare il modulo adattivo. Il modello dispone di layout, stili e struttura di contenuto iniziale di base preconfigurati.

Dopo la creazione di un modulo, le eventuali modifiche apportate alla struttura originale del contenuto del modello non verranno applicate al modulo.

## Modelli di modulo adattivo predefiniti {#default-adaptive-form-templates}

QuickStart per AEM fornisce i seguenti modelli di moduli adattivi:

* Modello di sondaggio: consente di creare un modulo adattivo a pagina singola utilizzando il layout reattivo con più colonne configurate. Il layout si regola automaticamente in base alle dimensioni delle varie schermate in cui si desidera visualizzare il modulo.
* Modello di iscrizione semplice: consente di creare un modulo adattivo con più passaggi utilizzando un layout di procedura guidata. In questo layout è possibile specificare un&#39;espressione di completamento del passaggio per ogni passaggio, che viene convalidata prima che la procedura guidata passi al passaggio successivo.
* Modello di iscrizione a schede: consente di creare un modulo adattivo con più schede utilizzando un layout tabulazioni a sinistra, in cui è possibile visitare le schede in qualsiasi ordine casuale.
* Modello di iscrizione avanzato: consente di creare un modulo con più schede e procedura guidata. Utilizza un layout tabulazioni a sinistra che consente di visitare le schede in qualsiasi ordine. Utilizza i servizi di progettazione Adobe Document Cloud per la firma e la verifica.
* Modello vuoto: consente di creare un modulo senza intestazione, piè di pagina e contenuto iniziale. È possibile aggiungere componenti quali caselle di testo, pulsanti e immagini. Il modello vuoto consente di creare un modulo [incorporare nelle pagine del sito AEM](/help/forms/using/embed-adaptive-form-aem-sites.md).

Questi modelli presentano `sling:resourceType` proprietà impostata sul componente pagina corrispondente. Il componente Pagina esegue il rendering della pagina CQ, contenente il contenitore di moduli adattivi, che a sua volta esegue il rendering del modulo adattivo.

La tabella seguente enumera l’associazione tra modelli e componente Pagina:

<table>
 <tbody>
  <tr>
   <td><p><strong>Modello</strong></p> </td>
   <td><p><strong>Componente Pagina </strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## Creazione di un modello di modulo adattivo tramite l’editor di modelli {#creating-an-adaptive-form-template-using-template-editor}

Puoi specificare la struttura e il contenuto iniziale di un modulo adattivo utilizzando l’Editor modelli. Ad esempio, si desidera che tutti gli autori di moduli dispongano di poche caselle di testo, pulsanti di spostamento e un pulsante di invio in un modulo di iscrizione. È possibile creare un modello utilizzabile dagli autori per creare un modulo coerente con altri moduli di iscrizione. L’editor di modelli AEM consente di:

* Aggiungere i componenti intestazione e piè di pagina di un modulo nel livello struttura
* Fornire il contenuto iniziale del modulo.
* Specifica un tema.
* Specifica azioni quali invio, ripristino e navigazione.

Per ulteriori informazioni, consulta [Editor modelli](../../forms/using/template-editor.md).

## Creazione di un modello di modulo adattivo da CRXDE {#creating-an-adaptive-form-template-from-crxde}

Invece di utilizzare i modelli disponibili, puoi creare un modello e utilizzarlo per creare moduli adattivi. I modelli personalizzati si basano su vari componenti di pagina che fanno riferimento a contenitori di moduli adattivi ed elementi di pagina, come intestazione e piè di pagina.

Puoi creare questi componenti utilizzando il componente pagina base per il tuo sito web. In alternativa, puoi estendere il componente Pagina del modulo adattivo utilizzato dai modelli predefiniti.

Per creare un modello personalizzato, ad esempio simpleEnrollmentTemplate, effettuare le seguenti operazioni.

1. Passa a CRXDE Liti nell’istanza di authoring.

1. Nella directory /apps, crea la struttura di cartelle per l’applicazione. Ad esempio, se il nome dell’applicazione è società, crea una cartella con questo nome. In genere, la cartella dell&#39;applicazione contiene componenti, configurazione, modelli, src e directory di installazione. Per questo esempio, crea le cartelle dei componenti, della configurazione e dei modelli.

1. Passa alla cartella /libs/fd/af/templates.
1. Copia il `simpleEnrollmentTemplate` nodo.
1. Passa alla cartella /apps/mycompany/templates. Fai clic con il pulsante destro del mouse e seleziona (Confronta periodi di tempo) **[!UICONTROL Incolla]**.
1. Se necessario, rinominate il nodo modello copiato. Ad esempio, rinominarlo come modello di iscrizione.

1. Passa alla posizione /apps/mycompany/templates/enrollment-template.

1. Modifica il `jcr:title` e `jcr:description` proprietà per `jcr:content` per distinguere il modello dal modello copiato.

1. Il `jcr:content` del modello modificato contiene `guideContainer` e `guideformtitle` componenti. `guideContainer` è il contenitore che contiene il modulo adattivo. Il `guideformtitle` Nel componente vengono visualizzati il nome, la descrizione e così via dell&#39;applicazione.

   Invece di `guideformtitle`, è possibile includere un componente personalizzato o `parsys` componente. Ad esempio, rimuovere `guideformtitle`e aggiungere un componente personalizzato o il `parsys` nodo del componente. Assicurati che `sling:resourceType` La proprietà del componente fa riferimento al componente e lo stesso è definito nella pagina `component.jsp` file.

1. Passa alla posizione /apps/mycompany/templates/enrollment-template/jcr:content.

1. Apri **[!UICONTROL Proprietà]** e modificare il valore della `cq:designPath` proprietà di /etc/designs/mycompany.

1. Ora crea un nodo /etc/designs/mycompany per `cq:Page` tipo.

## Creare un componente pagina modulo adattivo {#create-an-adaptive-form-page-component}

Il modello personalizzato ha lo stesso stile del modello predefinito perché il modello fa riferimento al componente pagina /libs/fd/af/components/page/base. Puoi trovare il riferimento al componente come proprietà `sling:resourceType` definito nel nodo /apps/mycompany/templates/enrollment-template/jcr:content. Poiché base è un componente di base, non modificare questo componente.

1. Passa al nodo /apps/mycompany/templates/enrollment-template/jcr:content e modifica il valore della proprietà `sling:resourceType` a /apps/mycompany/components/page/enrollmentpage
1. Copia il nodo /libs/fd/af/components/page/base nella cartella /apps/mycompany/components/page.

1. Rinomina il componente copiato in `enrollmentpage`.

1. **(Solo se si dispone già di una pagina di contenuto)** Effettua i seguenti passaggi (a-d), se disponi di un `contentpage`per il sito web. Se non disponi di un `contentpage`per il sito web, puoi lasciare il `resourceSuperType`per puntare alla pagina di base predefinita.

   1. Per `enrollmentpage` nodo, imposta il valore della proprietà `sling:resourceSuperType` alla pagina azienda/componenti/pagina/contenuto. Il `contentpage` è il componente pagina base del sito. Altri componenti della pagina possono estenderlo. Rimuovi i file script in `enrollmentpage`, tranne `head.jsp`, `content.jsp`, e `library.jsp`. Il `sling:resourceSuperType` componente, che è `contentpage` in questo caso, include tutti questi script. Le intestazioni, incluse la barra di navigazione e il piè di pagina, vengono ereditate da `contentpage` componente.

   1. Apri il file `head.jsp`.

      Il file JSP contiene la riga `<cq.include script="library.jsp"/>`.

      Il `library.jsp` il file contiene `guide.theme.simpleEnrollment` libreria client, che contiene lo stile del modulo adattivo.

      Il componente Pagina `enrollmentpage` dispone di un `head.jsp` file che sostituisce `head.jsp` file del `contentpage` componente.

   1. Includi tutti gli script in `head.jsp` file per `contentpage` componente per `head.jsp` file per `enrollmentpage` componente.
   1. In `content.jsp` , è possibile aggiungere contenuto di pagina aggiuntivo o riferimenti ad altri componenti inclusi durante il rendering di una pagina. Ad esempio, se aggiungi il componente personalizzato `applicationformheader`, accertati di aggiungere il seguente riferimento al componente nel file JSP:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Analogamente, se si aggiunge `parsys` nella struttura dei nodi del modello, includi anche il componente personalizzato.

## Creazione di una libreria client per moduli adattivi {#creating-an-adaptive-form-client-library}

Il `head.jsp` file del `enrollmentpage` il componente per il nuovo modello include una libreria client `guide.theme.simpleEnrollment`. Il modello predefinito utilizza anche questa libreria client. Modifica lo stile nel nuovo modello utilizzando uno dei seguenti metodi:

* Definisci un tema personalizzato e sostituisci il tema predefinito `guide.theme.simpleEnrollment` con il tema personalizzato.
* Definisci una nuova libreria client in /etc/designs/mycompany. Includi la libreria client dopo la voce del tema predefinito nella pagina jsp. Includi tutti gli stili sostituiti e file Java Script aggiuntivi in questa libreria client.

>[!NOTE]
>
>Il tema si riferisce a una libreria client inclusa nel componente pagina utilizzato per eseguire il rendering di un modulo adattivo. La libreria client regola principalmente l’aspetto di un modulo adattivo.
