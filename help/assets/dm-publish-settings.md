---
title: Configurare Impostazione pubblicazione Dynamic Medie per il server immagini
description: Scopri come configurare Dynamic Medie Publish Setup per Image Server per pubblicare le risorse. Puoi anche verificare le risorse prima di renderle pubbliche.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: c86e79c4-e887-4ee3-bb54-eeffb34a33c2
source-git-commit: 7f8cfe155af3b8831e746ced89c11c971e429f69
workflow-type: tm+mt
source-wordcount: '3511'
ht-degree: 3%

---

# Configurare Impostazione pubblicazione Dynamic Medie per il server immagini

La configurazione di Dynamic Medie Publish Setup è disponibile solo se:

* Dynamic Medie è in esecuzione in modalità Scene7. Consulta [Abilita Dynamic Medie in modalità Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Hai un *esistente* **[!UICONTROL Configurazione Dynamic Medie]** (in **[!UICONTROL Cloud Services]**) in Adobe Experience Manager 6.5.11 o versioni successive. Consulta [Creare una configurazione Dynamic Medie in Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Sei un amministratore di Experience Manager con privilegi di amministratore.

Dynamic Medie Publish Setup è destinato all&#39;utilizzo da parte di sviluppatori e programmatori esperti di siti Web. Adobe Dynamic Medie consiglia agli utenti che modificano queste impostazioni di pubblicazione di avere familiarità con Adobe Dynamic Medie, gli standard e le convenzioni del protocollo HTTP e la tecnologia di imaging di base.

La pagina Impostazione pubblicazione di Dynamic Medie stabilisce le impostazioni predefinite che determinano il modo in cui le risorse vengono consegnate dai server Adobe Dynamic Medie ai siti web o alle applicazioni. Se non viene specificata alcuna impostazione, il server Adobe Dynamic Medie distribuisce una risorsa in base a un’impostazione predefinita configurata nella pagina Impostazione pubblicazione Dynamic Medie.

Vedi anche [Facoltativo - Impostazione e configurazione di Dynamic Medie - Impostazioni modalità Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) per altre attività di configurazione facoltative.

>[!NOTE]
>
>Eseguire l’aggiornamento da Dynamic Media Classic a Dynamic Medie su Adobe Experience Manager? Il [Impostazioni generali](/help/assets/dm-general-settings.md) Le pagine Configurazione pubblicazione e Configurazione della pagina in Dynamic Medie sono precompilate con i valori presi dal tuo account Dynamic Media Classic. Le eccezioni sono tutti i valori elencati in **[!UICONTROL Opzioni di caricamento predefinite]** nella pagina Impostazioni generali. Questi valori sono già in Experience Manager. Di conseguenza, qualsiasi modifica apportata in **[!UICONTROL Opzioni di caricamento predefinite]**, in una qualsiasi delle cinque schede, tramite l’interfaccia utente di Experience Manager, si riflette in Dynamic Medie, non in Dynamic Media Classic. Tutte le altre impostazioni e i valori in [Impostazioni generali](/help/assets/dm-general-settings.md) e la pagina Publish Setup (Impostazione pubblicazione) sono gestite tra Dynamic Media Classic e Dynamic Medie in Experience Manager.

**Per configurare il server immagini dell&#39;installazione di Dynamic Medie Publish:**

1. In modalità Autore Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale.
1. Nella barra a sinistra, seleziona l’icona Strumenti, quindi vai a **[!UICONTROL Risorse]** > **[!UICONTROL Impostazione pubblicazione Dynamic Medie]**.
1. Nella pagina Server immagini, imposta il contesto Server immagini - pubblicazione, quindi utilizza le cinque schede per configurare le impostazioni di pubblicazione predefinite.

   * [Server immagini](#image-server)
   * [Sicurezza](#security-tab) scheda
   * [Gestione catalogo](#catalog-management-tab) scheda
   * [Attributi della richiesta](#request-attributes-tab) scheda
   * [Attributi miniatura comuni](#common-thumbnail-attributes-tab) scheda
   * [Attributi gestione colore](#color-management-attributes-tab) scheda

   ![Pagina Impostazione pubblicazione Dynamic Medie](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Medie Publish Setup, con **[!UICONTROL Attributi della richiesta]**scheda selezionata.*<br><br>

1. Al termine, vicino all’angolo superiore destro della pagina, seleziona **[!UICONTROL Salva]**.

## Server immagini {#image-server}

La pagina Server immagini stabilisce le impostazioni predefinite per la consegna delle immagini dai server immagini. Le impostazioni sono disponibili in cinque categorie

| Contesto di pubblicazione | Descrizione |
| --- | --- |
| Image Server | Specifica il contesto per le impostazioni di pubblicazione. |
| Image Server test | Specifica il contesto per la verifica delle impostazioni di pubblicazione.<br>Solo per i nuovi account Dynamic Medie, il valore predefinito **[!UICONTROL Indirizzo client]** è impostato su `127.0.0.1` automaticamente.<br>Consulta [Testare le risorse prima di renderle pubbliche](#test-assets-before-making-public). |

### Scheda Sicurezza {#security-tab}

**[!UICONTROL Indirizzo client]** : consente di specificare uno o più indirizzi IP o intervalli di indirizzi IP. Se specificato, le richieste a questo catalogo immagini generate da un client non presente nell&#39;elenco degli indirizzi IP vengono rifiutate. Questa regola si applica sia alla consegna di immagini che a quelle di cui è stato eseguito il rendering.

![Scheda Sicurezza ](/help/assets/assets-dm/dm-ipallowlist.png)<br>*Scheda Sicurezza che mostra il campo IP &quot;allow&quot; (Consenti).*

### Scheda Gestione catalogo {#catalog-management-tab}

**[!UICONTROL Percorso file definizione set regole]** - Specifica il file contenente le definizioni del set di regole per il catalogo immagini.

Vedi anche [FileSetRegole](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie.

>[!NOTE]
>
>Se il tuo account Dynamic Media Classic dispone già di un **[!UICONTROL Percorso file definizione set regole]** selezionato (come impostato in **[!UICONTROL Configurazione]** > **[!UICONTROL Applicazione]** > **[!UICONTROL Impostazione pubblicazione]**, in **[!UICONTROL Gestione catalogo]** ), il tuo account Dynamic Medie su Experience Manager recupera il file da Dynamic Media Classic. Il file viene quindi archiviato e reso disponibile in questo campo, quando si apre il file **[!UICONTROL Impostazione pubblicazione Dynamic Medie]** per la prima volta.

### Scheda Attributi della richiesta {#request-attributes-tab}

Queste impostazioni si riferiscono all&#39;aspetto predefinito delle immagini.

| Impostazione | Descrizione |
| --- | --- |
| **[!UICONTROL Limite dimensioni immagine di risposta]** | Obbligatorio.<br>Solo per i nuovi account Dynamic Medie, il limite di dimensione predefinito viene impostato automaticamente su Larghezza: `3000` e Altezza: `3000` per entrambi **[!UICONTROL Image Server]** e **[!UICONTROL Image Server di prova]**.<br>Specifica la larghezza e l&#39;altezza massima dell&#39;immagine di risposta restituita al client. Il server restituisce un errore se una richiesta causa un’immagine di risposta con larghezza, altezza o entrambi i valori maggiori di questa impostazione.<br>Vedi anche [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Modalità di offuscamento richiesta]** | Attiva se desideri applicare la codifica base64 alle richieste valide.<br>Vedi anche [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Modalità di blocco richieste]** | Attiva se desideri includere un blocco hash semplice nelle richieste.<br>Vedi anche [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Attributi richiesta predefiniti]** | |
| **[!UICONTROL Suffisso file immagine predefinito]** | Obbligatorio.<br>Estensione predefinita del file di dati che viene aggiunta ai valori dei campi Percorso e Percorso maschera del catalogo se il percorso non include un suffisso di file.<br>Vedi anche [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Nome tipo di font predefinito]** | Specifica quale font utilizzare se non viene fornito alcun font in una richiesta di livello di testo. Se specificato, deve corrispondere a un valore valido per il nome del carattere nella mappa dei caratteri di questo catalogo immagini o nella mappa dei caratteri del catalogo predefinito.<br>Vedi anche [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Immagine predefinita]** | Specifica un&#39;immagine predefinita da restituire in risposta a una richiesta che fa riferimento a un&#39;immagine non trovata.<br>Vedi anche [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie.<br>**NOTA**: se il tuo account Dynamic Media Classic dispone già di un **[!UICONTROL Immagine predefinita]** selezionato (come impostato in **[!UICONTROL Configurazione]** > **[!UICONTROL Applicazione]** > **[!UICONTROL Impostazione pubblicazione]**, in **[!UICONTROL Attributi di richiesta predefiniti]** ), il tuo account Dynamic Medie su Experience Manager recupera il file da Dynamic Media Classic. Il file viene quindi archiviato e reso disponibile in questo campo quando apri il file **[!UICONTROL Impostazione pubblicazione Dynamic Medie]** per la prima volta. |
| **[!UICONTROL Modalità immagine predefinita]** | Quando la casella del dispositivo di scorrimento è attivata (dispositivo di scorrimento a destra), **[!UICONTROL Immagine predefinita]** sostituisce ogni livello mancante nell&#39;immagine sorgente con l&#39;immagine predefinita e restituisce il composito come di consueto. Quando la casella del cursore è disattivata (cursore a sinistra), l&#39;immagine predefinita sostituisce l&#39;intera immagine composita, anche se l&#39;immagine mancante è solo uno dei vari livelli.<br>Vedi anche [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Dimensioni vista predefinite]** | Obbligatorio.<br>Solo per i nuovi account Dynamic Medie, la dimensione di visualizzazione predefinita viene impostata automaticamente su Larghezza: `1280` e Altezza: `1280` per entrambi **[!UICONTROL Image Server]** e **[!UICONTROL Image Server di prova]**.<br>Il server vincola le dimensioni delle immagini di risposta ai valori di larghezza e altezza specificati, se nella richiesta non sono specificate esplicitamente le dimensioni di visualizzazione tramite `wid=`, `hei=`, o `scl=`.<br>Vedi anche [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Dimensioni miniatura predefinite]** | Obbligatorio.<br>Utilizzato al posto dell&#39;attributo **[!UICONTROL Dimensioni di visualizzazione predefinite]** per richieste di miniature (`req=tmb`). Se viene richiesta una miniatura, il server vincola le dimensioni delle immagini di risposta ai valori di larghezza e altezza specificati`req=tmb`) non specifica esplicitamente la dimensione utilizzando `wid=`, `hei=`, o `scl=`.<br>Vedi anche [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Colore di sfondo predefinito]** | Specifica il valore RGB utilizzato per riempire qualsiasi area di un&#39;immagine di risposta che non contiene dati immagine effettivi.<br>Vedi anche [ColoreBkg](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Attributi di codifica JPEG]** |  |
| **[!UICONTROL Qualità]** | <br>Specifica gli attributi predefiniti per le immagini di risposta di JPEG.<br>Solo per i nuovi account Dynamic Medie, il **[!UICONTROL Qualità]** il valore predefinito è impostato automaticamente su `80` per entrambi **[!UICONTROL Image Server]** e **[!UICONTROL Image Server di prova]**.<br>Questo campo è definito in un intervallo compreso tra 1 e 100.<br>Vedi anche [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Downsampling cromaticità]** | Attiva o disattiva il downsampling cromatico utilizzato dai codificatori JPEG. |
| **[!UICONTROL Metodo di ricampionamento predefinito]** | Specifica gli attributi di ricampionamento e interpolazione predefiniti da utilizzare per il ridimensionamento dei dati immagine. Usa quando `resMode` non è specificato in una richiesta.<br>Solo per i nuovi account Dynamic Medie, la modalità di ricampionamento predefinita è impostata automaticamente su `Sharp2` per entrambi **[!UICONTROL Image Server]** e **[!UICONTROL Image Server di prova]**.<br>Vedi anche [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |

### Scheda Attributi miniatura comuni {#common-thumbnail-attributes-tab}

Queste impostazioni si riferiscono all&#39;aspetto e all&#39;allineamento predefiniti delle miniature.

| Impostazione | Descrizione |
| --- | --- |
| **[!UICONTROL Colore di sfondo predefinito per miniature]** | Specifica il valore RGB utilizzato per riempire l&#39;area di un&#39;immagine miniatura di output che non contiene dati immagine effettivi. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo miniature predefinito]** è impostato su **[!UICONTROL Adatta]** o **[!UICONTROL Texture]**.<br>Vedi anche [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Allineamento orizzontale]** | Specifica l&#39;allineamento orizzontale della miniatura nel rettangolo dell&#39;immagine di risposta specificato da `wid=` e `hei=` valori.<br>Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo miniature predefinito]** è impostato su **[!UICONTROL Adatta]**.<br>È possibile scegliere tra tre allineamenti orizzontali: **[!UICONTROL Allineamento al centro]**, **[!UICONTROL Allineamento a sinistra]**, e **[!UICONTROL Allineamento a destra]**.<br>Vedi anche [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Allineamento verticale]** | Specifica l&#39;allineamento verticale dell&#39;immagine miniatura nel rettangolo dell&#39;immagine di risposta specificato da `wid=` e `hei=` valori. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo miniature predefinito]** è impostato su **[!UICONTROL Adatta]**.<br>È possibile scegliere tra tre allineamenti verticali: **[!UICONTROL Allineamento in alto]**, **[!UICONTROL Allineamento al centro]**, e **[!UICONTROL Allineamento in basso]**.<br>Vedi anche [AllineamentoVertPollice](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Durata predefinita cache]** | Specifica un intervallo di scadenza predefinito, in ore, se un determinato record catalogo non contiene un valore Expiration valido per il catalogo. Imposta su `-1` per contrassegnare come senza scadenza. <br>Vedi anche [Scade](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Tipo miniature predefinito]** | Specifica un valore predefinito per il tipo di miniatura se un record catalogo non contiene un valore ThumbType valido per il catalogo. Utilizzato solo per le richieste di miniature (`req=tmb`).<br>È possibile scegliere tra tre tipi di miniature: **[!UICONTROL Ritaglio]**, **[!UICONTROL Adatta]**, e **[!UICONTROL Texture]**.<br>Vedi anche [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Risoluzione miniature predefinita]** | Specifica un valore predefinito per la risoluzione degli oggetti miniatura se un record catalogo non contiene un valore ThumbRes valido per il catalogo. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo miniature predefinito]** è impostato su **[!UICONTROL Texture]**.<br>Vedi anche [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |

### Scheda Attributi gestione colore {#color-management-attributes-tab}

Queste impostazioni determinano i profili colore ICC utilizzati per le immagini.

**Intento di rendering della conversione colore**
Un intento di rendering di conversione colore consente di ignorare l’intento di rendering predefinito dei profili di lavoro per determinare come vengono regolati i colori sorgente. Utilizzato quando:

1. Uno dei profili ICC predefiniti è lo spazio colore di destinazione di una conversione colore.
1. Un dispositivo di output (stampante o monitor) è caratterizzato da questo profilo.
1. L&#39;intento di rendering specificato è valido per questo profilo.

Intenti di rendering diversi utilizzano regole diverse per determinare come vengono regolati i colori di origine.

Vedi anche [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie.

>[!NOTE]
>
>In generale, è consigliabile utilizzare l’intento di rendering predefinito per l’impostazione di colore selezionata, che è stato testato da Adobe per soddisfare gli standard di settore. Ad esempio, se scegliete un&#39;impostazione di colore per il Nord America o l&#39;Europa, l&#39;intento di rendering predefinito per la conversione colore è **[!UICONTROL Colorimetrico relativo]**. Se scegliete un&#39;impostazione colore per il Giappone, l&#39;intento di rendering predefinito per la conversione colore è **[!UICONTROL Percettivo]**.

| Impostazione | Caratteristiche |
| --- | --- |
| **[!UICONTROL Spazio colore predefinito CMYK]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per dati CMYK. Se **[!UICONTROL Nessuno specificato]** è selezionata, la gestione del colore è disabilitata per questo catalogo immagini quando sono coinvolte immagini sorgente CMYK. Tutti gli spazi di lavoro CMYK sono dipendenti dal dispositivo, il che significa che si basano sulle effettive combinazioni di inchiostro e carta. Gli Adobi CMYK sono forniti in base alle condizioni standard di stampa commerciale.<br> Vedi anche [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Spazio colore predefinito scala di grigi]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per dati in scala di grigio. Se **[!UICONTROL Nessuno specificato]** è selezionata, la gestione del colore è disabilitata per questo catalogo immagini quando sono coinvolte immagini sorgente in scala di grigio.<br>Vedi anche [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Spazio colore predefinito RGB]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per dati RGB. Se **[!UICONTROL Nessuno specificato]** è selezionata, la gestione del colore è disabilitata per questo catalogo immagini quando sono coinvolte immagini di sorgenti RGB. In generale, è meglio scegliere **[!UICONTROL Adobe RGB]** o **[!UICONTROL sRGB]**, anziché il profilo per un dispositivo specifico (ad esempio un profilo monitor). **[!UICONTROL sRGB]** è consigliato quando si preparano immagini per il Web o per dispositivi mobili, in quanto definisce lo spazio colore del monitor standard utilizzato per visualizzare le immagini sul Web. **[!UICONTROL sRGB]** è anche una buona scelta quando si lavora con immagini provenienti da fotocamere digitali di livello consumer, perché la maggior parte di queste fotocamere utilizzano sRGB come spazio colore predefinito.<br>Vedi anche [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie. |
| **[!UICONTROL Intento di rendering per conversione colore]** | **[!UICONTROL Percettivo]** - Mira a preservare la relazione visiva tra i colori in modo che vengano percepiti come naturali per l&#39;occhio umano, anche se i valori di colore stessi possono cambiare. Questo intento è adatto per le immagini fotografiche con molti colori fuori gamma. Questa impostazione rappresenta l&#39;intento di rendering standard per il settore della stampa giapponese. |
|  | **[!UICONTROL Colorimetrico relativo]** - Confronta l&#39;evidenziazione estrema dello spazio colore di origine con quella dello spazio colore di destinazione e sposta tutti i colori di conseguenza. I colori fuori gamma vengono spostati sul colore riproducibile più simile nello spazio colore di destinazione. La colorimetrica relativa conserva più colori originali in un&#39;immagine rispetto alla percezione. Questa impostazione rappresenta l&#39;intento di rendering standard per la stampa in Nord America ed Europa. |
|  | **[!UICONTROL Saturazione]** - Tenta di produrre colori vividi in un&#39;immagine a scapito della precisione dei colori. Questo intento di rendering è adatto a elementi grafici aziendali come grafici o grafici, in cui i colori saturi brillanti sono più importanti della relazione esatta tra i colori. |
|  | **[!UICONTROL Colorimetrico assoluto]** - Lascia invariati i colori che rientrano nella gamma di destinazione. I colori fuori gamma vengono ritagliati. Non viene eseguita alcuna modifica in scala dei colori in base al punto bianco di destinazione. Questo intento mira a mantenere la precisione del colore a scapito della conservazione delle relazioni tra i colori ed è adatto per le prove per simulare l&#39;output di un particolare dispositivo. Questo intento è utile per visualizzare in anteprima come il colore della carta influisce sui colori stampati. |

## Testare le risorse prima di renderle pubbliche {#test-assets-before-making-public}

Il testing sicuro consente di definire un ambiente di test sicuro e di creare una soluzione business-to-business affidabile, basata su un set configurabile di intervalli e indirizzi IP. Questa funzionalità consente di abbinare le implementazioni Dynamic Medie di Adobe all’architettura del sistema di gestione dei contenuti e del sistema aziendale.

Con Test protetti, puoi visualizzare in anteprima la versione di staging del sito web con contenuto non pubblicato.

Se lo desideri, crea un ambiente di staging anziché rendere le risorse disponibili al pubblico per i seguenti motivi:

* Visualizza l&#39;anteprima dei siti Web prima del lancio pubblico (sito Web di staging).
* Distribuisci le risorse che richiedono un accesso limitato, ad esempio gli eCatalog che mostrano i prezzi in un’applicazione web B2B.
* Utilizza le risorse dietro un firewall come parte del sistema di gestione delle informazioni sui prodotti, dell’applicazione di assistenza clienti, del sito di formazione e così via.

>[!NOTE]
>
>Il test protetto non influisce sull’accesso a Adobe Dynamic Media Classic. La sicurezza di Adobe Dynamic Media Classic rimane coerente e richiede le credenziali abituali per l’accesso a Adobe Dynamic Media Classic e ai servizi web correlati.

### Come funziona il test protetto {#how-test-assets-works}

La maggior parte delle aziende gestisce Internet con un firewall. L’accesso a Internet è possibile attraverso determinate vie e, in genere, attraverso un numero limitato di indirizzi IP pubblici.

Dalla tua rete aziendale, puoi individuare il tuo indirizzo IP pubblico utilizzando siti web come [https://www.whatismyip.com](https://www.whatismyip.com/) o richiedere queste informazioni all&#39;organizzazione IT aziendale.

Con Secure Testing, Adobe Dynamic Medie stabilisce un server immagini dedicato per gli ambienti di staging o le applicazioni interne. Qualsiasi richiesta inviata a questo server controlla l’indirizzo IP di origine. Se la richiesta in ingresso non si trova nell’elenco approvato di indirizzi IP, viene restituita una risposta di errore. L’amministratore aziendale di Dynamic Medie Adobe configura l’elenco approvato di indirizzi IP per l’ambiente di test protetto della propria azienda.

Poiché la posizione della richiesta originale deve essere confermata, il traffico del servizio di test protetto non viene instradato attraverso una rete di distribuzione del contenuto come il traffico pubblico del server immagini di Dynamic Medie. Le richieste al servizio di test sicuro hanno una latenza leggermente superiore rispetto ai server immagini Dynamic Medie pubblici.

Le risorse non pubblicate sono immediatamente disponibili dai servizi di test protetto, senza dover essere pubblicate. In questo modo, puoi eseguire un’anteprima prima che le risorse vengano pubblicate sul loro server immagini rivolto al pubblico.

>[!NOTE]
>
>I servizi di test sicuri utilizzano il server di catalogo configurato con un contesto di pubblicazione interno. Pertanto, se l’azienda è configurata per la pubblicazione su Secure Testing, tutte le risorse caricate in Adobe Dynamic Medie diventano immediatamente disponibili sui servizi di Secure Testing. Questa funzionalità è true indipendentemente dal fatto che le risorse siano contrassegnate per la pubblicazione al caricamento.

I servizi di test sicuro supportano attualmente i seguenti tipi di risorse e funzionalità:

* Immagini.
* Vignette (richieste del server di rendering).
* Richieste di rendering del server (supportate, ma che devono essere richieste esplicitamente dal cliente).
* Set, inclusi set di immagini, eCatalog, set di rendering e set di file multimediali.
* Visualizzatori rich media Dynamic Medie di Adobe standard.
* Adobe di pagine JSP Dynamic Medie OnDemand.
* Contenuto statico, ad esempio file PDF e video distribuiti progressivamente.
* Streaming video HTTP.
* Streaming video progressivo.

I seguenti tipi di risorse e funzionalità non sono attualmente supportati:

* Ricerca in Adobe Dynamic Media Classic Info o eCatalog
* Streaming video RTMP
* Da web a stampa
* Servizi UGC (User-Generated Content)

  >[!IMPORTANT]
  >
  >A partire dal 1° maggio 2023, le risorse UGC in Dynamic Medie saranno disponibili per l’uso fino a 60 giorni dalla data di caricamento. Dopo 60 giorni, le risorse verranno rimosse.

  >[!NOTE]
  >
  >Il supporto per risorse di immagini vettoriali UGC nuove o esistenti in Adobe Dynamic Medie è terminato il 30 settembre 2021.

### Test del servizio di test protetto {#test-secure-testing-service}

Per garantire che il servizio di test protetto funzioni come previsto, eseguire le operazioni seguenti:

#### Prepara l’account

1. Contatta l’Assistenza clienti Adobe e richiedi l’abilitazione di Secure Testing sul tuo account.
1. In Adobe Experience Manager, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Impostazione pubblicazione Dynamic Medie]**.
1. Nella pagina Image Server, in **[!UICONTROL Contesto di pubblicazione]** elenco a discesa, seleziona **[!UICONTROL Image Server di prova]**.
1. Seleziona la **[!UICONTROL Sicurezza]** scheda.
1. Per **[!UICONTROL Indirizzo client]** filtro, seleziona **[!UICONTROL Aggiungi]**.
1. In **[!UICONTROL Indirizzo IP]** digitare un indirizzo IP.
1. In **[!UICONTROL Maschera]** digitare una maschera di rete.

   >[!NOTE]
   >
   >Se aggiungi più di un indirizzo IP e una maschera di rete, consente *tutto* Gli indirizzi IP per effettuare chiamate alle risorse vengono visualizzati tutti.

1. Effettua una delle operazioni seguenti:

   * Per aggiungere altri indirizzi IP, ripeti i tre passaggi precedenti.
   * Procedi al passaggio successivo.

1. Nell&#39;angolo superiore destro della pagina Image Server, seleziona **[!UICONTROL Salva]**.
1. Carica le immagini desiderate sul tuo account Dynamic Medie Adobe.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Assicurati che alcune delle immagini siano contrassegnate per la pubblicazione e altre non siano contrassegnate, quindi invia il processo di pubblicazione.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Per determinare il nome del servizio di test protetto, vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Impostazione generale di Dynamic Medie]**.
1. Il giorno **[!UICONTROL Server]** , trovare il nome del server a destra di **[!UICONTROL Nome server pubblicato]**.

Se manca il nome del server o se l’URL del server non funziona, contatta l’Adobe di assistenza.

#### Prepara varianti di sito web

Sono necessarie due varianti di un sito web che collega le risorse pubblicate e non pubblicate:

* Versione pubblica - Collega le risorse utilizzando la sintassi URL Dynamic Medie di Adobe tradizionale.
* Versione di staging - Collega le risorse utilizzando la stessa sintassi ma con il nome del sito di test protetto.

#### Eseguire i test

Eseguire i test seguenti:

1. Verifica se le risorse sono visibili dalla rete aziendale.

   All’interno della rete aziendale identificata dall’intervallo di indirizzi IP definito in precedenza, nella versione di staging del sito web vengono visualizzate tutte le immagini, contrassegnate per la pubblicazione o meno. Di conseguenza, è possibile eseguire il test senza rendere accidentalmente disponibili le immagini prima dell’approvazione in anteprima o del lancio del prodotto.

   Verifica che la versione pubblica del sito mostri le risorse pubblicate come precedentemente fatto con Adobe Dynamic Medie.

1. Dall’esterno della rete aziendale, verifica che le risorse non pubblicate (ossia, non contrassegnate per la pubblicazione) siano protette dall’accesso di terze parti.

   Accedi alla rete dall’esterno (ad esempio dal computer di casa o tramite una connessione 4G/5G), quindi verifica che nella versione pubblica del sito siano visualizzate tutte le risorse pubblicate ma nessun contenuto non pubblicato.

   Conferma che la versione di staging non mostri alcuna risorsa perché stai accedendo al servizio di test protetto da un indirizzo IP non approvato.
