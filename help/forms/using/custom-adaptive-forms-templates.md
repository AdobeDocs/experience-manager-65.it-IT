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
feature: Adaptive Forms,Foundation Components
source-git-commit: 5723e9990969dff1b508062d69a68f68a20eb576
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# Creazione di un modello di modulo adattivo personalizzato{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms ha introdotto modelli dinamici. È possibile utilizzare l&#39;editor modelli di AEM Sites per [creare o modificare modelli dinamici](../../forms/using/template-editor.md). I modelli menzionati nell’articolo seguente sono modelli statici. Non sono disponibili in un&#39;installazione predefinita. [Installa il pacchetto di compatibilità](../../forms/using/compatibility-package.md) per ottenere questi modelli nel tuo ambiente.

## Prerequisiti {#prerequisites}

* Informazioni su [Modello pagina](/help/sites-authoring/templates.md) e [Authoring moduli adattivi](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html) dell&#39;AEM

* Informazioni sulle [librerie lato client](/help/sites-developing/clientlibs.md) dell&#39;AEM

## Modello di modulo adattivo {#adaptive-form-template}

Un modello di modulo adattivo è un modello di pagina AEM specializzato, con determinate proprietà e struttura di contenuto utilizzate per creare il modulo adattivo. Il modello dispone di layout, stili e struttura di contenuto iniziale di base preconfigurati.

Dopo la creazione di un modulo, le eventuali modifiche apportate alla struttura originale del contenuto del modello non verranno applicate al modulo.

## Modelli di modulo adattivo predefiniti {#default-adaptive-form-templates}

QuickStart per AEM fornisce i seguenti modelli di moduli adattivi:

* Modello di sondaggio: consente di creare un modulo adattivo a pagina singola utilizzando il layout reattivo con più colonne configurate. Il layout si regola automaticamente in base alle dimensioni delle varie schermate in cui si desidera visualizzare il modulo.
* Modello di iscrizione semplice: consente di creare un modulo adattivo con più passaggi utilizzando un layout di procedura guidata. In questo layout è possibile specificare un&#39;espressione di completamento del passaggio per ogni passaggio, che viene convalidata prima che la procedura guidata passi al passaggio successivo.
* Modello di iscrizione a schede: consente di creare un modulo adattivo con più schede utilizzando un layout tabulazioni a sinistra, in cui è possibile visitare le schede in qualsiasi ordine casuale.
* Modello di iscrizione avanzato: consente di creare un modulo con più schede e procedura guidata. Utilizza un layout tabulazioni a sinistra che consente di visitare le schede in qualsiasi ordine. Utilizza i servizi di progettazione Adobe Document Cloud per la firma e la verifica.
* Modello vuoto: consente di creare un modulo senza intestazione, piè di pagina e contenuto iniziale. È possibile aggiungere componenti quali caselle di testo, pulsanti e immagini. Il modello vuoto ti consente di creare un modulo che puoi [incorporare nelle pagine del sito AEM](/help/forms/using/embed-adaptive-form-aem-sites.md).

Per questi modelli la proprietà `sling:resourceType` è impostata sul componente pagina corrispondente. Il componente Pagina esegue il rendering della pagina CQ, contenente il contenitore di moduli adattivi, che a sua volta esegue il rendering del modulo adattivo.

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

Per ulteriori informazioni, vedere [Editor modelli](../../forms/using/template-editor.md).

## Creazione di un modello di modulo adattivo da CRXDE {#creating-an-adaptive-form-template-from-crxde}

Invece di utilizzare i modelli disponibili, puoi creare un modello e utilizzarlo per creare moduli adattivi. I modelli personalizzati si basano su vari componenti di pagina che fanno riferimento a contenitori di moduli adattivi ed elementi di pagina, come intestazione e piè di pagina.

Puoi creare questi componenti utilizzando il componente pagina base per il tuo sito web. In alternativa, puoi estendere il componente Pagina del modulo adattivo utilizzato dai modelli predefiniti.

Per creare un modello personalizzato, ad esempio simpleEnrollmentTemplate, effettuare le seguenti operazioni.

1. Passa a CRXDE Lite nell’istanza di authoring.

1. Nella directory /apps, crea la struttura di cartelle per l’applicazione. Ad esempio, se il nome dell’applicazione è società, crea una cartella con questo nome. In genere, la cartella dell&#39;applicazione contiene componenti, configurazione, modelli, src e directory di installazione. Per questo esempio, crea le cartelle dei componenti, della configurazione e dei modelli.

1. Passa alla cartella /libs/fd/af/templates.
1. Copia il nodo `simpleEnrollmentTemplate`.
1. Passa alla cartella /apps/mycompany/templates. Fare clic con il pulsante destro del mouse e selezionare **[!UICONTROL Incolla]**.
1. Se necessario, rinominate il nodo modello copiato. Ad esempio, rinominarlo come modello di iscrizione.

1. Passa alla posizione /apps/mycompany/templates/enrollment-template.

1. Modificare le proprietà `jcr:title` e `jcr:description` per il nodo `jcr:content` per distinguere il modello dal modello copiato.

1. Il nodo `jcr:content` del modello modificato contiene i componenti `guideContainer` e `guideformtitle`. `guideContainer` è il contenitore che contiene il modulo adattivo. Il componente `guideformtitle` visualizza il nome, la descrizione e così via dell&#39;applicazione.

   Invece di `guideformtitle`, puoi includere un componente personalizzato o il componente `parsys`. Rimuovere ad esempio `guideformtitle` e aggiungere un componente personalizzato o il nodo del componente `parsys`. Assicurarsi che la proprietà `sling:resourceType` del componente faccia riferimento al componente e che lo stesso sia definito nel file `component.jsp` della pagina.

1. Passa alla posizione /apps/mycompany/templates/enrollment-template/jcr:content.

1. Aprire la scheda **[!UICONTROL Proprietà]** e modificare il valore della proprietà `cq:designPath` in /etc/designs/mycompany.

1. Ora crea un nodo /etc/designs/mycompany per il tipo `cq:Page`.

## Creare un componente pagina modulo adattivo {#create-an-adaptive-form-page-component}

Il modello personalizzato ha lo stesso stile del modello predefinito perché il modello fa riferimento al componente pagina /libs/fd/af/components/page/base. Il riferimento al componente è la proprietà `sling:resourceType` definita nel nodo /apps/mycompany/templates/enrollment-template/jcr:content. Poiché base è un componente di base, non modificare questo componente.

1. Passa al nodo /apps/mycompany/templates/enrollment-template/jcr:content e modifica il valore della proprietà `sling:resourceType` in /apps/mycompany/components/page/enrollmentpage
1. Copia il nodo /libs/fd/af/components/page/base nella cartella /apps/mycompany/components/page.

1. Rinomina il componente copiato in `enrollmentpage`.

1. **(Solo se si dispone già di una pagina di contenuto)** Eseguire i passaggi seguenti (a-d), se si dispone di un componente `contentpage` esistente per il sito Web. Se non disponi di un componente `contentpage` esistente per il sito Web, puoi lasciare la proprietà `resourceSuperType`per puntare alla pagina di base predefinita.

   1. Per il nodo `enrollmentpage`, impostare il valore della proprietà `sling:resourceSuperType` su mycompany/components/page/contentpage. Il componente `contentpage` è il componente della pagina base per il sito. Altri componenti della pagina possono estenderlo. Rimuovere i file di script in `enrollmentpage`, ad eccezione di `head.jsp`, `content.jsp` e `library.jsp`. Il componente `sling:resourceSuperType`, che in questo caso è `contentpage`, include tutti questi script. Le intestazioni, inclusi la barra di navigazione e il piè di pagina, sono ereditati dal componente `contentpage`.

   1. Aprire il file `head.jsp`.

      Il file JSP contiene la riga `<cq.include script="library.jsp"/>`.

      Il file `library.jsp` contiene la libreria client `guide.theme.simpleEnrollment`, che contiene lo stile del modulo adattivo.

      Il componente pagina `enrollmentpage` ha un file `head.jsp` esclusivo che sostituisce il file `head.jsp` del componente `contentpage`.

   1. Includere tutti gli script nel file `head.jsp` per il componente `contentpage` nel file `head.jsp` per il componente `enrollmentpage`.
   1. Nello script `content.jsp` è possibile aggiungere contenuto pagina aggiuntivo o riferimenti ad altri componenti inclusi durante il rendering di una pagina. Ad esempio, se aggiungi il componente personalizzato `applicationformheader`, accertati di aggiungere il seguente riferimento al componente nel file JSP:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Analogamente, se si aggiunge un componente `parsys` nella struttura del nodo del modello, includere anche il componente personalizzato.

## Creazione di una libreria client per moduli adattivi {#creating-an-adaptive-form-client-library}

Il file `head.jsp` del componente `enrollmentpage` per il nuovo modello include una libreria client `guide.theme.simpleEnrollment`. Il modello predefinito utilizza anche questa libreria client. Modifica lo stile nel nuovo modello utilizzando uno dei seguenti metodi:

* Definire un tema personalizzato e sostituire il tema predefinito `guide.theme.simpleEnrollment` con il tema personalizzato.
* Definisci una nuova libreria client in /etc/designs/mycompany. Includi la libreria client dopo la voce del tema predefinito nella pagina jsp. Includi tutti gli stili sostituiti e file Java Script aggiuntivi in questa libreria client.

>[!NOTE]
>
>Il tema si riferisce a una libreria client inclusa nel componente pagina utilizzato per eseguire il rendering di un modulo adattivo. La libreria client regola principalmente l’aspetto di un modulo adattivo.
