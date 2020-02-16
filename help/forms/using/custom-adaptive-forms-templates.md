---
title: Creazione di un modello di modulo adattivo personalizzato
seo-title: Creazione di un modello di modulo adattivo personalizzato
description: Questo articolo descrive come creare modelli di modulo adattivo personalizzati.
seo-description: Questo articolo descrive come creare modelli di modulo adattivo personalizzati.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe

---


# Creazione di un modello di modulo adattivo personalizzato{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms ha introdotto i modelli dinamici. Puoi usare l’editor modelli di AEM Sites per [creare o modificare modelli](../../forms/using/template-editor.md)dinamici. I modelli menzionati nell&#39;articolo seguente sono modelli statici. Non sono disponibili in un&#39;installazione predefinita. [Installate il pacchetto](../../forms/using/compatibility-package.md) Compatibilità per inserire questi modelli nell&#39;ambiente.

## Prerequisiti {#prerequisites}

* Informazioni sul modello [di](/help/sites-authoring/templates.md) pagina AEM e sull’authoring dei moduli [adattivi](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* Informazioni sulle librerie lato [client AEM](/help/sites-developing/clientlibs.md)

## Adaptive form template {#adaptive-form-template}

Un modello di modulo adattivo è un modello di pagina AEM specializzato, con determinate proprietà e struttura del contenuto utilizzata per creare il modulo adattivo. Il modello include layout, stili e struttura di contenuto iniziale preconfigurata.

Una volta creato il modulo, le modifiche apportate alla struttura del contenuto del modello originale non vengono applicate al modulo.

## Modelli di modulo adattivo predefiniti {#default-adaptive-form-templates}

AEM QuickStart offre i seguenti modelli di modulo adattivo:

* Modello di sondaggio: Consente di creare un singolo modulo adattivo per pagina utilizzando il layout Reattivo con più colonne configurate. Il layout si regola automaticamente in base alle dimensioni delle varie schermate sulle quali si desidera visualizzare il modulo.
* Modello di iscrizione semplice: Consente di creare un modulo adattivo con più passaggi utilizzando un layout guidato. In questo layout, è possibile specificare un&#39;espressione completamento passo per ogni passaggio, che viene convalidata prima che la procedura guidata prosegua con il passaggio successivo.
* Modello di iscrizione a schede: Consente di creare un modulo adattivo con più schede utilizzando un layout tabulazioni a sinistra, in cui è possibile consultare le schede in qualsiasi ordine casuale.
* Modello di iscrizione avanzata: Consente di creare un modulo con più schede e procedure guidate. Utilizza un layout tabulazioni a sinistra che consente di visitare le schede in qualsiasi ordine. Utilizza i servizi di progettazione di Adobe Document Cloud per la firma e la verifica.
* Modello vuoto: Consente di creare un modulo senza intestazione, piè di pagina e contenuto iniziale. È possibile aggiungere componenti quali caselle di testo, pulsanti e immagini. Il modello vuoto consente di creare un modulo da [incorporare nelle pagine](/help/forms/using/embed-adaptive-form-aem-sites.md)del sito AEM.

Questi modelli hanno la `sling:resourceType` proprietà impostata sul componente pagina corrispondente. Il componente Pagina esegue il rendering della pagina CQ, contenente un contenitore di moduli adattivi, che a sua volta esegue il rendering del modulo adattivo.

La tabella seguente elenca l&#39;associazione tra i modelli e il componente pagina:

<table>
 <tbody>
  <tr>
   <td><p><strong>Modello</strong></p> </td>
   <td><p><strong>Componente pagina</strong></p> </td>
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
   <td><p>/libs/fd/af/templates/taccollEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## Creazione di un modello di modulo adattivo mediante l&#39;editor modelli {#creating-an-adaptive-form-template-using-template-editor}

È possibile specificare la struttura e il contenuto iniziale di un modulo adattivo utilizzando l&#39;Editor modelli. Ad esempio, si desidera che tutti gli autori dei moduli dispongano di alcune caselle di testo, di pulsanti di navigazione e di un pulsante di invio in un modulo di iscrizione. È possibile creare un modello che gli autori possano utilizzare per creare un modulo coerente con altri moduli di iscrizione. AEM Template Editor consente di:

* Aggiungere componenti di intestazione e piè di pagina di un modulo nel livello struttura
* Fornire il contenuto iniziale per il modulo.
* Specificate un tema.
* Specificate azioni quali Invia, Reimposta e Naviga.

Per ulteriori informazioni, vedere Editor [](../../forms/using/template-editor.md)modelli.

## Creazione di un modello di modulo adattivo da CRXDE {#creating-an-adaptive-form-template-from-crxde}

Invece di utilizzare i modelli disponibili, è possibile creare un modello e utilizzarlo per creare moduli adattivi. I modelli personalizzati si basano su vari componenti di pagina che fanno riferimento ai contenitori di moduli adattivi e agli elementi di pagina, come intestazione e piè di pagina.

Potete creare questi componenti utilizzando il componente Pagina di base per il sito Web. In alternativa, è possibile estendere il componente pagina del modulo adattivo utilizzato dai modelli predefiniti.

Per creare un modello personalizzato, ad esempio simpleEnrollmentTemplate, effettuate le seguenti operazioni.

1. Passa a CRXDE Lite nell’istanza di authoring.

1. Nella directory /apps, create la struttura di cartelle per l’applicazione. Ad esempio, se il nome dell’applicazione è una mia società, create una cartella con questo nome. In genere, la cartella dell&#39;applicazione contiene componenti, configurazione, modelli, src e directory di installazione. Per questo esempio, create le cartelle componenti, configurazione e modelli.

1. Andate alla cartella /libs/fd/af/templates.
1. Copiare il `simpleEnrollmentTemplate` nodo.
1. Andate alla cartella /apps/mycompany/templates. Fare clic con il pulsante destro del mouse e selezionare **[!UICONTROL Incolla]**.
1. Se necessario, rinominare il nodo del modello copiato. Ad esempio, rinominatelo come modello di iscrizione.

1. Andate alla posizione /apps/mycompany/templates/enrollment-template.

1. Modificate le proprietà `jcr:title` e `jcr:description` del `jcr:content` nodo per distinguere il modello dal modello copiato.

1. Il `jcr:content` nodo del modello modificato contiene i `guideContainer` componenti e `guideformtitle` . `guideContainer` è il contenitore che contiene il modulo adattivo. Il `guideformtitle` componente visualizza il nome dell’applicazione, la descrizione e così via.

   Invece di `guideformtitle`, potete includere un componente personalizzato o il `parsys` componente. Ad esempio, rimuovere `guideformtitle`e aggiungere un componente personalizzato o il nodo del `parsys` componente. Assicurarsi che la `sling:resourceType` proprietà del componente faccia riferimento al componente e che lo stesso sia definito nel file della pagina `component.jsp` .

1. Andate alla posizione /apps/mycompany/templates/enrollment-template/jcr:content.

1. Aprite la scheda **[!UICONTROL Proprietà]** e modificate il valore della `cq:designPath` proprietà in /etc/designs/mycompany.

1. Ora create un nodo /etc/designs/mycompany per il `cq:Page` tipo.

## Creare un componente per pagina di modulo adattivo {#create-an-adaptive-form-page-component}

Il modello personalizzato ha lo stesso stile del modello predefinito, in quanto fa riferimento al componente di pagina /libs/fd/af/components/page/base. Potete trovare il riferimento al componente come proprietà `sling:resourceType` definita nel nodo /apps/mycompany/templates/enrollment-template/jcr:content. Poiché base è un componente di base, non modificate questo componente.

1. Andate al nodo /apps/mycompany/templates/enrollment-template/jcr:content e modificate il valore della proprietà `sling:resourceType` in /apps/mycompany/components/page/enrollpage
1. Copiate il nodo /libs/fd/af/components/page/base nella cartella /apps/mycompany/components/page.

1. Rinominare il componente copiato in `enrollmentpage`.

1. **(Solo se disponete già di una pagina di contenuto)** Effettuate i seguenti passaggi (a-d), se disponete di un `contentpage`componente esistente per il sito Web. Se non disponete di un `contentpage`componente esistente per il sito Web, potete lasciare la `resourceSuperType`proprietà in modo che punti alla pagina di base OOTB.

   1. Per il `enrollmentpage` nodo, impostate il valore della proprietà `sling:resourceSuperType` su miosocietà/componenti/pagina/contenuto. Il `contentpage` componente è il componente della pagina di base per il sito. È possibile estendere anche altri componenti della pagina. Rimuovete i file di script in `enrollmentpage`, tranne `head.jsp`, `content.jsp`e `library.jsp`. Il `sling:resourceSuperType` componente, che in questo caso `contentpage` include tutti questi script. Le intestazioni, inclusa la barra di navigazione e il piè di pagina, vengono ereditate dal `contentpage` componente.

   1. Aprire il file `head.jsp`.

      Il file JSP contiene la riga `<cq.include script="library.jsp"/>`.

      Il `library.jsp` file contiene la libreria `guide.theme.simpleEnrollment` client, che contiene lo stile del modulo adattivo.

      Il componente Pagina `enrollmentpage` dispone di un `head.jsp` file esclusivo che sostituisce il `head.jsp` file del `contentpage` componente.

   1. Includere tutti gli script nel `head.jsp` file del `contentpage` componente nel `head.jsp` file del `enrollmentpage` componente.
   1. Nello `content.jsp` script, è possibile aggiungere contenuto di pagina aggiuntivo o riferimenti ad altri componenti inclusi durante il rendering di una pagina. Ad esempio, se aggiungete il componente personalizzato `applicationformheader`, accertatevi di aggiungere il seguente riferimento al componente nel file JSP:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Analogamente, se aggiungete un `parsys` componente nella struttura del nodo del modello, includete anche il componente personalizzato.

## Creazione di una libreria client per moduli adattivi {#creating-an-adaptive-form-client-library}

Il `head.jsp` file del `enrollmentpage` componente per il nuovo modello include una libreria client `guide.theme.simpleEnrollment`. Anche il modello predefinito utilizza questa libreria client. Modificate lo stile nel nuovo modello utilizzando uno dei seguenti metodi:

* Definire un tema personalizzato e sostituire il tema predefinito `guide.theme.simpleEnrollment` con il tema personalizzato.
* Definite una nuova libreria client in /etc/designs/mycompany. Includete la libreria client dopo la voce tema predefinita nella pagina jsp. Includi tutti gli stili sovrascritti e i file Java Script aggiuntivi in questa libreria client.

>[!NOTE]
>
>Il tema si riferisce a una libreria client inclusa nel componente della pagina utilizzato per il rendering di un modulo adattivo. La libreria del client regola principalmente l&#39;aspetto di un modulo adattivo.

