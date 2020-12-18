---
title: Integrazione con Dynamic Media Classic (Scene7)
seo-title: Integrazione con Dynamic Media Classic (Scene7)
description: Scopri come integrare AEM con Dynamic Media Classic.
seo-description: Scopri come integrare AEM con Dynamic Media Classic.
uuid: b014d643-1cc1-47f3-a79c-7f6f9e45637a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: f55e68c3-3309-4400-bef9-fd3afa6e2b5f
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '5485'
ht-degree: 2%

---


# Integrazione con Dynamic Media Classic (Scene7){#integrating-with-dynamic-media-classic-scene}

[ Adobe Dynamic Media ](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) Classicis è una soluzione in hosting per la gestione, il miglioramento, la pubblicazione e la distribuzione di risorse multimediali su display e stampe Web, mobili, e-mail e connessi a Internet.

Per utilizzare Dynamic Media Classic, è necessario configurare la configurazione cloud in modo che Dynamic Media Classic e  AEM Assets possano interagire tra loro. Questo documento descrive come configurare AEM e Dynamic Media Classic.

Per informazioni sull&#39;utilizzo di tutti i componenti Dynamic Media Classic su una pagina e sull&#39;utilizzo dei video, vedere [Utilizzo di Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* La piattaforma di visualizzatori DHTML di Dynamic Media Classic ha ufficialmente raggiunto la fine del ciclo di vita il 31 gennaio 2014. Per ulteriori informazioni, consultate le [Domande frequenti sulla fine del ciclo di vita del visualizzatore DHTML](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* Prima di configurare Dynamic Media Classic per l&#39;utilizzo dei AEM, consultate [Best Practices](#best-practices-for-integrating-scene-with-aem) per l&#39;integrazione di Dynamic Media Classic con AEM.
>* Se utilizzate Dynamic Media Classic con una configurazione proxy personalizzata, è necessario configurare sia le configurazioni proxy HTTP Client in quanto alcune funzionalità di AEM utilizzano le API 3.x, sia quelle di 4.x. 3.x è configurato con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) e 4.x è configurato con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).

>



## Integrazione AEM/Dynamic Media Classic rispetto a Dynamic Media {#aem-scene-integration-versus-dynamic-media}

AEM utenti possono scegliere tra due soluzioni per lavorare con i supporti dinamici: Integrare la propria istanza di AEM con Dynamic Media Classic o utilizzare la soluzione Dynamic Media integrata in AEM.

Utilizzate i seguenti criteri per determinare quale soluzione scegliere:

* Se siete un cliente **esistente** Dynamic Media Classic le cui risorse multimediali risiedono in Dynamic Media Classic per la pubblicazione e la distribuzione, ma desiderate integrare tali risorse con l&#39;authoring di Siti (WCM) e/o  AEM Assets per la gestione, utilizzate l&#39;integrazione punto-punto [AEM/Dynamic Media Classic](#aem-scene-point-to-point-integration) descritta in questo documento.

* Se siete un cliente **nuovo** AEM con esigenze di distribuzione di contenuti multimediali avanzati, selezionate l&#39;opzione [Dynamic Media](#aem-dynamic-media). Questa opzione ha il massimo senso se non disponete di un account S7 esistente e di molte risorse memorizzate in tale sistema.

* In alcuni casi, è possibile utilizzare entrambe le soluzioni. Lo scenario [doppio utilizzo](/help/sites-administering/scene7.md#dual-use-scenario) descrive tale scenario.

### Integrazione punto-punto AEM/Dynamic Media Classic {#aem-scene-point-to-point-integration}

Quando lavorate con le risorse in questa soluzione, effettuate una delle seguenti operazioni:

* Caricate le risorse direttamente in Dynamic Media Classic e accedete tramite il browser del contenuto **Dynamic Media Classic** per l&#39;authoring delle pagine oppure
* Caricare  AEM Assets e quindi abilitare la pubblicazione automatica in Dynamic Media Classic; per l&#39;authoring delle pagine è possibile accedere tramite il browser del contenuto **Risorse**

I componenti utilizzati per questa integrazione si trovano nell&#39;area del componente **Dynamic Media Classic** in [modalità Progettazione.](/help/sites-authoring/author-environment-tools.md#page-modes)

### AEM Dynamic Media {#aem-dynamic-media}

AEM Dynamic Media è l&#39;unificazione delle funzionalità di Dynamic Media Classic direttamente all&#39;interno della piattaforma AEM.

Quando lavorate con le risorse in questa soluzione, seguite il seguente flusso di lavoro:

1. Caricate le singole risorse di immagini e video direttamente in AEM.
1. Codificate i video direttamente in AEM.
1. Creare set basati su immagini direttamente all’interno di AEM.
1. Se applicabile, aggiungete interattività alle immagini o ai video.

I componenti utilizzati per Dynamic Media si trovano nell&#39;area del componente **[!UICONTROL Dynamic Media]** in [modalità Progettazione](/help/sites-authoring/author-environment-tools.md#page-modes). Sono inclusi i seguenti elementi:

* **[!UICONTROL Dynamic Media]**  - Il componente  **[!UICONTROL Dynamic]** Mediacomponent è avanzato. A seconda se aggiungete un’immagine o un video, sono disponibili diverse opzioni. Il componente supporta i predefiniti per immagini e i visualizzatori basati su immagini, come set di immagini, set di rotazione, set di file multimediali diversi e video. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni reali dello stesso. Tutti i visualizzatori sono visualizzatori HTML5.

* **[!UICONTROL Contenuti multimediali]**  interattivi - Il componente  **[!UICONTROL Interattivo]** Mediacomponente è destinato a tali risorse, come banner carosello, immagini interattive e video interattivi, che dispongono di un’interattività come punti attivi o mappe immagine. Questo componente è avanzato: a seconda se aggiungete un’immagine o un video, sono disponibili diverse opzioni. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni reali dello stesso. Tutti i visualizzatori sono visualizzatori HTML5.

### Scenario a doppio uso {#dual-use-scenario}

Potete utilizzare simultaneamente le funzioni di integrazione di Dynamic Media e Dynamic Media Classic. Nella tabella dei casi d’uso riportata di seguito viene illustrato quando si attivano e disattivano determinate aree.

Per utilizzare contemporaneamente Dynamic Media e Dynamic Media Classic:

1. Configurare [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) nei servizi cloud.
1. Seguite le istruzioni specifiche relative al caso d’uso:

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
    <td><strong>Se siete...</strong></td>
    <td><strong>Flusso di lavoro casi d’uso</strong></td>
    <td><strong>Imaging/Video</strong></td>
    <td><strong>Componente elementi multimediali dinamici</strong></td>
    <td><strong>Browser e componenti di contenuto S7</strong></td>
    <td><strong>Caricamento automatico da risorse a S7</strong></td>
    </tr>
    <tr>
    <td>Nuovi siti e Dynamic Media</td>
    <td>Caricare le risorse per AEM e utilizzare AEM componente Dynamic Media per creare le risorse sulle pagine Siti</td>
    <td><p>Attivato</p> <p>(vedere il punto 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Attivato</a></td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    </tr>
    <tr>
    <td>Nella vendita al dettaglio e sono nuovi su Siti e Dynamic Media</td>
    <td>Caricate le risorse NON del prodotto in AEM per la gestione e la distribuzione. Caricate le risorse PRODOTTO in Dynamic Media Classic e utilizzate il browser dei contenuti Dynamic Media Classic in AEM e componente per creare pagine di dettagli prodotto sui siti.</td>
    <td><p>Attivato</p> <p>(vedere il punto 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Attivato</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Attivato</a></td>
    <td>Disattivato</td>
    </tr>
    <tr>
    <td>Nuove risorse e Dynamic Media</td>
    <td>Caricare le risorse su  AEM Assets e utilizzare l’URL pubblicato/il codice da Dynamic Media</td>
    <td><p>Attivato</p> <p>(vedere il punto 3)</p> </td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    </tr>
    <tr>
    <td>Nuovi prodotti Dynamic Media e modelli</td>
    <td>Utilizzate Dynamic Media per l'imaging e il video. Creare modelli di immagine in Dynamic Media Classic e utilizzare Dynamic Media Classic Content Finder per includere i modelli nelle pagine Siti.</td>
    <td><p>Attivato</p> <p>(vedere il punto 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Attivato</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Attivato</a></td>
    <td>Disattivato</td>
    </tr>
    <tr>
    <td>Un cliente Dynamic Media Classic esistente e nuovo a Sites</td>
    <td>Caricate le risorse in Dynamic Media Classic e utilizzate AEM browser dei contenuti Dynamic Media Classic per cercare e creare risorse nelle pagine Siti</td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Attivato</a></td>
    <td>Disattivato</td>
    </tr>
    <tr>
    <td>Un cliente Dynamic Media Classic esistente e nuovo a Siti e risorse</td>
    <td>Caricate le risorse in DAM e pubblicatele automaticamente in Dynamic Media Classic per la distribuzione. Utilizzate AEM browser del contenuto di Dynamic Media Classic per cercare e creare risorse nelle pagine Siti.</td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Attivato</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">Attivato</a></p> <p>(vedere il punto 4)</p> </td>
    </tr>
    <tr>
    <td>Cliente Dynamic Media Classic esistente e nuovo per le risorse</td>
    <td><p>Caricate le risorse in AEM e utilizzate Dynamic Media per generare rappresentazioni da scaricare/condividere. Pubblicare automaticamente AEM risorse in Dynamic Media Classic per la distribuzione.</p> <p><strong>Importante:</strong> Controlla l'elaborazione e le rappresentazioni duplicate generate in AEM non verranno sincronizzate in Dynamic Media Classic</p> </td>
    <td><p>Attivato</p> <p>(vedere il punto 3)</p> </td>
    <td>Disattivato</td>
    <td>Disattivato</td>
    <td><p><a href="#configuringautouploadingfromaemassets">Attivato</a></p> <p>(vedere il punto 4)</p> </td>
    </tr>
    </tbody>
    </table>

1. (Facoltativo; vedere la tabella dei casi d&#39;uso) - Impostare la [configurazione cloud Dynamic Media](/help/assets/config-dynamic.md) e [abilitare il server Dynamic Media](/help/assets/config-dynamic.md).
1. (Facoltativo; consultate la tabella dei casi d’uso) - Se scegliete di abilitare il caricamento automatico dalle risorse ad Dynamic Media Classic, dovete aggiungere quanto segue:

   1. Configurate il caricamento automatico in Dynamic Media Classic.
   1. Aggiungere il passaggio **Dynamic Media Classic upload** dopo tutti i passaggi del flusso di lavoro Dynamic Media *alla fine di* **Dam Update Asset** ( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. (Facoltativo) Limita il caricamento delle risorse Dynamic Media Classic per tipo MIME in [https://&lt;server>:&lt;porta>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). I tipi MIME della risorsa non inclusi in questo elenco non verranno caricati nel server Dynamic Media Classic.
   1. (Facoltativo) Impostare il video nella configurazione Dynamic Media Classic. Potete attivare la codifica video contemporaneamente per Dynamic Media e Dynamic Media Classic oppure per entrambi. Le rappresentazioni dinamiche vengono utilizzate per l&#39;anteprima e la riproduzione localmente nell&#39;istanza AEM, mentre le rappresentazioni video di Dynamic Media Classic vengono generate e memorizzate sui server Dynamic Media Classic. Quando configurate i servizi di codifica video per Dynamic Media e Dynamic Media Classic, applicate un [profilo di elaborazione video](/help/assets/video-profiles.md) alla cartella delle risorse di Dynamic Media Classic.
   1. (Facoltativo) [Configura anteprima protetta in Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### Limitazioni  {#limitations}

Se Dynamic Media Classic e Dynamic Media sono entrambi abilitati, sono presenti i seguenti limiti:

* Non è possibile caricare manualmente in Dynamic Media Classic selezionando una risorsa e trascinandola su un componente Dynamic Media Classic in una pagina AEM.
* Anche se le risorse sincronizzate AEM-Dynamic Media Classic vengono aggiornate automaticamente in Dynamic Media Classic quando la risorsa viene modificata in Risorse, un’azione di rollback non attiva un nuovo caricamento, quindi Dynamic Media Classic non ottiene la versione più recente subito dopo un ripristino. La soluzione alternativa consiste nel modificare nuovamente una volta completato il rollback.
* Se è necessario utilizzare Dynamic Media per un caso di utilizzo e l&#39;integrazione con Dynamic Media Classic per un altro caso di utilizzo, in modo che le risorse Dynamic Media non interagiscano con il sistema Dynamic Media Classic, non applicare la configurazione Dynamic Media Classic alla cartella Dynamic Media o alla configurazione Dynamic Media (profilo di elaborazione) a una cartella Dynamic Media Classic.

## Procedure ottimali per l&#39;integrazione di Dynamic Media Classic con AEM {#best-practices-for-integrating-scene-with-aem}

Durante l&#39;integrazione di Dynamic Media Classic con AEM, è necessario osservare alcune best practice importanti nelle seguenti aree:

* Test dell&#39;integrazione
* Caricamento delle risorse direttamente da Dynamic Media Classic consigliato per alcuni scenari

Vedere [limitazioni note](#known-limitations-and-design-implications).

### Test dell&#39;integrazione {#test-driving-your-integration}

 Adobe consiglia di testare l’integrazione facendo sì che la cartella principale indichi solo una sottocartella anziché un’intera società.

>[!CAUTION]
>
>L&#39;importazione di risorse da un account Dynamic Media Classic esistente potrebbe richiedere molto tempo per la visualizzazione in AEM. Accertatevi di specificare una cartella in Dynamic Media Classic che non contenga troppe risorse (ad esempio, la cartella principale avrà spesso troppe risorse e potrebbe arrestare in modo anomalo il sistema).

### Caricamento delle risorse da  AEM Assets e da Dynamic Media Classic {#uploading-assets-from-aem-assets-versus-from-scene}

Potete caricare le risorse sia mediante la funzionalità Risorse (gestione delle risorse digitali), sia accedendo ad Dynamic Media Classic direttamente in AEM tramite il browser dei contenuti di Dynamic Media Classic. La scelta dipende dai seguenti fattori:

* I tipi di risorse Dynamic Media Classic che  AEM Assets non supporta ancora devono essere aggiunti a un sito Web AEM da Dynamic Media Classic direttamente, tramite il browser dei contenuti Dynamic Media Classic, ad esempio i modelli di immagini.
* Per i tipi di risorse supportati da  AEM Assets e Dynamic Media Classic, la scelta di come caricarli dipende dalle seguenti opzioni:

   * Dove si trovano le attività correnti E
   * Quanto è importante gestirli in un archivio comune

Se le risorse sono già in Dynamic Media Classic e la loro gestione in un archivio comune non è così importante, esportarle in  AEM Assets solo per sincronizzarle nuovamente in Dynamic Media Classic per la distribuzione sarebbe un ciclo non necessario. In caso contrario, è preferibile conservare le risorse in un unico archivio e sincronizzarle solo per la distribuzione in Dynamic Media Classic.

## Configurazione dell&#39;integrazione Dynamic Media Classic {#configuring-scene-integration}

Potete configurare AEM per caricare le risorse in Dynamic Media Classic. Le risorse da una cartella di destinazione CQ possono essere caricate (automaticamente o manualmente) da AEM a un account società Dynamic Media Classic.

>[!NOTE]
>
> Adobe consiglia di usare solo la cartella di destinazione designata per importare le risorse di Dynamic Media Classic. Le risorse digitali che risiedono al di fuori della cartella di destinazione possono essere utilizzate solo nei componenti Dynamic Media Classic su pagine in cui è stata abilitata la configurazione di Dynamic Media Classic. Inoltre, vengono inseriti in una cartella ad hoc in Dynamic Media Classic. La cartella adhoc non è sincronizzata con AEM (ma le risorse sono reperibili nel browser dei contenuti di Dynamic Media Classic).

Per configurare Dynamic Media Classic per l&#39;integrazione con AEM, è necessario completare i seguenti passaggi:

1. [Definire una configurazione](#creating-a-cloud-configuration-for-scene)  cloud - Definisce la mappatura tra una cartella Dynamic Media Classic e una cartella Assets. È necessario completare questo passaggio anche se si desidera solo la sincronizzazione unidirezionale ( AEM Assets ad Dynamic Media Classic).
1. [Abilitare il  **Adobe CQ s7dam Dam Listener**](#enabling-the-adobe-cq-scene-dam-listener) - Fatto in   OSGiconsole.
1. Se desiderate che AEM risorse vengano caricate automaticamente in Dynamic Media Classic, dovete attivare tale opzione e aggiungere Dynamic Media Classic al flusso di lavoro [!UICONTROL Aggiorna risorsa DAM]. Potete anche caricare manualmente le risorse.
1. Aggiunta di componenti Dynamic Media Classic alla barra laterale. Questo consente agli utenti di utilizzare i componenti Dynamic Media Classic nelle loro pagine AEM.
1. [Mappa la configurazione sulla pagina in AEM](#enabling-scene-for-wcm) - Questo passaggio è necessario per visualizzare eventuali predefiniti video creati in Dynamic Media Classic. È inoltre richiesto se è necessario pubblicare una risorsa dall’esterno della cartella di destinazione di CQ in Dynamic Media Classic.

Questa sezione descrive come eseguire tutti questi passaggi ed elenca importanti limitazioni.

### Funzionamento della sincronizzazione tra Dynamic Media Classic e  AEM Assets {#how-synchronization-between-scene-and-aem-assets-works}

Quando configurate  sincronizzazione AEM Assets e Dynamic Media Classic, è importante comprendere quanto segue:

#### Caricamento in Dynamic Media Classic da  AEM Assets {#uploading-to-scene-from-aem-assets}

* Esiste una cartella di sincronizzazione specifica in AEM per i caricamenti di Dynamic Media Classic.
* I caricamenti in Dynamic Media Classic possono essere automatizzati se le risorse digitali sono inserite nella cartella di sincronizzazione designata.
* La struttura di cartelle e sottocartelle di AEM viene replicata in Dynamic Media Classic.

>[!NOTE]
>
>AEM tutti i metadati come XMP prima di caricarli in Dynamic Media Classic, pertanto tutte le proprietà sul nodo di metadati sono disponibili in Dynamic Media Classic come XMP.

#### Limitazioni note e implicazioni di progettazione {#known-limitations-and-design-implications}

Con la sincronizzazione tra  AEM Assets e Dynamic Media Classic, al momento esistono le seguenti limitazioni/implicazioni di progettazione:

<table>
 <tbody>
  <tr>
   <td><strong>Limitazione/implicazione di progettazione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Una cartella di sincronizzazione designata (destinazione)</td>
   <td>Per i caricamenti di Dynamic Media Classic potete avere una sola cartella designata per azienda in AEM. Potete creare più configurazioni se è necessario avere accesso a più account società in Dynamic Media Classic.</td>
  </tr>
  <tr>
   <td>Struttura delle cartelle</td>
   <td>Se eliminate una cartella sincronizzata con le risorse, tutte le risorse remote di Dynamic Media Classic vengono eliminate ma la cartella rimane.</td>
  </tr>
  <tr>
   <td>Cartella ad hoc</td>
   <td>Le risorse che risiedono al di fuori della cartella di destinazione e che vengono caricate manualmente in Dynamic Media Classic in WCM vengono automaticamente inserite in una cartella ad hoc separata in Dynamic Media Classic. Tale configurazione viene configurata nella configurazione cloud in AEM.</td>
  </tr>
  <tr>
   <td>Supporti misti</td>
   <td>I set di file multimediali diversi vengono visualizzati in AEM anche se non sono supportati in AEM.</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>I PDF generati dagli eCatalog in Dynamic Media Classic vengono importati nella cartella di destinazione CQ.</td>
  </tr>
  <tr>
   <td>Aggiornamento dell'interfaccia utente</td>
   <td>Durante la sincronizzazione tra AEM e Dynamic Media Classic, aggiornare l'interfaccia utente per visualizzare le modifiche. </td>
  </tr>
  <tr>
   <td>Miniature video</td>
   <td>Se caricate un video su  AEM Assets per la codifica tramite Dynamic Media Classic, le miniature video e i video codificati potrebbero richiedere del tempo per essere disponibili in  AEM Assets, a seconda del tempo di elaborazione del video.</td>
  </tr>
  <tr>
   <td>Sottocartelle di destinazione</td>
   <td><p>Se utilizzate sottocartelle all’interno della cartella di destinazione, accertatevi di usare nomi univoci per ciascuna risorsa (indipendentemente dalla posizione) oppure di configurare Dynamic Media Classic (nell’area Configurazione) per non sovrascrivere le risorse indipendentemente dalla posizione.</p> <p>In caso contrario, vengono caricate le risorse con lo stesso nome che vengono caricate in una sottocartella di destinazione Dynamic Media Classic, ma la risorsa con lo stesso nome viene eliminata nella cartella di destinazione. </p> </td>
  </tr>
 </tbody>
</table>

### Configurazione dei server Dynamic Media Classic {#configuring-scene-servers}

Se si esegue AEM dietro un proxy o si dispone di impostazioni firewall speciali, potrebbe essere necessario abilitare esplicitamente gli host delle diverse aree geografiche. I server vengono gestiti nel contenuto in `/etc/cloudservices/scene7/endpoints` e possono essere personalizzati come necessario. Toccate un URL e quindi modificate per modificare l’URL, se necessario. Nelle versioni precedenti di AEM, questi valori erano codificati.

Se andate a `/etc/cloudservices/scene7/endpoints.html`, potete vedere i server elencati (e modificarli facendo clic sull&#39;URL):

![chlimage_1-296](assets/chlimage_1-296.png)

### Creazione di una configurazione cloud per Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}

Una configurazione cloud definisce la mappatura tra una cartella Dynamic Media Classic e una cartella AEM Assets . Deve essere configurato per sincronizzare  AEM Assets con Dynamic Media Classic. Per ulteriori informazioni, consulta Come funziona la sincronizzazione.

>[!CAUTION]
>
>L&#39;importazione di risorse da un account Dynamic Media Classic esistente potrebbe richiedere molto tempo per la visualizzazione in AEM. Accertatevi di specificare una cartella in Dynamic Media Classic che non contenga troppe risorse (ad esempio, la cartella principale avrà spesso troppe risorse).
>
>Se desiderate testare l&#39;integrazione, potete fare in modo che la cartella principale punti solo a una sottocartella, invece che all&#39;intera società.

>[!NOTE]
>
>Potete avere più configurazioni: una configurazione cloud rappresenta un utente in una società Dynamic Media Classic. Se desiderate accedere ad altre società o utenti di Dynamic Media Classic, dovete creare più configurazioni.

Per configurare AEM per la pubblicazione delle risorse in Dynamic Media Classic:

1. Toccate l&#39;icona AEM e andate a **[!UICONTROL Distribuzione > Cloud Services]** per accedere  Adobe Dynamic Media Classic.

1. Toccate **[!UICONTROL Configura ora.]**

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. Nel campo **[!UICONTROL Titolo]** e, facoltativamente, nel campo **[!UICONTROL Nome]**, immettere le informazioni appropriate. Toccare **[!UICONTROL Crea.]**

   >[!NOTE]
   >
   >Quando si creano configurazioni aggiuntive, viene visualizzato il campo **[!UICONTROL configurazione padre]**.
   >
   >**not** modificare la configurazione padre. La modifica della configurazione padre può interrompere l&#39;integrazione.

1. Immettete l&#39;indirizzo e-mail, la password e l&#39;area geografica dell&#39;account Dynamic Media Classic e toccate **[!UICONTROL Connetti ad Dynamic Media Classic.]** Siete connessi al server Dynamic Media Classic e la finestra di dialogo si espande con altre opzioni.

1. Immettere il nome **[!UICONTROL Company]** e il nome **[!UICONTROL percorso principale]** (questo è il nome del server pubblicato insieme a qualsiasi percorso da specificare; se non si conosce il nome del server pubblicato, in Dynamic Media Classic passare a **[!UICONTROL Configurazione > Impostazione applicazione.]**)

   >[!NOTE]
   >
   >Il percorso principale di Dynamic Media Classic è la cartella Dynamic Media Classic a cui AEM. Può essere ridotto a una cartella specifica.

   >[!CAUTION]
   >
   >A seconda delle dimensioni della cartella Dynamic Media Classic, l’importazione di una cartella principale potrebbe richiedere molto tempo. Inoltre, i dati di Dynamic Media Classic potrebbero superare l&#39;archiviazione AEM. Assicuratevi di importare la cartella corretta. L&#39;importazione di troppi dati può arrestare il sistema.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. Fai clic su **[!UICONTROL OK.]** AEM salva la configurazione.

>[!NOTE]
>
>Se vi state riconnettendo:
>
>* Quando si riconnette ad Dynamic Media Classic al momento della pubblicazione, potrebbe essere necessario reimpostare la password al momento della pubblicazione, altrimenti la riconnessione non funzionerà. Non si tratta di un problema relativo all’istanza di creazione.
>* Se modificate valori come la vostra regione o il nome della società, dovete riconnettervi ad Dynamic Media Classic. Se le opzioni di configurazione sono state modificate ma non salvate, AEM erroneamente indica comunque che la configurazione è valida. Assicuratevi di ricollegarvi.

>



### Abilitazione del  Adobe CQ Dynamic Media Classic Dam Listener {#enabling-the-adobe-cq-scene-dam-listener}

È necessario attivare il listener  Adobe CQ Dynamic Media Classic Dam, che per impostazione predefinita è disabilitato.

Per attivarla:

1. Toccate l&#39;icona [!UICONTROL Strumenti], quindi andate a **[!UICONTROL Operazioni > Console Web.]** Viene visualizzata la console Web.
1. Andate a **[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]** e selezionate la casella di controllo **[!UICONTROL Enabled]**.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. Toccate **[!UICONTROL Salva.]**

### Aggiunta di timeout configurabile al flusso di lavoro di caricamento Dynamic Media Classic {#adding-configurable-timeout-to-scene-upload-workflow}

Quando un’istanza di AEM è configurata per gestire la codifica video tramite Dynamic Media Classic (Scene7), per impostazione predefinita viene impostato un timeout di 35 minuti per qualsiasi processo di caricamento. Per disporre di processi di codifica video potenzialmente più lunghi, potete configurare questa impostazione:

1. Andate a **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. Modificare il numero come desiderato nel campo **[!UICONTROL Timeout processo attivo]**. Qualsiasi numero non negativo viene accettato con l&#39;unità di misura in secondi. Per impostazione predefinita, è impostata su 2100.

   >[!NOTE]
   >
   >Procedura consigliata: La maggior parte delle risorse vengono assimilate al massimo in pochi minuti (ad esempio, immagini). Tuttavia, in alcuni casi - ad esempio video più grandi - il valore di timeout dovrebbe essere aumentato a 7200 secondi (2 ore) per contenere il tempo di elaborazione lungo. In caso contrario, nei metadati JCR il processo di caricamento di Dynamic Media Classic è contrassegnato come **[!UICONTROL UploadFailed]**.

1. Toccate **[!UICONTROL Salva.]**

### Caricamento automatico da  AEM Assets {#autouploading-from-aem-assets}

A partire da AEM 6.3.2,  AEM Assets è ora configurato per voi in modo che tutte le risorse digitali caricate in Gestione risorse digitali vengano automaticamente aggiornate in Dynamic Media Classic se le risorse si trovano in una cartella di destinazione CQ.

Quando una risorsa viene aggiunta  AEM Assets, viene caricata e pubblicata automaticamente in Dynamic Media Classic.

>[!NOTE]
>
>La dimensione massima per il caricamento automatico da  AEM Assets ad Dynamic Media Classic è 500 MB.

Per configurare il caricamento automatico da  AEM Assets:

1. Toccate l&#39;icona AEM e andate a **[!UICONTROL Distribuzione > Cloud Services]**, quindi, sotto l&#39;intestazione Dynamic Media, in Configurazioni disponibili, toccate **[!UICONTROL dms7 (Dynamic Media]**)
1. Toccate la scheda **[!UICONTROL Avanzate]**, selezionate la casella di controllo **[!UICONTROL Abilita caricamento automatico]**, quindi toccate **[!UICONTROL OK.]** È ora necessario configurare il flusso di lavoro delle risorse DAM per includere il caricamento in Dynamic Media Classic.

   >[!NOTE]
   >
   >Per informazioni su come spostare risorse in Dynamic Media Classic in uno stato non pubblicato, consultate [Configurazione dello stato (pubblicato/non pubblicato) delle risorse inviate ad Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Tornate alla pagina di AEM benvenuto e toccate **[!UICONTROL Flussi di lavoro.]** Fate doppio clic sul flusso di lavoro  **DAM Update** Assetworkflow per aprirlo.
1. Nella barra laterale, andate ai componenti **[!UICONTROL Workflow]** e selezionate **[!UICONTROL Dynamic Media Classic.]** Trascina  **[!UICONTROL Dynamic Media]** Classic nel flusso di lavoro e tocca  **[!UICONTROL Salva.]** Le risorse aggiunte  AEM Assets nella cartella di destinazione verranno caricate automaticamente in Dynamic Media Classic.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* Quando si aggiungono risorse dopo l’automazione, se non vengono inserite nella cartella di destinazione CQ, non vengono caricate in Dynamic Media Classic.
   >* AEM tutti i metadati come XMP prima di caricarli in Dynamic Media Classic, pertanto tutte le proprietà sul nodo di metadati sono disponibili in Dynamic Media Classic come XMP.


### Configurazione dello stato (pubblicato/non pubblicato) delle risorse inviate ad Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Se state spostando le risorse da  AEM Assets a Dynamic Media Classic, potete pubblicarle automaticamente (comportamento predefinito) oppure inviarle ad Dynamic Media Classic in uno stato non pubblicato.

È possibile che non sia necessario pubblicare immediatamente le risorse in Dynamic Media Classic se desiderate eseguirne il test in un ambiente di pubblicazione protetta prima di iniziare la pubblicazione. Puoi usare AEM con l’ambiente di verifica protetta di Dynamic Media Classic per spostare le risorse direttamente da Risorse in Dynamic Media Classic in uno stato non pubblicato.

Le risorse Dynamic Media Classic restano disponibili tramite anteprima protetta. Solo quando le risorse vengono pubblicate all’interno AEM, anche le risorse Dynamic Media Classic diventano live in produzione.

Per pubblicare immediatamente le risorse quando vengono inviate ad Dynamic Media Classic, non è necessario configurare alcuna opzione. Questo è il comportamento predefinito.

Tuttavia, se non desiderate che le risorse vengano inviate automaticamente ad Dynamic Media Classic per la pubblicazione, questa sezione descrive come configurare AEM e Dynamic Media Classic per eseguire questa operazione.

#### Prerequisiti per inviare le risorse ad Dynamic Media Classic non pubblicato {#prerequisites-to-push-assets-to-scene-unpublished}

Prima di inviare le risorse ad Dynamic Media Classic senza pubblicarle, dovete impostare quanto segue:

1. [Utilizzate l&#39;Admin Console  per creare un caso di supporto.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) Nel caso in cui si tratti di assistenza, è necessario abilitare l&#39;anteprima protetta per l&#39;account Dynamic Media Classic.
1. Seguite le indicazioni per [configurare l&#39;anteprima protetta per il vostro account Dynamic Media Classic.](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

Si tratta degli stessi passaggi da seguire per creare qualsiasi configurazione di test protetto in Dynamic Media Classic.

>[!NOTE]
>
>Se l&#39;ambiente di installazione è un sistema operativo Unix a 64 bit, vedere [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) per informazioni sulle opzioni di configurazione aggiuntive da impostare.

#### Limitazioni note per l&#39;invio di risorse nello stato non pubblicato {#known-limitations-for-pushing-assets-in-unpublished-state}

Se utilizzate questa funzione, tenete presenti le seguenti limitazioni:

* Non è supportato il controllo delle versioni.
* Se una risorsa è già pubblicata in AEM e viene creata una versione successiva, la nuova versione verrà immediatamente pubblicata dal vivo in produzione. La pubblicazione dopo l’attivazione funziona solo con la pubblicazione iniziale di una risorsa.

>[!NOTE]
>
>Se desiderate pubblicare immediatamente le risorse, è consigliabile mantenere l&#39;opzione **[!UICONTROL Abilita anteprima protetta]** impostata su **[!UICONTROL Immediatamente]** e utilizzare la funzione **[!UICONTROL Abilita caricamento automatico]**.

### Impostazione dello stato delle risorse inviate ad Dynamic Media Classic come non pubblicate {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>Se un utente pubblica la risorsa in AEM, attiva automaticamente la risorsa S7 nella risorsa produzione/live (la risorsa non sarà più in anteprima protetta/non verrà più pubblicata).

Per impostare lo stato delle risorse inviate ad Dynamic Media Classic come non pubblicate:

1. Toccate l&#39;icona AEM e andate a **[!UICONTROL Distribuzione > Cloud Services]**, toccate **[!UICONTROL Dynamic Media Classic]**, quindi selezionate la configurazione in Dynamic Media Classic.
1. Toccate la scheda **[!UICONTROL Avanzate]**. Nel menu a discesa **[!UICONTROL Abilita visualizzazione protetta]**, selezionate **[!UICONTROL Al momento dell&#39;attivazione della pubblicazione AEM]** per inviare le risorse ad Dynamic Media Classic senza eseguire la pubblicazione. Per impostazione predefinita, questo valore è impostato su **[!UICONTROL Immediatamente]**, dove le risorse Dynamic Media Classic vengono pubblicate immediatamente.

   Per ulteriori informazioni sul test delle risorse prima di renderle pubbliche, consultate [Documentazione Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html).

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. Toccare **[!UICONTROL OK.]**

Se si abilita Vista protetta, le risorse vengono inviate al server di anteprima protetto e non vengono pubblicate.

Per verificare questo aspetto, passa a un componente Dynamic Media Classic in una pagina AEM e tocca **[!UICONTROL Modifica.]** Il server di anteprima protetto della risorsa verrà elencato nell’URL. Dopo la pubblicazione in AEM, il dominio del server nel riferimento del file viene aggiornato dall&#39;URL di anteprima all&#39;URL di produzione.

### Abilitazione di Dynamic Media Classic per WCM {#enabling-scene-for-wcm}

L&#39;abilitazione di Dynamic Media Classic per WCM è necessaria per due motivi:

* Per attivare l’elenco a discesa dei profili video universali per l’authoring delle pagine. In caso contrario, il menu a discesa **[!UICONTROL Universal Video Preset]** è vuoto e non può essere impostato.
* Se una risorsa digitale non si trova nella cartella di destinazione, potete caricare la risorsa in Dynamic Media Classic se avete abilitato Dynamic Media Classic per tale pagina nelle proprietà della pagina e trascinare e rilasciare la risorsa su un componente Dynamic Media Classic. Si applicano le regole di ereditarietà normali (ovvero le pagine figlie erediteranno la configurazione dalla pagina padre).

Quando si abilita Dynamic Media Classic per WCM, si noti che, come con altre configurazioni, si applicano le regole di ereditarietà. Potete abilitare Dynamic Media Classic per WCM nell’interfaccia utente touch o classica.

#### Abilitazione di Dynamic Media Classic per WCM nell&#39;interfaccia utente ottimizzata per il tocco {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

Per abilitare Dynamic Media Classic per WCM nell’interfaccia touch:

1. Toccate l&#39;icona AEM e accedete a **[!UICONTROL Siti]**, quindi alla pagina principale del sito Web (non specifica della lingua).

1. Nella barra degli strumenti, selezionare l&#39;icona [!UICONTROL settings] e toccare **[!UICONTROL Apri proprietà.]**

1. Toccare **[!UICONTROL Cloud Services]** e toccare **[!UICONTROL Aggiungi configurazione]**, quindi selezionare **[!UICONTROL Dynamic Media Classic.]**
1. Nell&#39;elenco a discesa **[!UICONTROL Adobe Dynamic Media Classic]**, selezionare la configurazione desiderata e toccare **[!UICONTROL OK.]**

   ![chlimage_1-303](assets/chlimage_1-303.png)

   I predefiniti per video di tale configurazione di Dynamic Media Classic sono disponibili per l’utilizzo in AEM con il componente video Dynamic Media Classic in quella pagina e nelle pagine figlie.

#### Abilitazione di Dynamic Media Classic per WCM nell&#39;interfaccia utente classica {#enabling-scene-for-wcm-in-the-classic-user-interface}

Per abilitare Dynamic Media Classic per WCM nell’interfaccia classica:

1. In AEM, toccare **[!UICONTROL Siti Web]** e passare alla pagina principale del sito Web (non specifica della lingua).

1. Nella barra laterale, toccare l&#39;icona **[!UICONTROL Pagina]** e toccare **[!UICONTROL Proprietà pagina.]**

1. Toccare **[!UICONTROL Cloud Services > Aggiungi servizi > Dynamic Media Classic.]**
1. Nell&#39;elenco a discesa **[!UICONTROL Adobe Dynamic Media Classic]**, selezionare la configurazione desiderata e toccare **[!UICONTROL OK.]**

   I predefiniti per video di tale configurazione di Dynamic Media Classic sono disponibili per l’utilizzo in AEM con il componente video Dynamic Media Classic in quella pagina e nelle pagine figlie.

### Configurazione di una configurazione predefinita {#configuring-a-default-configuration}

Se disponete di più configurazioni Dynamic Media Classic, potete specificarne una come predefinita per il browser dei contenuti Dynamic Media Classic.

È possibile contrassegnare come predefinita una sola configurazione Dynamic Media Classic alla volta. La configurazione predefinita è costituita dalle risorse aziendali visualizzate per impostazione predefinita nel browser dei contenuti Dynamic Media Classic.

Per configurare la configurazione predefinita:

1. Toccate l&#39;icona AEM e andate a **[!UICONTROL Distribuzione > Cloud Services]**, toccate **[!UICONTROL Dynamic Media Classic]**, quindi selezionate la configurazione in Dynamic Media Classic.
1. Toccate **[!UICONTROL Modifica]** per aprire la configurazione.

1. Nella scheda **[!UICONTROL Generale]**, selezionare la casella di controllo **[!UICONTROL Configurazione predefinita]** per fare di questa la società predefinita e il percorso principale che vengono visualizzati nel browser dei contenuti di Dynamic Media Classic.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >Se è presente una sola configurazione, la casella di controllo **[!UICONTROL Configurazione predefinita]** non ha alcun effetto.

### Configurazione della cartella ad hoc {#configuring-the-ad-hoc-folder}

Potete configurare la cartella in cui vengono caricate le risorse in Dynamic Media Classic se la risorsa non si trova nella cartella di destinazione CQ. Consultate Pubblicazione di risorse dall’esterno della cartella di destinazione di CQ.

Per configurare la cartella adhoc:

1. Toccate l&#39;icona AEM e andate a **[!UICONTROL Distribuzione > Cloud Services]**, toccate **[!UICONTROL Dynamic Media Classic]**, quindi selezionate la configurazione in Dynamic Media Classic.
1. Toccate **[!UICONTROL Modifica]** per aprire la configurazione.

1. Toccate la scheda **[!UICONTROL Avanzate]**. Nel campo **[!UICONTROL Cartella ad hoc]** è possibile modificare la cartella **Ad-hoc**. Per impostazione predefinita, si tratta del **nome_della_società/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### Configurazione dei predefiniti universali {#configuring-universal-presets}

Per configurare i predefiniti universali per il componente video, consultate [Video](/help/assets/s7-video.md).

## Abilitazione del parametro del processo di caricamento di risorse/Dynamic Media Classic basato su tipi MIME supporto di {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Potete abilitare i parametri di caricamento configurabili di Dynamic Media Classic attivati dalla sincronizzazione di risorse Digital Asset Manager/Dynamic Media Classic.

Nello specifico, è possibile configurare il formato di file accettato per tipo MIME nell&#39;area OSGi (iniziativa Open Service Gateway) del pannello Configurazione AEM console Web. Potete quindi personalizzare i singoli parametri del processo di caricamento utilizzati per ciascun tipo MIME nel JCR (Java Content Repository).

**Per abilitare le risorse basate su tipi MIME:**

1. Toccate l&#39;icona AEM e accedete a **[!UICONTROL Strumenti > Operazioni > Console Web.]**
1. Nel pannello Configurazione console Web di Adobe Experience Manager, nel menu **[!UICONTROL OSGi]**, toccare **[!UICONTROL Configurazione.]**
1. Nella colonna Nome, individuare e toccare **[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME type Service]** per modificare la configurazione.
1. Nell&#39;area Mime Type Mapping, toccare un segno più (+) per aggiungere un tipo MIME.

   Vedere [Tipi MIME supportati](/help/assets/assets-formats.md#supported-mime-types).

1. Nel campo di testo, digitare il nuovo nome del tipo MIME.

   Ad esempio, digitare un `<file_extension>=<mime_type>` come in `EPS=application/postscript` OR `PSD=image/vnd.adobe.photoshop`.

1. Nell&#39;angolo inferiore destro della finestra di configurazione, toccare **[!UICONTROL Salva.]**
1. Ritornare a AEM e nella barra a sinistra, toccare CRXDE Lite.
1. Nella pagina CRXDE Lite, nella barra a sinistra, individuate `/etc/cloudservices/scene7/<environment>` (sostituite `<environment>` con il nome effettivo).
1. Espandere `<environment>` (sostituire `<environment>` con il nome effettivo) per visualizzare il nodo `mimeTypes`.
1. Toccate il mimeType appena aggiunto.

   Ad esempio, `mimeTypes > application_postscript` OR `mimeTypes > image_vnd.adobe.photoshop`.

1. Sul lato destro della pagina CRXDE Lite, toccate la scheda **[!UICONTROL Proprietà]**.
1. Specificate un parametro di processo di caricamento Dynamic Media Classic nel campo del valore **[!UICONTROL jobParam]**.

   Esempio, `psprocess="rasterize"&psresolution=120` .

   Per ulteriori parametri di processo di caricamento, consultate l&#39;API [ Adobe Dynamic Media Classic Image Production System API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html).

   >[!NOTE]
   >
   >Se caricate dei file PSD e desiderate elaborarli come modelli con estrazioni di livelli, immettete quanto segue nel campo **[!UICONTROL jobParam]** value:
   >
   >`process=MaintainLayers&createTemplate=true`
   >
   >Accertatevi che il file PSD contenga &quot;livelli&quot;. Se è strettamente un’immagine o un’immagine con maschera, viene elaborata come immagine perché non vi sono livelli da elaborare.

1. Nell&#39;angolo superiore sinistro della pagina dei CRXDE Lite, toccare **[!UICONTROL Salva tutto.]**

## Risoluzione dei problemi relativi all&#39;integrazione di Dynamic Media Classic e AEM {#troubleshooting-scene-and-aem-integration}

In caso di problemi durante l&#39;integrazione AEM con Dynamic Media Classic, consulta i seguenti scenari per le soluzioni.

**Se la pubblicazione delle risorse digitali in Dynamic Media Classic ha esito negativo:**

* Verificate che la risorsa che state tentando di caricare si trovi nella cartella **[!UICONTROL CQ target]** (specificate questa cartella nella configurazione cloud Dynamic Media Classic).
* In caso contrario, è necessario configurare la configurazione cloud in **[!UICONTROL Proprietà pagina]** per tale pagina per consentire il caricamento nella cartella **[!UICONTROL CQ adhoc]**.

* Controllate i registri per eventuali informazioni.

**Se i predefiniti video non vengono visualizzati:**

* Assicurarsi di aver configurato la configurazione cloud di tale pagina tramite **[!UICONTROL Proprietà pagina.]** I predefiniti per video sono disponibili nel componente video Dynamic Media Classic.

**Se le risorse video non vengono riprodotte in AEM:**

* Accertatevi di aver usato il componente video corretto. Il componente video Dynamic Media Classic è diverso dal componente Video di base. Consultate [Componente video di base e componente video di Dynamic Media Classic](/help/assets/s7-video.md).

**Se le risorse nuove o modificate in AEM non vengono caricate automaticamente in Dynamic Media Classic:**

* Verificate che le risorse si trovino nella cartella di destinazione CQ. Solo le risorse che si trovano nella cartella di destinazione CQ vengono aggiornate automaticamente (a condizione che sia stato configurato  AEM Assets per caricare automaticamente le risorse).
* Accertatevi di aver configurato la configurazione degli Cloud Services su Abilita caricamento automatico e di aver aggiornato e salvato il flusso di lavoro delle risorse DAM per includere il caricamento di Dynamic Media Classic.
* Quando caricate un’immagine in una sottocartella della cartella di destinazione Dynamic Media Classic, effettuate una delle seguenti operazioni:

   * Accertatevi che i nomi di tutte le risorse, indipendentemente dalla posizione, siano univoci. In caso contrario, la risorsa nella cartella di destinazione principale viene eliminata e rimane solo la risorsa nella sottocartella.
   * Modificate il modo in cui Dynamic Media Classic sovrascrive le risorse nell’area Configurazione dell’account Dynamic Media Classic. Non impostate Dynamic Media Classic per sovrascrivere le risorse indipendentemente dalla posizione in cui sono memorizzate, se usate risorse con lo stesso nome nelle sottocartelle.

**Se le risorse o le cartelle eliminate non sono sincronizzate tra Dynamic Media Classic e AEM:**

* Le risorse e le cartelle eliminate in  AEM Assets vengono comunque visualizzate nella cartella sincronizzata in Dynamic Media Classic. È necessario eliminarli manualmente.

**Se il caricamento del video non riesce**

* Se il caricamento del video non riesce e state utilizzando AEM per codificare il video tramite l&#39;integrazione Dynamic Media Classic, consultate [Aggiunta di timeout configurabile al flusso di lavoro di caricamento Dynamic Media Classic](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>L&#39;importazione di risorse da un account Dynamic Media Classic esistente potrebbe richiedere molto tempo per la visualizzazione in AEM. Accertatevi di specificare una cartella in Dynamic Media Classic che non contenga troppe risorse (ad esempio, la cartella principale avrà spesso troppe risorse).
>
>Se desiderate testare l&#39;integrazione, potete fare in modo che la cartella principale punti solo a una sottocartella, invece che all&#39;intera società.

