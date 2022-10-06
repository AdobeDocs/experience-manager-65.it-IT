---
title: Creazione di un modello di modulo adattivo personalizzato
seo-title: Creating a custom adaptive form template
description: Questo articolo descrive come creare modelli di moduli adattivi personalizzati.
seo-description: This article describes how to create custom adaptive form templates.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 0%

---

# Creazione di un modello di modulo adattivo personalizzato{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms ha introdotto i modelli dinamici. Puoi utilizzare l’editor modelli di AEM Sites per [creare o modificare modelli dinamici](../../forms/using/template-editor.md). I modelli menzionati nell’articolo seguente sono modelli statici. Non sono disponibili in un&#39;installazione predefinita. [Installa il pacchetto di compatibilità](../../forms/using/compatibility-package.md) per ottenere questi modelli nel tuo ambiente.

## Prerequisiti {#prerequisites}

* Comprensione di AEM [Modello di pagina](/help/sites-authoring/templates.md) e [Authoring di moduli adattivi](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* Comprensione di AEM [Librerie lato client](/help/sites-developing/clientlibs.md)

## Modello di modulo adattivo {#adaptive-form-template}

Un modello di modulo adattivo è specializzato AEM modello di pagina, con determinate proprietà e struttura del contenuto utilizzata per creare il modulo adattivo. Il modello dispone di layout, stili e struttura di contenuto iniziale di base preconfigurati.

Una volta creato un modulo, le eventuali modifiche apportate alla struttura del contenuto del modello originale non vengono applicate al modulo.

## Modelli di modulo adattivo predefiniti {#default-adaptive-form-templates}

AEM QuickStart fornisce i seguenti modelli di modulo adattivo:

* Modello di sondaggio: Consente di creare un singolo modulo adattivo per pagina utilizzando il layout reattivo con più colonne configurate. Il layout si regola automaticamente in base alle dimensioni delle varie schermate sulle quali si desidera visualizzare il modulo.
* Modello di iscrizione semplice: Consente di creare un modulo adattivo con più passaggi utilizzando un layout guidato. In questo layout è possibile specificare un&#39;espressione di completamento del passaggio per ogni passaggio, che viene convalidata prima che la procedura guidata passi al passaggio successivo.
* Modello di iscrizione a schede: Consente di creare un modulo adattivo con più schede utilizzando un layout tabulazioni a sinistra, in cui è possibile visualizzare le schede in qualsiasi ordine casuale.
* Modello di iscrizione avanzata: Consente di creare un modulo con più schede e procedure guidate. Utilizza un layout tabulazioni a sinistra che ti consente di visitare le schede in qualsiasi ordine. Utilizza i servizi di progettazione Adobe Document Cloud per la firma e la verifica.
* Modello vuoto: Consente di creare un modulo senza intestazione, piè di pagina e contenuto iniziale. È possibile aggiungere componenti quali caselle di testo, pulsanti e immagini. Il modello vuoto consente di creare un modulo che è possibile [incorporare nelle pagine AEM sito](/help/forms/using/embed-adaptive-form-aem-sites.md).

Questi modelli hanno `sling:resourceType` impostata sul componente pagina corrispondente. Il componente pagina esegue il rendering della pagina CQ, contenente il contenitore di moduli adattivi, che a sua volta esegue il rendering del modulo adattivo.

La tabella seguente elenca l’associazione tra modelli e componente pagina:

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
   <td><p>/libs/fd/af/templates/ttabsEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenregistrazione</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedensubscription</p> </td>
  </tr>
 </tbody>
</table>

## Creazione di un modello di modulo adattivo tramite l’editor di modelli {#creating-an-adaptive-form-template-using-template-editor}

È possibile specificare la struttura e il contenuto iniziale di un modulo adattivo utilizzando Editor modelli. Ad esempio, si desidera che tutti gli autori dei moduli dispongano di alcune caselle di testo, dei pulsanti di navigazione e di un pulsante di invio in un modulo di iscrizione. È possibile creare un modello che gli autori possono utilizzare per creare un modulo coerente con gli altri moduli di iscrizione. AEM Editor modelli consente di:

* Aggiunta di componenti di intestazione e piè di pagina di un modulo nel livello struttura
* Fornire il contenuto iniziale del modulo.
* Specifica un tema.
* Specifica azioni quali invio, ripristino e navigazione.

Per ulteriori informazioni, consulta [Editor modelli](../../forms/using/template-editor.md).

## Creazione di un modello di modulo adattivo da CRXDE {#creating-an-adaptive-form-template-from-crxde}

Invece di utilizzare i modelli disponibili, è possibile creare un modello e utilizzarlo per creare moduli adattivi. I modelli personalizzati si basano su vari componenti di pagina che fanno riferimento a contenitori di moduli adattivi e elementi di pagina, ad esempio intestazione e piè di pagina.

Puoi creare questi componenti utilizzando il componente pagina di base per il sito web. In alternativa, è possibile estendere il componente pagina del modulo adattivo utilizzato dai modelli predefiniti.

Esegui i seguenti passaggi per creare un modello personalizzato, ad esempio simpleEnRegistrationTemplate.

1. Passa ad CRXDE Lite nell’istanza di authoring.

1. Nella directory /apps , crea la struttura di cartelle per la tua applicazione. Ad esempio, se il nome dell’applicazione è azienda, crea una cartella con questo nome. In genere, la cartella dell&#39;applicazione contiene componenti, configurazione, modelli, src e directory di installazione. Per questo esempio, crea le cartelle componenti, configurazione e modelli.

1. Passa alla cartella /libs/fd/af/templates.
1. Copia il `simpleEnrollmentTemplate` nodo.
1. Passa alla cartella /apps/mycompany/templates. Fare clic con il pulsante destro del mouse e selezionare **[!UICONTROL Incolla]**.
1. Se necessario, rinominare il nodo del modello copiato. Ad esempio, rinominalo come modello di registrazione.

1. Passa alla posizione /apps/mycompany/templates/enrollment-template.

1. Modifica la `jcr:title` e `jcr:description` proprietà per `jcr:content` per distinguere il modello dal modello copiato.

1. La `jcr:content` il nodo del modello modificato contiene `guideContainer` e `guideformtitle` componenti. `guideContainer` è il contenitore che contiene il modulo adattivo. La `guideformtitle` visualizza il nome dell’applicazione, la descrizione e così via.

   Invece di `guideformtitle`, puoi includere un componente personalizzato o `parsys` componente. Ad esempio, rimuovi `guideformtitle`e aggiungi un componente personalizzato o `parsys` nodo componente. Assicurati che `sling:resourceType` La proprietà del componente fa riferimento al componente e lo stesso è definito nella pagina `component.jsp` file.

1. Passa alla posizione /apps/mycompany/templates/enrollment-template/jcr:content.

1. Apri **[!UICONTROL Proprietà]** e modifica il valore del `cq:designPath` a /etc/designs/mycompany.

1. Ora crea un nodo /etc/designs/mycompany per `cq:Page` digitare.

## Creare un componente per la pagina di un modulo adattivo {#create-an-adaptive-form-page-component}

Il modello personalizzato ha lo stesso stile del modello predefinito, perché fa riferimento al componente pagina /libs/fd/af/components/page/base. È possibile trovare il riferimento al componente come proprietà `sling:resourceType` definito nel nodo /apps/mycompany/templates/enrollment-template/jcr:content. Poiché base è un componente di base del prodotto, non modificare questo componente.

1. Passa al nodo /apps/mycompany/templates/enrollment-template/jcr:content e modifica il valore della proprietà `sling:resourceType` a /apps/mycompany/components/page/enrollpage
1. Copia il nodo /libs/fd/af/components/page/base nella cartella /apps/mycompany/components/page.

1. Rinomina il componente copiato in `enrollmentpage`.

1. **(Solo se disponi già di una pagina di contenuto)** Esegui i seguenti passaggi (a-d), se disponi di un `contentpage`per il sito web. Se non hai un `contentpage`per il sito web, puoi lasciare il `resourceSuperType`per puntare alla pagina di base OOTB.

   1. Per `enrollmentpage` nodo, imposta il valore della proprietà `sling:resourceSuperType` alla mioazienda/componenti/pagina/contentpage. La `contentpage` è il componente della pagina di base per il sito. È possibile estenderlo ad altri componenti della pagina. Rimuovi file di script in `enrollmentpage`, tranne `head.jsp`, `content.jsp`e `library.jsp`. La `sling:resourceSuperType` componente, che è `contentpage` in questo caso, include tutti questi script. Le intestazioni, comprese le barre di navigazione e i piè di pagina, vengono ereditate dal `contentpage` componente.

   1. Aprire il file `head.jsp`.

      Il file JSP contiene la riga `<cq.include script="library.jsp"/>`.

      La `library.jsp` il file contiene `guide.theme.simpleEnrollment` libreria client, che contiene lo stile del modulo adattivo.

      Componente pagina `enrollmentpage` ha un `head.jsp` file che sostituisce il `head.jsp` del `contentpage` componente.

   1. Includi tutti gli script nel `head.jsp` per `contentpage` nella `head.jsp` per `enrollmentpage` componente.
   1. In `content.jsp` è possibile aggiungere contenuto di pagina aggiuntivo o riferimenti ad altri componenti inclusi durante il rendering di una pagina. Ad esempio, se aggiungi il componente personalizzato `applicationformheader`, accertati di aggiungere il seguente riferimento al componente nel file JSP:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Allo stesso modo, se aggiungi un `parsys` nella struttura del nodo del modello, includi anche il componente personalizzato.

## Creazione di una libreria client per moduli adattivi {#creating-an-adaptive-form-client-library}

La `head.jsp` del `enrollmentpage` il componente per il nuovo modello include una libreria client `guide.theme.simpleEnrollment`. Il modello predefinito utilizza anche questa libreria client. Modificare lo stile nel nuovo modello utilizzando uno dei seguenti metodi:

* Definire un tema personalizzato e sostituire il tema predefinito `guide.theme.simpleEnrollment` con il tema personalizzato.
* Definisci una nuova libreria client in /etc/designs/mycompany. Includi la libreria client dopo la voce tema predefinita nella pagina jsp. Includi tutti gli stili ignorati e i file Java Script aggiuntivi in questa libreria client.

>[!NOTE]
>
>Il tema si riferisce a una libreria client inclusa nel componente pagina utilizzato per eseguire il rendering di un modulo adattivo. La libreria client gestisce principalmente l’aspetto di un modulo adattivo.
