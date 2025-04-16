---
title: Note sulla versione per  [!DNL Adobe Experience Manager] 6.5
description: Trova informazioni sulla versione, novità, procedure di installazione e un elenco dettagliato delle modifiche per  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 461ec6a48bc41d46338c2c0162869525e49de97f
workflow-type: tm+mt
source-wordcount: '6138'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione Service Pack |
| Data | Giovedì 21 novembre 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Cosa è incluso in [!DNL Experience Manager] 6.5.22.0 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e correzioni di bug. Include inoltre miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la data di disponibilità iniziale di 6.5 di aprile 2019. [Installa il Service Pack ](#install) in [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Funzioni principali e miglioramenti

### Moduli {#forms-sp22}

Le funzionalità e i miglioramenti principali di questa versione includono:

#### Nuove funzioni GA in AEM Forms {#ga-aem-forms-sp22}

* È stato aggiunto il supporto per abilitare l&#39;incorporamento dei font nelle [API Batch di comunicazioni interattive](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel). Le comunicazioni interattive ora includono il supporto per l&#39;incorporamento dei font Adobe Ming e Adobe Myungjo nei PDF generati tramite l&#39;API Batch. Questo miglioramento garantisce un rendering accurato del testo nei documenti generati, anche quando si utilizzano sottoinsiemi di font, fornendo un migliore supporto per contenuti multilingue negli output di PDF.

* [API per l&#39;accesso facilitato di PDF](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api) - AEM Forms su OSGi ora supporta la nuova API per tag TOC per migliorare PDF per gli standard di accesso facilitato. Rende i PDF più accessibili agli utenti con tecnologia assistiva.

* [Risoluzione XDP del frammento](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository): AEM Forms su OSGi ora risolve gli XDP del frammento a cui si fa riferimento negli XDP primari e memorizzati nell&#39;archivio AEM CRX.

* [Miglioramenti alla conformità di PDF/A](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents) - Ora gli utenti possono convertire i PDF in formati PDF/A (1a, 2a, 3a) a scopo di archiviazione, garantendo al contempo l&#39;accessibilità e verificando la conformità a questi standard.

* **Supporto per il ridimensionamento automatico dei caratteri per i documenti PDF statici** - AEM Forms Designer, OutputService e FormsService ora supportano il ridimensionamento automatico dei caratteri per i PDF statici. Se l&#39;utente imposta la dimensione del carattere 0 per i campi di tipo testo, numerico, password o datetime, la dimensione del carattere viene regolata automaticamente all&#39;interno di questi campi senza modificare la dimensione complessiva del campo. Per utilizzare la funzione, gli utenti passano un flag nell&#39;XCI personalizzato: `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`.

#### Nuove funzioni di Beta in AEM Forms {#beta-aem-forms-sp22}

La funzione beta offre un’opportunità unica per ottenere accesso esclusivo alle innovazioni all’avanguardia e aiutarti a modellarne lo sviluppo. Ti interessa abilitare una funzione beta per i tuoi ambienti? Invia un’e-mail dal tuo indirizzo ufficiale a aem-forms-ea@adobe.com con l’elenco delle funzionalità che ti interessano.

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) e [Servizi CAPTCHA di Cloudflare Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md): AEM Forms supporta i seguenti servizi Captcha:
   * Captcha protegge i moduli da bot, spam e abusi automatizzati sfidando gli utenti con un widget di casella di controllo. Garantisce che solo gli utenti umani procedano, migliorando la sicurezza per le transazioni online.
   * Cloudflare Turnstile offre una misura di sicurezza che mira a proteggere i moduli da bot automatizzati, attacchi dannosi, spam e traffico automatizzato indesiderato. Presenta una casella di controllo all’invio del modulo per verificare che sia umana, prima di consentire loro di inviare il modulo.

* Controllo delle versioni dei moduli adattivi:
   * [Creare più versioni di un modulo adattivo](/help/forms/using/add-versioning-reviews-comments.md) - Ora gli utenti possono gestire facilmente le varianti dei moduli esistenti. Questo processo semplifica il controllo delle versioni e facilita il confronto per l’ottimizzazione dei moduli, il tutto all’interno di un unico flusso di lavoro semplificato.
   * [Confronta Forms adattivo](/help/forms/using/compare-forms-core-components.md): ora gli utenti possono confrontare facilmente due moduli per identificare le differenze. Questo semplifica la collaborazione consentendo ai membri del gruppo di confrontare le revisioni e discutere le modifiche in modo efficiente.

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

### Sites {#sites}

[L&#39;editor universale](/help/sites-developing/universal-editor/introduction.md) è ora disponibile in AEM 6.5 per i casi d&#39;uso headless con l&#39;applicazione di un feature pack.

### [!DNL Assets]

La scheda IPTC ora supporta [!UICONTROL Alt Text] e [!UICONTROL Extended Description] campi di testo. (ASSETS-34918)

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Sono stati risolti dei problemi in Service Pack 22 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### Accessibilità {#sites-accessibility-6522}

* Il pulsante di selezione del campione dell’annotazione non conteneva un nome accessibile. In altre parole, utilizzando un’utilità per la lettura dello schermo, non esiste un nome comprensibile che il pulsante possa selezionare dopo l’immissione di un nuovo valore esadecimale. (SITES-11992)
* I seguenti elementi nel menu della barra a sinistra vengono visualizzati come un elenco ma non sono contrassegnati come tali nell’assistente vocale:

   * Sito
   * Live Copy
   * Lancio
   * Copia per lingua
   * Cartella
   * Rapporto CSV (SITES-2874)

* La gestione dei contenuti web di base AEM richiede un’etichetta di accessibilità per i collegamenti ipertestuali nell’editor Rich Text. Quando si utilizza un collegamento ipertestuale nel componente testo, il tag di ancoraggio deve includere l&#39;attributo `aria-label` per garantire che gli assistenti vocali possano leggere e trasmettere con precisione il testo del collegamento a scopo di accessibilità. (SITES-11511)
* In AEM, gli elementi interattivi nell’intestazione della tabella nella Vista a elenco non hanno il ruolo &quot;pulsante&quot; richiesto. Di conseguenza, l’assistente vocale NVDA non annuncia i ruoli di pulsante previsti per le intestazioni di tabella seguenti: Titolo, Nome, Modificato, Pubblicato, Anteprima, Modello, Operazione, Flusso di lavoro. A ogni elemento interattivo nell’intestazione della tabella deve essere assegnato un ruolo &quot;pulsante&quot; per garantire la compatibilità con tecnologie per l’accessibilità come NVDA. (SITES-10962)


#### Interfaccia utente amministratore{#sites-adminui-6522}

* In alcuni casi di AEM, le funzionalità di anteprima e confronto delle versioni non funzionavano come previsto su diverse pagine. In particolare:

   * **Anteprima problema:** Quando si tenta di visualizzare l&#39;anteprima di una versione della pagina, viene inizialmente visualizzato un errore. Dopo un nuovo tentativo, l’anteprima restituisce una pagina vuota.
   * **Problema relativo al confronto delle versioni:** La funzionalità &quot;Confronta con corrente&quot; visualizza solo la versione corrente, senza evidenziare alcuna differenza tra le versioni. (SITES-23988)

* Nel campo Editor Rich Text (RTE) viene visualizzato un tag `<br>` imprevisto quando si utilizza l&#39;impostazione `defaultPasteMode` su `plaintext` durante un&#39;azione di copia e incolla. Questo problema determina un markup diverso per lo stesso contenuto, con conseguente traduzione dello stesso contenuto di testo due volte nella memoria di traduzione di un cliente. (SITES-23606)
* In AEM 6.5.20.0 è stato riscontrato un problema di funzionalità con la funzionalità **Gestisci pubblicazione**. Quando si seleziona un nodo e lo si pianifica per la pubblicazione futura, potrebbe venire visualizzato un messaggio di errore, ovvero &quot;Impossibile recuperare le risorse secondarie per gli elementi selezionati&quot;, quando si tenta di includere nodi secondari. Questo problema impediva l&#39;utilizzo dell&#39;opzione **Includi elementi figlio**, impedendo la pubblicazione completa della gerarchia dei contenuti prevista. (SITES-23000)
* La marca temporale &quot;Pubblicato&quot; di un modello non veniva aggiornata nell’ambiente di authoring, anche se il modello era stato replicato correttamente nelle istanze di pubblicazione. Il comportamento previsto prevedeva che la marca temporale sull’istanza di authoring riflettesse l’ultima pubblicazione, ma questo aggiornamento non si verificava come previsto. (SITES-21585)
* Si è verificata una discrepanza nel conteggio dei collegamenti in arrivo nell’ambiente di authoring di AEM. La barra laterale sinistra mostrava un numero inferiore di collegamenti rispetto all’interfaccia classica. Inoltre, alcuni collegamenti in entrata legittimi non funzionano. (SITES-24837)
* Venivano segnalati tempi di caricamento molto lunghi durante la visualizzazione delle versioni delle pagine nella vista Timeline di AEM. La visualizzazione delle versioni impiegava fino a 19 minuti. Questo problema era in corso dal momento dell’aggiornamento da AEM 6.4.8 a 6.5.18, interrompendo in modo significativo l’efficienza del flusso di lavoro. (SITES-22468 &amp; SITES-22467)

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* In AEM 6.5.17 aggiornato, il salvataggio dei frammenti di contenuto ha provocato il seguente errore: *ERRORE: impossibile salvare il frammento di contenuto.* (SITES-22993)
* È stato identificato un problema con un risolutore risorse non chiuso in `ContentFragmentModelOmniSearchHandler` sull&#39;editore in AEM. (SITES-24903)


#### [!DNL Content Fragments] - Amministratore{#sites-admin-6522}

Facendo clic sul collegamento nella notifica e-mail, l’utente viene indirizzato al visualizzatore o all’editor di risorse predefinito. Lo fa invece dell’editor dei frammenti di contenuto, anche quando la risorsa nel flusso di lavoro è considerata un frammento di contenuto. (SITES-24338)


#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6522}

Quando si utilizzano frammenti di contenuto con elementi di campo Testo su più righe, il markup generato durante la query tramite GraphQL non manteneva la formattazione specificata in HTML. Ad esempio, manca una nuova riga dopo l’elenco. L&#39;effetto è stato che l&#39;ultimo paragrafo è diventato parte dell&#39;elenco. (SITES-23233)


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### Back-end core{#sites-core-backend-6522}

* Sono stati segnalati `SegmentNotFoundException` errori ricorrenti in un&#39;istanza Autore AEM. Il riavvio dell’autore ha temporaneamente risolto il problema, ma è stata necessaria una correzione a lungo termine per evitare ulteriori occorrenze. (SITES-22573)
* È stato sollevato un problema relativo alla funzionalità della timeline in AEM Sites, in particolare per quanto riguarda la gestione delle proprietà `cq:lastModified` mancanti nelle annotazioni. Dopo l’applicazione di AEM 6.5.20, non era chiaro se il contenuto esistente dovesse essere corretto per la proprietà mancante o se la timeline fosse stata aggiornata per funzionare correttamente in sua assenza. (SITES-21861)


#### Componenti core{#sites-core-components-6522}

* A seguito di un aggiornamento da AEM 6.5.18 a 6.5.21, è stato identificato un problema relativo alla funzionalità che controlla l’utilizzo live dei componenti. Quando si tentava di scorrere la pagina Utilizzo live per trovare elementi aggiuntivi, la tabella non riusciva a caricare altri risultati anche se nell’interfaccia utente veniva visualizzato &quot;Caricamento di altri elementi&quot;. (SITES-23919)
* È stato segnalato un problema relativo alla convalida dei campi obbligatori in una finestra di dialogo di un componente AEM contenente due schede. La scheda 1 includeva un editor Rich Text (RTE) e campi di testo, mentre la scheda 2 conteneva campi di percorso e campi di testo. Sebbene tutti i campi siano contrassegnati come obbligatori (`required=true`), le notifiche di errore persistono in modo errato nella scheda 1, anche dopo la compilazione di tutti i campi obbligatori. Al contrario, gli errori nella scheda 2 vengono cancellati come previsto. (SITES-23243)
* Dopo la migrazione ad AEM 6.5.21, l&#39;istruzione `data-sly-include` di HTML Template Language non funzionava più come previsto, in particolare non supportando le espressioni `appendPath` e `prependPath`. Di conseguenza, l’output della risorsa inclusa non veniva renderizzato correttamente, anche se funzionava correttamente prima della migrazione. Questo problema causava errori di rendering per le risorse che si basano su queste espressioni per la manipolazione dei percorsi. (GRANITE-52970)


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### Frammenti di esperienza{#sites-experiencefragments-6522}

* I frammenti esperienza non vengono ordinati in base al titolo come previsto quando si fa clic sull&#39;intestazione di colonna **Titolo** nella visualizzazione elenco. Si osserva uno sfarfallio rapido dello schermo, ma non si ordina. (SITES-23706)

* In AEM 6.5.17 è stato riscontrato un problema durante la conversione di un componente pagina in un frammento di esperienza utilizzando la funzione standard. Dopo la conversione, il frammento di esperienza è apparso vuoto durante la modifica, nonostante venisse visualizzato correttamente nella pagina in cui è stato utilizzato. Il problema è stato generato da una creazione di nodi errata: il nodo del componente è stato posizionato all’esterno del nodo principale/contenitore, violando la struttura del modello. Per ripristinare la modificabilità del frammento, era necessario spostare manualmente il nodo del componente nel nodo principale/contenitore corretto. (SITES-22974)

* Dopo la migrazione da AEM 6.5.11 a 6.5.20, le configurazioni cloud nei frammenti di esperienza non venivano salvate correttamente. Anche se le configurazioni sono state salvate in `crx/de`, non verranno visualizzate alla riapertura della console Configurazioni, a indicare un problema di persistenza. (SITES-22287)


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### Lanci{#sites-launches-6522}

Quando si aggiungono risorse di Frammenti di esperienza utilizzando il filtro di assegnazione tag nella produzione di AEM, l&#39;utente ha potuto selezionarlo, ma ha riscontrato un errore dopo aver selezionato **Crea copia per lingua**. Il comportamento previsto prevedeva che la risorsa Frammento esperienza selezionata dal filtro sui tag dovesse essere aggiunta al progetto di traduzione. (SITES-24152)

#### Verifica collegamenti{#sites-link-checker-6522}

LinkCheckerTask non riesce ad eseguire l&#39;autenticazione perché il client HTTP tenta di eseguire NTLM prima dell&#39;autenticazione di base, causando il blocco degli utenti da parte del proxy dopo più tentativi non riusciti. Il sistema deve invece utilizzare l&#39;autenticazione di base per eseguire l&#39;autenticazione sul proxy, consentendo il corretto funzionamento dei servizi LinkCheckerTask. (SITES-25034)


#### MSM - Live Copy{#sites-msm-live-copies-6522}

* Quando i tag robot SEO vengono applicati alla copia principale e distribuiti nelle pagine Live Copy, i valori sono visualizzati correttamente in `crx/de`. Tuttavia, i valori non venivano riportati nell’interfaccia utente nelle Proprietà pagina delle pagine Live Copy. (SITES-23475)
* Gli errori relativi ai lanci venivano visualizzati quando si tentava di promuovere un lancio tramite l’interfaccia utente. La procedura guidata Promuovi lancio è rimasta vuota, impedendo il completamento del processo di promozione. (SITES-19718)
* Sono sorti problemi con i Frammenti di esperienza in AEM in seguito ai tentativi di creazione di Live Copy ed esecuzione di rollout. Il problema si è verificato quando gli utenti hanno rilevato un errore `NotFound` durante il tentativo di tornare alla schermata di gestione dei frammenti di esperienza dalla schermata Rollout. (SITES-21933)


#### Editor pagina{#sites-pageeditor-6522}

* Il pulsante Annulla ha modificato la posizione del componente, oltre a modificare il testo nell’ultima versione. (SITES-17465)
* Quando un componente contenitore copiato veniva incollato, veniva visualizzato visivamente due volte, generando tre istanze sulla pagina. Tuttavia, dopo aver aggiornato la pagina, il duplicato è scomparso, suggerendo che il problema fosse probabilmente un problema visivo temporaneo. (SITES-21890)
* Quando si naviga nel riquadro a sinistra Componenti utilizzando i tasti TAB o MAIUSC+TAB, più elementi di testo non erano chiaramente visibili, sia visivamente che in modalità tabulazione. Questo problema influiva sull’accessibilità, rendendo difficile identificare o interagire con questi componenti durante la navigazione da tastiera. (SITES-2266)

#### Replica{#sites-replication-6522}

In AEM 6.5.18 e 6.5.19, al momento della disattivazione di una pagina padre, venivano generate più richieste di disattivazione per ogni pagina figlio. Questo problema causava anche l’annullamento in blocco della pubblicazione degli endpoint GraphQL. (NPR-42075 E NPR42010)


### [!DNL Assets]{#assets-6522}

* Quando si utilizza la funzione Connected Assets, gli aggiornamenti apportati in AEM Assets non si riflettono sull’ambiente AEM Sites. (ASSETS-42344)
* Problemi relativi allo stato di pubblicazione delle risorse quando si spostano le risorse da una posizione a un’altra in Experience Manager. (ASSETS-41158)
* Il caricamento delle risorse tramite API genera un messaggio di errore `unclosed resource resolver`. (ASSETS-41049)
* Problemi con la query di riferimento `AssetReferenceResolverImpl` dopo l&#39;aggiornamento a Adobe Experience Manager, Service Pack 21. (ASSETS-40384)
* In AEM versione 6.5.19, quando si rimuove un’opzione dai risultati del pannello di ricerca, vengono deselezionate anche tutte le altre caselle di controllo disponibili. (ASSETS-37335)
* I valori indesiderati vengono visualizzati nell&#39;output di Excel durante l&#39;operazione di esportazione di massa dei metadati. (ASSETS-37260)
* In AEM versione 6.5.19, quando carichi un file SVG in formato UTF-8, l’output risulta sfocato. (ASSETS-36616)
* Opzione `Fetch original rendition for Dynamic Media Connected Assets` mancante nella configurazione di Connected Assets. (ASSETS-41726)
* Le proprietà della risorsa vengono salvate anche se non si definisce un valore per i campi obbligatori. (ASSETS-37914)
* Se lo stato di elaborazione di una risorsa è Non riuscito o Metadati non riusciti, i sottotitoli e le tracce audio dell’interfaccia utente non funzionano in modo appropriato. (ASSETS-37281)
* Quando salvi i metadati di una risorsa e provi a modificarli, il nome della lingua non viene visualizzato. (ASSETS-37281)

#### [!DNL Dynamic Media]{#assets-dm-6522}

Un problema di produzione ha interrotto il processo di migrazione quando non è stato possibile caricare un video in Dynamic Media. Nell’interfaccia utente veniva visualizzato un errore di errore di processo. (ASSETS-36038)

<!--

### [!DNL Forms]{#forms-6522}

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.22.0 Forms add-on package release is scheduled for Thursday, November 28, 2024. A list of Forms fixes and enhancements is added to this section post the release.

-->

### Moduli {#forms-bug-fixes-sp22}

* Gli URL generati per gli allegati nelle bozze salvate in AEM Forms non riflettono le mappature configurate di Apache Sling Resource Resolver Factory. (FORMS-16949)
* Quando un utente di AEM Forms Service Pack 19 (6.5.19.0) visualizza l&#39;anteprima di una lettera, il contenuto non viene allineato correttamente, poiché gli spazi risultano mancanti e il carattere `x` viene visualizzato in alcune posizioni. (FORMS-16670)
* Quando un utente su AEM Forms Service Pack 18 (6.5.18.0) tenta di stampare i file utilizzando il protocollo CIFS, l&#39;operazione non riesce e viene visualizzato il messaggio di errore: (FORMS-16629)
  `ALC-OUT-001-401: Unknown error while printing using CIFS on the Printer: \\\\\\\\NSMVPLUETEST01\\\\TH_Test`.
* Quando un utente esegue l&#39;aggiornamento da AEM Forms Service Pack 17 (6.5.17.0) ad AEM Forms Service Pack 20 (6.5.20.0), l&#39;icona dell&#39;editor di regole non viene visualizzata a livello del Contenitore modulo. (FORMS-16430)
* Quando un utente esegue l&#39;aggiornamento da AEM Forms Service Pack 17 (6.5.17.0) ad AEM Forms Service Pack 21 (6.5.21.0), il percorso dell&#39;URL di invio del modulo adattivo modificato non funziona. (FORMS15894
* In AEM Forms Service Pack 19 (6.5.19.0), la convalida di AEM Forms 6.5 PDF/A non riesce per alcuni file con errore `creation date and modification date mismatch with timezone`, mentre viene eseguita senza problemi nella convalida di Acrobat Pro PDF/A per un controllo di conformità. (FORMS-15840)
* Quando un utente elimina le bozze dei moduli utilizzando il componente &quot;Bozze e invii&quot; in una pagina del sito in AEM Forms Service Pack 15 (6.5.15.0) su OSGi, l&#39;eliminazione non riesce. (FORMS-15755)
* Quando un utente dispone di un elenco SharePoint con più di 999 voci e il modulo include un allegato, l’invio del modulo non riesce. (FORMS-15057)
* Viene aggiunta una regola di convalida per garantire che la data di fine non sia precedente alla data di inizio, insieme a uno script personalizzato per il messaggio di convalida. Tuttavia, la convalida non viene attivata quando la data di fine è precedente alla data di inizio. (FORMS-14757)
* Quando un utente utilizza la funzionalità Mostra/Nascondi in una tabella di un modulo adattivo, la dimensione del campo si riduce. La dimensione del campo si corregge quando si aggiunge e si rimuove una riga. (FORMS-14756)
* Quando un utente stampa moduli in AEM Forms Service Pack 19 (6.5.19.0), alcuni moduli non vengono riprodotti correttamente sul server, causando errori durante il processo di stampa. (FORMS14734
* Quando un utente esegue l&#39;aggiornamento da AEM Forms Service Pack 15 (6.5.15.0) a Service Pack 19 (6.5.19.0), si verifica un problema. Un pattern di visualizzazione personalizzato impostato come `num{$zzz,zz9.99}` non viene riprodotto correttamente nell&#39;anteprima e nell&#39;interfaccia utente dell&#39;agente. (FORMS-14694)
* Quando un utente visualizza l’anteprima di una lettera in una comunicazione interattiva con un XML dati salvato, la lettera si blocca nello stato &quot;Caricamento&quot; nell’interfaccia utente di AEM. La visualizzazione in anteprima della lettera con lo stesso XML funziona correttamente. (FORMS-14521)
* In AEM Forms Service Pack 20 (6.5.20.0), gli utenti che inviano e-mail con allegati utilizzando il pulsante Invia e-mail nei moduli adattivi notano un problema. Il nome dell&#39;allegato viene visualizzato sulla riga successiva anziché in linea. (FORMS-14426)
* Quando un utente genera un PDF in AEM Forms con elenchi puntati impostati sullo stile predefinito &quot;Disco&quot;, PDF non riesce a eseguire il controllo dell’accessibilità nello strumento di accessibilità di Adobe Acrobat. L’elenco con stili &quot;Punto elenco&quot; e &quot;Quadrato&quot; supera il controllo di accessibilità. (FORMS-13802, LC-3922179)
* Quando un utente esegue l’aggiornamento da AEMForms-6.5.0-0065 a AEMForms-6.5.0-0087 durante la configurazione di JBoss® RHEL8 standalone, non riesce a connettersi al contenitore del servizio LiveCycle. (FORMS-15907)*
* In AEM Forms su JEE, in AEM Workspace, la selezione di un modulo precedentemente inviato per avviare un nuovo processo di modulo causa un problema. Forms con dati precompilati sovrascrive tutti i dati inviati in precedenza, rimuovendo i campi compilati manualmente. (FORMS-15376)
* In AEM Forms Service Pack 20 (6.5.20.0), quando un utente converte il file Tiff in PDF utilizzando il servizio PDFG, l&#39;operazione non riesce e viene restituito l&#39;errore: (FORMS-14879) ALC-PDG-011-028-Error durante la conversione del file di immagine di input in PDF. com/sun/image/codec/jpeg/JPEGCodec
* Aggiornamento in AEM Forms sui file JAR JEE: la libreria `commons-collections:commons-collections:jar` è ora inclusa per migliorare la risoluzione e la funzionalità delle dipendenze in vari processi JEE di AEM Forms, ad esempio:
   * Miglioramento del processo assemblatore per migliorare l’elaborazione dei processi e la gestione degli errori.
   * Miglioramento del processo PDF Generator (PDFG) per garantire operazioni più fluide per la generazione e la conversione dei documenti.
   * Miglioramento del processo di aggiornamento LC-Upgrade per migliorare il processo di aggiornamento garantendo al contempo una transizione stabile tra le versioni.
   * Miglioramento del processo Rights Management per garantire la gestione dei documenti e migliorare le funzionalità di Rights Management.
   * Gestione dei processi Miglioramento dei processi per un&#39;elaborazione dei processi e una gestione del sistema più affidabili.
* A partire da AEM Forms OSGi 6.5.22, l’operazione renderPDFForm del servizio Forms non eseguirà script solo client (runAt=client) sul server; solo quelli contrassegnati come runAt=server o runAt=both verranno eseguiti come descritto nella tabella seguente. (FORMS-16564)

  | Script contrassegnato come runAt | Eseguito sul server |
  |---------------------|-------------------------|
  | server | sì |
  | entrambi | sì |
  | client | no |

#### XLFM {#forms-xmlfm-sp22}

* In AEM Forms Service Pack 21 (6.5.21.0), quando un utente aggiunge tag non standard ai PDF utilizzando XMLFM, il documento non è conforme ai requisiti delle specifiche PDF. (LC-3922484)
* Quando un utente genera un PDF utilizzando il servizio di output di AEM Forms Service Pack 20 (6.5.20.0), l&#39;operazione non riesce e viene visualizzato CORBA.COMM_FAILURE: `15:04:35,973 ERROR [com.adobe.formServer.PA.XMLFormAgentWrapper] (default task-14) ALCOUT-002-013: XMLFormFactory, PAexecute failure: "org.omg.CORBA.COMM_FAILURE"`. Il servizio viene passato correttamente quando il ruolo di accessibilità &quot;Riferimento&quot; viene escluso dal sottomodulo del modello XDP. tuttavia, questo ruolo è necessario per la conformità 508. (LC-3922402)
* Quando un utente converte un modulo XFA in un AcroForm PDF, l’operazione ha esito negativo. (LC-3922363)
* In AEM Forms Service Pack 19 (6.5.19.0) quando un utente crea un XDP con sottomaschere senza nome, FS_DATA_SOM appare vuoto per le sottomaschere senza nome. (LC-3922034)

#### Forms Designer {#forms-designer-sp22}

* Quando un utente apre una libreria di frammenti selezionando una cartella di frammenti in AEM Forms Designer versione 6.5.21.0, si verifica un arresto anomalo. (LC-3922439)
* Quando un utente disinstalla AEM Forms Designer versione 6.5.20.0 a 32 bit e installa AEM Forms Designer versione 6.5.21.0, Forms Designer non si avvia. I registri di errore mostrano un’allocazione di memoria insufficiente per Java Runtime Environment (JRE). (LC-3922404)
* Dopo che un utente ha installato AEM Forms Designer versione 6.5.20.0, l&#39;opzione Macro non viene visualizzata nel menu. Viene visualizzata solo la macro &#39;Verifica accessibilità&#39; predefinita e l&#39;esecuzione non riesce. (LC-3922321)
* Quando un utente aggiunge un nuovo percorso per il modello per la creazione di XDP in AEM Forms Designer versione 6.5.20.0, Forms Designer si blocca. (LC-3922316)
* Quando un utente genera l&#39;output utilizzando il metodo ExportData in AEM Forms 6.5 Service Pack 15 (6.5.15.0) OSGI, vengono generati dati incompleti e non corretti. (LC-3922340)


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### Foundation {#foundation-6522}

Nella console AEM Assets si è verificato un problema durante il tentativo di riordinare i documenti DITA. La breadcrumb nella parte superiore della finestra di dialogo del browser percorsi visualizza erroneamente il nome del nodo invece del titolo del nodo per l’elemento padre principale. Il titolo corretto del nodo viene visualizzato solo dopo aver selezionato un elemento all’interno della breadcrumb, indicando un errore di visualizzazione temporaneo. (NPR-42106)


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### Communities {#foundation-communities-6522}

Dopo l&#39;aggiornamento da AEM 6.5.19 a 6.5.20, è emerso un problema che impediva la corretta chiusura di `Connection evic` thread dopo le chiamate a `UgcSearch`. Questo problema, osservato nell’ambiente di produzione, causa la persistenza e l’accumulo di questi thread nel tempo, con un potenziale impatto sulle prestazioni. (NPR-42019)


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* L&#39;ordinamento non funziona come per **Gruppi** nel menu a sinistra in Gestione pacchetti CRX. (GRANITE-53277)
* Gestione pacchetti in AEM limita l’installazione di versioni di pacchetti inferiori per impostazione predefinita, ma consente installazioni forzate di versioni precedenti. Tuttavia, l’utilizzo dell’opzione di installazione forzata può interferire con le installazioni future tramite la pipeline standard. Ad esempio, se è installata la versione 1.21 e viene aggiunta la versione 1.24, l’installazione ha esito positivo e vengono elencate entrambe le versioni. Tuttavia, il tentativo di installare la versione 1.22 su 1.24 non riesce attraverso la pipeline, ma funziona se installato forzatamente, elencando tutte le versioni. Analogamente, l’installazione della versione 1.23 è bloccata se è già presente la versione 1.24, in quanto la pipeline non consente il downgrade. (GRANITE-53263)


#### Granite{#foundation-granite-6522}

* I pacchetti snapshot venivano installati in AEM utilizzando i comandi CURL. Durante l’installazione, il programma di installazione JCR ha analizzato i pacchetti tramite il programma di installazione OSGI per garantire che non siano necessari bundle o configurazioni OSGI aggiuntivi. Se una versione del pacchetto conteneva &quot;SNAPSHOT&quot;, il programma di installazione OSGI attivava VLT per creare un pacchetto snapshot corrispondente. Tuttavia, poiché ogni istanza di AEM Author esegue il proprio programma di installazione OSGI, entrambe le istanze possono tentare di generare lo snapshot contemporaneamente, causando conflitti di sessione all’interno dell’archivio. (NPR-42003)
* Conflitto di blocco in `ScriptDependencyResolver` con AEM 6.5.21. (GRANITE-53181)
* Dopo l&#39;aggiornamento di AEM a 6.5.21, si sono verificati problemi quando si utilizzavano percorsi relativi nella sintassi HTL (Sightly), ad esempio `data-sly-use`. (GRANITE-53080)


#### Integrazioni{#foundation-integrations-6522}

* È stata aggiunta l’istruzione di attribuzione legale per l’interfaccia utente di Cloud Services. (FORMS-16373)
* Aggiunta delle autorizzazioni di lettura per l&#39;utente **fd-cloudservice** per accedere alle configurazioni hCaptcha e Turnstile, consentendo il recupero dell&#39;ID client e del segreto client necessari per il rendering e la convalida captcha. Inoltre, è stato implementato un modello di elenco di controllo di accesso per gestire l’accesso a queste configurazioni. (FORMS-16360)


#### Localizzazione{#foundation-localization-6522}

In ![Icona martello](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) Strumenti > **Sicurezza** > ![Icona utente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **Utenti**, nella pagina Gestione utente, i dati nella colonna **Stato** della tabella venivano visualizzati in verticale. (GRANITE-48304)


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### Platform{#foundation-platform-6522}

* Il tracciamento di Enterprise Information Management introdotto in AEM 6.5.18 ha causato anomalie nel calcolo dei punteggi di adozione dei prodotti. La libreria delle metriche di Adobe ha causato questo problema sovrascrivendo i dati utente forniti dalla libreria di tracciamento Omega. Di conseguenza, i punteggi di adozione per molti clienti di AEM Sites e AEM Assets sono scesi a zero a partire da febbraio 2024. (CQ-4358438)
* È stato identificato un problema critico nell’ambiente di produzione in cui Garbage Collector gestiva i tag in modo errato. In particolare, quando un tag è stato spostato o rinominato, Garbage Collector non è riuscito ad aggiornare la proprietà `cq:MovedTo`, causando la scomparsa del tag dalle pagine. (CQ-4358293)
* Un problema con ContextHub in AEM 6.5.19 causava la risoluzione errata dei segmenti quando un percorso di contesto veniva aggiunto a un’istanza AEM. Il problema ha interessato in modo specifico il campo URL all’interno degli oggetti JavaScript generati dal componente Pagina, in cui mancava il prefisso del percorso di contesto richiesto. Questa omissione impediva ai segmenti di funzionare come previsto. (SITES-21852)
* Aggiornamento di AEM Quickstart per l&#39;utilizzo della libreria `commons-collections-3.2.2-adobe-2`. L’aggiornamento garantisce il corretto funzionamento dell’applicazione. (NPR-42150)
* La configurazione di SMTP OAuth2 in AEM 6.5 differisce in modo significativo da quella utilizzata in AEM as a Cloud Service. Per semplificare la configurazione e garantire coerenza, era necessario allineare la configurazione in AEM 6.5 con gli standard utilizzati in AEM as a Cloud Service. (GRANITE-53273)
* È stato riscontrato un problema quando si è fatto clic su ![Icona bussola](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg) > ![Icona progetto](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg) Progetti, quindi si è posizionato il puntatore del mouse sopra ![Icona barra a sinistra](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![Icona freccia giù](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg), un accento grave è apparso prima del testo della descrizione comando &quot;Solo contenuto&quot;. (CQ-4356633)

#### Sicurezza{#foundation-security-6522}

* Sono stati riscontrati problemi con una libreria di crittografia JSAFE obsoleta (versione 6.0.0) in AEM. In AEM 6.5.22 è incluso un bundle con patch nella versione 6.2.5 di JSAFE. (NPR-42006)
* Durante la convalida dei protocolli consentiti durante i controlli XSS, i gestori si confrontano con &quot;http&quot; e &quot;https&quot;. La proprietà `protocol` di un oggetto URL ha restituito questi valori con due punti finali, ad esempio `http:` e `https:`. Questa mancata corrispondenza ha causato problemi di convalida. Per garantire un’analisi accurata, il controllo del protocollo doveva tenere conto dei due punti o regolare di conseguenza la logica di confronto.  (NPR-42119)
* Dopo aver installato AEM 6.5.21 (la versione precedente era AEM 6.5.19) su IBM® WebSphere® Liberty Profile e Semeru Java 8.0, non è stato possibile aprire alcuna pagina. I registri di errori indicavano problemi relativi alle versioni dei servlet richiesti da bundle diversi. Per risolvere questo problema, è stato necessario ripristinare la dipendenza da `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` perché era correlata al problema. (NPR-42116)
* Diversi browser stanno gradualmente eliminando il supporto per i cookie **SameSite=None**, utilizzati per consentire l&#39;accesso ai cookie tra siti diversi. In alternativa, verranno introdotti **cookie partizionati**. Questi cookie isolano l’archiviazione dal contesto in cui vengono utilizzati, migliorando la privacy e la sicurezza impedendo il tracciamento tra siti e consentendo al contempo ai cookie di funzionare all’interno di partizioni specifiche, ad esempio contenuto incorporato di terze parti. (GRANITE-51953)


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### Traduzione{#foundation-translation-6522}

* È stato aggiunto il supporto per le recenti modifiche nei Componenti core alle regole di traduzione predefinite. (NPR-42029)
* È stato identificato un problema con l’esportazione di file XLIFF in AEM Forms. Quando si utilizzava l&#39;opzione **Esporta selezione come XLIFF (solo stringhe)**, la sequenza dei componenti non veniva mantenuta in modo coerente. Tuttavia, la sequenza rimane corretta quando si esporta XLIFF per una lingua specifica. Sono stati forniti due file per dimostrare il problema: **DE-CH_Export.xliff** (sequenza corretta) e **String_Export.xliff** (sequenza errata). (NPR-42118)


#### Interfaccia utente{#foundation-ui-6522}

* `coralui-component-dialog` stava modificando il posizionamento di `cq-dialog-actions`, potenzialmente influenzando il layout o il comportamento dei pulsanti di azione nelle finestre di dialogo di AEM. (NPR-42294)
* La funzionalità del selettore colore in AEM non funzionava correttamente. Una volta effettuato l’accesso, veniva visualizzata una finestra modale vuota, che impediva la selezione del colore. Questo problema è iniziato dopo l’installazione di AEM 6.5.20 nell’ambiente Stage. Il selettore colore ha funzionato correttamente *prima* dell&#39;aggiornamento. (NPR-42163)
* In ![Icona Martello](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Strumenti** > **Flusso di lavoro** > **Modelli** > Seleziona un modello > **Avvia flusso di lavoro**, l&#39;icona Sfoglia non era presente nel campo Payload della finestra di dialogo **Esegui flusso di lavoro**. (NPR-42162)


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A -->


## Installa [!DNL Experience Manager] 6.5.22.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0 richiede [!DNL Experience Manager] 6.5. Per istruzioni dettagliate, consulta la [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md). <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del Service Pack è disponibile in Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip).
* In una distribuzione con MongoDB e più istanze, installare [!DNL Experience Manager] 6.5.22.0 in una delle istanze di authoring utilizzando Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe consiglia di non rimuovere o disinstallare il pacchetto [!DNL Experience Manager] 6.5.22.0. Pertanto, prima di installare il pacchetto, è necessario creare un backup di `crx-repository` nel caso sia necessario eseguirne il rollback. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installare il Service Pack in [!DNL Experience Manager] 6.5{#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). Adobe consiglia di riavviare il sistema se il tempo di attività corrente di un’istanza è elevato.

1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup dell&#39;istanza [!DNL Experience Manager].

1. Scarica il Service Sack da [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, vedere [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Selezionare il pacchetto, quindi selezionare **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l’istanza dopo l’installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l’istanza. Vedi [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Talvolta la finestra di dialogo nell’interfaccia utente di Gestione pacchetti si chiude durante l’installazione del Service Pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di avere la certezza che l’installazione sia andata a buon fine. Questo problema si verifica in genere nel browser [!DNL Safari], ma può verificarsi in modo intermittente in qualsiasi browser.

**Installazione automatica**

Per installare [!DNL Experience Manager] 6.5.22.0 è possibile utilizzare due metodi diversi.<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto nella cartella `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza l&#39;API HTTP [da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzare `cmd=install&recursive=true` per installare i pacchetti nidificati.

>[!NOTE]
>
>Experience Manager 6.5.22.0 non supporta l&#39;installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalida l&#39;installazione**

Per informazioni sulle piattaforme certificate per l&#39;utilizzo di questa versione, vedere i [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager (6.5.22.0)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tutti i bundle OSGi sono **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** nella console OSGi (usa la console Web: `/system/console/bundles`).

1. La versione del bundle OSGi `org.apache.jackrabbit.oak-core` è 1.22.20 o successiva (utilizzare la console Web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Installa Service Pack per [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Per istruzioni sull&#39;installazione del Service Pack in Experience Manager Forms, vedere [Istruzioni di installazione del Service Pack di Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funzione Forms adattivo, disponibile in [QuickStart per AEM 6.5](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), è progettata esclusivamente a scopo di esplorazione e valutazione. Per l’utilizzo in produzione, è essenziale ottenere una licenza valida per AEM Forms, in quanto la funzionalità Adaptive Forms richiede una licenza appropriata.

### Installare il pacchetto di indice GraphQL per i frammenti di contenuto Experience Manager{#install-aem-graphql-index-add-on-package}

I clienti che utilizzano GraphQL devono installare il [Frammento di contenuto Experience Manager con pacchetto indice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

In questo modo puoi aggiungere la definizione dell’indice richiesta in base alle funzioni effettivamente utilizzate.

Se non si installa questo pacchetto, è possibile che le query GraphQL risultino lente o non riuscite.

>[!NOTE]
>
>Installare il pacchetto una sola volta per istanza; non è necessario reinstallarlo con ogni Service Pack.

### UberJar{#uber-jar}

UberJar per [!DNL Experience Manager] 6.5.22.0 è disponibile nel [archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Per utilizzare UberJar in un progetto Maven, vedi [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includi nel POM del progetto la seguente dipendenza: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell&#39;archivio centrale di Maven anziché nell&#39;archivio pubblico Maven di Adobe (`repo.adobe.com`). Il file UberJar principale è stato rinominato in `uber-jar-<version>.jar`. Non esiste alcun `classifier`, con `apis` come valore, per il tag `dependency`.


## Funzioni obsolete e rimosse{#removed-deprecated-features}

Vedere [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md/).

## Problemi noti{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


* **Correlato ad Oak**
Da Service Pack 13 e versioni successive è stato avviato il seguente log degli errori che influisce sulla cache di persistenza:

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  Oppure

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Per risolvere l&#39;eccezione, eseguire le operazioni seguenti:

   1. Elimina le due cartelle seguenti da `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Installa il Service Pack o riavvia Experience Manager as a Cloud Service.
Le nuove cartelle di `cache` e `diff-cache` vengono create automaticamente e non si verifica più un&#39;eccezione relativa a `mvstore` in `error.log`.

* Aggiorna le query GraphQL che potrebbero aver utilizzato un nome API personalizzato per il modello di contenuto in modo da utilizzare il nome predefinito del modello di contenuto.

* Una query GraphQL può utilizzare l&#39;indice `damAssetLucene` anziché l&#39;indice `fragments`. Questa azione potrebbe causare l’errore o richiedere molto tempo per l’esecuzione delle query GraphQL.

  Per risolvere il problema, è necessario configurare `damAssetLucene` in modo da includere le due proprietà seguenti in `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Dopo aver modificato la definizione dell&#39;indice, è necessario reindicizzare (`reindex` = `true`).

  Dopo questi passaggi, le query GraphQL dovrebbero funzionare più rapidamente.

* Quando si tenta di spostare, eliminare o pubblicare frammenti di contenuto, siti o pagine, si verifica un problema durante il recupero dei riferimenti ai frammenti di contenuto. La query in background non riesce. In altre parole, la funzionalità non funziona.
Per garantire il corretto funzionamento, è necessario aggiungere le seguenti proprietà al nodo di definizione dell&#39;indice `/oak:index/damAssetLucene` (non è richiesta alcuna reindicizzazione):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Se si aggiorna l&#39;istanza di [!DNL Experience Manager] dalla versione 6.5.0 alla versione 6.5.4 al Service Pack più recente in Java™ 11, vengono visualizzate `RRD4JReporter` eccezioni nel file `error.log`. Per interrompere le eccezioni, riavviare l&#39;istanza di [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Gli utenti possono rinominare una cartella in una gerarchia in [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene ripubblicata.

* Durante l&#39;installazione di [!DNL Experience Manager] 6.5.x.x potrebbero essere visualizzati i seguenti errori e messaggi di avviso:
   * &quot;Quando l&#39;integrazione Adobe Target è configurata in [!DNL Experience Manager] utilizzando l&#39;API Target Standard (autenticazione IMS), l&#39;esportazione di frammenti di esperienza in Target genera la creazione di tipi di offerta errati. Invece del tipo &quot;Frammento di esperienza&quot;/sorgente &quot;Adobe Experience Manager&quot;, Target crea diverse offerte con il tipo &quot;HTML&quot;/sorgente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nessuna finestra di manutenzione trovata in `granite/operations/maintenance`.
   * La convalida lato server di Moduli adattivi non riesce quando vengono utilizzate funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nessuna finestra di manutenzione trovata in `granite/operations/maintenance`.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro per l&#39;annullamento della registrazione.

* A partire da AEM 6.5.15, il motore JavaScript Rhino fornito dal bundle ```org.apache.servicemix.bundles.rhino``` ha un nuovo comportamento di posizionamento. Gli script che utilizzano la modalità rigorosa (```use strict;```) devono dichiarare le variabili corrette. In caso contrario, non vengono eseguiti e finiscono per generare un errore di runtime.

* Se si installa il contenuto predefinito correlato ai tag tramite un pacchetto di aggiornamento ufficiale, la proprietà Languages del nodo `/content/cq:tags` viene ripristinata sul valore predefinito. Questa azione è valida per Service Pack, Service Pack di sicurezza, Feature Pack estesi, Feature Pack cumulativi, patch e così via. Pertanto, è necessario aggiungerlo dalle proprietà prima dell’installazione.

### Problema noto per AEM Sites {#known-issues-aem-sites-6522}

* Frammenti di contenuto-Anteprima non riuscita a causa della protezione DoS per una grande struttura ad albero di frammenti. Vedi l&#39;articolo [KB sulle opzioni di configurazione predefinite di GraphQL Query Executor](https://experienceleague.adobe.com/it/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)


### Problemi noti per AEM Forms {#known-issues-aem-forms-6522}

* Se la conversione da HTML a PDF non riesce su un server SUSE® Linux® (SLES 15 SP6 e versioni successive) con il seguente errore:

  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
quindi impostare la variabile di ambiente seguente e riavviare il server:
  `OPENSSL_CONF=/etc/ssl`

* Dopo aver installato AEM Forms JEE Service Pack 21 (6.5.21.0), se trovi voci duplicate dei file jar Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` nella cartella `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926), effettua le seguenti operazioni per risolvere il problema:

   1. Fermate i localizzatori, se sono in esecuzione.
   1. Arresta il server AEM.
   1. Passare a `<AEM_Forms_Installation>/lib/caching/lib`.
   1. Rimuovere tutti i file patch Geode ad eccezione di `geode-*-1.15.1.2.jar`. Verificare che siano presenti solo i file jar Geode con `version 1.15.1.2`.
   1. Apri il prompt dei comandi in modalità amministratore.
   1. Installare la patch Geode utilizzando il file `geode-*-1.15.1.2.jar`.

* Se un utente tenta di visualizzare in anteprima una bozza di lettera con dati XML salvati, per alcune lettere specifiche si blocca nello stato `Loading`. Per scaricare e installare l&#39;aggiornamento rapido, consulta l&#39;articolo [Aggiornamenti rapidi di Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-14521)

* Dopo l&#39;aggiornamento ad AEM Forms Service Pack 6.5.21.0, il servizio `PaperCapture` non è in grado di eseguire operazioni OCR (riconoscimento ottico dei caratteri) sui PDF. Il servizio non genera output sotto forma di PDF o file di registro. Per scaricare e installare l&#39;aggiornamento rapido, consulta l&#39;articolo [Aggiornamenti rapidi di Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (CQDOC-21680)

* Quando si esegue l’aggiornamento da AEM 6.5 Forms Service Pack 18 o 19 a Service Pack 20 o 21, si verifica un errore di compilazione JSP. Questo errore impediva loro di aprire o creare moduli adattivi. Inoltre, ha causato problemi con altre interfacce AEM. Tali interfacce includevano l’editor pagina, l’interfaccia utente di AEM Forms, l’editor flusso di lavoro e l’interfaccia utente per la panoramica del sistema. (FORMS-15256)

  In caso di problemi di questo tipo, effettua le seguenti operazioni per risolverli:
   1. Passare alla directory `/libs/fd/aemforms/install/` in CRXDE.
   1. Eliminare il bundle con il nome `com.adobe.granite.ui.commons-5.10.26.jar`.
   1. Riavvia il server AEM.

* Dopo l&#39;aggiornamento ad AEM Forms Service Pack 20 (6.5.20.0) con il componente aggiuntivo Forms, le configurazioni basate sul servizio Adobe Analytics Cloud legacy che utilizzano l&#39;autenticazione basata sulle credenziali cessano di funzionare. Questo problema impediva la corretta esecuzione delle regole di analisi. Per scaricare e installare l&#39;aggiornamento rapido, consulta l&#39;articolo [Aggiornamenti rapidi di Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-15428)

* Quando un utente si aggiorna a AEM Forms Service Pack 20 (6.5.20.0) sul server JEE e genera PDF utilizzando i servizi di output, i PDF vengono riprodotti con problemi di accessibilità. Per scaricare e installare l&#39;aggiornamento rapido, consulta l&#39;articolo [Aggiornamenti rapidi di Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922112)
* Quando un utente genera PDF con tag utilizzando il servizio di output su JEE, viene visualizzato il messaggio di avvertenza sulla struttura inappropriata. Per scaricare e installare l&#39;aggiornamento rapido, consulta l&#39;articolo [Aggiornamenti rapidi di Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922038)
* Quando un modulo viene inviato in AEM Forms JEE, le istanze di un elemento XML ripetuto vengono rimosse dai dati. Per scaricare e installare l&#39;aggiornamento rapido, consulta l&#39;articolo [Aggiornamenti rapidi di Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922017)
* Quando un utente in un ambiente Linux® esegue il rendering di un modulo adattivo (su JEE) in HTML, il rendering non riesce. Per scaricare e installare l&#39;aggiornamento rapido, consulta l&#39;articolo [Aggiornamenti rapidi di Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921957)
* Quando un utente converte un file XTG in formato PostScript utilizzando il servizio di output in AEM Forms JEE, l&#39;operazione non riesce e viene visualizzato l&#39;errore: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. Per scaricare e installare l&#39;aggiornamento rapido, consulta l&#39;articolo [Aggiornamenti rapidi di Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921720)
* Dopo l&#39;aggiornamento ad AEM Forms Service Pack 18 (6.5.18.0) sul server JEE, quando un utente invia un modulo, non riesce a eseguire il rendering degli arresti anomali di HTML5 o PDF forms e XMLFM. Per scaricare e installare l&#39;aggiornamento rapido, consulta l&#39;articolo [Aggiornamenti rapidi di Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921718)
* Nell’anteprima di stampa dell’interfaccia utente di Interactive Communications Agent, il simbolo di valuta (ad esempio il simbolo del dollaro $) viene visualizzato in modo incoerente per tutti i valori dei campi. Viene visualizzato per valori fino a 999 ma non per valori di 1000 e superiori. (FORMS-16557)
* Eventuali modifiche apportate all’XDP dei frammenti di layout nidificati in una comunicazione interattiva non vengono riportate nell’editor IC. (FORMS-16575)
* Nell’anteprima di stampa dell’interfaccia utente di Interactive Communications Agent, alcuni valori calcolati non vengono visualizzati correttamente. (FORMS-16603)
* Quando la lettera viene visualizzata in Anteprima di stampa, il contenuto viene modificato. In altre parole, alcuni spazi scompaiono e alcune lettere vengono sostituite con una &quot;x&quot;. (FORMS-15681)
* Quando un utente configura un&#39;istanza WebLogic 14c, il servizio PDFG in AEM Forms Service Pack 21 (6.5.21.0) su JEE in esecuzione su JBoss® non riesce a causa di conflitti del caricatore di classi che interessano la libreria SLF4J. L’errore viene visualizzato come segue (CQDOC-22178):

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature
  ```

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in questa versione di [!DNL Experience Manager] 6.5 Service Pack:

* [Elenco dei bundle OSGi inclusi in Experience Manager 6.5.22.0](/help/release-notes/assets/65220-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.22.0](/help/release-notes/assets/65220-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti Web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedervi, contatta il tuo account manager Adobe.

* [Download del prodotto all&#39;indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta L&#39;Assistenza Clienti Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina prodotto](https://business.adobe.com/it/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Iscriviti agli aggiornamenti dei prodotti con priorità Adobe](https://www.adobe.com/subscription/priority-product-update.html)
