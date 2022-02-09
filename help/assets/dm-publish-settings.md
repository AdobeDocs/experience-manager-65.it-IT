---
title: Configurare l’impostazione di pubblicazione Dynamic Media per il server immagini
description: Scopri come configurare la pubblicazione in Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: c86e79c4-e887-4ee3-bb54-eeffb34a33c2
source-git-commit: 8561eb8b4b5164188ebf387c8f0344b462b830ec
workflow-type: tm+mt
source-wordcount: '3467'
ht-degree: 3%

---

# Configurare l’impostazione di pubblicazione Dynamic Media per il server immagini

La configurazione di Dynamic Media Publish Setup è disponibile solo se:

* Stai eseguendo Dynamic Media in modalità Scene7. Vedi [Abilitare Dynamic Media in modalità Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Hai un *esistente* **[!UICONTROL Configurazione Dynamic Media]** in **[!UICONTROL Cloud Services]**) in Adobe Experience Manager 6.5.11 o versione successiva. Vedi [Creare una configurazione Dynamic Media nei Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Sei un amministratore di sistema di Experience Manager con privilegi di amministratore.

Dynamic Media Publish Setup è destinato all&#39;utilizzo da parte di sviluppatori e programmatori di siti web esperti. Adobe Dynamic Media consiglia agli utenti che modificano queste impostazioni di pubblicazione di avere familiarità con Dynamic Media di Adobe, gli standard e le convenzioni del protocollo HTTP e la tecnologia di imaging di base.

La pagina Configurazione pubblicazione di Dynamic Media stabilisce le impostazioni predefinite che determinano come le risorse vengono distribuite dai server Dynamic Media di Adobe ai siti web o alle applicazioni. Se non viene specificata alcuna impostazione, il server Adobe Dynamic Media distribuisce una risorsa in base a un’impostazione predefinita configurata nella pagina Configurazione pubblicazione Dynamic Media.

Vedi anche [Facoltativo - Configurazione e configurazione di Dynamic Media - Impostazioni della modalità Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) per ulteriori attività di configurazione opzionali.

>[!NOTE]
>
>Aggiornamento da Dynamic Media Classic a Dynamic Media su Adobe Experience Manager? La [Impostazioni generali](/help/assets/dm-general-settings.md) La pagina e la pagina Configurazione pubblicazione in Dynamic Media sono precompilate con i valori presi dal tuo account Dynamic Media Classic. Le eccezioni sono tutti i valori elencati in **[!UICONTROL Opzioni di caricamento predefinite]** Area della pagina Impostazioni generali. Questi valori sono già in Experience Manager. Di conseguenza, eventuali modifiche apportate in **[!UICONTROL Opzioni di caricamento predefinite]**, in una qualsiasi delle cinque schede, tramite l’interfaccia utente di Experience Manager, si riflette in Dynamic Media, non in Dynamic Media Classic. Tutte le altre impostazioni e valori nel [Impostazioni generali](/help/assets/dm-general-settings.md) La pagina e la pagina Pubblica configurazione vengono mantenute ad Experience Manager tra Dynamic Media Classic e Dynamic Media.

**Per configurare Dynamic Media Publish Setup Image Server:**

1. In modalità Creazione Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale.
1. Nella barra a sinistra, seleziona l’icona Strumenti , quindi vai a **[!UICONTROL Risorse]** > **[!UICONTROL Installazione di Dynamic Media Publish]**.
1. Nella pagina Image Server , imposta il contesto Image Server - Publish e quindi utilizza le cinque schede per configurare le impostazioni di pubblicazione predefinite.

   * [Server immagini](#image-server)
   * [Sicurezza](#security-tab) scheda
   * [Gestione catalogo](#catalog-management-tab) scheda
   * [Attributi della richiesta](#request-attributes-tab) scheda
   * [Attributi comuni delle miniature](#common-thumbnail-attributes-tab) scheda
   * [Attributi di gestione del colore](#color-management-attributes-tab) scheda

   ![Pagina di installazione di Dynamic Media Publish](/help/assets/assets-dm/dm-publish-setup.png)
   *Pagina di installazione di Dynamic Media Publish, con **[!UICONTROL Attributi della richiesta]**scheda selezionata.*<br><br>

1. Al termine, seleziona **[!UICONTROL Salva]**.

## Server immagini {#image-server}

La pagina Image Server stabilisce le impostazioni predefinite per la distribuzione delle immagini dai server di immagini. Le impostazioni sono disponibili in cinque categorie

| Contesto di pubblicazione | Descrizione |
| --- | --- |
| Image Server | Specifica il contesto per le impostazioni di pubblicazione. |
| Image Server test | Specifica il contesto in cui verificare le impostazioni di pubblicazione.<br>Solo per i nuovi account Dynamic Media, l&#39;impostazione predefinita **[!UICONTROL Indirizzo client]** campo impostato su `127.0.0.1` automaticamente.<br>Vedi [Verificare le risorse prima di renderle pubbliche](#test-assets-before-making-public). |

### Scheda Sicurezza {#security-tab}

**[!UICONTROL Indirizzo client]** - Consente di specificare uno o più indirizzi IP o intervalli di indirizzi IP. Se specificato, le richieste a questo catalogo immagini provenienti da un client con un indirizzo IP non elencato vengono rifiutate. Questa regola si applica sia alla distribuzione di immagini che di immagini renderizzate.

![Scheda Sicurezza ](/help/assets/assets-dm/dm-ipallowlist.png)<br>*Scheda Sicurezza che mostra il campo &quot;allow&quot; IP.*

### Scheda Gestione catalogo {#catalog-management-tab}

**[!UICONTROL Percorso del file di definizione del set di regole]** - Specifica il file che contiene le definizioni dei set di regole per il catalogo immagini.

Vedi anche [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) nella Guida di riferimento visualizzatori di Dynamic Media.

>[!NOTE]
>
>Se il tuo account Dynamic Media Classic ha già un **[!UICONTROL Percorso del file di definizione del set di regole]** selezionato (come impostato in **[!UICONTROL Configurazione]** > **[!UICONTROL Applicazione]** > **[!UICONTROL Impostazione di pubblicazione]**, **[!UICONTROL Gestione catalogo]** gruppo), il tuo account Dynamic Media su Experience Manager recupera il file da Dynamic Media Classic. Il file viene quindi memorizzato e reso disponibile in questo campo quando si apre il **[!UICONTROL Installazione di Dynamic Media Publish]** per la prima volta.

### Scheda Attributi richiesta {#request-attributes-tab}

Queste impostazioni riguardano l&#39;aspetto predefinito delle immagini.

| Impostazione | Descrizione |
| --- | --- |
| **[!UICONTROL Limite dimensioni immagine di risposta]** | Obbligatorio.<br>Solo per i nuovi account Dynamic Media, il limite di dimensione predefinito viene impostato automaticamente su Larghezza: `3000` e altezza: `3000` per entrambi **[!UICONTROL Image Serving]** e **[!UICONTROL Test Image Serving]**.<br>Specifica la larghezza e l&#39;altezza massime dell&#39;immagine di risposta restituite al client. Il server restituisce un errore se una richiesta causa un&#39;immagine di risposta la cui larghezza, altezza o entrambi sono maggiori di questa impostazione.<br>Vedi anche [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Modalità di offuscamento richiesta]** | Abilita questa opzione se desideri applicare la codifica base64 alle richieste valide.<br>Vedi anche [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Modalità di blocco richieste]** | Abilita se desideri un semplice blocco hash incluso nelle richieste.<br>Vedi anche [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Attributi richiesta predefiniti]** |  |
| **[!UICONTROL Suffisso file immagine predefinito]** | Obbligatorio.<br>Estensione predefinita del file di dati aggiunta ai valori dei campi Percorso e MaskPath del catalogo se il percorso non include un suffisso di file.<br>Vedi anche [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Nome tipo di font predefinito]** | Specifica quale font viene utilizzato se una richiesta di livello di testo non fornisce alcun font. Se specificato, deve essere un valore valido per il nome del font nella mappa dei font di questo catalogo di immagini o nella mappa dei font del catalogo predefinito.<br>Vedi anche [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Immagine predefinita]** | Fornisce un&#39;immagine predefinita da restituire in risposta a una richiesta in cui l&#39;immagine richiesta non viene trovata.<br>Vedi anche [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) nella Guida di riferimento visualizzatori di Dynamic Media.<br>**NOTA**: Se il tuo account Dynamic Media Classic ha già un **[!UICONTROL Immagine predefinita]** selezionato (come impostato in **[!UICONTROL Configurazione]** > **[!UICONTROL Applicazione]** > **[!UICONTROL Impostazione di pubblicazione]**, **[!UICONTROL Attributi di richiesta predefiniti]** gruppo), il tuo account Dynamic Media su Experience Manager recupera il file da Dynamic Media Classic. Il file viene quindi memorizzato e reso disponibile in questo campo quando si apre il **[!UICONTROL Installazione di Dynamic Media Publish]** per la prima volta. |
| **[!UICONTROL Modalità immagine predefinita]** | Quando la casella di scorrimento è attivata (cursore a destra), la **[!UICONTROL Immagine predefinita]** sostituisce ogni livello mancante nell&#39;immagine sorgente con l&#39;immagine predefinita e restituisce il composito come di consueto. Quando la casella di scorrimento è disattivata (cursore a sinistra), l&#39;immagine predefinita sostituisce l&#39;intera immagine composita, anche se l&#39;immagine mancante è solo uno dei vari livelli.<br>Vedi anche [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Dimensioni vista predefinite]** | Obbligatorio.<br>Solo per i nuovi account Dynamic Media, la dimensione predefinita della visualizzazione viene impostata automaticamente su Larghezza: `1280` e altezza: `1280` per entrambi **[!UICONTROL Image Serving]** e **[!UICONTROL Test Image Serving]**.<br>Il server vincola le immagini di risposta a non superare questa larghezza e altezza, se la richiesta non specifica esplicitamente la dimensione di visualizzazione utilizzando `wid=`, `hei=`oppure `scl=`.<br>Vedi anche [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Dimensioni miniatura predefinite]** | Obbligatorio.<br>Utilizzato al posto dell&#39;attributo **[!UICONTROL Dimensione predefinita della visualizzazione]** per le richieste miniature (`req=tmb`). Il server vincola le immagini di risposta a una dimensione non superiore a questa larghezza e altezza, se viene richiesta una miniatura (`req=tmb`) non specifica esplicitamente la dimensione utilizzando `wid=`, `hei=`oppure `scl=`.<br>Vedi anche [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Colore di sfondo predefinito]** | Specifica il valore RGB utilizzato per compilare un&#39;area qualsiasi di un&#39;immagine di risposta che non contiene dati immagine effettivi.<br>Vedi anche [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Attributi di codifica JPEG]** |  |
| **[!UICONTROL Qualità]** | <br>Specifica gli attributi predefiniti per le immagini di risposta di JPEG.<br>Solo per i nuovi account Dynamic Media, la variabile **[!UICONTROL Qualità]** il valore predefinito viene impostato automaticamente su `80` per entrambi **[!UICONTROL Image Serving]** e **[!UICONTROL Test Image Serving]**.<br>Questo campo è definito nell&#39;intervallo da 1 a 100.<br>Vedi anche [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Downsampling cromaticità]** | Attivare o disattivare il downsampling cromatico utilizzato dagli encoder JPEG. |
| **[!UICONTROL Metodo di ricampionamento predefinito]** | Specifica gli attributi di ricampionamento e interpolazione predefiniti da utilizzare per il ridimensionamento dei dati immagine. Usa quando `resMode` non è specificato in una richiesta.<br>Solo per i nuovi account Dynamic Media, la modalità di ricampionamento predefinita viene impostata automaticamente su `Sharp2` per entrambi **[!UICONTROL Image Serving]** e **[!UICONTROL Test Image Serving]**.<br>Vedi anche [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) nella Guida di riferimento visualizzatori di Dynamic Media. |

### Scheda Attributi comuni delle miniature {#common-thumbnail-attributes-tab}

Queste impostazioni riguardano l’aspetto e l’allineamento predefiniti delle immagini in miniatura.

| Impostazione | Descrizione |
| --- | --- |
| **[!UICONTROL Colore di sfondo predefinito per miniature]** | Specifica il valore RGB utilizzato per riempire l&#39;area di un&#39;immagine miniatura di output che non contiene dati immagine effettivi. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo di miniatura predefinito]** è impostato su **[!UICONTROL Adatta]** o **[!UICONTROL Texture]**.<br>Vedi anche [Colore pollice](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Allineamento orizzontale]** | Specifica l&#39;allineamento orizzontale dell&#39;immagine miniatura nel rettangolo dell&#39;immagine di risposta specificato da `wid=` e `hei=` valori.<br>Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo di miniatura predefinito]** è impostato su **[!UICONTROL Adatta]**.<br>Ci sono tre allineamenti orizzontali tra cui scegliere: **[!UICONTROL Allineamento al centro]**, **[!UICONTROL Allineamento a sinistra]** e **[!UICONTROL Allineamento a destra]**.<br>Vedi anche [AllineaOrizzontale](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Allineamento verticale]** | Specifica l&#39;allineamento verticale dell&#39;immagine miniatura nel rettangolo dell&#39;immagine di risposta specificato da `wid=` e `hei=` valori. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo di miniatura predefinito]** è impostato su **[!UICONTROL Adatta]**.<br>Ci sono tre allineamenti verticali tra cui scegliere: **[!UICONTROL Allineamento superiore]**, **[!UICONTROL Allineamento al centro]** e **[!UICONTROL Allineamento in basso]**.<br>Vedi anche [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Durata predefinita cache]** | Fornisce un intervallo di scadenza predefinito in ore nel caso in cui un particolare record di catalogo non contenga un valore di scadenza del catalogo valido. Imposta su `-1` da contrassegnare come non scaduto mai. <br>Vedi anche [Scadenza](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Tipo miniature predefinito]** | Fornisce un valore predefinito per il tipo di miniatura nel caso in cui un particolare record di catalogo non contenga un valore ThumbType del catalogo valido. Utilizzato solo per le richieste di miniature (`req=tmb`).<br>Sono disponibili tre tipi di miniature tra cui scegliere: **[!UICONTROL Ritaglio]**, **[!UICONTROL Adatta]** e **[!UICONTROL Texture]**.<br>Vedi anche [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Risoluzione miniature predefinita]** | Fornisce un valore predefinito per la risoluzione dell&#39;oggetto miniatura nel caso in cui un particolare record di catalogo non contenga un valore ThumbRes di catalogo valido. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo di miniatura predefinito]** è impostato su **[!UICONTROL Texture]**.<br>Vedi anche [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) nella Guida di riferimento visualizzatori di Dynamic Media. |

### Scheda Attributi di gestione del colore {#color-management-attributes-tab}

Queste impostazioni determinano quali profili di colore ICC vengono utilizzati per le immagini.

**Intento di rendering della conversione del colore**
Un intento di rendering della conversione del colore consente di ignorare l’intento di rendering predefinito dei profili di lavoro per determinare come vengono regolati i colori di origine. Utilizzato quando:

1. Uno dei profili ICC predefiniti è lo spazio colore di destinazione di una conversione del colore.
1. Una periferica di output (stampante o monitor) è caratterizzata da questo profilo.
1. Inoltre, l&#39;intento di rendering specificato è valido per questo profilo.

Tenti di rendering diversi utilizzano regole diverse per determinare come vengono regolati i colori di origine.

Vedi anche [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) nella Guida di riferimento visualizzatori di Dynamic Media.

>[!NOTE]
>
>In generale, è consigliabile utilizzare l’intento di rendering predefinito per l’impostazione colore selezionata, che è stata testata da Adobe per soddisfare gli standard di settore. Ad esempio, se scegli un’impostazione di colore per Nord America o Europa, l’intento predefinito di rendering della conversione del colore è **[!UICONTROL Colorimetrico relativo]**. Se scegli un’impostazione di colore per il Giappone, l’intento predefinito di rendering della conversione del colore è **[!UICONTROL Percettivo]**.

| Impostazione | Caratteristiche |
| --- | --- |
| **[!UICONTROL Spazio colore predefinito CMYK]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per i dati CMYK. Se **[!UICONTROL Nessuno specificato]** se si sceglie , la gestione del colore è disabilitata per questo catalogo di immagini quando sono coinvolte immagini sorgente CMYK. Tutti gli spazi di lavoro CMYK dipendono dal dispositivo, il che significa che sono basati su combinazioni effettive di inchiostro e carta. L&#39;Adobe degli spazi di lavoro CMYK si basa sulle condizioni di stampa commerciale standard.<br> Vedi anche [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Spazio colore predefinito scala di grigi]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per i dati in scala di grigi. Se **[!UICONTROL Nessuno specificato]** se si sceglie , la gestione del colore viene disabilitata per questo catalogo di immagini quando sono coinvolte immagini sorgente in scala di grigi.<br>Vedi anche [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Spazio colore predefinito RGB]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per i dati di RGB. Se **[!UICONTROL Nessuno specificato]** se si sceglie , la gestione del colore è disabilitata per questo catalogo di immagini quando sono interessate immagini di sorgenti RGB. In generale, è meglio scegliere **[!UICONTROL Adobe RGB]** o **[!UICONTROL sRGB]**, anziché il profilo di un dispositivo specifico (ad esempio un profilo di monitoraggio). **[!UICONTROL sRGB]** è consigliato quando si preparano le immagini per il web o i dispositivi mobili, in quanto definisce lo spazio colore del monitor standard utilizzato per visualizzare le immagini sul web. **[!UICONTROL sRGB]** è anche una buona scelta quando si lavora con immagini provenienti da fotocamere digitali consumer, perché la maggior parte di queste telecamere utilizza sRGB come spazio colore predefinito.<br>Vedi anche [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Intento di rendering per conversione colore]** | **[!UICONTROL Percettivo]** - Mira a preservare il rapporto visivo tra i colori in modo che sia percepito come naturale per l’occhio umano, anche se i valori dei colori stessi possono cambiare. Questo intento è adatto per immagini fotografiche con molti colori fuori gamma. Questa impostazione è l’intento di rendering standard per l’industria di stampa giapponese. |
|  | **[!UICONTROL Colorimetrico relativo]** - Confronta l&#39;estrema evidenziazione dello spazio colore sorgente a quello dello spazio colore di destinazione e sposta tutti i colori di conseguenza. I colori fuori gamma vengono spostati sul colore riproducibile più vicino nello spazio colore di destinazione. Colorimetrico relativo conserva più i colori originali in un&#39;immagine rispetto a Perceptual. Questa impostazione è l’intento di rendering standard per la stampa in Nord America ed Europa. |
|  | **[!UICONTROL Saturazione]** - Cerca di produrre colori vividi in un&#39;immagine a scapito della precisione del colore. Questo intento di rendering è adatto a elementi grafici aziendali come grafici o grafici, in cui i colori satura brillante sono più importanti della relazione esatta tra i colori. |
|  | **[!UICONTROL Colorimetrico assoluto]** - Lascia invariati i colori che rientrano nella gamma di destinazione. I colori fuori gamma vengono ritagliati. Non viene eseguita alcuna scala dei colori al punto bianco di destinazione. Questo intento mira a mantenere la precisione del colore a scapito della conservazione delle relazioni tra i colori ed è adatto per la correzione per simulare l&#39;output di un particolare dispositivo. Questo intento è utile per visualizzare in anteprima come il colore della carta influisce sui colori stampati. |

## Verificare le risorse prima di renderle pubbliche {#test-assets-before-making-public}

Il test protetto consente di definire un ambiente di test sicuro e di creare una solida soluzione business-to-business basata su un set configurabile di indirizzi IP e intervalli. Questa funzionalità ti consente di abbinare le distribuzioni Dynamic Media di Adobe all’architettura della gestione dei contenuti e del sistema aziendale.

Con Secure Testing è possibile visualizzare in anteprima la versione di staging del sito web con contenuto non pubblicato.

Se lo desideri, crea un ambiente di staging anziché rendere le risorse disponibili al pubblico per i seguenti motivi:

* Anteprima dei siti web prima del lancio pubblico (sito web di staging).
* Distribuisci risorse che richiedono accesso limitato, ad esempio eCatalog che mostrano i prezzi in un’applicazione web B2B.
* Utilizza le risorse dietro un firewall come parte del sistema di gestione delle informazioni sui prodotti, dell’applicazione per il servizio clienti, del sito di formazione e così via.

>[!NOTE]
>
>La verifica sicura non influisce sull’accesso a Adobe Dynamic Media Classic. La sicurezza Adobe Dynamic Media Classic rimane coerente e richiede le credenziali usuali per l’accesso a Adobe Dynamic Media Classic e ai servizi Web correlati.

### Come funziona il test sicuro {#how-test-assets-works}

La maggior parte delle aziende gestisce Internet dietro un firewall. L’accesso a Internet è possibile tramite determinati percorsi e in genere attraverso una gamma limitata di indirizzi IP pubblici.

Dalla tua rete aziendale, puoi capire il tuo indirizzo IP pubblico utilizzando siti web come [https://www.whatismyip.com](https://www.whatismyip.com/) oppure richiedi queste informazioni alla tua organizzazione IT aziendale.

Con Secure Testing, Adobe Dynamic Media stabilisce un server di immagini dedicato per gli ambienti di staging o le applicazioni interne. Qualsiasi richiesta a questo server controlla l&#39;indirizzo IP di origine. Se la richiesta in entrata non si trova nell’elenco di indirizzi IP approvato, viene restituita una risposta di errore. L’amministratore aziendale di Adobe Dynamic Media configura l’elenco approvato di indirizzi IP per l’ambiente Secure Testing della propria azienda.

Poiché la posizione della richiesta originale deve essere confermata, il traffico del servizio Secure Testing non viene instradato attraverso una rete di distribuzione del contenuto come il traffico pubblico di Dynamic Media Image Server. Le richieste al servizio Secure Testing hanno una latenza leggermente più elevata rispetto ai server immagini pubblici di Dynamic Media.

Le risorse non pubblicate sono immediatamente disponibili dai servizi Secure Testing, senza necessità di pubblicare. In questo modo, puoi eseguire un’anteprima prima che le risorse vengano pubblicate sul server di immagini rivolto al pubblico.

>[!NOTE]
>
>I servizi di verifica protetta utilizzano il server di catalogo configurato con un contesto di pubblicazione interno. Pertanto, se la tua azienda è configurata per la pubblicazione su Secure Testing, tutte le risorse caricate in Adobe Dynamic Media diventano immediatamente disponibili sui servizi Secure Testing. Questa funzionalità è valida anche se le risorse sono contrassegnate per la pubblicazione al momento del caricamento.

I servizi di verifica sicura supportano attualmente i seguenti tipi di risorse e funzionalità:

* Immagini.
* Vignette (richieste server di rendering).
* Richieste server di rendering (supportate, ma richieste esplicitamente dal cliente).
* Set, compresi set di immagini, eCatalog, set di rendering e set di file multimediali.
* Visualizzatori Dynamic Media rich media standard.
* Adobe pagine JSP Dynamic Media OnDemand.
* Contenuto statico, ad esempio file PDF e video distribuiti progressivamente.
* Streaming video HTTP.
* Streaming video progressivo.

Al momento non sono supportati i seguenti tipi di risorse e funzionalità:

* Ricerca di Adobe Dynamic Media Classic Info o eCatalog
* Streaming video RTMP
* Web-stampa
* Servizi UGC (User-Generated Content)

>[!IMPORTANT]
>
>Il supporto per risorse di immagini vettoriali nuove o esistenti UGC in Adobe Dynamic Media è terminato il 30 settembre 2021.

### Test del servizio Secure Testing {#test-secure-testing-service}

Per garantire il funzionamento previsto del servizio di test Secure, procedi come segue:

#### Prepara l&#39;account

1. Contatta l’Assistenza clienti Adobe e richiedi l’abilitazione del test protetto sul tuo account.
1. In Adobe Experience Manager, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Installazione di Dynamic Media Publish]**.
1. Nella pagina Image Server , **[!UICONTROL Contesto di pubblicazione]** elenco a discesa, seleziona **[!UICONTROL Test Image Serving]**.
1. Seleziona la **[!UICONTROL Sicurezza]** scheda .
1. Per **[!UICONTROL Indirizzo client]** filtro, seleziona **[!UICONTROL Aggiungi]**.
1. In **[!UICONTROL Indirizzo IP]** campo , digita un indirizzo IP.
1. In **[!UICONTROL Maschera]** campo, digitare una maschera di rete.

   >[!NOTE]
   >
   >Se si aggiungono più di un indirizzo IP e una maschera di rete, ciò consente efficacemente *tutto* Gli indirizzi IP per effettuare chiamate alle risorse e vengono visualizzati tutti.

1. Effettua una delle operazioni seguenti:

   * Per aggiungere altri indirizzi IP, ripeti i tre passaggi precedenti.
   * Procedi al passaggio successivo.

1. Nell’angolo in alto a destra della pagina Image Server, seleziona **[!UICONTROL Salva]**.
1. Carica le immagini desiderate nel tuo account Dynamic Media di Adobe.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Assicurati che alcune delle immagini siano contrassegnate per la pubblicazione e altre non siano contrassegnate, quindi invia il lavoro di pubblicazione.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Determinare il nome del servizio Secure Testing andando a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Impostazione generale Dynamic Media]**.
1. Sulla **[!UICONTROL Server]** , trova il nome del server a destra di **[!UICONTROL Nome server pubblicato]**.

Se il nome del server è mancante o se l’URL del server non funziona, contatta l’Assistenza Adobe.

#### Preparare le varianti del sito web

Sono necessarie due varianti di un sito web che collega le risorse pubblicate e non pubblicate:

* Versione pubblica : collega le risorse utilizzando la sintassi URL Dynamic Media tradizionale.
* Versione di staging : collega le risorse utilizzando la stessa sintassi ma con il nome del sito di Secure Testing.

#### Eseguire i test

Esegui i seguenti test:

1. Verifica se le risorse sono visibili dalla rete aziendale.

   Dall&#39;interno della rete aziendale identificata dall&#39;intervallo di indirizzi IP precedentemente definito, la versione di staging del sito web visualizza tutte le immagini, contrassegnate per la pubblicazione o meno. Puoi eseguire il test senza rendere accidentalmente disponibili le immagini prima dell’approvazione dell’anteprima o del lancio del prodotto.

   Conferma che la versione pubblica del sito mostri le risorse pubblicate come precedentemente sperimentato con Adobe Dynamic Media.

1. Dall’esterno della rete aziendale, verifica che le risorse non pubblicate (cioè non contrassegnate per la pubblicazione) siano protette dall’accesso di terze parti.

   Accedi alla rete dall’esterno (ad esempio dal computer di casa o tramite una connessione 4G/5G), quindi verifica che la versione pubblica del sito mostri tutte le risorse pubblicate ma nessuno dei contenuti non pubblicati.

   Conferma che la versione di staging non mostri alcuna risorsa perché accedi al servizio Secure Testing da un indirizzo IP non approvato.
