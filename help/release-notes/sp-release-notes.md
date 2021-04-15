---
title: '[!DNL Experience Manager] Note sulla versione 6.5 del service pack'
description: Note sulla versione specifiche di  [!DNL Adobe Experience Manager] 6.5 service pack 8
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
translation-type: tm+mt
source-git-commit: e2eb007eb7660004f98b4c26aba00a6a6e2a2f1a
workflow-type: tm+mt
source-wordcount: '3418'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] Note sulla versione 6.5 del service pack  {#aem-service-pack-release-notes}

## Informazioni sulla versione {#release-information}

| Prodotti | [!DNL Adobe Experience Manager] 6,5 |
| -------- | ---------------------------- |
| Versione | 6.5.8.0 |
| Tipo | Versione Service Pack |
| Data | 11 marzo 2021 |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## Contenuto in [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] La versione 6.5.8.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza, rilasciati a partire dalla versione 6.5 di aprile 2019. Il service pack è installato su [!DNL Adobe Experience Manager] 6.5.

Le funzioni chiave e i miglioramenti introdotti in [!DNL Adobe Experience Manager] 6.5.8.0 sono:

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* Quando utilizzi la funzionalità [Risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md), ora puoi visualizzare un elenco di tutte le [!DNL Sites] pagine che utilizzano la risorsa. Questi riferimenti a una risorsa sono disponibili nella pagina [!UICONTROL Proprietà] di una risorsa. Questo consente agli amministratori, agli esperti di marketing e ai bibliotecari di visualizzare in modo completo l’utilizzo delle risorse, consentendo un migliore monitoraggio, gestione e coerenza del marchio.

* Quando si elimina una risorsa a cui viene fatto riferimento in una pagina web, [!DNL Experience Manager] [visualizza un avviso](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references). Puoi forzare l’eliminazione di una risorsa di riferimento oppure controllare e modificare i riferimenti visualizzati nella pagina [!DNL Properties] della risorsa. Facendo clic sui riferimenti vengono aperte le pagine locali e remote [!DNL Sites] .

* Ordinamento delle pagine Live Copy disponibili per il rollout utilizzando le proprietà [!UICONTROL Name], [!UICONTROL Last modified date,] e [!UICONTROL Last rollout date] .

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.6. <!-- TBD: Mention the version -->

Per un elenco completo delle funzioni e dei miglioramenti introdotti in [!DNL Experience Manager] 6.5.8.0, consulta [novità in [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md).

Di seguito è riportato l&#39;elenco delle correzioni apportate in [!DNL Experience Manager] 6.5.8.0 .

### [!DNL Sites] {#sites-6580}

* Quando una pagina viene spostata in blueprint, la destinazione dei collegamenti non viene aggiornata (NPR-35724).
* Il lettore basato su Tizen non riesce ad autenticarsi su alcuni browser. Il problema si verifica con i browser che non supportano l&#39;attributo samesite=none (NPR-35589).
* Un contenitore dinamico sbloccato non visualizza i componenti consentiti (NPR-35565).
* Quando crei una Live Copy di una pagina appena aggiunta, il Language Master crea due copie per ciascun dominio (NPR-35545).
* Deadlock nel Registro componenti SCR quando molti thread sono bloccati a causa del timer `org.apache.felix.scr.impl.ComponentRegistry`. Come risultato, [!DNL Experience Manager] smette di rispondere per un tempo indeterminato (GRANITE-33125,FELIX-6252).
* Quando esegui la ricerca di una risorsa specifica nella barra laterale, il risultato contiene alcune risorse non sottoposte a ricerca (NPR-35524).
* Quando si abilita SSL per un&#39;istanza di Experience Manager, il percorso contestuale viene rimosso (NPR-35477).
* Quando crei un elenco, aggiungi del testo come primo elemento, aggiungi una tabella come secondo elemento e aggiungi un elenco all’interno della tabella, l’elenco principale si distorce (NPR-35465).
* Quando si utilizzano plug-in diversi su voci di elenco consecutive, agli elementi di elenco viene aggiunto un tag aggiuntivo <br> (NPR-35464).
* Quando si inserisce un elenco tra due paragrafi, non è possibile aggiungere una tabella all’elenco (NPR-35356).
* Quando avvii un aggiornamento di un&#39;istanza AEM da AEM 6.3 a AEM 6.5, l&#39;avvio dell&#39;istanza di aggiornamento richiede più tempo (NPR-35323).
* Quando replichi una risorsa AEM che include una parentesi graffa (). nel nome, la replica non riesce (GRANITE-27004, NPR-35315).
* Quando si aggiungono titoli a un editor Rich Text, il pulsante paragrafo è disattivato (NPR-35256).
* Quando aggiungi un elemento a un elenco esistente, questo elimina l’elenco comprimibile o attivabile successivo (NPR-35206).
* Quando l’opzione Rollout pagina è selezionata, viene visualizzata una finestra di dialogo con tutte le Live Copy disponibili e viene eseguito il rollout automatico. Le Live Copy delle pagine vengono distribuite in tutte le aree geografiche senza l’intervento dell’utente (NPR-35138).
* Quando utilizzi l’opzione Includi elementi figlio, l’opzione Gestisci pubblicazione non elenca tutte le pagine. Sono elencate solo 22 pagine (NPR-35086).
* Quando un criterio viene modificato, il componente di testo non mantiene le modifiche ai criteri (NPR-35070).
* Quando si applicano un rientro ad alcuni elementi di un elenco numerato, tutti gli elementi mantengono lo stesso numero, anche se la numerazione deve iniziare da 1 per gli elementi con lo stesso rientro (CQ-4313011).
* Quando la minimizzazione è abilitata, non puoi modificare alcuna pagina o componente. I problemi sono iniziati dopo l&#39;installazione di AEM 6.5 Service Pack 7 (CQ-4311133).
* I filtri di ricerca e risorse Omni restituiscono risultati irrilevanti o nessun risultato (CQ-4312322, NPR-35793).
* Quando più pagine accedono contemporaneamente a una libreria client, il gestore della libreria HTML non carica la libreria client. Porta al rendering non corretto delle pagine (NPR-35538).
* Il percorso contestuale viene rimosso automaticamente quando si imposta un SSL in [!DNL Experience Manager] (NPR-35294).
* La gestione dei pacchetti non disconnette gli utenti dopo aver fatto clic sull’opzione di disconnessione (NPR-35160).

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0  [!DNL Assets] risolve i seguenti problemi e fornisce i seguenti miglioramenti.

* Al ripristino di una versione precedente di una risorsa, l’evento DamEvent.Type RESTORED non viene attivato nella console OSGi (NPR-35789).
* `IndexWriter.merge` causa  `OutOfMemoryError` errori poiché la funzionalità di assegnazione tag avanzati crea  `/oak:index/lucene` indici  `/oak:index/ntBaseLucene` e di grandi dimensioni (NPR-35651).
* Viene visualizzato un messaggio di errore quando si tenta di salvare una cartella di tipo [!UICONTROL Contributo risorse] con caratteri multibyte nel nome (NPR-35605).
* Quando si utilizzano i campi del sottotipo metadati a cascata, si verifica un errore &quot;Compila questo campo&quot; errato (NPR-35643).
* Quando una risorsa esistente viene trascinata sull’ interfaccia utente [!DNL Assets] e viene creata una nuova versione, le modifiche nei metadati non sono persistenti (NPR-34940).
* Quando crei regole nell&#39;editor dello schema metadati per un menu a cascata, l&#39;opzione [!UICONTROL Dipendente da] ripete lo stesso nome (NPR-35596).
* La ricerca per similarità non funziona dopo la modifica della [!UICONTROL Barra di ricerca amministrazione risorse] (NPR-35588).
* Dall&#39;interno di una cartella, se apri la ricerca delle risorse nella barra a sinistra facendo clic su [!UICONTROL Filtro], il filtro in [!UICONTROL Stato] > [!UICONTROL Pagamento] > [!UICONTROL Estratto] non funziona (NPR-35530).
* Se tenti di eliminare tutti i tag avanzati di una risorsa e salvi le modifiche, i tag non vengono rimossi. Tuttavia, l’interfaccia utente indica che le modifiche sono state salvate (NPR-35519).
* Gli utenti non possono ridisporre o ordinare le risorse nella vista a elenco in una cartella ordinabile (NPR-35516).
* Se modifichi lo schema metadati predefinito, il campo tag della pagina [!UICONTROL Proprietà] della risorsa diventa un campo di testo. La modifica consente agli utenti inconsapevoli di aggiungere tag on-demand e i tag vengono memorizzati come stringa nell&#39;archivio (NPR-35478).
* Durante il download di una risorsa, se fornisci un nome che non dispone di un indirizzo e-mail valido, l’opzione di download non è disponibile. Tuttavia, se è selezionata un’altra opzione nella finestra di dialogo di download, il pulsante è abilitato, ma non viene inviato un messaggio e-mail (NPR-35365).
* Gli utenti non possono archiviare le risorse dopo aver modificato quelle in [!DNL Adobe InDesign] e ricevono un errore per mancanza di autorizzazioni (NPR-35341).
* La libreria JavaScript Handlebars viene aggiornata alla versione 4.7.6 (NPR-35333).
* L’interfaccia dell’editor di metadati smette di funzionare come previsto quando si inizia dalla modifica in serie dei metadati e si deselezionano gli elementi fino a quando non viene selezionato un singolo elemento (NPR-35144).
* La navigazione globale non apre la console corretta quando si fa clic all’interno della pagina `assets.html` (CQ-4312311).
* [!DNL Assets] non visualizza il rendering RGB per una risorsa con rendering RGB (CQ-4310190).
* L&#39;opzione [!UICONTROL Relate] nel menu non viene visualizzata correttamente nella pagina [!UICONTROL Proprietà] (CQ-4310188).
* Se il filtro filetype per i documenti viene utilizzato per cercare le risorse e creare una Raccolta avanzata, il filtro non viene applicato quando si accede alla raccolta. Nella ricerca vengono invece visualizzati tutti i tipi di risorse (NPR-35759).
* Non puoi trascinare e aggiungere risorse in una Lightbox dall’ interfaccia utente di [!DNL Assets] (NPR-35901).
* Quando viene creata una nuova versione di una risorsa esistente dopo la risoluzione del conflitto di denominazione, i metadati della risorsa originale vengono sovrascritti (CQ-4313594).
* Quando filtri la ricerca delle risorse utilizzando un filtro di ricerca o un predicato, apri una risorsa per visualizzarla o modificarla e torna alla pagina dei risultati della ricerca, il filtro non funziona. Tutte le risorse ricercate sono elencate come non filtrate (NPR-35913).

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* L’opzione URL per il predefinito immagine RESS è abilitata nella pagina dei dettagli della risorsa. Ora, nella pagina dei dettagli della risorsa sono disponibili entrambe le opzioni URL e RESS quando nella sezione delle rappresentazioni dinamiche è selezionato il predefinito immagine RESS . (CQ-4311241)
* Componente multimediale interattivo : il video interattivo non funziona se l’utente ha [!DNL Experience Manager] con configurazione di pubblicazione selettiva (CQ-4311054).
* Se sposti le risorse tra le cartelle, la sincronizzazione tra [!DNL Experience Manager] e [!DNL Dynamic Media–Scene7] tramite API è molto lenta (CQ-4310001).
* Quando si utilizza Omnisearch, le dimensioni dei registri aumentano in modo significativo (CQ-4309153).
* Quando la sincronizzazione selettiva è abilitata e una risorsa viene copiata (non spostata) in una cartella di sincronizzazione, non viene sincronizzata come previsto (CQ-4307122).
* Per le risorse caricate che vengono pubblicate automaticamente in DM, lo stato non viene visualizzato Pubblicato in AEM. Inoltre, la colonna dello stato di pubblicazione di Dynamic Media non mostra lo stato di pubblicazione corretto (CQ-4306415).
* Se una risorsa viene pubblicata su [!DNL Experience Manager] e è impostata per la pubblicazione su [!DNL Dynamic Media] all’attivazione, il valore dei metadati `scene7FileStatus` non viene aggiornato come previsto (CQ-4308269).
* Durante la modifica del profilo video, [!DNL Experience Manager] non visualizza i valori di altezza e bitrate impostati per il predefinito video. I campi appaiono vuoti (CQ-4311828).

### [!DNL Commerce] {#commerce-6580}

* Impossibile creare un tag personalizzato per tutti i prodotti in Commerce (CQ-4310682).

* L’aggiornamento del riferimento delle risorse di prodotto fa sì che i thread di replica siano nello stato di attesa fino a quando il thread ProductAssetListener non completa i suoi impegni verso il JCR (NPR-35269).

### Platform {#platform-6580}

* Quando si utilizza un componente Visualizzazione tabulazione Coral senza schede e si attiva una convalida Foundation, si verifica il seguente errore (NPR-35636):

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* La replica in avanti SCD non riesce per gli eventi Delete per i nodi che includono una virgola nel nome (NPR-35191).

* Dopo l&#39;aggiornamento a AEM 6.5.7, le build iniziano a non riuscire. Il motivo è che una vecchia versione o nessun jackson-core è incorporato nel uber-jar (GRANITE-33006).

### Interfaccia utente {#ui-6580}

* Quando si passa dalla vista a schede alla vista a elenco per i documenti presenti in una cartella della console Risorse, l’ordinamento non funziona correttamente (NPR-35842).

* Quando si crea un collegamento ipertestuale a un testo in un componente di testo, la funzione di ricerca non visualizza i risultati appropriati (NPR-35849).

* Quando un valore non viene fornito a un campo nascosto contrassegnato come obbligatorio, impedisce il salvataggio di un componente (NPR-35219).

### Integrazioni {#integrations-6580}

* Quando utilizzi valori diversi per l’ID tenant IMS e il codice client di Target, [!DNL Experience Manager] non riesce a integrarsi con [!DNL Adobe Target] (NPR-35342).

### Progetti di traduzione {#translation-6580}

* Problemi durante l’esportazione o l’importazione di un processo di traduzione in [!DNL Experience Manager] (NPR-35259).

### Campaign {#campaign-6580}

* Quando crei una pagina della campagna utilizzando un modello predefinito nell’interfaccia utente touch e apri la scheda E-mail nella finestra di dialogo delle proprietà della pagina, la variabile di personalizzazione per i campi oggetto e corpo rimane disabilitata (CQ-4312388).

### [!DNL Communities] {#communities-6580}

* Quando si aggiunge una struttura di pagina a un gruppo community, il titolo [!UICONTROL Gruppo] nel breadcrumb viene modificato nel titolo del primo [!UICONTROL Pagina] (NPR-35803).
* A differenza dei moderatori, un membro della comunità standard non è in grado di accedere e modificare alcun post provvisorio (NPR-35339).
* Controllo degli accessi non funzionante e rifiuto del servizio con `DSRPReindexServlet` che riduce il sito community fino al completamento dell&#39;indicizzazione (NPR-35591).
* La rimozione di [!UICONTROL Tutti gli utenti] dal campo [!UICONTROL Amministratori] in realtà non li rimuove dal back-end (NPR-35592, NPR-35611).
* Il componente [!UICONTROL Componi messaggio] non restituisce alcun risultato quando il testo immesso è una corrispondenza parziale (NPR-35666).

* Quando si tenta di aggiungere tag a un nuovo blog selezionando **Aggiungi tag**, si nota un certo impatto sulle prestazioni. Per migliorare le prestazioni, installa [cqTagLucene-0.0.1.zip hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip) che risolve il problema dei suggerimenti sui tag. Puoi scaricare l&#39;hotfix da [!DNL Software Distribution].

### [!DNL Brand Portal] {#brandportal-6580}

* L’aggiunta di un membro a una cartella di tipo [!UICONTROL Contributo risorse] mostra la didascalia [!UICONTROL Aggiungi utente o gruppo] nell’interfaccia utente, anche se sono supportati solo gli utenti attivi di Brand Portal e non i gruppi (NPR-35332).

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>Per [!DNL Experience Manager Forms] vengono rilasciati pacchetti del componente aggiuntivo una settimana dopo la data di rilascio pianificata per il Service Pack di [!DNL Experience Manager].

**Moduli adattivi**

* Quando si inserisce una tabella con una riga ripetibile in un pannello ripetibile con più istanze in un modulo adattivo, la tabella viene sempre aggiunta alla prima istanza del pannello (NPR-35635).

* Quando lo stato attivo raggiunge nuovamente il componente CAPTCHA dopo averlo verificato correttamente in un modulo adattivo, [!DNL Experience Manager Forms] visualizza il messaggio di errore `Provide Captcha phrase to proceed` (NPR-35539).

**Comunicazione interattiva**

* Quando si invia un modulo tradotto, i messaggi di invio vengono visualizzati in inglese e non vengono tradotti nella lingua appropriata (NPR-35808).

* Quando si include una condizione Nascondi nell&#39;XDP o nei frammenti di documento allegati, la comunicazione interattiva non viene caricata (NPR-35745).

**Gestione della corrispondenza**

* Quando si modifica una lettera, il caricamento dei moduli con condizioni richiede un tempo maggiore (NPR-35325).

* Quando selezioni una risorsa dal riquadro di navigazione a sinistra che non è inclusa in una lettera e quindi selezioni la risorsa successiva, l’evidenziazione blu non viene rimossa dalla risorsa selezionata in precedenza (NPR-35851).

* Quando si modificano i campi di testo in una lettera, [!DNL Experience Manager Forms] visualizza il messaggio di errore `Text Edit Failed` (CQ-4313770).

**Flusso di lavoro**

* Quando tenti di aprire un modulo adattivo su un&#39;applicazione mobile [!DNL Experience Manager Forms] per iOS, l&#39;applicazione si ferma per rispondere (CQ-4314825).

* La scheda [!UICONTROL To-do] nell’area di lavoro HTML visualizza i caratteri HTML (NPR-35298).

**XMLFM**

* Quando si genera un documento XML utilizzando il servizio di output, si verifica l&#39;errore `OutputServiceException` per alcuni dei file XML (CQ-4311341, CQ-4313893).

* Quando applichi la proprietà apice al primo carattere del punto elenco, la dimensione del punto elenco diventa più piccola (CQ-4306476).

* I PDF forms generati utilizzando il servizio di output non includono bordi (CQ-4312564).

**Designer**

* Quando si apre un file XDP in [!DNL Experience Manager Forms] Designer, viene generato un file designer.log nella stessa cartella del file XDP (CQ-4309427, CQ-4310865).

**Moduli HTML5**

* Quando selezioni una casella di controllo in un modulo adattivo nel browser Web [!DNL Safari] per [!DNL iOS 14.1 or 14.2], non vengono visualizzati altri campi (NPR-35652).

**Gestione Forms**

* Nessun messaggio di conferma per indicare il corretto caricamento in massa di file XDP nell’archivio CRX (NPR-35546).

**Sicurezza dei documenti**

* Sono stati segnalati diversi problemi per l’opzione [!UICONTROL Modifica criterio] in AdminUI (NPR-35747).

Per informazioni sugli aggiornamenti di sicurezza, vedere [pagina dei bollettini sulla sicurezza degli Experienci Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## Installa 6.5.8.0 {#install}

**Requisiti di configurazione e ulteriori informazioni**

* Experience Manager 6.5.8.0 richiede Experience Manager 6.5. Per istruzioni dettagliate, consulta la [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) .
* Il download del service pack è disponibile ad Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* In una distribuzione con MongoDB e più istanze, installa Experience Manager 6.5.8.0 in una delle istanze Autore utilizzando Gestione pacchetti.

>[!NOTE]
>
>Adobe sconsiglia di rimuovere o disinstallare il pacchetto [!DNL Adobe Experience Manager] 6.5.8.0.

### Installa il service pack {#install-service-pack}

Per installare il service pack su un&#39;istanza [!DNL Adobe Experience Manager] 6.5, segui questi passaggi:

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (e questo accade quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia inoltre di riavviare se l&#39;orario di attività corrente per un&#39;istanza è elevato.

1. Prima di installare, scegli uno snapshot o un nuovo backup dell&#39;istanza [!DNL Experience Manager].

1. Scarica il service pack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip).

1. Apri Gestione pacchetti e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l&#39;istanza dopo l&#39;installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l&#39;istanza. Consulta [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La finestra di dialogo nell’interfaccia utente di Gestione pacchetti talvolta si chiude durante l’installazione del service pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di essere certi che le installazioni abbiano esito positivo. In genere questo accade su [!DNL Safari] ma può accadere in modo intermittente su qualsiasi browser.

**Installazione automatica**

Esistono due modi per installare automaticamente Adobe Experience Manager 6.5.8.0 in un&#39;istanza funzionante:

A. Posiziona il pacchetto nella cartella `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.

B. Utilizza l’ [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizza `cmd=install&recursive=true` in modo che i pacchetti nidificati siano installati.

>[!NOTE]
>
>Adobe Experience Manager 6.5.8.0 non supporta l’installazione di Bootstrap.

**Convalidare l’installazione**

1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager (6.5.8.0)` in [!UICONTROL Prodotti installati].

1. Tutti i bundle OSGi sono **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** nella console OSGi (Usa la console Web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.3 o successiva (Usa console Web: `/system/console/bundles`).

Per conoscere le piattaforme certificate per l’utilizzo con questa versione, consulta i [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

### Installa il pacchetto aggiuntivo di Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignora questa sezione se non utilizzi Experience Manager Forms. Le correzioni apportate in Experience Manager Forms vengono distribuite tramite un pacchetto aggiuntivo separato una settimana dopo il rilascio pianificato di [!DNL Experience Manager] Service Pack .

1. Assicurati di aver installato il Service Pack di Adobe Experience Manager.
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) per il sistema operativo in uso.
1. Installa il pacchetto aggiuntivo di Forms come descritto in [Installazione dei pacchetti aggiuntivi di AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>AEM 6.5.8.0 include una nuova versione di [Pacchetto compatibilità AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases). Se utilizzi una versione precedente del pacchetto di compatibilità di AEM Forms e aggiorni AEM 6.5.8.0, installa la versione più recente del pacchetto dopo l’installazione del pacchetto aggiuntivo di Forms.

### Installare Adobe Experience Manager Forms su JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms in JEE. Le correzioni in Adobe Experience Manager Forms su JEE vengono distribuite tramite un programma di installazione separato.

Per informazioni sull&#39;installazione del programma di installazione cumulativo per Experience Manager Forms su JEE e sulla configurazione post-distribuzione, consulta le [note sulla versione](jee-patch-installer-65.md).

>[!NOTE]
>
>Dopo aver installato il programma di installazione cumulativo per Experience Manager Forms su JEE, installa il pacchetto aggiuntivo Forms più recente, elimina il pacchetto aggiuntivo Forms dalla cartella `crx-repository\install` e riavvia il server.

### UberJar {#uber-jar}

UberJar per Experience Manager 6.5.8.0 è disponibile nell’ [archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/).

Per utilizzare UberJar in un progetto Maven, consulta [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includi nel POM del progetto la seguente dipendenza:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.8</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell’archivio centrale Maven invece dell’archivio pubblico Maven di Adobe (`repo.adobe.com`). Il file UberJar principale viene rinominato in `uber-jar-<version>.jar`. Pertanto, non esiste `classifier`, con `apis` come valore, per il tag `dependency`.

## Funzioni obsolete {#removed-deprecated-features}

Di seguito è riportato un elenco di funzioni e funzionalità contrassegnate come obsolete con [!DNL Experience Manager] 6.5.7.0. Le funzioni vengono contrassegnate come obsolete inizialmente e successivamente rimosse in una versione futura. In genere viene fornita un’opzione alternativa.

Controlla se utilizzi una funzione o una funzionalità in una distribuzione. Inoltre, pianifica di modificare l’implementazione in modo da utilizzare un’opzione alternativa.

| Area | Funzione obsoleta | Sostituzione |
|---|---|---|
| Integrations (Integrazioni) | La schermata **[!UICONTROL Opt-in di AEM Cloud Services]** è obsoleta. Con l’integrazione Experience Manager e Adobe Target aggiornata all’Experience Manager 6.5 per supportare l’API Adobe Target Standard, che utilizza l’autenticazione tramite Adobe IMS e I/O, e il ruolo crescente di Adobe Launch nella strumentazione delle pagine di Experience Manager per l’analisi e la personalizzazione, la procedura guidata Opt-in è diventata irrilevante dal punto di vista funzionale. | Configura le connessioni di sistema, l’autenticazione Adobe IMS e le integrazioni [!DNL Adobe I/O] tramite i rispettivi servizi cloud Experience Manager. |
| Connettori | Il connettore Adobe JCR per Microsoft SharePoint 2010 e Microsoft SharePoint 2013 è obsoleto, ad Experience Manager 6.5. | N/D |

## Problemi noti {#known-issues}

* Se aggiorni la tua istanza [!DNL Experience Manager] dalla versione 6.5 alla versione 6.5.8.0, puoi visualizzare le eccezioni `RRD4JReporter` nel file `error.log` . Riavvia l&#39;istanza per risolvere il problema.

* Se si installa [!DNL Experience Manager] 6.5 Service Pack 5 o un precedente service pack su [!DNL Experience Manager] 6.5, la copia in runtime del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminata.
Per recuperare la copia runtime, Adobe consiglia di sincronizzare la copia in fase di progettazione del modello di flusso di lavoro personalizzato con la relativa copia in fase di esecuzione utilizzando l’API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Contatta l’Assistenza clienti Adobe in caso di problemi durante la modifica e la creazione di regole a cascata nella finestra di dialogo [!UICONTROL Folder Metadata Schema Forms Editor] e [!UICONTROL Metadata Schema Forms Editor] utilizzando [!UICONTROL Define Rule] (Definisci regola). Le regole già create e salvate funzionano come previsto.

* Se una cartella nella gerarchia viene rinominata in [!DNL Experience Manager Assets] e la cartella nidificata contenente una risorsa viene pubblicata in [!DNL Brand Portal], il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene pubblicata nuovamente.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata in Browser proprietà. Se si seleziona per configurare altri campi del modulo adattivo nello stesso editor, il problema viene risolto.

* Se la procedura guidata [!UICONTROL Configurazione risorse collegate] restituisce un messaggio di errore 404 dopo l&#39;installazione, reinstallare manualmente i pacchetti `cq-remotedam-client-ui-content` e `cq-remotedam-client-ui-components` utilizzando Gestione pacchetti.

* Durante l’installazione di Experience Manager 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * &quot;Quando l’integrazione di Adobe Target è configurata in Experience Manager utilizzando l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti di esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce quando si utilizzano funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner acquistabili.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro.

## Bundle OSGi e pacchetti di contenuti inclusi {#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.8.0:

* [Elenco dei bundle OSGi inclusi nell&#39;Experience Manager 6.5.8.0](assets/6580_bundles.txt)

* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.8.0](assets/6580_packages.txt)

## Siti web limitati {#restricted-sites}

Questi siti web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* Consulta [come contattare l&#39;Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Note sulla versione 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] pagina di prodotto](https://www.adobe.com/it/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Abbonati ad Adobe priority product update](https://www.adobe.com/subscription/priority-product-update.html)

