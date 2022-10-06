---
title: Personalizzare l’interfaccia utente per la creazione della corrispondenza
seo-title: Customize create correspondence UI
description: Scopri come personalizzare l’interfaccia utente per la corrispondenza.
seo-description: Learn how to customize create correspondence UI.
uuid: 9dee9b6f-4129-4560-9bf8-db48110b76f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 13a93111-c08c-4457-b69a-a6f6eb6da330
docset: aem65
feature: Correspondence Management
exl-id: 9593ca2a-7f9e-4487-a1a5-ca44114bff17
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---

# Personalizzare l’interfaccia utente per la creazione della corrispondenza{#customize-create-correspondence-ui}

## Panoramica {#overview}

Gestione della corrispondenza ti consente di ridefinire il modello di soluzione per migliorare il valore del marchio e di rispettare gli standard di branding della tua organizzazione. Il rebranding dell’interfaccia utente include la modifica del logo dell’organizzazione, visualizzato nell’angolo in alto a sinistra dell’interfaccia utente Crea corrispondenza.

Puoi modificare il logo nell’interfaccia utente Crea corrispondenza con il logo della tua organizzazione.

![Icona personalizzata nell’interfaccia utente Crea corrispondenza](assets/0_1_introscreenshot.png)

Icona personalizzata nell’interfaccia utente Crea corrispondenza

### Modifica del logo nell’interfaccia utente Crea corrispondenza {#changing-the-logo-in-the-create-correspondence-ui}

Per impostare un&#39;immagine del logo desiderato, procedi come segue:

1. Crea il [struttura delle cartelle in CRX](#creatingfolderstructure).
1. [Carica il nuovo file del logo](#uploadlogo) nella cartella creata in CRX.

1. [Configurare il CSS](#createcss) su CRX per fare riferimento al nuovo logo.
1. Cancella la cronologia del browser e [aggiorna l’interfaccia utente Crea corrispondenza](#refreshccrui).

## Creazione della struttura di cartelle richiesta {#creatingfolderstructure}

Creare la struttura delle cartelle, come illustrato di seguito, per ospitare l&#39;immagine del logo personalizzato e il foglio di stile. La nuova struttura di cartelle con la cartella principale /apps è simile alla struttura della cartella /libs .

Per qualsiasi personalizzazione, crea una struttura di cartelle parallela, come spiegato di seguito, nel ramo /apps .

Il ramo /apps (struttura cartelle):

* Assicurati che i file siano sicuri in caso di aggiornamento del sistema. In caso di aggiornamento, feature pack o hotfix, il ramo /libs viene aggiornato e se si ospitano le modifiche nel ramo /libs, queste vengono sovrascritte.
* Ti aiuta a non disturbare il sistema/ramo attuale, che è possibile risolvere per errore se utilizzi le posizioni predefinite per la memorizzazione dei file personalizzati.
* Aiuta le tue risorse a ottenere una priorità più elevata quando AEM ricerca delle risorse. AEM è configurato per cercare prima il ramo /apps e poi il ramo /libs per trovare una risorsa. Questo meccanismo significa che il sistema utilizza la sovrapposizione (e le personalizzazioni ivi definite).

Utilizza i seguenti passaggi per creare la struttura di cartelle richiesta nel ramo /apps :

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Nella cartella delle app, crea una cartella denominata `css` con percorso/struttura simile alla cartella css (che si trova nella cartella ccrui).

   Passaggi per creare la cartella css:

   1. Fai clic con il pulsante destro del mouse sul pulsante **css** nel seguente percorso e seleziona **Nodo di sovrapposizione**: `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![nodo di sovrapposizione](assets/1_overlaynode_css.png)

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css

      **Posizione sovrapposizione:** /apps/

      **Tipi di nodo di corrispondenza:** Selezionato

      ![Percorso del nodo di sovrapposizione](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >Non apportare modifiche al ramo /libs. Eventuali modifiche apportate potrebbero andare perse, in quanto questo ramo è soggetto a modifiche ogni volta che:
      >
      >    
      >    
      >    * Aggiorna l&#39;istanza
      >    * Applicare un hotfix
      >    * Installare un feature pack


   1. Fai clic su **OK**. La cartella css viene creata nel percorso specificato.

1. Nella cartella delle app, crea una cartella denominata `imgs` con percorso/struttura simile alla cartella imgs (che si trova nella cartella ccrui).

   1. Fai clic con il pulsante destro del mouse sul pulsante **imgs** nel seguente percorso e seleziona **Nodo di sovrapposizione**: `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs`
   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs

      **Posizione sovrapposizione:** /apps/

      **Tipi di nodo di corrispondenza:** Selezionato

   1. Fai clic su **OK**.

      >[!NOTE]
      >
      >Puoi anche creare manualmente la struttura delle cartelle nella cartella /apps .

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

## Carica il nuovo logo su CRX {#uploadlogo}

Carica il file del logo personalizzato in CRX. Le regole HTML standard disciplinano il rendering del logo. I formati di file immagine supportati dipendono dal browser utilizzato per accedere ad AEM Forms. Tutti i browser supportano JPEG, GIF e PNG. Per ulteriori informazioni, consulta la documentazione specifica del browser sui formati immagine supportati.

* Le dimensioni predefinite dell’immagine logo sono 48 px &#42; 48 px Assicurati che l&#39;immagine sia simile a questa dimensione o superiore a 48 px &#42; 48 px
* Se l’altezza dell’immagine logo è superiore a 50 px, l’interfaccia utente Crea corrispondenza ridimensiona l’immagine fino a un’altezza massima di 50 px, poiché questa è l’altezza dell’intestazione. Quando si ridimensiona l’immagine, l’interfaccia utente Crea corrispondenza mantiene le proporzioni dell’immagine.
* L’interfaccia utente Crea corrispondenza non ridimensiona l’immagine se è piccola, quindi assicurati di utilizzare un’immagine logo con altezza di almeno 48 px e larghezza sufficiente per chiarezza.

Utilizza i seguenti passaggi per caricare il file del logo personalizzato su CRX:

1. Passa a `https://'[server]:[port]'/[contextpath]/crx/de`. Se necessario, accedi come Amministratore.
1. In CRXDE, fai clic con il pulsante destro del mouse sul pulsante **imgs** nel seguente percorso e seleziona **Crea > Crea file**:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![Crea un nuovo nodo nella cartella imgs](assets/2_contentexplorernewnode.png)

1. Nella finestra di dialogo Crea file , immetti il nome del file come CustomLogo.png (o il nome del file del logo).

   ![CustomLogo.png come nuovo nodo](assets/3_contentexplorernewnode_customlogo.png)

1. Fai clic su **Salva tutto**.

   Sotto il nuovo file creato (qui CustomLogo.png), viene visualizzata la proprietà jcr:content.

1. Fai clic su jcr:content nella struttura delle cartelle.

   vengono visualizzate le proprietà di jcr:content.

   ![jcrcontentproperties](assets/jcrcontentproperties.png)

1. Fai doppio clic sul pulsante **jcr:data** proprietà.

   Viene visualizzata la finestra di dialogo Modifica jcr:data .

   Ora fai clic sulla cartella newlogo.png , fai doppio clic su jcr:content (opzione dim) e imposta il tipo nt:resource. Se non presente, crea una proprietà con nome jcr:content.

1. Nella finestra di dialogo Modifica jcr:data , fai clic su **Sfoglia** e selezionare il file immagine che si desidera utilizzare come logo (qui CustomLogo.png).

   I formati di file immagine supportati dipendono dal browser utilizzato per accedere ad AEM Forms. Tutti i browser supportano JPEG, GIF e PNG. Per ulteriori informazioni, consulta la documentazione specifica del browser sui formati immagine supportati.

   ![Esempio di file di logo personalizzato](assets/geometrixx-outdoors.png)

   Esempio: CustomLogo.png da utilizzare come logo personalizzato

1. Fai clic su **Salva tutto**.

## Crea il CSS per integrare il logo con l’interfaccia utente {#createcss}

L’immagine del logo personalizzato richiede il caricamento di un foglio di stile aggiuntivo nel contesto del contenuto.

Per impostare il foglio di stile per il rendering del logo, attenersi alla procedura descritta di seguito.

1. Passa a `https://'[server]:[port]'/[contextpath]/crx/de`. Se necessario, accedi come Amministratore.
1. Crea un file denominato customcss.css (non puoi usare un nome di file diverso) nella posizione seguente:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   Passaggi per creare il file customcss.css:

   1. Fai clic con il pulsante destro del mouse sul pulsante **css** e seleziona **Crea > Crea file**.
   1. Nella finestra di dialogo Nuovo file , specifica il nome del CSS come `customcss.css`(non è possibile utilizzare un nome di file diverso) e fare clic su **OK**.
   1. Aggiungi il codice seguente al file css appena creato. In content:url nel codice, specifica il nome immagine caricato nella cartella imgs in CRXDE.

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. Fai clic su **Salva tutto**.

## Aggiorna l’interfaccia utente Crea corrispondenza per visualizzare il logo personalizzato {#refreshccrui}

Cancella la cache del browser e apri l’istanza dell’interfaccia utente Crea corrispondenza nel browser. Dovresti visualizzare il tuo logo personalizzato.

![Creare un’interfaccia utente per la corrispondenza con il logo personalizzato](assets/0_1_introscreenshot-1.png)

Icona personalizzata nell’interfaccia utente Crea corrispondenza
