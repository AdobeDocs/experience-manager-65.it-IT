---
title: Configurare Impostazione pubblicazione Dynamic Media per il server immagini
description: Scopri come configurare Dynamic Media Publish Setup per Image Server per pubblicare le risorse. Puoi anche verificare le risorse prima di renderle pubbliche.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: c86e79c4-e887-4ee3-bb54-eeffb34a33c2
solution: Experience Manager, Experience Manager Assets
autotag-review: '2026-05-18T18:46:26.981Z'
TQID: 'https://experienceleague.adobe.com/DfSAGGSoBR-9TOXKA89X3U4VReVbP-Ej70vUK1Zfczk'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 3751
ht-degree: 0%

---

# Configurare Impostazione pubblicazione Dynamic Media per il server immagini

Le opzioni di configurazione di Dynamic Media Publish Setup sono disponibili solo se:

* Stai eseguendo Dynamic Media in modalità Scene7. Vedi [Abilitare Dynamic Media in modalità Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Hai *esistente* **[!UICONTROL Configurazione elemento multimediale dinamico]** (in **[!UICONTROL Servizi cloud]**) in Adobe Experience Manager 6.5.11 o versione successiva. Consulta [Creare una configurazione Dynamic Media in Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Sei un amministratore di sistema di Experience Manager con privilegi di amministratore.

Gli sviluppatori e i programmatori di siti web esperti devono utilizzare Dynamic Media Publish Setup. Adobe Dynamic Media consiglia agli utenti che modificano le impostazioni di pubblicazione di avere familiarità con Adobe Dynamic Media, gli standard e le convenzioni del protocollo HTTP e la tecnologia di imaging di base.

La pagina Impostazione pubblicazione Dynamic Media stabilisce le impostazioni predefinite che determinano il modo in cui le risorse vengono distribuite dai server Adobe Dynamic Media ai siti web o alle applicazioni. Se non viene specificata alcuna impostazione, il server Adobe Dynamic Media distribuisce una risorsa in base a un’impostazione predefinita configurata nella pagina Impostazione pubblicazione Dynamic Media.

Vedi anche [Facoltativo - Impostazione e configurazione di Dynamic Media - Impostazioni modalità Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) per altre attività di configurazione facoltative.

>[!NOTE]
>
>Eseguire l’aggiornamento da Dynamic Media Classic a Dynamic Media su Adobe Experience Manager? Le pagine [Impostazioni generali](/help/assets/dm-general-settings.md) e Impostazione pubblicazione in Dynamic Media sono precompilate con i valori presi dall&#39;account Dynamic Media Classic. Le eccezioni sono tutti i valori elencati nell&#39;area **[!UICONTROL Opzioni di caricamento predefinite]** della pagina Impostazioni generali. Questi valori sono già presenti in Experience Manager. Di conseguenza, qualsiasi modifica apportata in **[!UICONTROL Opzioni di caricamento predefinite]**, in una qualsiasi delle cinque schede, tramite l&#39;interfaccia utente di Experience Manager, si riflette in Dynamic Media, non in Dynamic Media Classic. Tutte le altre impostazioni e i valori della pagina [Impostazioni generali](/help/assets/dm-general-settings.md) e della pagina Impostazione pubblicazione vengono mantenuti tra Dynamic Media Classic e Dynamic Media in Experience Manager.

**Per configurare il server immagini di installazione pubblicazione Dynamic Media:**

1. In modalità Autore Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale.
1. Nella barra a sinistra, fai clic sull&#39;icona Strumenti, quindi vai a **[!UICONTROL Assets]** > **[!UICONTROL Impostazione pubblicazione Dynamic Media]**.
1. Nella pagina Server immagini, dall&#39;elenco a discesa, scegliere il contesto di pubblicazione per definire le impostazioni predefinite per la consegna delle immagini dai server immagini.

| Contesto di pubblicazione | Descrizione |
| --- | --- |
| Image Server | Specifica il contesto per le impostazioni di pubblicazione. |
| Image Server test | Specifica il contesto per la verifica delle impostazioni di pubblicazione.<br>Solo per i nuovi account Dynamic Media, il campo predefinito **[!UICONTROL Indirizzo client]** è impostato automaticamente su `127.0.0.1`.<br>Consulta [Verifica le risorse prima di renderle pubbliche](#test-assets-before-making-public). |

1. Utilizza le cinque schede per configurare le impostazioni predefinite del contesto di pubblicazione.

   * Scheda [Sicurezza](#security-tab)
   * Scheda [Gestione catalogo](#catalog-management-tab)
   * Scheda [Attributi richiesta](#request-attributes-tab)
   * [Scheda Attributi miniatura comuni](#common-thumbnail-attributes-tab)
   * Scheda [Attributi gestione colore](#color-management-attributes-tab)

   ![Pagina Impostazione pubblicazione Dynamic Media](/help/assets/assets-dm/dm-publish-setup.png)
   *Pagina Impostazione pubblicazione Dynamic Media, con la scheda **[!UICONTROL Attributi richiesta]**&#x200B;selezionata.*<br><br>

1. Al termine, nell&#39;angolo superiore destro della pagina, fare clic su **[!UICONTROL Salva]**.

## Scheda Sicurezza {#security-tab}

>[!NOTE]
>
>Impostazioni di protezione non supportate per il contesto di pubblicazione di *Image Server*.

Se *Test Image Server* è impostato come contesto di pubblicazione, è possibile impostare la seguente impostazione di sicurezza:

**[!UICONTROL Indirizzo client]** - Consente di specificare uno o più indirizzi IP o intervalli di indirizzi IP. Se specificato, le richieste a questo catalogo immagini generate da un client non presente nell&#39;elenco degli indirizzi IP vengono rifiutate. Questa regola si applica sia alla consegna di immagini che a quelle di cui è stato eseguito il rendering.

![Scheda Sicurezza &#x200B;](/help/assets/assets-dm/dm-ipallowlist.png)<br>*Scheda Sicurezza che mostra il campo &quot;Consenti&quot; dell&#39;IP.*

## Scheda Gestione catalogo {#catalog-management-tab}

**[!UICONTROL Percorso file definizione set regole]** - Specifica il file contenente le definizioni del set regole per il catalogo immagini.

Vedi anche il parametro [RuleSetFile](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile) nella Guida di riferimento dei visualizzatori Dynamic Media.

>[!NOTE]
>
>Se il percorso del file di definizione del **[!UICONTROL set di regole]** dell&#39;account Dynamic Media Classic è selezionato in **[!UICONTROL Configurazione]** > **[!UICONTROL Applicazione]** > **[!UICONTROL Impostazione pubblicazione]**, Experience Manager recupera il file. L’account Dynamic Media recupera il file da Dynamic Media Classic. Il file viene quindi archiviato e reso disponibile in questo campo quando apri la pagina **[!UICONTROL Impostazione pubblicazione Dynamic Media]** per la prima volta.

## Scheda Attributi della richiesta {#request-attributes-tab}

Queste impostazioni si riferiscono all&#39;aspetto predefinito delle immagini.

| Impostazione | Descrizione |
| --- | --- |
| **[!UICONTROL Limite dimensioni immagine di risposta]** | Obbligatorio.<br>Solo per i nuovi account Dynamic Media, i limiti di dimensione predefiniti sono impostati automaticamente su Larghezza: `3000` e Altezza: `3000` sia per **[!UICONTROL Image Server]** che per **[!UICONTROL Test Image Server]**.<br>Specifica la larghezza e l&#39;altezza massime restituite al client per l&#39;immagine di risposta. Il server restituisce un errore se una richiesta causa un’immagine di risposta con larghezza, altezza o entrambi i valori maggiori di questa impostazione.<br>Vedere anche il parametro [MaxPix](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix) nella Guida di riferimento dei visualizzatori Dynamic Media. |
| **[!UICONTROL Modalità offuscamento richiesta]** | Attiva se desideri applicare la codifica base64 alle richieste valide.<br>Consulta anche il parametro [RequestObfuscation](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation) nella Guida di riferimento dei visualizzatori Dynamic Media. |
| **[!UICONTROL Modalità di blocco richieste]** | Attiva se desideri includere un blocco hash semplice nelle richieste.<br>Vedere anche il parametro [RequestLock](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock) nella Guida di riferimento per visualizzatori Dynamic Media. |
| **[!UICONTROL Attributi di richiesta predefiniti]** | |
| **[!UICONTROL Suffisso file immagine predefinito]** | Obbligatorio.<br>Estensione predefinita del file di dati che viene aggiunta ai valori dei campi Percorso e Percorso maschera del catalogo se il percorso non include un suffisso di file.<br>Vedere anche il parametro [DefaultExt](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext) nella Guida di riferimento dei visualizzatori Dynamic Media. |
| **[!UICONTROL Nome font predefinito]** | Specifica quale font utilizzare se non viene fornito alcun font in una richiesta di livello di testo. Se è specificato, deve essere un valore valido per il nome del carattere nella mappa dei caratteri di questo catalogo immagini o nella mappa dei caratteri del catalogo predefinito.<br>Vedere anche il parametro [DefaultFont](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont) nella Guida di riferimento dei visualizzatori Dynamic Media. |
| **[!UICONTROL Immagine predefinita]** | Un’immagine predefinita viene restituita in risposta a una richiesta in cui l’immagine richiesta non viene trovata.<br>Vedere anche il parametro [DefaultImage](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage) nella Guida di riferimento dei visualizzatori Dynamic Media.<br>**NOTA**: se per l&#39;account Dynamic Media Classic è selezionata un&#39;immagine **[!UICONTROL Predefinita]** in **[!UICONTROL Configurazione]** > **[!UICONTROL Applicazione]** > **[!UICONTROL Impostazione pubblicazione]**, nel gruppo **[!UICONTROL Attributi richiesta predefiniti]** Experience Manager recupera il file. Il file viene quindi archiviato e reso disponibile in questo campo quando apri la pagina **[!UICONTROL Impostazione pubblicazione Dynamic Media]** per la prima volta. |
| **[!UICONTROL Modalità immagine predefinita]** | Quando la casella del cursore è attivata (cursore a destra), l&#39;**[!UICONTROL immagine predefinita]** sostituisce ogni livello mancante nell&#39;immagine di origine con l&#39;immagine predefinita e restituisce il composito come di consueto. Quando la casella del cursore è disattivata (cursore a sinistra), l&#39;immagine predefinita sostituisce l&#39;intera immagine composita, anche se l&#39;immagine mancante è solo uno dei vari livelli.<br>Vedere anche il parametro [DefaultImageMode](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode) nella Guida di riferimento per visualizzatori Dynamic Media. |
| **[!UICONTROL Dimensioni visualizzazione predefinite]** | Obbligatorio.<br>Solo per i nuovi account Dynamic Media, le dimensioni di visualizzazione predefinite vengono impostate automaticamente su Larghezza: `1280` e Altezza: `1280` per **[!UICONTROL Image Server]** e **[!UICONTROL Test Image Server]**.<br>Le dimensioni delle immagini di risposta non devono superare queste dimensioni se nella richiesta non sono specificate esplicitamente le dimensioni di visualizzazione utilizzando `wid=`, `hei=` o `scl=`.<br>Vedere anche il parametro [DefaultPix](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix) nella Guida di riferimento per visualizzatori Dynamic Media. |
| **[!UICONTROL Dimensioni miniatura predefinite]** | Obbligatorio.<br>Utilizzato al posto dell&#39;attributo **[!UICONTROL Dimensioni visualizzazione predefinite]** per le richieste di miniature (`req=tmb`). Se in una richiesta di miniature (`req=tmb`) non sono specificate esplicitamente le dimensioni tramite `wid=`, `hei=` o `scl=`, il server vincola le dimensioni delle immagini di risposta ai valori di larghezza e altezza specificati.<br>Vedere anche il parametro [DefaultThumbPix](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix) nella Guida di riferimento per visualizzatori Dynamic Media. |
| **[!UICONTROL Colore di sfondo predefinito]** | Specifica il valore RGB utilizzato per riempire qualsiasi area di un&#39;immagine di risposta che non contiene dati immagine effettivi.<br>Vedere anche il parametro [BkgColor](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor) nella Guida di riferimento dei visualizzatori Dynamic Media. |
| **[!UICONTROL Attributi di codifica JPEG]** |  |
| **[!UICONTROL Qualità]** | <br>Specifica gli attributi predefiniti per le immagini di risposta di JPEG.<br>Solo per i nuovi account Dynamic Media, i valori predefiniti **[!UICONTROL Quality]** sono impostati automaticamente su `80` per **[!UICONTROL Image Server]** e **[!UICONTROL Test Image Server]**.<br>Questo campo è definito nell&#39;intervallo da 1 a 100.<br>Vedere anche il parametro [JpegQuality](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality) nella Guida di riferimento per i visualizzatori Dynamic Media. |
| **[!UICONTROL Downsampling cromatico]** | Abilita o disabilita il downsampling cromatico, utilizzato dagli encoder JPEG. |
| **[!UICONTROL Metodo di ricampionamento predefinito]** | Specifica gli attributi di ricampionamento e interpolazione predefiniti da utilizzare per il ridimensionamento dei dati immagine. Usare quando `resMode` non è specificato in una richiesta.<br>Solo per i nuovi account Dynamic Media, le modalità di ricampionamento predefinite sono impostate automaticamente su `Sharp2` sia per **[!UICONTROL Image Server]** che per **[!UICONTROL Test Image Server]**.<br>Vedere anche il parametro [ResMode](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode) nella Guida di riferimento per i visualizzatori Dynamic Media. |

## Scheda Attributi miniatura comuni {#common-thumbnail-attributes-tab}

Queste impostazioni si riferiscono all&#39;aspetto e all&#39;allineamento predefiniti delle miniature.

| Impostazione | Descrizione |
| --- | --- |
| **[!UICONTROL Colore di sfondo predefinito per miniatura]** | Specifica il valore RGB utilizzato per riempire l&#39;area di un&#39;immagine miniatura di output che non contiene dati immagine effettivi. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo miniatura predefinito]** è impostato su **[!UICONTROL Adatta]** o **[!UICONTROL Texture]**.<br>Vedere anche il parametro [ThumbBkgColor](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor) nella Guida di riferimento per visualizzatori Dynamic Media. |
| **[!UICONTROL Allineamento orizzontale]** | Specifica l&#39;allineamento orizzontale della miniatura nel rettangolo dell&#39;immagine di risposta specificato dai valori `wid=` e `hei=`.<br>Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo miniatura predefinito]** è impostato su **[!UICONTROL Adatta]**.<br>Sono disponibili tre allineamenti orizzontali tra cui scegliere: **[!UICONTROL Allineamento centrale]**, **[!UICONTROL Allineamento sinistro]** e **[!UICONTROL Allineamento destro]**.<br>Vedere anche il parametro [ThumbHorizAlign](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign) nella Guida di riferimento per i visualizzatori Dynamic Media. |
| **[!UICONTROL Allineamento verticale]** | Specifica l&#39;allineamento verticale dell&#39;immagine miniatura nel rettangolo dell&#39;immagine di risposta specificato dai valori `wid=` e `hei=`. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo miniatura predefinito]** è impostato su **[!UICONTROL Adatta]**.<br>Sono disponibili tre allineamenti verticali tra cui scegliere: **[!UICONTROL Allineamento superiore]**, **[!UICONTROL Allineamento centrale]** e **[!UICONTROL Allineamento inferiore]**.<br>Vedere anche il parametro [ThumbVertAlign](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign) nella Guida di riferimento per i visualizzatori Dynamic Media. |
| **[!UICONTROL Durata predefinita cache]** | Se un record catalogo non contiene un valore Expiration valido, viene fornito un intervallo di scadenza predefinito in ore. Imposta su `-1` per contrassegnare come senza scadenza. <br>Consulta anche il parametro [Expiration](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration) nella Guida di riferimento dei visualizzatori Dynamic Media. |
| **[!UICONTROL Tipo miniatura predefinito]** | Se un determinato record catalogo non contiene un valore ThumbType valido per il catalogo, viene fornito un valore predefinito per il tipo di miniatura. Utilizzato solo per le richieste di miniature (`req=tmb`).<br>Sono disponibili tre tipi di miniature tra cui scegliere: **[!UICONTROL Ritaglia]**, **[!UICONTROL Adatta]** e **[!UICONTROL Texture]**.<br>Vedere anche il parametro [ThumbType](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype) nella Guida di riferimento per visualizzatori Dynamic Media. |
| **[!UICONTROL Risoluzione miniature predefinita]** | Se un record catalogo non contiene un valore ThumbRes valido, viene fornita un&#39;impostazione predefinita per la risoluzione dell&#39;oggetto miniatura. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando l&#39;impostazione **[!UICONTROL Tipo di miniatura predefinito]** è impostata su **[!UICONTROL Texture]**.<br>Vedere anche il parametro [ThumbRes](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres) nella Guida di riferimento per visualizzatori Dynamic Media. |

## Scheda Attributi gestione colore {#color-management-attributes-tab}

Queste impostazioni determinano i profili colore ICC utilizzati per le immagini.

**Intento di rendering della conversione colore**
Un intento di rendering di conversione colore consente di ignorare l’intento di rendering predefinito dei profili di lavoro per determinare come vengono regolati i colori sorgente. Utilizzato quando:

1. Uno dei profili ICC predefiniti è lo spazio colore di destinazione di una conversione colore.
1. Questo profilo caratterizza una periferica di output, ad esempio una stampante o un monitor.
1. L&#39;intento di rendering specificato è valido per questo profilo.

Intenti di rendering diversi utilizzano regole diverse per determinare come vengono regolati i colori di origine.

Vedi anche il parametro [IccRenderIntent](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent) nella Guida di riferimento dei visualizzatori Dynamic Media.

>[!NOTE]
>
>In generale, utilizzate l&#39;intento di rendering predefinito per l&#39;impostazione di colore selezionata, che Adobe ha testato per soddisfare gli standard del settore. Ad esempio, se scegli un&#39;impostazione di colore per Nord America o Europa, l&#39;intento di rendering predefinito per la conversione colore è **[!UICONTROL Colorimetrico relativo]**. Se si sceglie un&#39;impostazione colore per il Giappone, l&#39;intento di rendering predefinito per la conversione colore è **[!UICONTROL Percettivo]**.

| Impostazione | Caratteristiche |
| --- | --- |
| **[!UICONTROL Spazio colore predefinito CMYK]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per dati CMYK. Se si sceglie **[!UICONTROL Nessuno specificato]**, la gestione del colore per questo catalogo immagini è disabilitata per le immagini sorgente CMYK. Tutti gli spazi di lavoro CMYK sono dipendenti dal dispositivo, il che significa che si basano sulle effettive combinazioni di inchiostro e carta. Le aree di lavoro CMYK fornite da Adobe si basano su condizioni di stampa commerciali standard.<br> Vedi anche il parametro [IccProfileCMYK](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk) nella Guida di riferimento dei visualizzatori Dynamic Media. |
| **[!UICONTROL Spazio colore predefinito scala di grigi]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per dati in scala di grigio. Se si sceglie **[!UICONTROL Nessuno specificato]**, la gestione del colore per questo catalogo immagini è disabilitata per le immagini sorgente in scala di grigio.<br>Vedere anche il parametro [IccProfileGray](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray) nella Guida di riferimento per visualizzatori Dynamic Media. |
| **[!UICONTROL Spazio colore predefinito di RGB]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per i dati RGB. Se si sceglie **[!UICONTROL Nessuno specificato]**, la gestione del colore per questo catalogo immagini è disabilitata quando sono coinvolte immagini di origini RGB. In generale, è consigliabile scegliere **[!UICONTROL Adobe RGB]** o **[!UICONTROL sRGB]**, anziché il profilo per un dispositivo specifico, ad esempio un profilo di monitoraggio. **[!UICONTROL sRGB]** è consigliato quando si preparano immagini per il Web o per dispositivi mobili, in quanto definisce lo spazio colore del monitor standard utilizzato per visualizzare immagini sul Web. **[!UICONTROL sRGB]** è inoltre una buona scelta quando si utilizzano immagini di fotocamere digitali di fascia consumer, poiché la maggior parte di queste fotocamere utilizza sRGB come spazio colore predefinito.<br>Vedere anche il parametro [IccProfileRBG](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb) nella Guida di riferimento per visualizzatori Dynamic Media. |
| **[!UICONTROL Intento di rendering della conversione colore]** | **[!UICONTROL Percettivo]** - Mira a mantenere la relazione visiva tra i colori in modo che venga percepita come naturale per l&#39;occhio umano, anche se i valori di colore stessi possono cambiare. Questo intento è adatto per le immagini fotografiche con molti colori fuori gamma. Questa impostazione rappresenta l&#39;intento di rendering standard per il settore della stampa giapponese. |
|  | **[!UICONTROL Colorimetrico relativo]** - Confronta l&#39;evidenziazione estrema dello spazio colore di origine con quella dello spazio colore di destinazione e sposta tutti i colori di conseguenza. I colori fuori gamma vengono spostati sul colore riproducibile più simile nello spazio colore di destinazione. La colorimetrica relativa conserva più colori originali in un&#39;immagine rispetto alla percezione. Questa impostazione rappresenta l&#39;intento di rendering standard per la stampa in Nord America ed Europa. |
|  | **[!UICONTROL Saturazione]** - Tenta di produrre colori vividi in un&#39;immagine a scapito della precisione dei colori. Questo intento di rendering è adatto a elementi grafici aziendali come grafici o grafici, in cui i colori saturi brillanti sono più importanti della relazione esatta tra i colori. |
|  | **[!UICONTROL Colorimetrico assoluto]** - Lascia invariati i colori che rientrano nella gamma di destinazione. I colori fuori gamma vengono ritagliati. Non viene eseguita alcuna modifica in scala dei colori in base al punto bianco di destinazione. Questo intento mira a mantenere la precisione del colore a scapito della conservazione delle relazioni tra i colori ed è adatto per le prove per simulare l&#39;output di un particolare dispositivo. Questo intento è utile per visualizzare in anteprima come il colore della carta influisce sui colori stampati. |

## Testare le risorse prima di renderle pubbliche {#test-assets-before-making-public}

Il testing sicuro consente di definire un ambiente di test sicuro e di creare una soluzione business-to-business affidabile, basata su un set configurabile di intervalli e indirizzi IP. Questa funzionalità consente di abbinare le implementazioni di Adobe Dynamic Media all’architettura del sistema di gestione dei contenuti e del sistema aziendale.

Con Test protetti, puoi visualizzare in anteprima la versione di staging del sito web con contenuto non pubblicato.

Se lo desideri, crea un ambiente di staging anziché rendere le risorse disponibili al pubblico per i seguenti motivi:

* Visualizza l&#39;anteprima dei siti Web prima del lancio pubblico (sito Web di staging).
* Distribuisci le risorse che richiedono un accesso limitato, ad esempio gli eCatalog che mostrano i prezzi in un’applicazione web B2B.
* Utilizza le risorse dietro un firewall come parte di un sistema di gestione delle informazioni sui prodotti, di un&#39;applicazione di assistenza clienti, di un sito di formazione e così via.

>[!NOTE]
>
>Il test protetto non influisce sull’accesso a Adobe Dynamic Media Classic. La sicurezza di Adobe Dynamic Media Classic rimane coerente e richiede le credenziali abituali per l’accesso a Adobe Dynamic Media Classic e ai servizi web correlati.

### Come funziona il test protetto {#how-test-assets-works}

La maggior parte delle aziende gestisce Internet con un firewall. L’accesso a Internet è possibile attraverso determinate vie e, in genere, attraverso un numero limitato di indirizzi IP pubblici.

Dalla rete aziendale è possibile individuare l&#39;indirizzo IP pubblico utilizzando siti Web come [https://www.whatismyip.com](https://www.whatismyip.com/) o richiedere queste informazioni all&#39;organizzazione IT aziendale.

Con Secure Testing, Adobe Dynamic Media stabilisce un server immagini dedicato per gli ambienti di staging o le applicazioni interne. Qualsiasi richiesta inviata a questo server controlla l’indirizzo IP di origine. Se la richiesta in ingresso non si trova nell’elenco approvato di indirizzi IP, viene restituita una risposta di errore. L’amministratore della società Adobe Dynamic Media configura l’elenco approvato di indirizzi IP per l’ambiente di test sicuro della propria società.

Poiché la posizione della richiesta originale deve essere confermata, il traffico del servizio di test protetto non viene instradato attraverso una rete di distribuzione del contenuto come il traffico pubblico del server di immagini Dynamic Media. Le richieste al servizio di test sicuro hanno una latenza leggermente superiore rispetto ai server di immagine Dynamic Media pubblici.

Le risorse non pubblicate sono immediatamente disponibili dai servizi di test protetto, senza dover essere pubblicate. In questo modo, puoi eseguire un’anteprima prima che le risorse vengano pubblicate sul loro server immagini rivolto al pubblico.

>[!NOTE]
>
>I servizi di test sicuri utilizzano il server di catalogo configurato con un contesto di pubblicazione interno. Pertanto, se l’azienda è configurata per la pubblicazione su Secure Testing, tutte le risorse caricate in Adobe Dynamic Media diventano immediatamente disponibili sui servizi di Secure Testing. Questa funzionalità è true indipendentemente dal fatto che le risorse siano contrassegnate per la pubblicazione al caricamento.

I servizi di test sicuro supportano attualmente i seguenti tipi di risorse e funzionalità:

* Immagini.
* Vignette (richieste del server di rendering).
* I clienti devono richiedere esplicitamente il supporto del server di rendering, che è disponibile.
* Set, inclusi set di immagini, eCatalog, set di rendering e set di file multimediali.
* Visualizzatori rich media Adobe Dynamic Media standard.
* Pagine JSP Adobe Dynamic Media OnDemand.
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
  >A partire dal 1° maggio 2023, le risorse UGC in Dynamic Media sono disponibili per l’uso fino a 60 giorni dalla data di caricamento. Dopo 60 giorni, le risorse vengono rimosse.

  >[!NOTE]
  >
  >Il supporto per le risorse di immagini vettoriali UGC nuove o esistenti in Adobe Dynamic Media è terminato il 30 settembre 2021.

### Test del servizio di test protetto {#test-secure-testing-service}

Per garantire che il servizio di test protetto funzioni come previsto, eseguire le operazioni seguenti:

#### Prepara l’account

1. Contatta l’Assistenza clienti di Adobe e richiedi l’abilitazione di Secure Testing sul tuo account.
1. In Adobe Experience Manager, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Impostazione pubblicazione Dynamic Media]**.
1. Nell&#39;elenco a discesa **[!UICONTROL Contesto di pubblicazione]** della pagina Image Server selezionare **[!UICONTROL Test Image Server]**.
1. Selezionare la scheda **[!UICONTROL Protezione]**.
1. Per il filtro **[!UICONTROL Indirizzo client]**, selezionare **[!UICONTROL Aggiungi]**.
1. Nel campo **[!UICONTROL Indirizzo IP]** digitare un indirizzo IP.
1. Nel campo **[!UICONTROL Maschera]** digitare una maschera di rete.

   >[!NOTE]
   >
   >Se aggiungi più di un indirizzo IP e di una maschera di rete, questo consente effettivamente a *tutti* gli indirizzi IP di effettuare chiamate alle risorse, che vengono visualizzati tutti.

1. Effettua una delle seguenti operazioni:

   * Per aggiungere altri indirizzi IP, ripeti i tre passaggi precedenti.
   * Procedi al passaggio successivo.

1. Nell&#39;angolo superiore destro della pagina Server immagini, selezionare **[!UICONTROL Salva]**.
1. Carica le immagini desiderate sul tuo account Adobe Dynamic Media.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Assicurati che alcune delle immagini siano contrassegnate per la pubblicazione e altre non siano contrassegnate, quindi invia il processo di pubblicazione.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Determinare il nome del servizio di test protetto scegliendo **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Impostazione generale di Dynamic Media]**.
1. Nella pagina **[!UICONTROL Server]**, trovare il nome del server a destra di **[!UICONTROL Nome server pubblicato]**.

Se manca il nome del server o se l’URL del server non funziona, contatta l’Assistenza Adobe.

#### Prepara varianti di sito web

Sono necessarie due varianti di un sito web che collega le risorse pubblicate e non pubblicate:

* Versione pubblica - Collega le risorse utilizzando la sintassi URL tradizionale di Adobe Dynamic Media.
* Versione di staging - Collega le risorse utilizzando la stessa sintassi ma con il nome del sito di test protetto.

#### Eseguire i test

Eseguire i test seguenti:

1. Verifica se le risorse sono visibili dalla rete aziendale.

   All’interno della rete aziendale identificata dall’intervallo di indirizzi IP definito in precedenza, nella versione di staging del sito web vengono visualizzate tutte le immagini, contrassegnate per la pubblicazione o meno. Di conseguenza, è possibile eseguire il test senza rendere accidentalmente disponibili le immagini prima dell’approvazione in anteprima o del lancio del prodotto.

   Verifica che la versione pubblica del sito mostri le risorse pubblicate come in precedenza avveniva con Adobe Dynamic Media.

1. Dall’esterno della rete aziendale, verifica che le risorse non pubblicate (ossia, non contrassegnate per la pubblicazione) siano protette dall’accesso di terze parti.

   Accedi alla rete dall’esterno (ad esempio dal computer di casa o tramite una connessione 4G/5G), quindi verifica che nella versione pubblica del sito siano visualizzate tutte le risorse pubblicate ma nessun contenuto non pubblicato.

   Conferma che la versione di staging non mostri alcuna risorsa perché stai accedendo al servizio di test protetto da un indirizzo IP non approvato.
