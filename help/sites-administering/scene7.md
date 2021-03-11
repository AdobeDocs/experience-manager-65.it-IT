---
title: Integrazione con Dynamic Media Classic
description: Scopri come integrare Adobe Experience Manager con Dynamic Media Classic.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
workflow-type: tm+mt
source-wordcount: '5452'
ht-degree: 2%

---


# Integrazione con Dynamic Media Classic {#integrating-with-dynamic-media-classic-scene}

Adobe Dynamic Media Classic è una soluzione in hosting per la gestione, l’ottimizzazione, la pubblicazione e la distribuzione di risorse multimediali sul Web, su dispositivi mobili, su e-mail e su schermi e stampe collegati a Internet.

Per utilizzare Dynamic Media Classic, è necessario configurare la configurazione cloud in modo che Dynamic Media Classic e AEM Assets possano interagire tra loro. Questo documento descrive come configurare AEM e Dynamic Media Classic.

Per informazioni sull&#39;utilizzo di tutti i componenti di Dynamic Media Classic su una pagina e sull&#39;utilizzo dei video, consulta [Utilizzo di Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* La piattaforma di visualizzatori DHTML di Dynamic Media Classic ha ufficialmente raggiunto la fine del ciclo di vita il 31 gennaio 2014. Per ulteriori informazioni, consulta le [Domande frequenti sulla fine del ciclo di vita del visualizzatore DHTML](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* Prima di configurare Dynamic Media Classic per l&#39;utilizzo con AEM, consulta [Best practice](#best-practices-for-integrating-scene-with-aem) per l&#39;integrazione di Dynamic Media Classic con AEM.
>* Se utilizzi Dynamic Media Classic con una configurazione proxy personalizzata, devi configurare entrambe le configurazioni proxy del client HTTP, in quanto alcune funzionalità di AEM utilizzano le API 3.x e altre le API 4.x. 3.x è configurato con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) e 4.x è configurato con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).

>



## Integrazione AEM/Dynamic Media Classic rispetto a Dynamic Media {#aem-scene-integration-versus-dynamic-media}

AEM gli utenti possono scegliere tra due soluzioni da utilizzare con Dynamic Media: Integrando la propria istanza di AEM con Dynamic Media Classic o utilizzando la soluzione Dynamic Media integrata in AEM.

Utilizza i seguenti criteri per determinare quale soluzione scegliere:

* Se sei un cliente **esistente** Dynamic Media Classic le cui risorse multimediali risiedono in Dynamic Media Classic per la pubblicazione e la distribuzione, ma desideri integrare tali risorse con l’authoring di Sites (WCM) e/o AEM Assets per la gestione, utilizza l’ [integrazione punto-punto AEM/Dynamic Media Classic](#aem-scene-point-to-point-integration) descritta in questo documento.

* Se sei un cliente **nuovo** AEM che ha esigenze di consegna di contenuti multimediali avanzati, seleziona l&#39;opzione [Dynamic Media](#aem-dynamic-media). Questa opzione ha senso se non disponi di un account S7 esistente e molte risorse memorizzate in tale sistema.

* In alcuni casi, è possibile utilizzare entrambe le soluzioni. Lo scenario [a doppio uso](/help/sites-administering/scene7.md#dual-use-scenario) descrive tale scenario.

### Integrazione punto-punto AEM/Dynamic Media Classic {#aem-scene-point-to-point-integration}

Quando lavori con le risorse in questa soluzione, effettua una delle seguenti operazioni:

* Carica le risorse direttamente in Dynamic Media Classic e accedi quindi tramite il browser dei contenuti **Dynamic Media Classic** per la creazione delle pagine o
* Carica in AEM Assets e quindi abilita la pubblicazione automatica in Dynamic Media Classic; accedi tramite il browser dei contenuti **Risorse** per la creazione delle pagine

I componenti utilizzati per questa integrazione si trovano nell&#39;area del componente **Dynamic Media Classic** in modalità [Progettazione.](/help/sites-authoring/author-environment-tools.md#page-modes)

### AEM Dynamic Media {#aem-dynamic-media}

AEM Dynamic Media è l’unificazione delle funzionalità di Dynamic Media Classic direttamente all’interno della piattaforma AEM.

Quando lavori con le risorse in questa soluzione, segui questo flusso di lavoro:

1. Consente di caricare risorse singole di immagini e video direttamente in AEM.
1. Codifica i video direttamente in AEM.
1. Crea set basati su immagini direttamente in AEM.
1. Se applicabile, aggiungi l’interattività alle immagini o ai video.

I componenti utilizzati per Dynamic Media si trovano nell&#39;area dei componenti **[!UICONTROL Dynamic Media]** in [Modalità Progettazione](/help/sites-authoring/author-environment-tools.md#page-modes). Includono quanto segue:

* **[!UICONTROL Dynamic Media]**  - Il componente  **[!UICONTROL Dynamic]** Mediacomponent è intelligente - a seconda che si aggiunga un’immagine o un video, sono disponibili varie opzioni. Il componente supporta i predefiniti per immagini e i visualizzatori basati su immagini, come set di immagini, set di rotazione, set di file multimediali diversi e video. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni reali dello stesso. Tutti i visualizzatori sono visualizzatori HTML5.

* **[!UICONTROL File multimediali interattivi]**  - Il componente  **** Mediacomponente interattivo è destinato a tali risorse, come banner a carosello, immagini interattive e video interattivi, che dispongono di interattività come punti attivi o mappe immagine. Questo componente è intelligente: a seconda che si aggiunga un’immagine o un video, sono disponibili varie opzioni. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni reali dello stesso. Tutti i visualizzatori sono visualizzatori HTML5.

### Scenario a doppio uso {#dual-use-scenario}

È possibile utilizzare contemporaneamente le funzioni di integrazione di Dynamic Media e Dynamic Media Classic di AEM. Nella tabella dei casi d’uso riportata di seguito viene descritto quando si attivano e disattivano determinate aree.

Per utilizzare contemporaneamente Dynamic Media e Dynamic Media Classic:

1. Configura [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) nei servizi cloud.
1. Segui le istruzioni specifiche relative al tuo caso d’uso:

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Integrazione Dynamic Media Classic</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>Se ...</strong></td>
    <td><strong>Flusso di lavoro del caso d’uso</strong></td>
    <td><strong>Imaging/Video</strong></td>
    <td><strong>Componente elementi multimediali dinamici</strong></td>
    <td><strong>Browser e componenti dei contenuti S7</strong></td>
    <td><strong>Caricamento automatico da Assets a S7</strong></td>
    </tr>
    <tr>
    <td>Novità di Sites e Dynamic Media</td>
    <td>Caricare le risorse AEM e utilizzare AEM componente Dynamic Media per creare le risorse sulle pagine Sites</td>
    <td><p>Attivato</p> <p>(Vedere il passaggio 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Attivato</a></td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    </tr>
    <tr>
    <td>Nel settore retail e sono nuovi su Sites e Dynamic Media</td>
    <td>Caricare risorse NON di prodotto in AEM per la gestione e la distribuzione. Carica le risorse PRODUCT in Dynamic Media Classic e utilizza il browser dei contenuti Dynamic Media Classic in AEM e componente per creare pagine di dettagli prodotto su Sites.</td>
    <td><p>Attivato</p> <p>(Vedere il passaggio 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Attivato</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Attivato</a></td>
    <td>Disattivato</td>
    </tr>
    <tr>
    <td>Novità di Assets e Dynamic Media</td>
    <td>Carica le risorse in AEM Assets e utilizza l’URL/codice di incorporamento pubblicato da Dynamic Media</td>
    <td><p>Attivato</p> <p>(Vedere il passaggio 3)</p> </td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    </tr>
    <tr>
    <td>Novità di Dynamic Media e modelli</td>
    <td>Utilizza Dynamic Media per immagini e video. Creare modelli di immagine in Dynamic Media Classic e utilizzare Content Finder di Dynamic Media Classic per includere modelli nelle pagine Sites.</td>
    <td><p>Attivato</p> <p>(Vedere il passaggio 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Attivato</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Attivato</a></td>
    <td>Disattivato</td>
    </tr>
    <tr>
    <td>Un cliente Dynamic Media Classic esistente e sono nuovi di Sites</td>
    <td>Carica le risorse in Dynamic Media Classic e utilizza AEM browser dei contenuti di Dynamic Media Classic per cercare e creare le risorse nelle pagine Sites</td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Attivato</a></td>
    <td>Disattivato</td>
    </tr>
    <tr>
    <td>Un cliente Dynamic Media Classic esistente e sono nuovi di Sites e Assets</td>
    <td>Carica le risorse in DAM e pubblica automaticamente in Dynamic Media Classic per la distribuzione. Utilizza AEM browser dei contenuti di Dynamic Media Classic per cercare e creare risorse nelle pagine Sites.</td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Attivato</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">Attivato</a></p> <p>(Vedere il passaggio 4)</p> </td>
    </tr>
    <tr>
    <td>Cliente Dynamic Media Classic esistente e nuovo di Assets</td>
    <td><p>Carica le risorse in AEM e utilizza Dynamic Media per generare rappresentazioni da scaricare/condividere. Pubblicare automaticamente AEM risorse in Dynamic Media Classic per la distribuzione.</p> <p><strong>Importante:</strong> assicura che l'elaborazione e le rappresentazioni duplicate generate in AEM non vengano sincronizzate con Dynamic Media Classic</p> </td>
    <td><p>Attivato</p> <p>(Vedere il passaggio 3)</p> </td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    <td><p><a href="#configuringautouploadingfromaemassets">Attivato</a></p> <p>(Vedere il passaggio 4)</p> </td>
    </tr>
    </tbody>
    </table>

1. (Facoltativo; vedi tabella dei casi d&#39;uso) - Imposta la [configurazione cloud Dynamic Media](/help/assets/config-dynamic.md) e [abilita il server Dynamic Media](/help/assets/config-dynamic.md).
1. (Facoltativo; consulta la tabella dei casi d’uso): se scegli di abilitare il caricamento automatico da Assets a Dynamic Media Classic, devi aggiungere quanto segue:

   1. Imposta il caricamento automatico su Dynamic Media Classic.
   1. Aggiungi il passaggio **Caricamento Dynamic Media Classic** dopo tutti i passaggi del flusso di lavoro Dynamic Media *alla fine di* **Aggiorna risorsa Dam** del flusso di lavoro ( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. (Facoltativo) Limita il caricamento delle risorse Dynamic Media Classic per tipo MIME in [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). I tipi MIME delle risorse non inclusi in questo elenco non verranno caricati nel server Dynamic Media Classic.
   1. (Facoltativo) Configura il video nella configurazione di Dynamic Media Classic. È possibile abilitare la codifica video sia per Dynamic Media che per Dynamic Media Classic simultaneamente. Le rappresentazioni dinamiche vengono utilizzate per l’anteprima e la riproduzione locale AEM’istanza, mentre le rappresentazioni video di Dynamic Media Classic vengono generate e memorizzate sui server Dynamic Media Classic. Quando configuri servizi di codifica video sia per Dynamic Media che per Dynamic Media Classic, applica un [profilo di elaborazione video](/help/assets/video-profiles.md) alla cartella delle risorse di Dynamic Media Classic.
   1. (Facoltativo) [Configura anteprima protetta in Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### Limitazioni  {#limitations}

Quando sono abilitati sia Dynamic Media Classic che Dynamic Media, sono presenti le seguenti limitazioni:

* Il caricamento manuale in Dynamic Media Classic selezionando una risorsa e trascinandola su un componente Dynamic Media Classic in una pagina di AEM non funziona.
* Anche se le risorse sincronizzate AEM-Dynamic Media Classic vengono aggiornate automaticamente in Dynamic Media Classic quando la risorsa viene modificata in Assets, un’azione di rollback non attiva un nuovo caricamento, pertanto Dynamic Media Classic non riceverà la versione più recente immediatamente dopo un rollback. La soluzione consiste nel modificare nuovamente una volta completato il rollback.
* Se devi utilizzare Dynamic Media per un caso d’uso e l’integrazione Dynamic Media Classic per un altro caso d’uso, in modo che le risorse Dynamic Media non interagiscano con il sistema Dynamic Media Classic, non applicare la configurazione Dynamic Media Classic alla cartella Dynamic Media o alla configurazione Dynamic Media (profilo di elaborazione) in una cartella Dynamic Media Classic.

## Best practice per l’integrazione di Dynamic Media Classic con AEM {#best-practices-for-integrating-scene-with-aem}

Quando si integra Dynamic Media Classic con AEM, sono necessarie alcune best practice importanti da osservare nelle seguenti aree:

* Testare l&#39;integrazione
* Caricamento delle risorse direttamente da Dynamic Media Classic consigliato per alcuni scenari

Vedere [limitazioni note](#known-limitations-and-design-implications).

### Testare l&#39;integrazione {#test-driving-your-integration}

Adobe consiglia di eseguire un test dell’integrazione facendo sì che la cartella principale punti a una sottocartella solo anziché a un’intera azienda.

>[!CAUTION]
>
>L’importazione di risorse da un account aziendale Dynamic Media Classic esistente potrebbe richiedere molto tempo per la visualizzazione in AEM. Assicurati di designare una cartella in Dynamic Media Classic priva di troppe risorse (ad esempio, la cartella principale avrà spesso troppe risorse e potrebbe causare l’arresto anomalo del sistema).

### Caricamento delle risorse da AEM Assets rispetto a Dynamic Media Classic {#uploading-assets-from-aem-assets-versus-from-scene}

Puoi caricare le risorse utilizzando la funzionalità Risorse (gestione delle risorse digitali) o accedendo direttamente a Dynamic Media Classic in AEM tramite il browser dei contenuti di Dynamic Media Classic. Quale scelta dipende dai seguenti fattori:

* I tipi di risorse Dynamic Media Classic non ancora supportati da AEM Assets devono essere aggiunti direttamente a un sito web AEM da Dynamic Media Classic, tramite il browser dei contenuti Dynamic Media Classic, ad esempio i modelli di immagine.
* Per i tipi di risorse supportati sia da AEM Assets che da Dynamic Media Classic, la decisione su come caricarli dipende dai seguenti elementi:

   * Dove sono presenti le attività E
   * Quanto è importante gestirli in un archivio comune

Se le risorse sono già in Dynamic Media Classic e la loro gestione in un archivio comune non è così importante, esportarle in AEM Assets solo per sincronizzarle di nuovo in Dynamic Media Classic per la distribuzione sarebbe un ciclo non necessario. In caso contrario, potrebbe essere preferibile mantenere le risorse in un unico archivio e sincronizzarle solo con Dynamic Media Classic per la distribuzione.

## Configurazione dell&#39;integrazione di Dynamic Media Classic {#configuring-scene-integration}

Puoi configurare AEM per caricare le risorse in Dynamic Media Classic. Le risorse da una cartella di destinazione CQ possono essere caricate (automaticamente o manualmente) da AEM a un account aziendale Dynamic Media Classic.

>[!NOTE]
>
>L’Adobe consiglia di utilizzare solo la cartella di destinazione designata per l’importazione delle risorse di Dynamic Media Classic. Le risorse digitali che risiedono al di fuori della cartella di destinazione possono essere utilizzate solo nei componenti di Dynamic Media Classic nelle pagine in cui è stata abilitata la configurazione di Dynamic Media Classic. Inoltre, vengono posizionate in una cartella ad hoc in Dynamic Media Classic. La cartella ad hoc non viene sincronizzata con AEM (ma le risorse sono individuabili nel browser dei contenuti di Dynamic Media Classic).

Per configurare Dynamic Media Classic per l&#39;integrazione con AEM, è necessario completare i seguenti passaggi:

1. [Definire una configurazione](#creating-a-cloud-configuration-for-scene)  cloud: definisce la mappatura tra una cartella Dynamic Media Classic e una cartella Assets. Devi completare questo passaggio anche se desideri la sincronizzazione unidirezionale (da AEM Assets a Dynamic Media Classic).
1. [Abilita  **Adobe CQ s7dam Dam Listener**](#enabling-the-adobe-cq-scene-dam-listener)  - Fatto in   OSGiconsole.
1. Se desideri caricare AEM risorse automaticamente in Dynamic Media Classic, devi attivare tale opzione e aggiungere Dynamic Media Classic al flusso di lavoro [!UICONTROL Aggiorna risorsa DAM]. Puoi anche caricare manualmente le risorse.
1. Aggiunta di componenti Dynamic Media Classic alla barra laterale. Questo consente agli utenti di utilizzare i componenti di Dynamic Media Classic nelle loro pagine AEM.
1. [Mappa la configurazione alla pagina in AEM](#enabling-scene-for-wcm) : questo passaggio è necessario per visualizzare eventuali predefiniti video creati in Dynamic Media Classic. È necessario anche se devi eseguire una pubblicazione di una risorsa dall’esterno della cartella di destinazione di CQ in Dynamic Media Classic.

Questa sezione descrive come eseguire tutti questi passaggi ed elenca limitazioni importanti.

### Funzionamento della sincronizzazione tra Dynamic Media Classic e AEM Assets {#how-synchronization-between-scene-and-aem-assets-works}

Quando si configura la sincronizzazione di AEM Assets e Dynamic Media Classic, è importante comprendere quanto segue:

#### Caricamento in Dynamic Media Classic da AEM Assets {#uploading-to-scene-from-aem-assets}

* È presente una cartella di sincronizzazione designata in AEM per i caricamenti di Dynamic Media Classic.
* I caricamenti in Dynamic Media Classic possono essere automatizzati se le risorse digitali vengono inserite nella cartella di sincronizzazione designata.
* La struttura di cartelle e sottocartelle in AEM viene replicata in Dynamic Media Classic.

>[!NOTE]
>
>AEM incorpora tutti i metadati come XMP prima di caricarli in Dynamic Media Classic, in modo che tutte le proprietà sul nodo di metadati siano disponibili in Dynamic Media Classic come XMP.

#### Limitazioni note e implicazioni di progettazione {#known-limitations-and-design-implications}

Con la sincronizzazione tra AEM Assets e Dynamic Media Classic, sono attualmente presenti le seguenti limitazioni/implicazioni di progettazione:

<table>
 <tbody>
  <tr>
   <td><strong>Limitazione/implicazione del progetto</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Una cartella di sincronizzazione designata (target)</td>
   <td>Per i caricamenti di Dynamic Media Classic puoi avere una sola cartella designata per azienda in AEM. Puoi creare più configurazioni se devi avere accesso a più account aziendali in Dynamic Media Classic.</td>
  </tr>
  <tr>
   <td>Struttura a cartelle</td>
   <td>Se elimini una cartella sincronizzata con le risorse, tutte le risorse remote di Dynamic Media Classic vengono eliminate ma la cartella rimane.</td>
  </tr>
  <tr>
   <td>Cartella ad hoc</td>
   <td>Le risorse che risiedono al di fuori della cartella di destinazione e caricate manualmente in Dynamic Media Classic in WCM vengono automaticamente posizionate in una cartella ad-hoc separata in Dynamic Media Classic. Puoi configurarlo nella configurazione cloud in AEM.</td>
  </tr>
  <tr>
   <td>Supporti misti</td>
   <td>I set di file multimediali diversi vengono visualizzati in AEM anche se non sono supportati in AEM.</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>I PDF generati dagli eCatalog in Dynamic Media Classic vengono importati nella cartella di destinazione di CQ.</td>
  </tr>
  <tr>
   <td>Aggiornamento dell’interfaccia utente</td>
   <td>Durante la sincronizzazione tra AEM e Dynamic Media Classic, assicurati di aggiornare l’interfaccia utente per visualizzare le modifiche. </td>
  </tr>
  <tr>
   <td>Miniature video</td>
   <td>Se carichi un video in AEM Assets per la codifica tramite Dynamic Media Classic, le miniature video e i video codificati potrebbero richiedere un po’ di tempo per essere disponibili in AEM Assets, a seconda del tempo di elaborazione del video.</td>
  </tr>
  <tr>
   <td>Sottocartelle di Target</td>
   <td><p>Se utilizzi sottocartelle all’interno della cartella di destinazione, accertati di utilizzare nomi univoci per ciascuna risorsa (indipendentemente dalla posizione) o di configurare Dynamic Media Classic (nell’area Configurazione) per non sovrascrivere le risorse indipendentemente dalla posizione.</p> <p>In caso contrario, vengono caricate le risorse con lo stesso nome e caricate in una sottocartella di destinazione di Dynamic Media Classic, ma la risorsa con lo stesso nome nella cartella di destinazione viene eliminata. </p> </td>
  </tr>
 </tbody>
</table>

### Configurazione dei server Dynamic Media Classic {#configuring-scene-servers}

Se esegui AEM dietro un proxy o disponi di impostazioni firewall speciali, potrebbe essere necessario abilitare esplicitamente gli host delle diverse aree geografiche. I server sono gestiti in contenuti in `/etc/cloudservices/scene7/endpoints` e possono essere personalizzati in base alle esigenze. Tocca un URL e quindi modifica per modificare l’URL, se necessario. Nelle versioni precedenti di AEM, questi valori erano hardcoded.

Se passi a `/etc/cloudservices/scene7/endpoints.html`, vengono visualizzati i server elencati e puoi modificarli facendo clic sull’URL:

![chlimage_1-296](assets/chlimage_1-296.png)

### Creazione di una configurazione cloud per Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}

Una configurazione cloud definisce la mappatura tra una cartella Dynamic Media Classic e una cartella AEM Assets. Deve essere configurato per sincronizzare AEM Assets con Dynamic Media Classic. Per ulteriori informazioni, consulta Funzionamento della sincronizzazione .

>[!CAUTION]
>
>L’importazione di risorse da un account aziendale Dynamic Media Classic esistente potrebbe richiedere molto tempo per la visualizzazione in AEM. Assicurati di designare una cartella in Dynamic Media Classic che non abbia troppe risorse (ad esempio, la cartella principale spesso avrà troppe risorse).
>
>Se desideri testare l&#39;integrazione dell&#39;unità, è possibile che la cartella principale punti solo a una sottocartella, anziché all&#39;intera azienda.

>[!NOTE]
>
>Puoi avere più configurazioni: una configurazione cloud rappresenta un utente in una società Dynamic Media Classic. Se desideri accedere ad altre società o utenti di Dynamic Media Classic, devi creare più configurazioni.

Per configurare AEM per la pubblicazione delle risorse in Dynamic Media Classic:

1. Tocca l’icona AEM e passa a **[!UICONTROL Implementazione > Cloud Services]** per accedere ad Adobe Dynamic Media Classic.

1. Tocca **[!UICONTROL Configura ora.]**

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. Nel campo **[!UICONTROL Titolo]** e facoltativamente nel campo **[!UICONTROL Nome]**, immetti le informazioni appropriate. Tocca **[!UICONTROL Crea.]**

   >[!NOTE]
   >
   >Quando crei configurazioni aggiuntive, viene visualizzato il campo **[!UICONTROL configurazione padre]** .
   >
   >Eseguire **non** la modifica della configurazione padre. La modifica della configurazione padre può interrompere l&#39;integrazione.

1. Immetti l&#39;indirizzo e-mail, la password e la regione del tuo account Dynamic Media Classic e tocca **[!UICONTROL Connetti a Dynamic Media Classic.]** Sei connesso al server Dynamic Media Classic e la finestra di dialogo si espande con altre opzioni.

1. Immettere il nome **[!UICONTROL Società]** e il nome **[!UICONTROL Percorso radice]** (questo è il nome del server pubblicato insieme a qualsiasi percorso si desidera specificare; se non conosci il nome del server pubblicato, in Dynamic Media Classic vai a **[!UICONTROL Configurazione > Impostazione applicazione.]**)

   >[!NOTE]
   >
   >Il percorso principale di Dynamic Media Classic è la cartella Dynamic Media Classic a cui si AEM. Può essere ridotto a una cartella specifica.

   >[!CAUTION]
   >
   >A seconda delle dimensioni della cartella Dynamic Media Classic, l’importazione di una cartella principale può richiedere molto tempo. Inoltre, i dati di Dynamic Media Classic potrebbero superare lo spazio di archiviazione AEM. Assicurati di importare la cartella corretta. L&#39;importazione di troppi dati può arrestare il sistema.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. Fai clic su **[!UICONTROL OK.]** AEM salva la configurazione.

>[!NOTE]
>
>Se si sta riconnettendo:
>
>* Quando ci si riconnette a Dynamic Media Classic al momento della pubblicazione, potrebbe essere necessario reimpostare la password al momento della pubblicazione o la riconnessione non funzionerà. Questo non è un problema sull&#39;istanza dell&#39;autore.
>* Se modifichi valori come la tua area geografica, il nome della società, devi riconnetterti a Dynamic Media Classic. Se le opzioni di configurazione sono state modificate ma non salvate, AEM erroneamente indica ancora che la configurazione è valida. Assicurati di riconnettersi.

>



### Abilitazione del listener Adobe CQ Dynamic Media Classic Dam {#enabling-the-adobe-cq-scene-dam-listener}

Devi abilitare il listener Adobe CQ Dynamic Media Classic Dam, che è disabilitato per impostazione predefinita.

Per abilitarlo:

1. Toccare l’icona [!UICONTROL Strumenti], quindi passare a **[!UICONTROL Operazioni > Console web.]** Viene visualizzata la console Web.
1. Passa a **[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]** e seleziona la casella di controllo **[!UICONTROL Enabled]** .

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. Tocca **[!UICONTROL Salva.]**

### Aggiunta di un timeout configurabile al flusso di lavoro di caricamento Dynamic Media Classic {#adding-configurable-timeout-to-scene-upload-workflow}

Quando un’istanza di AEM è configurata per gestire la codifica video tramite Dynamic Media Classic, per impostazione predefinita, si verifica un timeout di 35 minuti su qualsiasi processo di caricamento. Per gestire lavori di codifica video potenzialmente più lunghi, puoi configurare questa impostazione:

1. Passa a **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. Modifica il numero desiderato nel campo **[!UICONTROL Timeout processo attivo]** . Qualsiasi numero non negativo è accettato con l&#39;unità di misura in secondi. Per impostazione predefinita, è impostato su 2100.

   >[!NOTE]
   >
   >Procedure consigliate: La maggior parte delle risorse vengono acquisite al massimo in pochi minuti (ad esempio, immagini). Ma in alcuni casi - video di dimensioni maggiori, ad esempio - il valore di timeout dovrebbe essere aumentato a 7200 secondi (2 ore) per adattarsi a tempi di elaborazione lunghi. In caso contrario, questo processo di caricamento di Dynamic Media Classic è contrassegnato come **[!UICONTROL UploadFailed]** nei metadati JCR.

1. Tocca **[!UICONTROL Salva.]**

### Caricamento automatico da AEM Assets {#autouploading-from-aem-assets}

A partire da AEM 6.3.2, AEM Assets è ora configurato per te in modo che tutte le risorse digitali caricate nel gestore risorse digitali vengano aggiornate automaticamente in Dynamic Media Classic se le risorse si trovano in una cartella di destinazione CQ.

Quando una risorsa viene aggiunta in AEM Assets, viene caricata e pubblicata automaticamente in Dynamic Media Classic.

>[!NOTE]
>
>La dimensione massima del file per il caricamento automatico da AEM Assets a Dynamic Media Classic è 500 MB.

Per configurare il caricamento automatico da AEM Assets:

1. Tocca l’icona AEM e passa a **[!UICONTROL Implementazione > Cloud Services]**, quindi, sotto l’intestazione Dynamic Media, in Configurazioni disponibili, tocca **[!UICONTROL dms7 (Dynamic Media]**)
1. Tocca la scheda **[!UICONTROL Avanzate]**, seleziona la casella di controllo **[!UICONTROL Abilita caricamento automatico]**, quindi tocca **[!UICONTROL OK.]** È ora necessario configurare il flusso di lavoro DAM Asset per includere il caricamento in Dynamic Media Classic.

   >[!NOTE]
   >
   >Consulta [Configurazione dello stato (pubblicato/non pubblicato) delle risorse inviate a Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) per informazioni sul push delle risorse a Dynamic Media Classic in uno stato non pubblicato.

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Torna alla pagina di benvenuto AEM e tocca **[!UICONTROL Flussi di lavoro.]** Fai doppio clic sul flusso di lavoro Aggiorna risorsa  **DAM per** aprirlo.
1. Nella barra laterale passate ai componenti **[!UICONTROL Flusso di lavoro]** e selezionate **[!UICONTROL Dynamic Media Classic.]** Trascina  **[!UICONTROL Dynamic Media]** Classic nel flusso di lavoro e tocca  **[!UICONTROL Salva.]** Le risorse aggiunte ad AEM Assets nella cartella di destinazione verranno caricate automaticamente in Dynamic Media Classic.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* Quando si aggiungono risorse dopo l’automazione, se non si trovano nella cartella di destinazione di CQ, non vengono caricate in Dynamic Media Classic.
   >* AEM incorpora tutti i metadati come XMP prima di caricarli in Dynamic Media Classic, in modo che tutte le proprietà sul nodo di metadati siano disponibili in Dynamic Media Classic come XMP.


### Configurazione dello stato (pubblicato/non pubblicato) delle risorse inviate a Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Se invii le risorse da AEM Assets a Dynamic Media Classic, puoi pubblicarle automaticamente (comportamento predefinito) o inviarle in Dynamic Media Classic in uno stato non pubblicato.

Potrebbe non essere utile pubblicare immediatamente le risorse in Dynamic Media Classic se desideri testarle in un ambiente di staging prima di diventare live. Puoi utilizzare AEM con l’ambiente di test sicuro di Dynamic Media Classic per inviare le risorse direttamente da Assets a Dynamic Media Classic in uno stato non pubblicato.

Le risorse di Dynamic Media Classic rimangono disponibili tramite anteprima protetta. Solo quando le risorse vengono pubblicate in AEM, anche le risorse Dynamic Media Classic diventano live in produzione.

Se desideri pubblicare immediatamente le risorse quando le invii a Dynamic Media Classic, non è necessario configurare alcuna opzione. Questo è il comportamento predefinito.

Tuttavia, se non desideri che le risorse inviate a Dynamic Media Classic vengano pubblicate automaticamente, questa sezione descrive come configurare AEM e Dynamic Media Classic per eseguire questa operazione.

#### Prerequisiti per inviare risorse in Dynamic Media Classic senza pubblicazione {#prerequisites-to-push-assets-to-scene-unpublished}

Prima di poter inviare le risorse a Dynamic Media Classic senza pubblicarle, è necessario impostare quanto segue:

1. [Utilizza l’Admin Console per creare un caso di supporto.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) Nel tuo caso di assistenza, richiedi che l’anteprima protetta sia abilitata per il tuo account Dynamic Media Classic.
1. Segui le indicazioni per [configurare l&#39;anteprima protetta per il tuo account Dynamic Media Classic.](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

Questi sono gli stessi passaggi da seguire per creare qualsiasi configurazione di test sicuro in Dynamic Media Classic.

>[!NOTE]
>
>Se l&#39;ambiente di installazione è un sistema operativo Unix a 64 bit, consulta [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) per informazioni sulle opzioni di configurazione aggiuntive da impostare.

#### Limitazioni note per il push delle risorse in stato non pubblicato {#known-limitations-for-pushing-assets-in-unpublished-state}

Se utilizzi questa funzione, tieni presente le seguenti limitazioni:

* Nessun supporto per il controllo delle versioni.
* Se una risorsa è già pubblicata in AEM e viene creata una versione successiva, la nuova versione verrà pubblicata immediatamente dal vivo in produzione. La pubblicazione all’attivazione funziona solo con la pubblicazione iniziale di una risorsa.

>[!NOTE]
>
>Se desideri pubblicare le risorse all’istante, la best practice consiste nel mantenere **[!UICONTROL Abilita anteprima protetta]** impostato su **[!UICONTROL Immediatamente]** e utilizzare la funzione **[!UICONTROL Abilita caricamento automatico]**.

### Impostazione dello stato delle risorse inviate a Dynamic Media Classic come non pubblicate {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>Se un utente pubblica la risorsa in AEM, attiva automaticamente la risorsa S7 alla risorsa produzione/live (la risorsa non sarà più in anteprima protetta/non verrà più pubblicata).

Per impostare lo stato delle risorse inviate a Dynamic Media Classic come non pubblicate:

1. Tocca l’icona AEM e passa a **[!UICONTROL Implementazione > Cloud Services]**, tocca **[!UICONTROL Dynamic Media Classic]** e seleziona la configurazione in Dynamic Media Classic.
1. Tocca la scheda **[!UICONTROL Avanzate]** . Nel menu a discesa **[!UICONTROL Abilita visualizzazione protetta]** , seleziona **[!UICONTROL All’attivazione della pubblicazione AEM]** per inviare le risorse a Dynamic Media Classic senza la pubblicazione. (Per impostazione predefinita, questo valore è impostato su **[!UICONTROL Immediatamente]**, dove le risorse Dynamic Media Classic vengono pubblicate immediatamente.)

   Per ulteriori informazioni sui test delle risorse prima di renderle pubbliche, consulta [Documentazione di Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html) .

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. Tocca **[!UICONTROL OK.]**

Se abiliti la visualizzazione protetta, le risorse vengono inviate al server di anteprima protetto e la pubblicazione viene annullata.

Per controllare questo passaggio, passa a un componente Dynamic Media Classic su una pagina in AEM e tocca **[!UICONTROL Modifica.]** La risorsa avrà il server di anteprima protetto elencato nell’URL. Dopo la pubblicazione in AEM, il dominio del server nel riferimento al file viene aggiornato dall&#39;URL di anteprima all&#39;URL di produzione.

### Abilitazione di Dynamic Media Classic per WCM {#enabling-scene-for-wcm}

L’abilitazione di Dynamic Media Classic per WCM è necessaria per due motivi:

* Per abilitare l’elenco a discesa dei profili video universali per la creazione delle pagine. In caso contrario, il menu a discesa **[!UICONTROL Predefinito video universale]** è vuoto e non può essere impostato.
* Se una risorsa digitale non si trova nella cartella di destinazione, puoi caricarla in Dynamic Media Classic se abiliti Dynamic Media Classic per tale pagina nelle proprietà della pagina e trascinare e rilasciare la risorsa su un componente Dynamic Media Classic. Si applicano le normali regole di ereditarietà (ovvero le pagine figlie erediteranno la configurazione dalla pagina padre).

Quando si abilita Dynamic Media Classic per WCM, si applicano le regole di ereditarietà, come per altre configurazioni. È possibile abilitare Dynamic Media Classic per WCM nell’interfaccia utente touch o classica.

#### Abilitazione di Dynamic Media Classic per WCM nell&#39;interfaccia utente ottimizzata per il tocco {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

Per abilitare Dynamic Media Classic per WCM nell’interfaccia touch:

1. Tocca l’icona AEM e passa a **[!UICONTROL Sites]** e quindi alla pagina principale del sito web (non specifica la lingua).

1. Nella barra degli strumenti, seleziona l’icona [!UICONTROL Impostazioni] e tocca **[!UICONTROL Apri proprietà.]**

1. Tocca **[!UICONTROL Cloud Services]** e tocca **[!UICONTROL Aggiungi configurazione]** e seleziona **[!UICONTROL Dynamic Media Classic.]**
1. Nell&#39;elenco a discesa **[!UICONTROL Adobe Dynamic Media Classic]**, seleziona la configurazione desiderata e tocca **[!UICONTROL OK.]**

   ![chlimage_1-303](assets/chlimage_1-303.png)

   I predefiniti video di tale configurazione di Dynamic Media Classic sono disponibili per l’uso in AEM con il componente video Dynamic Media Classic in quella pagina e le pagine figlie.

#### Abilitazione di Dynamic Media Classic per WCM nell&#39;interfaccia utente classica {#enabling-scene-for-wcm-in-the-classic-user-interface}

Per abilitare Dynamic Media Classic per WCM nell’interfaccia classica:

1. In AEM, tocca **[!UICONTROL Siti web]** e passa alla pagina principale del sito web (non specifica per la lingua).

1. Nella barra laterale, tocca l’icona **[!UICONTROL Pagina]** e tocca **[!UICONTROL Proprietà pagina.]**

1. Tocca **[!UICONTROL Cloud Services > Aggiungi servizi > Dynamic Media Classic.]**
1. Nell&#39;elenco a discesa **[!UICONTROL Adobe Dynamic Media Classic]**, seleziona la configurazione desiderata e tocca **[!UICONTROL OK.]**

   I predefiniti video di tale configurazione di Dynamic Media Classic sono disponibili per l’uso in AEM con il componente video Dynamic Media Classic in quella pagina e le pagine figlie.

### Configurazione di una configurazione predefinita {#configuring-a-default-configuration}

Se disponi di più configurazioni di Dynamic Media Classic, puoi specificarne una come predefinita per il browser dei contenuti di Dynamic Media Classic.

È possibile contrassegnare come predefinita una sola configurazione di Dynamic Media Classic alla volta. La configurazione predefinita è quella delle risorse aziendali visualizzate per impostazione predefinita nel browser dei contenuti di Dynamic Media Classic.

Per configurare la configurazione predefinita:

1. Tocca l’icona AEM e passa a **[!UICONTROL Implementazione > Cloud Services]**, tocca **[!UICONTROL Dynamic Media Classic]** e seleziona la configurazione in Dynamic Media Classic.
1. Tocca **[!UICONTROL Modifica]** per aprire la configurazione.

1. Nella scheda **[!UICONTROL Generale]** , seleziona la casella di controllo **[!UICONTROL Configurazione predefinita]** per rendere questa azienda predefinita e il percorso principale visualizzato nel browser dei contenuti di Dynamic Media Classic.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >Se esiste una sola configurazione, la selezione della casella di controllo **[!UICONTROL Configurazione predefinita]** non ha alcun effetto.

### Configurazione della cartella ad-hoc {#configuring-the-ad-hoc-folder}

Puoi configurare la cartella in cui vengono caricate le risorse in Dynamic Media Classic quando la risorsa non si trova nella cartella di destinazione di CQ. Consulta Pubblicazione di risorse dall’esterno della cartella di destinazione CQ.

Per configurare la cartella adhoc:

1. Tocca l’icona AEM e passa a **[!UICONTROL Implementazione > Cloud Services]**, tocca **[!UICONTROL Dynamic Media Classic]** e seleziona la configurazione in Dynamic Media Classic.
1. Tocca **[!UICONTROL Modifica]** per aprire la configurazione.

1. Tocca la scheda **[!UICONTROL Avanzate]** . Nel campo **[!UICONTROL Cartella ad hoc]** puoi modificare la cartella **Ad-hoc** . Per impostazione predefinita, è il **nome_dell_azienda/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### Configurazione dei predefiniti universali {#configuring-universal-presets}

Per configurare i predefiniti universali per il componente video, consulta [Video](/help/assets/s7-video.md).

## Abilitazione del supporto per i parametri di processo di caricamento di Assets/Dynamic Media Classic basati su tipi MIME {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Puoi abilitare i parametri di processi di caricamento configurabili di Dynamic Media Classic attivati dalla sincronizzazione di risorse digitali Manager/Dynamic Media Classic.

Nello specifico, puoi configurare il formato di file accettato per tipo MIME nell’area OSGi (iniziativa Open Service Gateway) del pannello Configurazione della console Web AEM. Puoi quindi personalizzare i singoli parametri del lavoro di caricamento utilizzati per ogni tipo MIME nel JCR (Java Content Repository).

**Per abilitare le risorse basate su tipi MIME:**

1. Tocca l’icona AEM e passa a **[!UICONTROL Strumenti > Operazioni > Console web.]**
1. Nel pannello Configurazione console Web di Adobe Experience Manager, nel menu **[!UICONTROL OSGi]**, tocca **[!UICONTROL Configurazione.]**
1. Nella colonna Nome , tocca **[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME type Service]** per modificare la configurazione.
1. Nell’area Mime Type Mapping (Mime Type Mapping), tocca un segno più (+) per aggiungere un tipo MIME.

   Consulta [Tipi MIME supportati](/help/assets/assets-formats.md#supported-mime-types).

1. Nel campo di testo, digita il nuovo nome del tipo MIME.

   Ad esempio, digitare un `<file_extension>=<mime_type>` come in `EPS=application/postscript` O `PSD=image/vnd.adobe.photoshop`.

1. Nell&#39;angolo in basso a destra della finestra di configurazione, tocca **[!UICONTROL Salva.]**
1. Torna a AEM e, nella barra a sinistra, tocca CRXDE Lite.
1. Nella pagina CRXDE Lite, nella barra a sinistra, passa a `/etc/cloudservices/scene7/<environment>` (sostituisci `<environment>` con il nome effettivo).
1. Espandi `<environment>` (sostituisci `<environment>` per il nome effettivo) per visualizzare il nodo `mimeTypes`.
1. Tocca il mimeType appena aggiunto.

   Ad esempio, `mimeTypes > application_postscript` O `mimeTypes > image_vnd.adobe.photoshop`.

1. Sul lato destro della pagina CRXDE Lite, tocca la scheda **[!UICONTROL Proprietà]** .
1. Specifica un parametro di processo di caricamento di Dynamic Media Classic nel campo del valore **[!UICONTROL jobParam]** .

   Esempio, `psprocess="rasterize"&psresolution=120` .

   Per ulteriori parametri di processo di caricamento, consulta l’ [Adobe Dynamic Media Classic Image Production System API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html) .

   >[!NOTE]
   >
   >Se carichi file PSD e desideri elaborarli come modelli con estrazioni di livello, immetti quanto segue nel campo **[!UICONTROL jobParam]** value :
   >
   >`process=MaintainLayers&createTemplate=true`
   >
   >Assicurati che il tuo file PSD abbia &quot;livelli&quot;. Se è rigorosamente un&#39;immagine o un&#39;immagine con maschera, viene elaborata come immagine perché non ci sono livelli da elaborare.

1. Nell’angolo in alto a sinistra della pagina CRXDE Lite, tocca **[!UICONTROL Salva tutto.]**

## Risoluzione dei problemi relativi all&#39;integrazione di Dynamic Media Classic e AEM {#troubleshooting-scene-and-aem-integration}

Se riscontri problemi nell’integrazione di AEM con Dynamic Media Classic, consulta i seguenti scenari per le soluzioni .

**Se la pubblicazione delle risorse digitali in Dynamic Media Classic non riesce:**

* Verifica che la risorsa che stai tentando di caricare si trovi nella cartella **[!UICONTROL CQ target]** (specifica questa cartella nella configurazione cloud di Dynamic Media Classic).
* In caso contrario, devi configurare la configurazione cloud in **[!UICONTROL Proprietà pagina]** per quella pagina per consentire il caricamento nella cartella **[!UICONTROL CQ adhoc]** .

* Controlla i registri per eventuali informazioni.

**Se i predefiniti video non vengono visualizzati:**

* Assicurati di aver configurato la configurazione cloud di quella pagina tramite **[!UICONTROL Proprietà pagina.]** I predefiniti video sono disponibili nel componente video Dynamic Media Classic.

**Se le risorse video non vengono riprodotte in AEM:**

* Assicurati di aver utilizzato il componente video corretto. Il componente video Dynamic Media Classic è diverso dal componente video di base. Consulta [Componente video di base e componente video di Dynamic Media Classic](/help/assets/s7-video.md).

**Se le risorse nuove o modificate in AEM non vengono caricate automaticamente in Dynamic Media Classic:**

* Assicurati che le risorse siano nella cartella di destinazione di CQ. Solo le risorse che si trovano nella cartella di destinazione di CQ vengono aggiornate automaticamente (purché sia stato configurato AEM Assets per caricare automaticamente le risorse).
* Assicurati di aver configurato la configurazione dei Cloud Services su Abilita caricamento automatico e di aver aggiornato e salvato il flusso di lavoro DAM Asset per includere il caricamento di Dynamic Media Classic.
* Quando carichi un’immagine in una sottocartella della cartella di destinazione di Dynamic Media Classic, effettua una delle seguenti operazioni:

   * Assicurati che i nomi di tutte le risorse, indipendentemente dalla posizione, siano univoci. In caso contrario, la risorsa nella cartella di destinazione principale viene eliminata e la risorsa nella sottocartella rimane solo.
   * Modifica il modo in cui Dynamic Media Classic sovrascrive le risorse nell&#39;area Configurazione dell&#39;account Dynamic Media Classic. Non impostare Dynamic Media Classic per sovrascrivere le risorse indipendentemente dalla posizione, se utilizzate le risorse con lo stesso nome nelle sottocartelle.

**Se le risorse o le cartelle eliminate non sono sincronizzate tra Dynamic Media Classic e AEM:**

* Le risorse e le cartelle eliminate in AEM Assets vengono comunque visualizzate nella cartella sincronizzata in Dynamic Media Classic. È necessario eliminarli manualmente.

**Se il caricamento del video non riesce**

* Se il caricamento del video non riesce e stai utilizzando AEM per codificare i video tramite l&#39;integrazione Dynamic Media Classic, consulta [Aggiunta di un timeout configurabile al flusso di lavoro di caricamento di Dynamic Media Classic](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>L’importazione di risorse da un account aziendale Dynamic Media Classic esistente potrebbe richiedere molto tempo per la visualizzazione in AEM. Assicurati di designare una cartella in Dynamic Media Classic che non abbia troppe risorse (ad esempio, la cartella principale spesso avrà troppe risorse).
>
>Se desideri testare l&#39;integrazione dell&#39;unità, è possibile che la cartella principale punti solo a una sottocartella, anziché all&#39;intera azienda.

