---
title: Profili immagine Dynamic Media
description: Crea profili immagine contenenti impostazioni per maschera non affilata, ritaglio avanzato, campione avanzato o entrambi, quindi applica il profilo a una cartella di risorse immagine.
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
feature: Image Profiles
role: User, Admin
exl-id: 67240ad0-1a7c-4e58-a518-1e36d771f1a1
source-git-commit: d83a647d8ac5466ba09230c584d5d501aab55274
workflow-type: tm+mt
source-wordcount: '2831'
ht-degree: 10%

---

# Profili immagine Dynamic Media {#image-profiles}

Quando carichi le immagini, puoi ritagliare automaticamente l’immagine al momento del caricamento applicando un profilo immagine alla cartella.

>[!NOTE]
>
>Smart Crop è disponibile solo in modalità Dynamic Media - Scene7.

>[!IMPORTANT]
>
>I profili immagine non sono applicabili ai file PDF, animated GIF o INDD (Adobe InDesign).

## Opzioni di ritaglio {#crop-options}

Quando implementi il ritaglio avanzato sulle immagini, Adobe consiglia la seguente best practice e applica il seguente limite:

| Tipo di limite | Best practice | Limite imposto | Modifica del limite il 31 dicembre 2022 |
| --- | --- | --- | --- |
| Numero di ritagli avanzati per immagine | 5 | 100 | 20 |

Vedi anche [Limiti Dynamic Media](/help/assets/limitations.md).

<!-- CQDOC-16069 for paragraph directly below -->

Le coordinate di ritaglio avanzato dipendono dalle proporzioni. Per le varie impostazioni di ritaglio avanzato in un profilo immagine, se le proporzioni sono le stesse per le dimensioni aggiunte nel profilo immagine, le stesse proporzioni vengono inviate a Dynamic Media. Adobe consiglia di utilizzare la stessa area di ritaglio. In questo modo si garantisce che non vi sia alcun impatto sulle diverse dimensioni utilizzate nel profilo immagine.

Per ogni generazione di ritaglio avanzato creata è necessaria un’elaborazione aggiuntiva. Ad esempio, l’aggiunta di più di cinque rapporti di formato Ritaglio avanzato può causare un tasso di inserimento delle risorse lento. Provoca inoltre un aumento del carico sui sistemi. Poiché è possibile applicare Smart Crop a livello di cartella, Adobe consiglia di utilizzarlo nelle cartelle *only* dove è necessario.

Potete scegliere tra due opzioni di ritaglio immagine. È inoltre disponibile un’opzione per automatizzare la creazione di campioni di colore e immagine.

| Opzione | Quando utilizzare | Descrizione |
| --- | --- | --- |
| Ritaglio pixel | Le immagini ritagliate in blocco in base solo alle dimensioni. | Per utilizzare questa opzione, seleziona **[!UICONTROL Ritaglio pixel]** dall’elenco a discesa Opzioni di ritaglio .<br><br>Per ritagliare dai lati di un’immagine, immetti il numero di pixel da ritagliare da qualsiasi lato o lato dell’immagine. La quantità di immagine ritagliata dipende dall’impostazione ppi (pixel per pollice) nel file di immagine.<br><br>Il rendering di un ritaglio pixel del profilo immagine avviene nel modo seguente:<br>・ I valori sono Superiore, Inferiore, Sinistra e Destra.<br>・ In alto a sinistra è considerato `0,0` e il ritaglio pixel viene calcolato da lì.<br>・ Punto di partenza del ritaglio: La sinistra è X e la parte superiore è Y<br>・ Calcolo orizzontale: dimensione pixel orizzontale dell&#39;immagine originale meno sinistro e quindi meno destro.<br>・ Calcolo verticale: altezza pixel verticale meno superiore, quindi meno inferiore.<br><br>Ad esempio, supponiamo di avere un&#39;immagine di 4000 x 3000 pixel. I valori vengono utilizzati: Top=250, Bottom=500, Left=300, Right=700.<br><br>Dall’alto a sinistra (300.250) ritagliare utilizzando lo spazio di riempimento di (4000-300-700, 3000-250-500, o 3000.2250). |
| Ritaglio avanzato | Ritaglio in serie di immagini in base al loro punto focale visivo. | Smart Crop utilizza la potenza dell&#39;intelligenza artificiale in Adobe Sensei per automatizzare rapidamente il ritaglio delle immagini in blocco. Smart Crop rileva e ritaglia automaticamente il punto focale in qualsiasi immagine per catturare il punto di interesse desiderato, indipendentemente dalle dimensioni dello schermo.</p> <p>Per utilizzare il ritaglio avanzato, seleziona **[!UICONTROL Ritaglio avanzato]** dall’elenco a discesa Opzioni di ritaglio , a destra di Ritaglio immagine reattivo, abilita (attiva) la funzione.</p> <p>Le dimensioni predefinite dei punti di interruzione di grandi, medi e piccoli coprono in genere l&#39;intera gamma di dimensioni che la maggior parte delle immagini vengono utilizzate su dispositivi mobili e tablet, desktop e banner. Se lo desideri, puoi modificare i nomi predefiniti di Grande, Medio e Piccolo.</p> <p>Per aggiungere altri punti di interruzione, seleziona **[!UICONTROL Aggiungi ritaglio]** per eliminare un ritaglio, seleziona l’icona Garbage Can . |
| Campione immagine e colore | Bulk genera un campione immagine per ogni immagine. | **Nota**: Lo Smart Swatch non è supportato in Dynamic Media Classic.<br><br>Individua e genera automaticamente campioni di alta qualità dalle immagini dei prodotti che mostrano colore o texture.<br><br>Per utilizzare Colore e Campione immagine, selezionare **[!UICONTROL Ritaglio avanzato]** dall’elenco a discesa Opzioni di ritaglio, quindi a destra di Colore e Campione immagine, abilita (attiva) la funzione. Immettere un valore in pixel nelle caselle di testo Larghezza e Altezza.<br><br>Mentre tutti i ritagli immagine sono disponibili nella barra Rendering , i campioni vengono utilizzati solo tramite la funzione Copia URL . Utilizza il tuo componente di visualizzazione per eseguire il rendering del campione sul sito. (L’eccezione a questa regola è rappresentata dai banner a carosello. Dynamic Media fornisce il componente di visualizzazione per il campione utilizzato nei banner a carosello.)<br><br>**Utilizzo dei campioni immagine**<br> L’URL per i campioni immagine è semplice. È:<br><br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>dove `:Swatch` viene aggiunto alla richiesta di risorse.<br><br>**Utilizzo dei campioni colore**<br> Per utilizzare i campioni colore, effettuate una `req=userdata` richiedere quanto segue:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Ad esempio, di seguito è riportata una risorsa campione in Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>ed ecco il corrispondente della risorsa campione `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br><br>La `req=userdata` la risposta è la seguente:<br>`SmartCropDef=Swatch SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br><br>Puoi anche richiedere un `req=userdata` risposta in formato XML o JSON, come nei seguenti esempi URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Nota:** Crea il tuo componente WCM per richiedere un campione di colore e analizzare il `SmartSwatchColor` , rappresentato da un valore esadecimale RGB a 24 bit.<br><br>Vedi anche [`userdata` nella guida di riferimento visualizzatori](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html). |

## Maschera di contrasto {#unsharp-mask}

Usa **[!UICONTROL Maschera definizione dettagli]** per regolare con precisione un effetto filtro di nitidezza sull’immagine ricampionata verso il basso finale. Puoi controllare l’intensità dell’effetto, il raggio in pixel e una soglia di contrasto da ignorare. Questo effetto utilizza le stesse opzioni di Adobe Photoshop *Maschera definizione dettagli* filtro.

>[!NOTE]
>
>Maschera definizione dettagli viene applicata solo alle rappresentazioni ridimensionate all’interno del PTIFF (TIFF piramidale) che vengono sottoposte a sottocampionamento superiore al 50%. Ciò significa che le rappresentazioni di grandi dimensioni all’interno del font non sono influenzate da una maschera di contrasto, mentre le rappresentazioni di dimensioni più piccole, come le miniature, vengono modificate (e mostrano la maschera di contrasto).

In **[!UICONTROL Maschera definizione dettagli]**, sono disponibili le seguenti opzioni di filtro:

| Opzione | Descrizione |
| --- | --- |
| Quantità | Controlla la quantità di contrasto applicata ai pixel del bordo. Il valore predefinito è 1,75. Per le immagini ad alta risoluzione, è possibile aumentarlo fino a 5. Considera Importo come una misura dell&#39;intensità del filtro. L&#39;intervallo è compreso tra 0 e 5. |
| Raggio | Determina quanti pixel attorno al bordo vengono interessati dalla nitidezza. Per le immagini ad alta risoluzione, inserite un valore da 1 a 2. Un valore basso agisce solo sui pixel del bordo; un valore più elevato agisce su una fascia più ampia di pixel. Il valore adatto dipende dalle dimensioni dell&#39;immagine. Il valore predefinito è 0,2. Intervallo compreso tra 0 e 250. |
| Soglia | Determina l&#39;intervallo di contrasto da ignorare quando viene applicato il filtro Maschera definizione dettagli. In altre parole, questa opzione determina la differenza tra i pixel da rendere più nitidi rispetto all’area circostante, prima che vengano considerati pixel del bordo e resi più nitidi. Per evitare di introdurre rumore, prova con valori compresi tra 0 e 255. |

La nitidezza è descritta in [Nitidezza delle immagini](/help/assets/assets/sharpening_images.pdf)

## Creare profili immagine Dynamic Media {#creating-image-profiles}

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione delle risorse](config-dms7.md#configuring-asset-processing).

Vedi [Profili per elaborazione di metadati, immagini e video](processing-profiles.md).

Vedi anche [Tecniche consigliate per l’organizzazione delle risorse digitali per l’utilizzo dei profili di elaborazione](/help/assets/organize-assets.md).

**Per creare profili immagine Dynamic Media:**

1. Seleziona il logo Adobe Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Seleziona **[!UICONTROL Crea]** puoi aggiungere un profilo immagine.
1. Inserisci un nome di profilo e valori per maschera non affilata, ritaglio o campione o entrambi.

   Utilizza un nome di profilo specifico per lo scopo a cui è destinato. Ad esempio, se desideri creare un profilo che generi solo i campioni, ovvero se Smart Crop è disattivato e se Color e Image Swatch è abilitato (attivato), utilizza il nome del profilo &quot;Smart Swatches&quot;.

   Consulta anche la sezione [Opzioni di ritaglio avanzato e campione avanzato](#crop-options) e [Maschera definizione dettagli](#unsharp-mask).

   ![coltura](assets/crop.png)

1. Seleziona **[!UICONTROL Salva]**. Il nuovo profilo creato viene visualizzato nell’elenco dei profili disponibili.

## Modificare o eliminare profili immagine Dynamic Media {#editing-or-deleting-image-profiles}

1. Seleziona il logo dell’Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Seleziona il profilo immagine da modificare o rimuovere. Per modificarlo, seleziona **[!UICONTROL Modifica profilo immagine]**. Per rimuoverlo, seleziona **[!UICONTROL Elimina profilo immagine]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. In caso di modifica, salva le modifiche. Se si esegue l’eliminazione, confermare la rimozione del profilo.

## Applicare un profilo immagine Dynamic Media alle cartelle {#applying-an-image-profile-to-folders}

Quando assegni un profilo immagine a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla relativa cartella principale. Questo flusso di lavoro consente di assegnare un solo profilo immagine a una cartella. Considera attentamente la struttura delle cartelle in cui caricare, archiviare, utilizzare e archiviare le risorse.

Se hai assegnato un profilo immagine diverso a una cartella, il nuovo profilo sostituisce il profilo precedente. Le risorse della cartella esistenti in precedenza rimangono invariate. Il nuovo profilo viene applicato alle risorse aggiunte successivamente alla cartella.

Le cartelle a cui è assegnato un profilo sono indicate nell’interfaccia utente utilizzando il nome del profilo visualizzato nella scheda.

<!-- When you add smart crop to an existing image profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Puoi applicare i profili immagine a cartelle specifiche o globalmente a tutte le risorse.

È possibile rielaborare le risorse in una cartella che dispone già di un profilo immagine esistente modificato in seguito. Vedi [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](processing-profiles.md#reprocessing-assets).

### Applicare profili immagine Dynamic Media a cartelle specifiche {#applying-image-profiles-to-specific-folders}

Puoi applicare un profilo immagine a una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come applicare i profili immagine alle cartelle con entrambe le soluzioni.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo video esistente che hai successivamente modificato. Vedi [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](processing-profiles.md#reprocessing-assets).

#### Applicare profili immagine Dynamic Media alle cartelle dall’interfaccia utente Profili {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Seleziona il logo dell’Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Seleziona il profilo immagine da applicare a una o più cartelle.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Seleziona **[!UICONTROL Applica profilo di elaborazione alle cartelle]** e seleziona la cartella o più cartelle da utilizzare per ricevere le risorse appena caricate, quindi seleziona **[!UICONTROL Applica]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

#### Applicare profili immagine Dynamic Media alle cartelle da Proprietà {#applying-image-profiles-to-folders-from-properties}

1. Seleziona il logo dell’Experience League e passa a **[!UICONTROL Risorse]**. Quindi passa alla cartella principale della cartella a cui desideri applicare un profilo immagine.
1. Nella cartella, selezionare il segno di spunta per selezionarlo, quindi selezionare **[!UICONTROL Proprietà]**.
1. Seleziona la **[!UICONTROL Profili immagine]** scheda . Da **[!UICONTROL Nome profilo]** elenco a discesa, seleziona il profilo, quindi seleziona **[!UICONTROL Salva e chiudi]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Applicare un profilo immagine Dynamic Media a livello globale {#applying-an-image-profile-globally}

Oltre ad applicare un profilo a una cartella, puoi anche applicarne uno a livello globale in modo che a qualsiasi contenuto caricato in risorse di Experience Manager in una cartella sia applicato il profilo selezionato.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo video esistente che hai successivamente modificato. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](processing-profiles.md#reprocessing-assets).

**Per applicare globalmente un profilo immagine Dynamic Media:**

1. Effettua una delle operazioni seguenti:

   * Passa a `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e applicare il profilo appropriato e selezionare **[!UICONTROL Salva]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Passa a CRXDE Lite al seguente nodo: `/content/dam/jcr:content`.

      Aggiungi la proprietà `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` e seleziona **[!UICONTROL Salva tutto]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## Modificare il ritaglio avanzato o il campione avanzato di una singola immagine {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!NOTE]
>
>Smart Crop è disponibile solo in modalità Dynamic Media - Scene7.

È possibile riallineare o ridimensionare manualmente la finestra di ritaglio avanzato di un’immagine per perfezionarne ulteriormente il punto focale.

Dopo aver modificato e salvato un ritaglio avanzato, la modifica viene propagata ovunque si utilizzi il ritaglio per le immagini specifiche.

Se necessario, potete eseguire di nuovo il ritaglio avanzato per generare di nuovo il raccolto aggiuntivo.

Vedi anche [Modificare il ritaglio avanzato o il campione avanzato di più immagini](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Per modificare il ritaglio avanzato o il campione avanzato di una singola immagine:**

1. Seleziona il logo dell’Experience Manager e passa a **[!UICONTROL Risorse]**, quindi alla cartella a cui è applicato un profilo immagine di ritaglio avanzato o campione avanzato.

1. Seleziona la cartella per aprirne il contenuto.
1. Selezionate l’immagine di cui desiderate regolare il ritaglio avanzato o il campione avanzato.
1. Nella barra degli strumenti, seleziona **[!UICONTROL Ritaglio avanzato]**.

1. Effettua una delle operazioni seguenti:

   * Nell’angolo in alto a destra della pagina, trascinate la barra di scorrimento verso sinistra o verso destra per aumentare o diminuire rispettivamente la visualizzazione dell’immagine.
   * Sull&#39;immagine, trascinate una maniglia d&#39;angolo per regolare le dimensioni dell&#39;area visibile del ritaglio o del campione.
   * Sull’immagine, trascinate la casella o il campione in una nuova posizione. È possibile modificare solo i campioni immagine; i campioni colore sono statici.
   * Sopra l&#39;immagine, seleziona  **[!UICONTROL Ripristina]** per annullare tutte le modifiche e ripristinare il ritaglio o il campione originale.

1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL Chiudi]** per tornare alla cartella delle risorse.

## Modificare il ritaglio avanzato o il campione avanzato di più immagini {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

Dopo aver applicato un profilo immagine contenente Smart Crop a una cartella, a tutte le immagini in tale cartella viene applicato un ritaglio. Se lo desideri, puoi *manuale* riallineare o ridimensionare la finestra di ritaglio avanzato in più immagini per perfezionare ulteriormente il punto focale.

Dopo aver modificato e salvato un ritaglio avanzato, la modifica viene propagata ovunque si utilizzi il ritaglio per le immagini specifiche.

Se necessario, potete eseguire di nuovo il ritaglio avanzato per generare di nuovo il raccolto aggiuntivo.

**Per modificare il ritaglio avanzato o il campione avanzato di più immagini:**

1. Seleziona il logo dell’Experience Manager e passa a **[!UICONTROL Risorse]**, quindi a una cartella a cui è applicato un profilo immagine di ritaglio avanzato o campione avanzato.
1. Nella cartella, seleziona la **[!UICONTROL Altre azioni]** Icona (..), quindi seleziona **[!UICONTROL Ritaglio avanzato]**.

1. Sulla **[!UICONTROL Modifica ritaglio avanzato]** eseguire una delle operazioni seguenti:

   * Regola le dimensioni di visualizzazione delle immagini sulla pagina.

      A destra dell’elenco a discesa Nome punto di interruzione , trascina la barra di scorrimento a sinistra o a destra per modificare le dimensioni della visualizzazione dell’immagine visualizzabile.

      ![edit_smart_crop-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtra l’elenco delle immagini visualizzabili in base ai nomi dei punti di interruzione. Nell’esempio seguente, le immagini vengono filtrate sul nome del punto di interruzione &quot;Medium&quot;.

      Seleziona un nome di punto di interruzione dall’elenco a discesa nell’angolo in alto a destra della pagina per filtrare le immagini visualizzate. (Vedi l&#39;immagine qui sopra).

      ![edit_smart_crop-elenco a discesa](assets/edit_smart_crops-dropdownlist.png)

   * Ridimensiona la casella di ritaglio avanzato. Effettua una delle seguenti operazioni:

      * Se l’immagine presenta solo un ritaglio avanzato o un campione avanzato, trascinate sull’immagine la maniglia d’angolo della casella di ritaglio per regolare le dimensioni dell’area visibile del ritaglio.
      * Se l’immagine presenta sia un ritaglio avanzato che un campione avanzato, trascinate sull’immagine la maniglia d’angolo della casella di ritaglio per regolare le dimensioni dell’area visibile del ritaglio. Oppure, selezionate il campione intelligente sotto l&#39;immagine (i campioni colore sono statici), quindi trascinate la maniglia d&#39;angolo della casella di ritaglio per regolare le dimensioni dell&#39;area visibile del campione.

      ![Ridimensionare il ritaglio avanzato di un’immagine](assets/edit_smart_crops-resize.png)

   * Spostate la casella di ritaglio avanzato. Effettua una delle seguenti operazioni:

      * Se l’immagine dispone solo di un ritaglio avanzato o di un campione avanzato, trascinate la casella di ritaglio in una nuova posizione.
      * Se l’immagine presenta sia un ritaglio avanzato che un campione avanzato, trascinate la casella di ritaglio avanzato in una nuova posizione. In alternativa, selezionate il campione avanzato sotto l’immagine (i campioni colore sono statici), quindi trascinate la casella di ritaglio campione avanzato in una nuova posizione.

      ![edit_smart_crop-move](assets/edit_smart_crops-move.png)

   * Annulla tutte le modifiche e ripristina il ritaglio avanzato o il campione avanzato originale (applicabile solo alla sessione di modifica corrente).

      Seleziona **[!UICONTROL Ripristina]** sopra l&#39;immagine.

      ![edit_smart_crop-revert](assets/edit_smart_crops-revert.png)



1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL Chiudi]** per tornare alla cartella delle risorse.

## Rimuovere un profilo immagine Dynamic Media dalle cartelle {#removing-an-image-profile-from-folders}

Quando rimuovi un profilo immagine da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla relativa cartella principale. Tuttavia, l’elaborazione dei file che si è verificata all’interno delle cartelle rimane intatta.

Puoi rimuovere un profilo immagine da una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come rimuovere i profili immagine dalle cartelle con entrambe le soluzioni.

### Rimuovere i profili immagine Dynamic Media dalle cartelle tramite l’interfaccia utente Profili {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Seleziona il logo dell’Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Seleziona il profilo immagine da rimuovere da una o più cartelle.
1. Seleziona **[!UICONTROL Rimuovi profilo elaborazione da cartelle]** e seleziona la cartella o le cartelle multiple da cui vuoi rimuovere il profilo e seleziona **[!UICONTROL Rimuovi]**.

   Puoi confermare che il profilo immagine non viene più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimuovere i profili immagine Dynamic Media dalle cartelle tramite Proprietà {#removing-image-profiles-from-folders-via-properties}

1. Seleziona il logo dell’Experience Manager e naviga **[!UICONTROL Risorse]** e quindi alla cartella da cui si desidera rimuovere un profilo immagine.
1. Nella cartella, selezionare il segno di spunta per selezionarlo, quindi selezionare **[!UICONTROL Proprietà]**.
1. Seleziona la **[!UICONTROL Profili immagine]** scheda .
1. Da **[!UICONTROL Nome profilo]** elenco a discesa, seleziona **[!UICONTROL Nessuno]**, quindi seleziona **[!UICONTROL Salva e chiudi]**.

   Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.
