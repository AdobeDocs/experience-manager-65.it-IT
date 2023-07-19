---
title: Personalizzare l’interfaccia utente per la creazione di corrispondenza
seo-title: Customize create correspondence UI
description: Scopri come personalizzare l’interfaccia utente per la creazione di corrispondenza.
seo-description: Learn how to customize create correspondence UI.
uuid: 9dee9b6f-4129-4560-9bf8-db48110b76f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 13a93111-c08c-4457-b69a-a6f6eb6da330
docset: aem65
feature: Correspondence Management
exl-id: 9593ca2a-7f9e-4487-a1a5-ca44114bff17
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# Personalizzare l’interfaccia utente per la creazione di corrispondenza{#customize-create-correspondence-ui}

## Panoramica {#overview}

Gestione della corrispondenza consente di modificare il modello della soluzione per migliorare il valore del brand e aderire agli standard di branding della tua organizzazione. Il rebranding dell’interfaccia utente comporta la modifica del logo dell’organizzazione, visualizzato nell’angolo in alto a sinistra dell’interfaccia utente per la creazione di corrispondenza.

Puoi modificare il logo nell’interfaccia utente per la creazione di corrispondenza con il logo dell’organizzazione.

![Icona personalizzata nell’interfaccia utente per la creazione di corrispondenza](assets/0_1_introscreenshot.png)

Icona personalizzata nell’interfaccia utente per la creazione di corrispondenza

### Modifica del logo nell’interfaccia utente per la creazione di corrispondenza {#changing-the-logo-in-the-create-correspondence-ui}

Per impostare un&#39;immagine del logo a scelta, effettuare le seguenti operazioni:

1. Creare il [struttura delle cartelle in CRX](#creatingfolderstructure).
1. [Carica il nuovo file del logo](#uploadlogo) nella cartella creata in CRX.

1. [Configurare il CSS](#createcss) su CRX per fare riferimento al nuovo logo.
1. Cancella la cronologia del browser e [aggiornare l’interfaccia utente per la creazione di corrispondenza](#refreshccrui).

## Creazione della struttura di cartelle richiesta {#creatingfolderstructure}

Crea la struttura di cartelle, come spiegato di seguito, per ospitare l’immagine del logo personalizzato e il foglio di stile. La nuova struttura di cartelle con la cartella principale /apps è simile alla struttura della cartella /libs.

Per qualsiasi personalizzazione, crea una struttura di cartelle parallela, come spiegato di seguito, nel ramo /apps.

Il ramo /apps (struttura di cartelle):

* Garantisce la sicurezza dei file in caso di aggiornamento del sistema. In caso di aggiornamento, feature pack o correzione rapida, il ramo /libs viene aggiornato e le modifiche nel ramo /libs vengono sovrascritte.
* Consente di non disturbare il sistema/ramo attuale, che è possibile risolvere per errore se si utilizzano i percorsi predefiniti per la memorizzazione dei file personalizzati.
* Consente alle risorse di ottenere una priorità più elevata quando l’AEM cerca le risorse. L’AEM è configurato per cercare prima il ramo /apps e quindi il ramo /libs per trovare una risorsa. Questo meccanismo significa che il sistema utilizza la sovrapposizione (e le personalizzazioni qui definite).

Utilizza i seguenti passaggi per creare la struttura di cartelle richiesta nel ramo /apps:

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedere come amministratore.
1. Nella cartella delle app, crea una cartella denominata `css` con un percorso/struttura simile alla cartella css (che si trova nella cartella ccrui).

   Passaggi per creare la cartella css:

   1. Fare clic con il pulsante destro del mouse **css** cartella nel percorso seguente e selezionare **Sovrapponi nodo**: `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![Sovrapponi nodo](assets/1_overlaynode_css.png)

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css

      **Posizione sovrapposizione:** /apps/

      **Corrispondenza tipi di nodo:** Selezionato

      ![Percorso nodo di sovrapposizione](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >Non apportare modifiche nel ramo /libs. Qualsiasi modifica apportata potrebbe andare persa, poiché questo ramo potrebbe subire modifiche ogni volta che:
      >
      >    
      >    
      >    * Eseguire l’aggiornamento all’istanza
      >    * Applicare un hotfix
      >    * Installare un feature pack
      >    
      >

   1. Fai clic su **OK**. La cartella css viene creata nel percorso specificato.

1. Nella cartella delle app, crea una cartella denominata `imgs` con un percorso/struttura simile alla cartella imgs (che si trova nella cartella ccrui).

   1. Fare clic con il pulsante destro del mouse **img** cartella nel percorso seguente e selezionare **Sovrapponi nodo**: `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs`
   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs

      **Posizione sovrapposizione:** /apps/

      **Corrispondenza tipi di nodo:** Selezionato

   1. Fai clic su **OK**.

      >[!NOTE]
      >
      >Puoi anche creare manualmente la struttura di cartelle nella cartella /apps.

1. Clic **Salva tutto** per salvare le modifiche sul server.

## Carica il nuovo logo in CRX {#uploadlogo}

Carica il file del logo personalizzato su CRX. Il rendering del logo è disciplinato dalle regole standard di HTML. I formati di file di immagine supportati dipendono dal browser utilizzato per accedere ad AEM Forms. Tutti i browser supportano JPEG, GIF e PNG. Per ulteriori informazioni, consulta la documentazione specifica per il browser sui formati di immagine supportati.

* Le dimensioni predefinite dell&#39;immagine del logo sono 48 px &#42; 48 px Assicurati che l’immagine sia simile a questa dimensione o superiore a 48 px &#42; 48 px
* Se l’altezza dell’immagine del logo è superiore a 50 px, l’interfaccia utente Crea corrispondenza ridimensiona l’immagine fino a un’altezza massima di 50 px, in quanto si tratta dell’altezza dell’intestazione. Durante il ridimensionamento dell’immagine, l’interfaccia utente Crea corrispondenza mantiene le proporzioni dell’immagine.
* L&#39;interfaccia utente per la creazione di corrispondenza non consente di ridimensionare l&#39;immagine se è piccola, quindi assicurati di utilizzare un&#39;immagine con logo di almeno 48 px in altezza e larghezza sufficiente per una maggiore chiarezza.

Per caricare il file del logo personalizzato in CRX, effettua le seguenti operazioni:

1. Passa a `https://'[server]:[port]'/[contextpath]/crx/de`. Se necessario, accedi come amministratore.
1. In CRXDE, fai clic con il pulsante destro del mouse su **img** cartella nel percorso seguente e selezionare **Crea > Crea file**:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![Crea nuovo nodo nella cartella imgs](assets/2_contentexplorernewnode.png)

1. Nella finestra di dialogo Crea file, immetti il nome del file come CustomLogo.png (o il nome del file del logo).

   ![CustomLogo.png come nuovo nodo](assets/3_contentexplorernewnode_customlogo.png)

1. Clic **Salva tutto**.

   Nel nuovo file creato (qui CustomLogo.png), viene visualizzata la proprietà jcr:content.

1. Fare clic su jcr:content nella struttura di cartelle.

   jcr:vengono visualizzate le proprietà del contenuto.

   ![jcrcontentproperties](assets/jcrcontentproperties.png)

1. Fai doppio clic su **jcr:data** proprietà.

   Viene visualizzata la finestra di dialogo Modifica jcr:data.

   Ora fai clic sulla cartella newlogo.png, fai doppio clic su jcr:content (opzione dim) e imposta il tipo nt:resource. Se non presente, crea una proprietà denominata jcr:content.

1. Nella finestra di dialogo Modifica jcr:dati, fai clic su **Sfoglia** e selezionare il file di immagine da utilizzare come logo (qui CustomLogo.png).

   I formati di file di immagine supportati dipendono dal browser utilizzato per accedere ad AEM Forms. Tutti i browser supportano JPEG, GIF e PNG. Per ulteriori informazioni, consulta la documentazione specifica per il browser sui formati di immagine supportati.

   ![Esempio di file del logo personalizzato](assets/geometrixx-outdoors.png)

   Esempio: CustomLogo.png da utilizzare come logo personalizzato

1. Clic **Salva tutto**.

## Creare il CSS per integrare il logo con l’interfaccia utente {#createcss}

L&#39;immagine logo personalizzata richiede il caricamento di un foglio di stile aggiuntivo nel contesto del contenuto.

Per impostare il foglio di stile per il rendering del logo, attenersi alla procedura descritta di seguito.

1. Passa a `https://'[server]:[port]'/[contextpath]/crx/de`. Se necessario, accedi come amministratore.
1. Crea un file denominato customcss.css (non è possibile utilizzare un nome file diverso) nel percorso seguente:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   Passaggi per creare il file custom.css:

   1. Fare clic con il pulsante destro del mouse **css** cartella e seleziona **Crea > Crea file**.
   1. Nella finestra di dialogo Nuovo file, specifica il nome del file CSS come `customcss.css`(non è possibile utilizzare un nome file diverso), quindi fare clic su **OK**.
   1. Aggiungi il codice seguente al file css appena creato. In content:url nel codice, specifica il nome dell&#39;immagine caricata nella cartella imgs in CRXDE.

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. Clic **Salva tutto**.

## Aggiorna l’interfaccia utente Crea corrispondenza per visualizzare il logo personalizzato {#refreshccrui}

Cancella la cache del browser e apri l’istanza dell’interfaccia utente Crea corrispondenza nel browser. Dovresti visualizzare il tuo logo personalizzato.

![Creare un’interfaccia utente per la corrispondenza con un logo personalizzato](assets/0_1_introscreenshot-1.png)

Icona personalizzata nell’interfaccia utente per la creazione di corrispondenza
