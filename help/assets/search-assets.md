---
title: Cercare risorse digitali e immagini in [!DNL Adobe Experience Manager]
description: Scoprite come trovare le risorse necessarie in [!DNL Adobe Experience Manager] utilizzando il pannello Filtri e come utilizzare le risorse visualizzate nella ricerca.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 38ef8d8bd574933fdc57d7475831518f9d7f293e
workflow-type: tm+mt
source-wordcount: '5716'
ht-degree: 5%

---


# Cerca risorse in [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] fornisce solidi metodi di individuazione delle risorse che consentono di ottenere una maggiore velocità del contenuto. I team possono ridurre i tempi di immissione sul mercato grazie a un’esperienza di ricerca intelligente e senza soluzione di continuità, grazie alla funzionalità e ai metodi personalizzati. La ricerca delle risorse è fondamentale per l’utilizzo di un sistema di gestione delle risorse digitali, sia per l’ulteriore utilizzo da parte dei creativi, per una gestione affidabile delle risorse da parte degli utenti aziendali e degli esperti di marketing, sia per l’amministrazione da parte degli amministratori DAM. Ricerche semplici, avanzate e personalizzate che potete eseguire tramite l&#39;interfaccia utente [!DNL Assets] o altre app e superfici aiutano a soddisfare questi casi di utilizzo.

[!DNL Experience Manager Assets] supporta i seguenti casi d’uso e questo articolo descrive l’utilizzo, i concetti, le configurazioni, i limiti e la risoluzione dei problemi per questi casi d’uso.

| Cercare risorse | Configurazione e amministrazione | Utilizzo dei risultati di ricerca |
|---|---|---|
| [Ricerche di base](#searchbasics) | [Indice di ricerca](#searchindex) | [Ordinare i risultati](#sort) |
| [Comprendere l’interfaccia di ricerca](#searchui) | [Ricerca visiva o per similarità](#configvisualsearch) | [Verificare le proprietà e i metadati di una risorsa](#checkinfo) |
| [Suggerimenti per la ricerca](#searchsuggestions) | [Metadati obbligatori](#mandatorymetadata) | [Scarica](#download) |
| [Comprendere i risultati della ricerca e il comportamento](#searchbehavior) | [Modificare i facet di ricerca](#searchfacets) | [Aggiornamenti di massa dei metadati](#metadataupdates) |
| [Classificazione e incremento della ricerca](#searchrank) | [Estrazione del testo](#extracttextupload) | [Raccolte intelligenti](#collections) |
| [Ricerca avanzata: filtraggio e ambito di ricerca](#scope) | [predicati personalizzati](#custompredicates) | [Comprendere e risolvere problemi relativi a risultati imprevisti](#unexpectedresults) |
| [Cerca da altre soluzioni e app](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[ app desktop Experience Manager](#desktopapp)</li><li>[ immagini Adobe Stock](#adobestock)</li><li>[Risorse Dynamic Media](#dynamicmedia)</li></ul> |  |  |
| [Selettore risorse](#assetpicker) |  |  |
| [](#limitations) Limitazioni e  [suggerimenti](#tips) |  |  |
| [Esempi illustrati](#samples) |  |  |

Cercate le risorse utilizzando il campo Omnisearch nella parte superiore dell&#39;interfaccia Web [!DNL Experience Manager]. Vai a **[!UICONTROL Risorse]** > **[!UICONTROL File]** in [!DNL Experience Manager], fai clic su ![search_icon](assets/do-not-localize/search_icon.png) nella barra superiore, immetti la parola chiave di ricerca e seleziona `Return`. In alternativa, utilizzate la scelta rapida per le parole chiave `/` (barra) per aprire il campo di ricerca Omnisearch. `Location:Assets` è preselezionata per limitare le ricerche alle risorse DAM. [!DNL Experience Manager] fornisce suggerimenti durante la digitazione iniziale di una parola chiave di ricerca.

Usate il pannello **[!UICONTROL Filtri]** per cercare risorse, cartelle, tag e metadati. Potete filtrare i risultati di ricerca in base alle varie opzioni (predicati), come il tipo di file, la dimensione del file, la data dell&#39;ultima modifica, lo stato della risorsa, i dati di approfondimento e  licenza Adobe Stock. Potete personalizzare il pannello Filtri e aggiungere o rimuovere i predicati di ricerca utilizzando [facet di ricerca](/help/assets/search-facets.md). Il filtro [!UICONTROL Tipo di file] nel pannello [!UICONTROL Filtri] dispone di caselle di controllo con stato misto. Pertanto, a meno che non si selezionino tutti i predicati (o i formati) nidificati, le caselle di controllo di primo livello sono selezionate parzialmente.

[!DNL Experience Manager] la funzionalità di ricerca supporta la ricerca di raccolte e la ricerca di risorse all&#39;interno di una raccolta. Vedere [raccolte di ricerca](/help/assets/manage-collections.md).

## Comprendere l&#39;interfaccia di ricerca {#searchui}

Acquisisci familiarità con l’interfaccia di ricerca e le azioni disponibili.

![Comprendere  Experience Manager Interfaccia dei risultati della ricerca Risorse](assets/aem_search_results.png)

*Figura: Comprendere l’interfaccia dei risultati della  [!DNL Experience Manager Assets] ricerca.*

**A.** Salvare la ricerca come raccolta avanzata. **B.** Filtri o predicati per limitare i risultati della ricerca. **C.** Visualizzare file, cartelle o entrambi. **D.** Fai clic su Filtri per aprire o chiudere la barra a sinistra. **E.** Il percorso di ricerca è DAM. **F.Campo di ricerca** Omnisearch con parola chiave di ricerca fornita dall&#39;utente. **G.** Selezionare i risultati di ricerca caricati. **H.** Numero di risultati di ricerca visualizzati rispetto al totale dei risultati di ricerca. **I.** Chiudere la ricerca. **J.** Passare dalla vista a scheda a quella a elenco.

### Facet di ricerca dinamici {#dynamicfacets}

Dalla pagina dei risultati della ricerca potete individuare più rapidamente le risorse desiderate utilizzando il numero dinamico di risultati di ricerca previsti nei facet di ricerca. Il numero previsto di risorse viene aggiornato anche prima dell’applicazione del filtro di ricerca. La visualizzazione del conteggio previsto rispetto al filtro consente di navigare nei risultati di ricerca in modo rapido ed efficiente.

![Visualizzate il numero approssimativo di risorse senza filtrare i risultati di ricerca nei facet di ricerca.](assets/asset_search_results_in_facets_filters.png)

*Figura: Visualizzate il numero approssimativo di risorse senza filtrare i risultati di ricerca nei facet di ricerca.*

## Comprendere i risultati della ricerca e il comportamento {#searchbehavior}

### Termini e risultati di ricerca di base {#searchbasics}

Potete eseguire ricerche per parole chiave dal campo OmniSearch. La ricerca per parola chiave non fa distinzione tra maiuscole e minuscole ed è una ricerca full-text (nei più comuni campi di metadati). Se vengono utilizzate più parole chiave, `AND` è l&#39;operatore predefinito tra le parole chiave.

I risultati sono ordinati in base alla rilevanza, a partire da corrispondenze più simili. Per più parole chiave, i risultati più rilevanti sono le risorse che contengono entrambi i termini nei metadati. All’interno dei metadati, le parole chiave che appaiono come smart tag hanno una classificazione più alta rispetto alle parole chiave che vengono visualizzate in altri campi di metadati. [!DNL Experience Manager] consente di assegnare a un particolare termine di ricerca maggiore peso. Inoltre, è possibile [incrementare la classifica](#searchrank) di alcune risorse con targeting per termini di ricerca specifici.

Per trovare rapidamente le risorse rilevanti, l’interfaccia avanzata offre meccanismi di filtraggio, ordinamento e selezione. Potete filtrare i risultati in base a più criteri e visualizzare il numero di risorse ricercate per vari filtri. In alternativa, potete eseguire nuovamente la ricerca modificando la query nel campo Omnisearch. Quando modificate i termini di ricerca o i filtri, gli altri filtri rimangono applicati per mantenere il contesto della ricerca.

Quando i risultati sono molte risorse, [!DNL Experience Manager] visualizza i primi 100 nella vista a schede e 200 nella vista a elenco. Quando gli utenti scorrono, vengono caricate più risorse. Questo per migliorare le prestazioni. Guardate una dimostrazione video del numero [di risorse visualizzate](https://www.youtube.com/watch?v=LcrGPDLDf4o).

In alcuni casi, nei risultati della ricerca potrebbero essere presenti risorse impreviste. Per ulteriori informazioni, vedere [risultati imprevisti](#troubleshoot-unexpected-search-results-and-issues).

[!DNL Experience Manager] può cercare in molti formati di file e i filtri di ricerca possono essere personalizzati in base alle tue esigenze aziendali. Per conoscere le opzioni di ricerca disponibili per l&#39;archivio DAM e le limitazioni applicate all&#39;account, contattare l&#39;amministratore.

### Risultati con e senza smart tag avanzati {#withsmarttags}

Per impostazione predefinita, la ricerca [!DNL Experience Manager] combina i termini di ricerca con una clausola AND. Ad esempio, è consigliabile cercare le parole chiave che una donna esegue. Per impostazione predefinita nei risultati di ricerca vengono visualizzate solo le risorse con sia donna che parole chiave in esecuzione nei metadati. Lo stesso comportamento viene mantenuto quando con le parole chiave vengono usati caratteri speciali (punti, trattini o trattini). Le seguenti query di ricerca restituiscono gli stessi risultati:

* `woman running`
* `woman.running`
* `woman-running`

Tuttavia, la query `woman -running` restituisce le risorse senza `running` nei relativi metadati.
L&#39;utilizzo di smart tag aggiunge una clausola `OR` aggiuntiva per trovare i termini di ricerca come smart tag applicati. Anche una risorsa con tag `woman` o `running` utilizzando gli smart tag viene visualizzata in una query di ricerca di questo tipo. Quindi i risultati della ricerca sono una combinazione di:

* Risorse con `woman` e `running` parole chiave nei metadati (comportamento predefinito).

* Risorse con tag avanzati a una delle parole chiave (comportamento smart tag).

### Cerca suggerimenti durante la digitazione di {#searchsuggestions}

Quando si inizia a digitare le parole chiave, [!DNL Experience Manager] suggerisce le possibili parole chiave o frasi da cercare. I suggerimenti si basano sui metadati delle risorse esistenti. [!DNL Experience Manager] indicizza tutti i campi di metadati per facilitare la ricerca. Per fornire suggerimenti per la ricerca, il sistema utilizza i valori dei seguenti campi di metadati. Per fornire suggerimenti per la ricerca, è consigliabile compilare i campi seguenti con le parole chiave appropriate:

* Tag risorsa. (mappe a `jcr:content/metadata/cq:tags`)
* Titolo risorsa. (mappe a `jcr:content/metadata/dc:title`)
* Descrizione della risorsa. (mappe a `jcr:content/metadata/dc:description`)
* Titolo nell’archivio JCR. Il valore può essere mappato sul titolo della risorsa. (mappe a `jcr:content/jcr:title`)
* Descrizione nell’archivio JCR. Il valore può essere mappato sulla descrizione della risorsa. (mappe a `jcr:content/jcr:description`)

Per ricevere suggerimenti per più parole chiave di ricerca, continuate a digitare tutte le parole chiave senza selezionare alcun suggerimento per una sola parola chiave.

![Digitate più parole chiave per visualizzare i suggerimenti che vi rientrano](assets/search_suggestionsmanykeywords.gif)

*Figura: Digitate più parole chiave per visualizzare i suggerimenti adatti a tutti.*

### Classificazione e incremento della ricerca {#searchrank}

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a uno qualsiasi dei termini di ricerca negli smart tag. Nell&#39;esempio precedente, l&#39;ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. Corrisponde a `woman running` nei vari campi di metadati.
1. Corrisponde a `woman running` negli smart tag.
1. Corrisponde a `woman` o `running` negli smart tag.

Potete migliorare la rilevanza delle parole chiave per risorse particolari per migliorare le ricerche in base alle parole chiave. In altre parole, le immagini per le quali vengono promosse parole chiave specifiche vengono visualizzate nella parte superiore dei risultati della ricerca quando si esegue una ricerca basata su tali parole chiave.

1. Dall&#39;interfaccia utente di [!DNL Assets], aprite la pagina delle proprietà della risorsa. Fare clic su **[!UICONTROL Avanzate]** e fare clic su **[!UICONTROL Aggiungi]** in **[!UICONTROL Elevate for search keywords]**.
1. Nella casella **[!UICONTROL Search Promote]**, specificare una parola chiave per la quale si desidera incrementare la ricerca dell&#39;immagine, quindi fare clic su **[!UICONTROL Add]**. Potete specificare più parole chiave nello stesso modo.
1. Fai clic su **[!UICONTROL Salva e chiudi]**. La risorsa promossa per questa parola chiave viene visualizzata tra i primi risultati della ricerca.

Potete usarlo a proprio vantaggio aumentando il livello di alcune risorse nei risultati della ricerca per la parola chiave di destinazione. Guardate il video di esempio riportato di seguito. Per informazioni dettagliate, vedere [cercare in [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Video: Come classificare i risultati della ricerca e come influenzarne la classificazione.*

## Ricerca avanzata {#scope}

[!DNL Experience Manager] sono disponibili vari metodi, come i filtri, che consentono di individuare più rapidamente le risorse ricercate. Di seguito sono descritti alcuni metodi di uso comune. Alcuni esempi [illustrati](#samples) sono condivisi di seguito.

**Cercare file o cartelle**: Nei risultati della ricerca, consultate file, cartelle o entrambi. Dal pannello **[!UICONTROL Filtri]** è possibile selezionare l&#39;opzione appropriata. Vedere [interfaccia di ricerca](#searchui).

**Cercare risorse all’interno di una cartella**: Potete limitare la ricerca a una cartella specifica. Nel pannello **[!UICONTROL Filtri]**, aggiungete il percorso di una cartella. Potete selezionare una sola cartella alla volta.

![Limitare i risultati di ricerca in una cartella aggiungendo un percorso di cartella nel pannello Filtri](assets/search_folder_select.gif)

*Figura: Per limitare i risultati della ricerca a una cartella, aggiungete il percorso di una cartella nel pannello Filtri.*

### Trova immagini simili {#visualsearch}

Per trovare immagini visivamente simili a quelle selezionate dall’utente, fai clic su **[!UICONTROL Trova simili]** nella vista a schede di un’immagine o nella barra degli strumenti. [!DNL Experience Manager]Dall’archivio DAM,  visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. Scopri [come configurare la ricerca per similarità](#configvisualsearch).

![Trovare immagini simili utilizzando l&#39;opzione nella vista a schede](assets/search_find_similar.png)

*Figura: Trovate immagini simili utilizzando l&#39;opzione nella vista a schede.*

###  immagini Adobe Stock {#adobestock}

Dall&#39;interfaccia utente [!DNL Experience Manager], gli utenti possono eseguire ricerche in [ risorse Adobe Stock](/help/assets/aem-assets-adobe-stock.md) e ottenere la licenza per le risorse necessarie. Aggiungete `Location: Adobe Stock` nella barra di ricerca Omnisearch. Potete anche usare il pannello Filtri per trovare tutte le risorse con o senza licenza o per cercare una risorsa specifica usando  numero di file Adobe Stock.

### Risorse Dynamic Media {#dmassets}

Per filtrare le immagini in base a Dynamic Media, dal pannello **[!UICONTROL Filtri]** seleziona **[!UICONTROL Dynamic Media]** > **[!UICONTROL Set]**. Filtra e visualizza le risorse come set di immagini, caroselli, set di file multimediali diversi e set 360 gradi.

### Ricerca utilizzando valori specifici nei campi di metadati {#gqlsearch}

Potete cercare le risorse in base ai valori esatti di specifici campi di metadati, ad esempio titolo, descrizione e autore. La funzione di ricerca full-text GQL raccoglie solo le risorse il cui valore di metadati corrisponde esattamente alla query di ricerca. I nomi delle proprietà (ad esempio autore, titolo e così via) e i valori seguono la distinzione tra maiuscole e minuscole.

| Campo metadati | Valore e utilizzo dei facet |
| ----------------------------------------- | --------------------------------------- |
| Titolo | `title:John` |
| Creatore | `creator:John` |
| Dove si trova | `location:NA` |
| Descrizione | `description:"Sample Image"` |
| Strumento di creazione | `creatortool:"Adobe Photoshop CC 2020"` |
| Proprietario copyright | `copyrightowner:"Adobe Systems"` |
| Collaboratore | `contributor:John` |
| Condizioni d&#39;uso | `usageterms:"CopyRights Reserved"` |
| Creato | `created`:YYYY-MM-DDTHH |
| Data scadenza | `expires`:YYYY-MM-DDTHH |
| Ora di attivazione | `ontime`:YYYY-MM-DDTHH |
| Ora di disattivazione | `offtime`:YYYY-MM-DDTHH |
| Intervallo di tempo (data di scadenza, ora di disattivazione) | `facet field`: in basso..upperbound |
| Percorso | /content/dam/&lt;nome cartella> |
| Titolo PDF | `pdftitle`:&quot;Documento  Adobe&quot; |
| Oggetto | `subject:"Training"` |
| Tag | `tags:"Location And Travel"` |
| Tipo | `type:"image\png"` |
| Larghezza dell’immagine | `width`:lowerbound..upperbound |
| Altezza dell’immagine | `height`:lowerbound..upperbound |
| Person | `person:John` |

Non è possibile combinare le proprietà `path`, `limit`, `size` e `orderby` utilizzando l&#39;operatore `OR` con qualsiasi altra proprietà.

La parola chiave per una proprietà generata dall&#39;utente è la relativa etichetta campo nell&#39;editor delle proprietà in lettere minuscole, con la rimozione degli spazi.

Di seguito sono riportati alcuni esempi di formati di ricerca per query complesse:

* Per visualizzare tutte le risorse con più campi facet (ad esempio: title=John Doe e strumento di creazione =  Adobe Photoshop): `title:"John Doe" creatortool:Adobe*`
* Per visualizzare tutte le risorse quando il valore dei facet non è una singola parola ma una frase (ad esempio: title=Scott Reynolds): `title:"Scott Reynolds"`
* Per visualizzare le risorse con più valori di una singola proprietà (ad esempio: title=Scott Reynolds o John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Per visualizzare le risorse con valori di proprietà che iniziano con una stringa specifica (ad esempio: title is Scott Reynolds): `title:Scott*`
* Per visualizzare le risorse con valori di proprietà che terminano con una stringa specifica (ad esempio: title is Scott Reynolds): `title:*Reynolds`
* Per visualizzare le risorse con un valore di proprietà contenente una stringa specifica (ad esempio: title = Sala riunioni di Basilea): `title:*Meeting*`
* Per visualizzare le risorse che contengono una stringa particolare e hanno un valore di proprietà specifico (ad esempio: cercare una stringa  Adobe nelle risorse con title=John Doe): `*Adobe* title:"John Doe"`

## Cercare risorse da altre [!DNL Experience Manager] offerte o interfacce {#beyondomnisearch}

[!DNL Adobe Experience Manager] collega l&#39;archivio DAM a varie altre  [!DNL Experience Manager] soluzioni per fornire un accesso più rapido alle risorse digitali e semplificare i flussi di lavoro creativi. Qualsiasi individuazione di risorse inizia con ricerca o ricerca. Il comportamento di ricerca rimane in gran parte lo stesso per le diverse superfici e soluzioni. Alcuni metodi di ricerca cambiano man mano che l&#39;audience di destinazione, i casi di utilizzo e l&#39;interfaccia utente variano tra le soluzioni [!DNL Experience Manager]. I metodi specifici sono documentati per le singole soluzioni ai link seguenti. I suggerimenti e i comportamenti universalmente applicabili sono documentati in questo articolo.

### Cercare risorse dal pannello Collegamento risorse  Adobe {#aal}

Utilizzando  collegamento risorse di Adobe, i creativi professionisti ora possono accedere al contenuto memorizzato in [!DNL Experience Manager Assets], senza uscire dalle app Adobe Creative Cloud supportate. I creativi possono sfogliare, cercare, estrarre e archiviare facilmente le risorse utilizzando il pannello in-app in [!DNL Adobe Creative Cloud apps]: [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign]. Collegamento risorsa consente anche agli utenti di effettuare ricerche con risultati visivamente simili. I risultati della visualizzazione della ricerca visiva sono basati  algoritmi di machine learning Adobe Sensei e consentono agli utenti di trovare immagini esteticamente simili. Consultate [cercare e sfogliare le risorse](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) utilizzando  collegamento risorsa Adobe.

### Cerca risorse nell&#39;app [!DNL Experience Manager] desktop {#desktopapp}

I professionisti creativi utilizzano l&#39;app desktop per rendere facilmente ricercabile [!DNL Experience Manager Assets] e disponibile sul desktop locale (Win o Mac). I creativi possono rivelare facilmente le risorse desiderate in Mac Finder o Windows Explorer, aperte nelle applicazioni desktop e modificate localmente - le modifiche vengono salvate in [!DNL Experience Manager] con una nuova versione creata nell&#39;archivio. L&#39;applicazione supporta le ricerche di base utilizzando una o più parole chiave, caratteri jolly `*` e `?` e operatore `AND`. Consultate [sfogliare, cercare e visualizzare in anteprima le risorse](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) nell&#39;app desktop.

### Cerca risorse in [!DNL Brand Portal] {#brandportal}

Gli utenti e i professionisti del settore della linea di business utilizzano Brand Portal per condividere in modo efficiente e sicuro le risorse digitali approvate con i team interni, i partner e i rivenditori estesi. Consultate [cercare risorse su Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Cerca immagini [!DNL Adobe Stock] {#adobestock-1}

Dall&#39;interfaccia utente di [!DNL Experience Manager], gli utenti possono effettuare ricerche  risorse Adobe Stock e ottenere la licenza per le risorse necessarie. Aggiungete `Location: Adobe Stock` nel campo Omnisearch. Potete anche utilizzare il pannello **[!UICONTROL Filtri]** per trovare tutte le risorse con o senza licenza o per cercare una risorsa specifica utilizzando  numero di file Adobe Stock. Vedere [gestire  immagini Adobe Stock in  Experience Manager](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Ricerca risorse Dynamic Media {#dynamicmedia}

Per filtrare le immagini in base a Dynamic Media, dal pannello **[!UICONTROL Filtri]** seleziona **[!UICONTROL Dynamic Media]** > **[!UICONTROL Set]**. Filtra e visualizza le risorse come set di immagini, caroselli, set di file multimediali diversi e set 360 gradi. Durante la creazione di pagine web, gli autori possono cercare i set direttamente da Content Finder. Nel menu pop-up è disponibile un filtro per i set.

### Cercare risorse in Content Finder durante la creazione di pagine Web {#contentfinder}

Gli autori possono utilizzare Content Finder per ricercare nell&#39;archivio DAM le risorse pertinenti e utilizzare le risorse nelle pagine Web che creano. Gli autori possono inoltre utilizzare la funzionalità Risorse collegate per cercare le risorse disponibili in una [!DNL Experience Manager] distribuzione remota. Gli autori possono quindi utilizzare queste risorse nelle pagine Web in una distribuzione [!DNL Experience Manager] locale. Vedere [utilizzare risorse remote](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Cerca raccolte {#collections}

[!DNL Experience Manager] la funzionalità di ricerca supporta la ricerca di raccolte e la ricerca di risorse all&#39;interno di una raccolta. Vedere [raccolte di ricerca](/help/assets/manage-collections.md).

## Selettore risorse {#assetpicker}

>[!NOTE]
>
>Il selettore delle risorse era denominato [selettore risorse](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) nelle versioni precedenti di [!DNL Adobe Experience Manager].

Il selettore delle risorse consente di sfogliare, cercare e filtrare le risorse DAM in modo speciale. Potete avviare il selettore delle risorse nell&#39;istanza [!DNL Experience Manager] utilizzando `https://[aem-server]:[port]/aem/assetpicker.html`. Questo URL apre il selettore delle risorse in modalità Sfoglia. Utilizzate i parametri di richiesta supportati come suffisso, ad esempio `mode` (selezioni singole o multiple) o `viewmode` con `assettype` (immagine, video, testo) e `mimetype`. Questi parametri definiscono il contesto del selettore delle risorse per una particolare istanza di ricerca e rimangono intatti per tutta la selezione. Potete anche recuperare i metadati delle risorse selezionate utilizzando questa funzionalità.

Il selettore delle risorse utilizza il messaggio HTML5 `Window.postMessage` per inviare al destinatario i dati per la risorsa selezionata. Funziona solo in modalità Sfoglia e solo con la pagina dei risultati Omnisearch.

Trasferite i seguenti parametri di richiesta in un URL per avviare il selettore risorse in un contesto particolare:

| Nome | Valori | Esempio | Scopo |
|---|---|---|---|
| suffisso risorsa (B) | Percorso della cartella come suffisso della risorsa nell&#39;URL:[https://localhost:4502/aem/assetpicker.html/&lt;percorso_cartella>](https://localhost:4502/aem/assetpicker.html) | Per avviare il selettore risorse con una particolare cartella selezionata, ad esempio con la cartella `/content/dam/we-retail/en/activities` selezionata, l&#39;URL deve essere del modulo: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | Se al momento dell’avvio del selettore delle risorse è necessario selezionare una determinata cartella, passatela come suffisso di risorsa. |
| `mode` | singolo, multiplo | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | In modalità multipla, potete selezionare più risorse contemporaneamente utilizzando il selettore delle risorse. |
| `dialog` | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Usate questi parametri per aprire il selettore delle risorse come finestra di dialogo Granite. Questa opzione è applicabile solo quando si avvia il selettore delle risorse tramite Granite Path Field e lo si configura come URL pickerSrc. |
| `root` | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | Utilizzate questa opzione per specificare la cartella principale per il selettore di risorse. In questo caso, il selettore delle risorse consente di selezionare solo le risorse secondarie (dirette/indirette) sotto la cartella principale. |
| `viewmode` | ricerca |  | Per avviare il selettore delle risorse in modalità di ricerca, con i parametri relativi al tipo di risorsa e al tipo di mime. |
| `assettype` | immagini, documenti, elementi multimediali, archivi. | <ul><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=images](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=multimedia](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=archives](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=archives)</li></ul> | Utilizzate l&#39;opzione per filtrare i tipi di risorse in base al valore fornito. |
| `mimetype` | Tipo MIME (`/jcr:content/metadata/dc:format`) di una risorsa (supportato anche il carattere jolly). | <ul><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=image/png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation&amp;mimetype=*png)</li></ul> | Utilizzatelo per filtrare le risorse in base al tipo MIME. |

Per accedere all’interfaccia del selettore delle risorse, passate a `https://[aem_server]:[port]/aem/assetpicker`. Individuate la cartella desiderata e selezionate una o più risorse. In alternativa, cercate la risorsa desiderata dalla casella di ricerca Omnico, applicate il filtro in base alle vostre esigenze, quindi selezionatela.

![Sfogliare e selezionare la risorsa nel selettore delle risorse](assets/assetpicker.png)

*Figura: Sfogliate e selezionate la risorsa nel selettore delle risorse.*

## Limitazioni  {#limitations}

La funzionalità di ricerca in [!DNL Experience Manager Assets] presenta le seguenti limitazioni:

* Non inserite uno spazio iniziale nella query di ricerca, altrimenti la ricerca non funziona.
* [!DNL Experience Manager] può continuare a visualizzare il termine di ricerca dopo che hai selezionato le proprietà di una risorsa dai risultati della ricerca e quindi hai annullato la ricerca.  <!-- (CQ-4273540) -->
* Durante la ricerca di cartelle, file e cartelle, i risultati della ricerca non possono essere ordinati in base ad alcun parametro.
* Se si seleziona `Return` senza digitare nella barra di ricerca Omnisearch, [!DNL Experience Manager] restituisce un elenco di soli file e non di cartelle. Se cercate specificamente delle cartelle senza utilizzare una parola chiave, [!DNL Experience Manager] non restituisce alcun risultato.

La ricerca visiva o la ricerca per similarità presenta le seguenti limitazioni:

* La ricerca visiva funziona meglio con un archivio di grandi dimensioni. Anche se non è richiesto un numero minimo di immagini per risultati ottimali, la qualità delle corrispondenze con alcune immagini non è altrettanto buona di quella delle corrispondenze di un grande archivio.
* Non è possibile modificare il modello o il treno [!DNL Experience Manager] per trovare immagini simili. Ad esempio, l&#39;aggiunta o la rimozione di smart tag ad alcune risorse non modifica il modello. Le risorse vengono effettivamente escluse dai risultati di ricerca visivamente simili.

La funzionalità di ricerca può presentare dei limiti di prestazioni nei seguenti scenari:

* Rispetto alla visualizzazione a elenco, la visualizzazione a schede presenta un tempo di caricamento più rapido per visualizzare i risultati della ricerca.

## Suggerimenti per la ricerca {#tips}

* Durante il monitoraggio dello stato di revisione delle risorse, utilizzate l&#39;opzione appropriata per individuare le risorse approvate o in attesa di approvazione.
* Utilizzate il predicato Insights per cercare le risorse supportate in base alle statistiche di utilizzo ottenute da diverse app Creative. I dati di utilizzo sono raggruppati in Valutazione utilizzo, Impressioni, Clic e Canali multimediali in cui le risorse appaiono categorie.
* Utilizzate la casella di controllo **[!UICONTROL Seleziona tutto]** per selezionare le risorse ricercate. [!DNL Experience Manager] inizialmente visualizza 100 risorse nella vista a schede e 200 risorse nella vista a elenco. Quando scorrete i risultati della ricerca, vengono caricate più risorse. Potete selezionare più risorse rispetto alle risorse caricate. Il conteggio delle risorse selezionate viene visualizzato nell’angolo superiore destro della pagina dei risultati della ricerca. Potete gestire la selezione, ad esempio scaricare le risorse selezionate, aggiornare le proprietà dei metadati in blocco per le risorse selezionate o aggiungere le risorse selezionate a una raccolta. Quando più risorse sono selezionate rispetto a quelle visualizzate, un’azione viene applicata a tutte le risorse selezionate oppure viene visualizzata una finestra di dialogo con il numero di risorse a cui sono applicate. Per applicare un’azione alle risorse non caricate, accertatevi che tutte le risorse siano selezionate in modo esplicito.
* Per cercare risorse che non contengono metadati obbligatori, consultate [mandatory metadata](#mandatorymetadata) (Metadati obbligatori).
* La ricerca utilizza tutti i campi di metadati. Una ricerca generica, come la ricerca di 12, in genere restituisce molti risultati. Per risultati ottimali, utilizzate virgolette doppie (non singole) o assicuratevi che il numero sia contiguo a una parola senza un carattere speciale (ad esempio `shoe12`).
* La ricerca full-text supporta operatori quali `-` e `^`. Per cercare queste lettere come stringhe letterali, racchiudere l&#39;espressione di ricerca tra virgolette. Ad esempio, utilizzare `"Notebook - Beauty"` invece di `Notebook - Beauty`.
* Se i risultati della ricerca sono troppi, limita l&#39;ambito [della ricerca](#scope) a zero sulle risorse desiderate. Questa funzione è particolarmente utile se avete qualche idea su come cercare meglio le risorse desiderate, ad esempio un tipo di file specifico, una posizione specifica, metadati specifici e così via.

* **Assegnazione tag**: I tag consentono di classificare le risorse che possono essere cercate e cercate in modo più efficiente. I tag consentono di estendere la tassonomia appropriata ad altri utenti e flussi di lavoro. [!DNL Experience Manager] offre metodi per assegnare automaticamente tag alle risorse utilizzando  servizi intelligenti di Adobe Sensei che consentono di aggiungere tag con utilizzo e formazione sempre più avanzati alle risorse. Quando ricercate le risorse, gli smart tag vengono inseriti se la funzione è attivata nel vostro account. Funziona insieme alla funzionalità di ricerca integrata. Vedere [comportamento di ricerca](#searchbehavior). Per ottimizzare l&#39;ordine di visualizzazione dei risultati di ricerca, è possibile [incrementare la classifica di ricerca](#searchrank) di alcune risorse selezionate.

* **Indicizzazione**: Nei risultati della ricerca vengono restituiti solo i metadati e le risorse indicizzati. Per una migliore copertura e migliori prestazioni, accertatevi che l&#39;indicizzazione sia corretta e seguite le best practice. Vedere [indicizzazione](#searchindex).

* Per escludere risorse specifiche dai risultati della ricerca, utilizzate la proprietà `excludedPath` nell&#39;indice di Lucene.

## Alcuni esempi illustrano la ricerca {#samples}

Usate virgolette doppie intorno alle parole chiave per trovare le risorse che contengono la frase esatta nell’ordine esatto specificato dall’utente.

![Comportamento di ricerca con e senza virgolette](assets/search_with_quotes.gif)

*Figura: Funzionamento della ricerca con e senza virgolette.*

**Cerca con carattere jolly asterisco**: Per ampliare la ricerca, usate un asterisco prima o dopo la parola di ricerca per far corrispondere un numero qualsiasi di caratteri. Ad esempio, la ricerca di un&#39;esecuzione senza un asterisco non restituisce risorse contenenti variazioni della parola (anche nei metadati). Un asterisco sostituisce qualsiasi numero di caratteri. Esempio,

* `run` restituisce le risorse con la parola chiave run esatta
* `run*` restituisce risorse con  `running`,  `run`,  `runaway`e così via.
* `*run` restituisce risorse con  `outrun`,  `rerun` e così via.
* `*run*` restituisce tutte le possibili combinazioni.

![Illustrazione dell’uso del carattere jolly asterisco nella ricerca delle risorse tramite un esempio](assets/search_with_asterisk_run.gif)

*Figura: Illustrazione dell’utilizzo del carattere jolly asterisco nella ricerca delle risorse tramite un esempio.*

**Cerca con il carattere jolly** punto interrogativo: Per ampliare la ricerca, utilizzare uno o più caratteri &#39;?&#39; caratteri per corrispondere al numero esatto di caratteri. Ad esempio, nell&#39;illustrazione seguente,

* `run???` la query non corrisponde ad alcuna risorsa.

* `run????` query restituisce la parola  `running` con quattro caratteri dopo  `run`.

* `??run` La query corrisponde alla parola  `rerun` con due caratteri prima  `run`.

![Illustrazione dell’uso del carattere jolly punto interrogativo nella ricerca di risorse tramite un esempio](assets/search_with_questionmark_run.gif)

*Figura: Illustrazione dell’uso del carattere jolly punto interrogativo nella ricerca di risorse tramite un esempio.*

**Escludere una parola chiave**: Usate il trattino per cercare risorse che non contengono una parola chiave. Ad esempio, la query `running -shoe` restituisce risorse contenenti `running`, ma non `shoe`. Analogamente, la query `camp -night` restituisce risorse contenenti `camp` ma non `night`. La query `camp-night` restituisce risorse contenenti sia `camp` che `night`.

![Utilizzo del trattino per cercare risorse non contenenti una parola chiave esclusa](assets/search_dash_exclude_keyword.gif)

*Figura: Utilizzo del trattino per cercare risorse non contenenti una parola chiave esclusa.*

## Attività di configurazione e amministrazione relative alla funzionalità di ricerca {#configadmin}

### Configurazioni indice di ricerca {#searchindex}

L&#39;individuazione delle risorse si basa sull&#39;indicizzazione dei contenuti DAM, inclusi i metadati. L’individuazione delle risorse è rapida e accurata e si basa su un’indicizzazione ottimizzata e configurazioni appropriate. Vedere [indice di ricerca](/help/assets/performance-tuning-guidelines.md#search-indexes), [query di quercia e indicizzazione](/help/sites-deploying/queries-and-indexing.md) e [best practice](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

Per escludere risorse specifiche dai risultati della ricerca, utilizzate la proprietà `excludedPath` nell&#39;indice di Lucene.

### Ricerca visiva o similare {#configvisualsearch}

La ricerca visiva utilizza i tag avanzati e richiede [!DNL Experience Manager] 6.5.2.0 o versione successiva. Dopo aver configurato la funzionalità di smart tag, effettuate le seguenti operazioni:

1. In [!DNL Experience Manager] CRXDE, nel nodo `/oak:index/lucene` aggiungere le proprietà e i valori seguenti e salvare le modifiche.

   * `costPerEntry` proprietà di tipo  `Double` con il valore  `10`.
   * `costPerExecution` proprietà di tipo  `Double` con il valore  `2`.
   * `refresh` proprietà di tipo  `Boolean` con il valore  `true`.

   Questa configurazione consente le ricerche dall&#39;indice appropriato.

1. Per creare l&#39;indice Lucene, in CRXDE, in `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, creare il nodo denominato `imageFeatures` di tipo `nt-unstructured`. In `imageFeatures` nodo,

   * Aggiungere la proprietà `name` di tipo `String` con il valore `jcr:content/metadata/imageFeatures/haystack0`.
   * Aggiungete la proprietà `nodeScopeIndex` di tipo `Boolean` con il valore di `true`.
   * Aggiungete la proprietà `propertyIndex` di tipo `Boolean` con il valore di `true`.
   * Aggiungere la proprietà `useInSimilarity` di tipo `Boolean` con il valore `true`.

   Salva le modifiche.

1. Accedere a `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` e aggiungere la proprietà `similarityTags` di tipo `Boolean` con il valore di `true`.
1. Applicate smart tag alle risorse presenti nell&#39;archivio [!DNL Experience Manager].
1. In CRXDE, nel nodo `/oak-index/damAssetLucene`, impostare la proprietà `reindex` su `true`. Salva le modifiche.
1. (Facoltativo) Se si dispone di un modulo di ricerca personalizzato, copiare il nodo `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` in `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Salva le modifiche.

Per informazioni correlate, vedere [come comprendere gli smart tag in  Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) e [come gestire gli smart tag](/help/assets/enhanced-smart-tags.md).

>[!CAUTION]
>
>Se l&#39;indicizzazione Lucene viene effettuata su [!DNL Adobe Experience Manager], la ricerca basata sugli smart tag non funziona come previsto.

### Metadati obbligatori {#mandatorymetadata}

Gli utenti aziendali, gli amministratori o i bibliotecari DAM possono definire alcuni metadati come metadati obbligatori che è un requisito indispensabile per il funzionamento dei processi aziendali. Per diversi motivi, ad alcune risorse potrebbero mancare questi metadati, ad esempio risorse legacy o risorse migrate in massa. Le risorse con metadati mancanti o non validi vengono rilevate e riportate in base alla proprietà dei metadati indicizzati. Per configurarlo, vedere [metadata obbligatori](/help/assets/metadata-schemas.md#define-mandatory-metadata).

### Modificare i facet di ricerca {#searchfacets}

Per migliorare la velocità di individuazione, [!DNL Experience Manager Assets] offre facet di ricerca con cui è possibile filtrare i risultati di ricerca. Per impostazione predefinita, il pannello Filtri include alcuni facet standard. Gli amministratori possono personalizzare il pannello Filtri per modificare i facet predefiniti utilizzando i predicati incorporati. [!DNL Experience Manager] fornisce una buona raccolta di predicati incorporati e un editor per personalizzare i facet. Vedere [facet di ricerca](/help/assets/search-facets.md).

### Estrarre testo durante il caricamento delle risorse {#extracttextupload}

Potete configurare [!DNL Experience Manager] per estrarre il testo dalle risorse quando gli utenti caricano risorse, come file PSD o PDF. [!DNL Experience Manager] indicizza il testo estratto e consente agli utenti di eseguire ricerche in base al testo estratto. Consultate [caricare risorse](/help/assets/manage-assets.md#uploading-assets).

Se l&#39;estrazione del testo richiede troppo risorse per la distribuzione, prendete in considerazione la possibilità di [disattivare l&#39;estrazione del testo](https://helpx.adobe.com/experience-manager/kb/Disable-binary-text-extraction-to-optimize-Lucene-indexing-AEM.html).

### Predefiniti personalizzati per filtrare i risultati di ricerca {#custompredicates}

I predicati vengono utilizzati per creare facet. Gli amministratori possono personalizzare i facet di ricerca nel pannello Filtri utilizzando i predicati preconfigurati. Questi predicati possono essere personalizzati utilizzando le sovrapposizioni. Consultate [creare predicati personalizzati](/help/assets/searchx.md).

Potete cercare risorse digitali in base a una o più delle seguenti proprietà. I filtri applicati ad alcune di queste proprietà sono disponibili per impostazione predefinita e altri filtri possono essere creati personalizzati per essere applicati alle altre proprietà.

| Campo di ricerca | Valori delle proprietà di ricerca |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Tipi MIME | Immagini, documenti, contenuti multimediali, archivi o altri elementi. |
| Ultima modifica | Ora, Giorno, Settimana, Mese o Anno. |
| Dimensione file | Piccolo, Medio o Grande. |
| Stato pubblicazione | Pubblicato o Non pubblicato. |
| Stato approvato | Approvato o Rifiutato. |
| Orientamento | Orizzontale, Verticale o Quadrato. |
| Stile | Colore o Bianco e nero. |
| Altezza video | Specificato come valore minimo e massimo. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |
| Larghezza video | Specificato come valore minimo e massimo. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |
| Formato video | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Il valore viene memorizzato nei metadati del video sorgente e delle eventuali rappresentazioni. |
| Codec video | x264. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |
| Bitrate video | Specificato come valore minimo e massimo. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |
| Codec audio | Libvorbis, Lame MP3, codifica AAC. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |
| Bitrate audio | Specificato come valore minimo e massimo. Il valore viene memorizzato solo nei metadati delle rappresentazioni video. |

## Utilizzo dei risultati di ricerca delle risorse {#aftersearch}

Con le risorse che hai cercato in [!DNL Experience Manager] puoi effettuare le seguenti operazioni:

* Visualizzare le proprietà dei metadati e altre informazioni.
* Scaricate una o più risorse.
* Utilizzate Azioni desktop per aprire queste risorse nell&#39;app desktop.
* Creare raccolte intelligenti.

### Ordinare i risultati della ricerca {#sort}

Ordinate i risultati della ricerca per individuare più rapidamente le risorse necessarie. È possibile ordinare i risultati della ricerca solo quando si seleziona **[[!UICONTROL File]](#searchui)** dal pannello **[!UICONTROL Filtri]**. [!DNL Assets] utilizza l’ordinamento lato server per ordinare rapidamente tutte le risorse all’interno di una cartella o nei risultati di una query di ricerca, indipendentemente dal numero. L’ordinamento lato server fornisce risultati più rapidi e precisi rispetto all’ordinamento lato client.

Potete ordinare i risultati della ricerca esattamente come potete ordinare le risorse in qualsiasi cartella. L&#39;ordinamento funziona su queste colonne: Nome, Titolo, Stato, Dimension, Dimensioni, Valutazione, Utilizzo, (Data) Creata, (Data) Modificata, (Data) Pubblicata, Flusso di lavoro e Estratta.

Per le limitazioni della funzionalità di ordinamento, vedere [limitazioni](#limitations).

### Controllare informazioni dettagliate su una risorsa {#checkinfo}

Potete controllare informazioni dettagliate su una risorsa ricercata dalla pagina dei risultati della ricerca.

Per visualizzare tutti i metadati di una risorsa, selezionate la risorsa e fate clic su **[!UICONTROL proprietà]** nella barra degli strumenti.

Per controllare i commenti relativi a una risorsa o alla sua cronologia della versione, fai clic sulla risorsa per aprirne l’anteprima di grandi dimensioni. Apri la timeline nella barra a sinistra e seleziona **[!UICONTROL Commenti]** o **[!UICONTROL Versioni]**. Puoi anche ordinare l’attività della timeline come commenti o versioni in ordine cronologico.

![Ordinare le voci della cronologia per una risorsa di ricerca](assets/sort_timeline_search_results.gif)

*Figura: Ordinare le voci della cronologia per una risorsa di ricerca.*

### Download delle risorse ricercate {#download}

Potete scaricare le risorse ricercate e le relative rappresentazioni esattamente come potete scaricare le risorse normali dalle cartelle. Selezionate una o più risorse dai risultati della ricerca e fate clic su **[!UICONTROL Scarica]** nella barra degli strumenti.

### Proprietà dei metadati di aggiornamento in blocco {#metadataupdates}

È possibile eseguire aggiornamenti in blocco ai campi di metadati comuni di più risorse. Dai risultati della ricerca, selezionate una o più risorse. Fare clic su **[!UICONTROL Proprietà]** nella barra degli strumenti e aggiornare i metadati come necessario. Fare clic su **[!UICONTROL Save and Close]** al termine. I metadati esistenti in precedenza nei campi aggiornati vengono sovrascritti.

Per le risorse disponibili in una singola cartella o raccolta, è più semplice [aggiornare i metadati in massa](/help/assets/metadata.md) senza utilizzare la funzionalità di ricerca. Per le risorse disponibili in più cartelle o che corrispondono a criteri comuni, è più rapido aggiornare in massa i metadati tramite la ricerca.

### Raccolte intelligenti {#smart-collections}

Una raccolta è un set ordinato di risorse che può includere risorse da posizioni diverse, perché le raccolte contengono solo riferimenti a tali risorse. Le raccolte sono dei due tipi seguenti:

* Un elenco di riferimento statico di risorse, cartelle e altre raccolte.
* Un elenco dinamico (raccolta avanzata) che popola le risorse nella raccolta in base a un criterio di ricerca.

Puoi creare raccolte avanzate in base ai criteri di ricerca. Dal pannello **[!UICONTROL Filtri]**, seleziona **[!UICONTROL File]** e fai clic su **[!UICONTROL Salva raccolta avanzata]**. Consulta la sezione [Gestisci raccolte](/help/assets/manage-collections.md).

## Risultati e problemi di ricerca imprevisti {#unexpectedresults}

| Errore, problemi, sintomi | Possibile motivo | Possibile correzione o comprensione del problema |
|---|---|---|
| Risultati errati durante la ricerca di risorse con metadati mancanti. | Durante la ricerca di risorse per le quali mancano i metadati obbligatori, [!DNL Experience Manager] potrebbe essere possibile visualizzare alcune risorse con metadati validi. I risultati si basano sulle proprietà dei metadati indicizzati. | Una volta aggiornati i metadati, è necessario reindicizzarli per riflettere lo stato corretto dei metadati delle risorse. Vedere [metadati obbligatori](metadata-schemas.md#define-mandatory-metadata). |
| Troppi risultati di ricerca. | Parametro di ricerca ampio. | Considerare la limitazione dell&#39; [ambito di ricerca](#scope). Gli smart tag consentono di ottenere più risultati di quanto previsto. Vedere [comportamento di ricerca con smart tag](#withsmarttags). |
| Risultati di ricerca non correlati o in parte correlati. | Il comportamento di ricerca cambia con l’assegnazione di smart tag. | Comprendere [come cambia la ricerca dopo l&#39;assegnazione di smart tag](#withsmarttags). |
| Nessun suggerimento di completamento automatico per le risorse. | Le risorse appena caricate non sono ancora indicizzate. I metadati non sono immediatamente disponibili come suggerimenti quando iniziate a digitare una parola chiave di ricerca nella barra di ricerca Omnyser. | [!DNL Experience Manager] attende la scadenza di un periodo di timeout (per impostazione predefinita, un’ora) prima di eseguire un processo in background per indicizzare i metadati per tutte le risorse caricate o aggiornate di recente e quindi aggiungere i metadati all’elenco dei suggerimenti. |
| Nessun risultato di ricerca. | <ul><li>Le risorse corrispondenti alla query non esistono. </li><li> Spazi bianchi aggiunti prima della query di ricerca. </li><li> Il campo di metadati non supportato contiene la parola chiave cercata.</li><li> Ricerca eseguita durante la disattivazione di una risorsa. </li></ul> | <ul><li>Effettuate ricerche utilizzando un&#39;altra parola chiave. In alternativa, potete usare tag avanzati o ricerche per similarità per migliorare i risultati della ricerca. </li><li>[Limitazione](#limitations) nota.</li><li>Non tutti i campi di metadati sono considerati come ricerche. Vedere [scope](#scope).</li><li>Effettuate ricerche in un secondo momento o modificate i tempi di attivazione e disattivazione delle risorse richieste.</li></ul> |
| Filtro di ricerca o predicato non disponibile. | <ul><li>Il filtro di ricerca non è configurato.</li><li>Non è disponibile per l&#39;accesso.</li><li>(Meno probabile) Le opzioni di ricerca non vengono personalizzate sulla distribuzione in uso.</li></ul> | <ul><li>Contattate l’amministratore per verificare se le personalizzazioni della ricerca sono disponibili o meno.</li><li>Contattate l’amministratore per verificare se l’account dispone dei privilegi o delle autorizzazioni necessari per utilizzare la personalizzazione.</li><li>Contattate l&#39;amministratore e controllate le personalizzazioni disponibili per la distribuzione [!DNL Assets] in uso.</li></ul> |
| Quando si ricercano immagini visivamente simili, manca un&#39;immagine prevista. | <ul><li>L&#39;immagine non è disponibile in [!DNL Experience Manager].</li><li>L&#39;immagine non è indicizzata. In genere, quando viene caricato di recente.</li><li>L&#39;immagine non è dotata di smart tag.</li></ul> | <ul><li>Aggiungete l&#39;immagine a [!DNL Assets].</li><li>Contattate l’amministratore per reindirizzare la directory archivio. Inoltre, accertatevi di utilizzare l&#39;indice appropriato.</li><li>Contattate l’amministratore per assegnare tag avanzati alle risorse pertinenti.</li></ul> |
| Quando si ricercano immagini visivamente simili, viene visualizzata un’immagine irrilevante. | Comportamento di ricerca visiva. | [!DNL Experience Manager] visualizza il maggior numero possibile di risorse potenzialmente rilevanti. Eventuali immagini meno rilevanti vengono aggiunte ai risultati, ma con una classificazione di ricerca più bassa. La qualità delle corrispondenze e la rilevanza delle risorse ricercate diminuiscono mano a mano che scorrete i risultati della ricerca. |
| Quando si selezionano e si utilizzano i risultati della ricerca, non vengono utilizzate tutte le risorse ricercate. | L&#39;opzione [!UICONTROL Seleziona tutto] seleziona solo i primi 100 risultati di ricerca nella vista a schede e i primi 200 risultati di ricerca nella vista a elenco. |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] guida all&#39;implementazione della ricerca](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Configurazione avanzata per migliorare i risultati della ricerca](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [Configurare la ricerca per la traduzione intelligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

