---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6.5
description: Trova informazioni sulla versione, novità, procedure di installazione e un elenco dettagliato delle modifiche per [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
contentOwner: Rick Brough
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 56b13809475a59f188750b86503e316e69171fe1
workflow-type: tm+mt
source-wordcount: '7273'
ht-degree: 3%
---
# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## Riepilogo delle versioni {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.26.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione del Service Pack |
| Data | 12 novembre 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |


<!-- REWRITE AI GENERATED SUMMARY OF NOTES BELOW FOR EACH NEW SERVICE PACK RELEASE -->

Experience Manager 6.5.26.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e correzioni di bug. Include inoltre miglioramenti a livello di accessibilità, localizzazione, prestazioni, stabilità e sicurezza basati sulla base 6.5 disponibile da aprile 2019.

Gli elementi di rilievo del Service Pack 26 sono i seguenti:

* Sicurezza. Due correzioni critiche chiudono una vulnerabilità di inserimento di modelli lato server nell’Editor metadati e violazioni cross-site scripting (XSS) nei servlet dell’interfaccia utente Coral.
* Conformità C2PA. Assets ora rileva le credenziali C2PA e firma le rappresentazioni generate dal flusso di lavoro Aggiorna risorsa. La firma viene eseguita localmente in ogni istanza e l’infrastruttura di firma dedicata o di proprietà del cliente non è supportata.
* Accessibilità. Oltre 25 correzioni aiutano l’Editor pagina e la console Sites a soddisfare i requisiti di contrasto, tastiera e utilità per la lettura dello schermo delle linee guida WCAG.
* Localizzazione. Decine di correzioni traducono stringhe e correggono problemi di layout in Sites, Assets, Security e Operations.
* Affidabilità Sono stati risolti i conflitti di blocco degli indirizzi GraphQL nelle istanze di pubblicazione, nei rollout MSM, nelle azioni della barra degli strumenti dell’Editor Rich Text e nell’attivazione delle pagine nell’interfaccia classica.
* Analytics. L’integrazione di Launch utilizza l’API di Adobe Analytics 2.0 prima della fine del ciclo di vita di Analytics 1.4, il 31 agosto 2026.


<!-- UPDATE FOR EACH NEW RELEASE -->

## Problemi risolti, miglioramenti e miglioramenti in Service Pack 26 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6526}

#### Accessibilità {#sites-accessibility-6526}

* Gli autori possono aggiungere, spostare e rimuovere componenti utilizzando solo la tastiera. L’interazione di trascinamento della selezione ha richiesto l’uso di un puntatore, pertanto non è riuscito il criterio WCAG 2.1.1 Keyboard. L’editor ora fornisce i componenti Inserisci a comparsa, Taglia e Incolla ed Elimina come equivalenti utilizzabili da tastiera. (SITES-25359)

* Gli autori possono ora visualizzare il pulsante Formato (&quot;T&quot;) attivo nel menu in linea del componente Testo. Dopo che gli autori hanno applicato la formattazione in grassetto o corsivo, l’icona del pulsante è rimasta scura su uno sfondo grigio scuro e non ha rispettato il rapporto di contrasto minimo di 4,5:1 delle linee guida WCAG 2.1 AA. Il CSS aggiornato schiarisce l’icona, ripristinando il contrasto fornito dai service pack precedenti. (SITES-51864)

* Nella scheda Assets dell’Editor pagina ora viene visualizzata una stringa tradotta nel menu a discesa Seleziona componenti, dopo aver scelto Paragrafi dal menu a discesa Immagini. In precedenza, la stringa &quot;OTHER&quot; appariva in inglese perché mancava nelle risorse di localizzazione. Il dizionario aggiornato fornisce la traduzione in tutte le lingue. (SITES-24525)




* L’iframe ContextHub nell’Editor pagina ora dispone di un attributo titolo descrittivo. In precedenza, l&#39;elemento `contexthub-ui-iframe` non aveva alcun titolo, pertanto gli utenti di utilità di lettura dello schermo non erano in grado di identificarlo quando lo stato attivo veniva spostato su di esso. Il titolo ora viene visualizzato in ogni pagina e visualizzazione dell’editor, inclusi Canvas, Side Rail e Layout Preview. (SITES-24650)
* Il pulsante Filtri nella barra dei filtri della console Sites non aggiunge etichette visibili sopra i campi Ricerche salvate e Seleziona directory di ricerca. Un controllo di audit ha segnalato che le etichette venivano visualizzate quando lo stato attivo lasciava il pulsante, quando veniva premuto un tasto o quando si faceva clic sul pulsante. Il test non è riuscito a riprodurre il comportamento, quindi non è stata necessaria alcuna modifica. (SITES-24706)
* I collegamenti nella console Sites per la navigazione nelle app ora si distinguono più chiaramente. Il testo del collegamento ha un rapporto di contrasto di 4,5:1, ma lo spessore sottile e le dimensioni ridotte del carattere hanno reso i collegamenti difficili da vedere. Un font più grande e dimensioni maggiori facilitano la lettura del testo per gli utenti con disabilità visive. (SITES-24723)
* Gli assistenti vocali non visualizzano più il messaggio &quot;vuoto&quot; prima del contenuto della descrizione comando nella finestra modale Preferenze utente. In precedenza, l&#39;icona Info utilizzava `role="tooltip"` con un riferimento `aria-labelledby`, quindi NVDA leggeva prima un&#39;etichetta vuota. L&#39;icona ora utilizza `role="button"` e un `aria-label` di &quot;informazioni&quot; e la modifica si applica ai componenti del modulo Coral che condividono il modello. (SITES-24732)
* Il pulsante Elimina nella finestra modale Elimina ora soddisfa il requisito di contrasto di 4.5:1 delle linee guida WCAG 1.4.3. In precedenza, il testo bianco su sfondo rosso dava un rapporto di 3,9:1 dopo che gli autori avevano selezionato un elemento e fatto clic su Elimina nella barra degli strumenti Azione. Il colore più scuro del pulsante rende l’etichetta leggibile per gli autori con disabilità visive. (SITES-24772)
* L&#39;intestazione Riferimenti nella barra Riferimenti della console Sites ora utilizza un elemento intestazione invece di `div`. In precedenza, gli assistenti vocali non riuscivano ad annunciare il testo come intestazione, pertanto gli utenti non riuscivano a spostarsi per intestazione. L&#39;intestazione viene visualizzata anche nella parte superiore della vista Riferimenti iniziale. (SITES-24967)
* L’indicatore di messa a fuoco per i pulsanti a soffietto nella barra dei filtri della console Sites ora soddisfa il requisito di contrasto 3:1 di WCAG 1.4.11. In precedenza, l’indicatore blu mostrava un rapporto di 2,3:1 sullo sfondo, il che rendeva difficile trovare il pulsante del Pannello a soffietto Tag per gli utenti che utilizzano la tastiera. Il colore aggiornato offre agli utenti della tastiera un chiaro segnale di messa a fuoco. (SITES-24986)
* L’indicatore della messa a fuoco per i pulsanti di scelta nella barra dei filtri della console Sites ora soddisfa il requisito di contrasto WCAG 1.4.11 di 3:1. In precedenza, l&#39;indicatore blu chiaro mostrava un rapporto di 1,7:1 sullo sfondo. Gli utenti che utilizzano la tastiera ora possono tenere traccia della loro posizione nel pannello a soffietto Data di modifica. (SITES-24987)
* Il pulsante Seleziona accanto ai campi Percorso e Tag nella barra laterale dell’Editor pagina non utilizza più un’icona di casella di controllo. In precedenza, l’icona suggeriva di attivare o disattivare il pulsante, ma quest’ultimo apriva una finestra modale contenente la directory ad albero. Il pulsante Select ora comunica correttamente la sua funzione e lo stesso vale per i moduli Image e Teaser. (SITES-25210)
* Gli assistenti vocali ora ignorano le miniature delle risorse nella barra laterale dell’Editor pagina. Precedentemente, ogni immagine conteneva del testo alternativo che duplicava il nome della risorsa visibile, in modo che gli utenti potessero ascoltare lo stesso testo due volte. Un attributo `alt` vuoto contrassegna l&#39;immagine come decorativa e mantiene il nome nel titolo della scheda. (SITES-25213)
* Gli assistenti vocali riconoscono l’elenco dei componenti della barra laterale come un elenco. Un controllo di audit ha segnalato gli elementi come elementi non correlati, ma il test ha confermato che il markup utilizza un elemento elenco e voci elenco. Non è stata necessaria alcuna modifica del codice. (SITES-25214)
* Le icone delle informazioni per i componenti nella barra laterale dell’Editor pagina sono più grandi e più facili da visualizzare. In precedenza, le icone utilizzavano dimensioni molto piccole, pari a circa 12 px, difficili da vedere per gli utenti con disabilità visive. Le icone ora utilizzano le dimensioni medie.(SITES-25217)
* L’indicatore di stato attivo sul pulsante Campione nella finestra modale Annotazione ora si distingue dal pulsante. In precedenza, l’indicatore corrispondeva al colore del campione. Ciò rendeva difficile per gli utenti di tastiera vedere quale pulsante aveva lo stato attivo. Un offset fornisce all&#39;indicatore un contrasto sufficiente rispetto allo sfondo e lo mantiene chiaramente visibile. (SITES-25253)
* Il campo Data nella finestra modale Timewarp non contiene più `aria-haspopup="dialog"`. In precedenza, gli assistenti vocali avevano annunciato che il campo apriva una finestra di dialogo, anche se non lo faceva. La rimozione dell’attributo fornisce agli utenti di utilità di lettura dello schermo informazioni accurate. (SITES-25263)
* Le etichette di testo nella barra degli strumenti Demografia, ad esempio &quot;Consigliato&quot;, soddisfano ora il requisito di contrasto di 4.5:1 delle linee guida WCAG 1.4.3. In precedenza, il testo grigio su uno sfondo grigio scuro restituiva un rapporto di 2,8:1 in modalità Anteprima. Testo più scuro o più chiaro, a seconda dello sfondo, rende leggibile ogni etichetta. (SITES-25307)
* L’indicatore di focus sui pulsanti Commerce, Persona e Device nella barra degli strumenti Demografia soddisfa ora il requisito di contrasto WCAG 1.4.11 di 3:1. In precedenza, l’indicatore mostrava un rapporto di 1,9:1 sullo sfondo della barra degli strumenti. Gli utenti che utilizzano la tastiera ora possono tenere traccia della loro posizione. (SITES-25308)
* Il testo digitato dagli autori nei campi di testo della barra degli strumenti Demografia soddisfa ora il requisito di contrasto di 4.5:1 delle linee guida WCAG 1.4.3. In precedenza, il testo bianco su sfondo grigio produceva un rapporto di 2,9:1 nei campi, ad esempio nel campo a discesa Profilo `displayName` in modalità Anteprima. I colori aggiornati consentono agli autori con disabilità visive di leggere i valori digitati. (SITES-25318)
* Gli assistenti vocali ora leggono la descrizione quando lo stato attivo raggiunge le caselle di controllo nelle finestre di dialogo Teaser, Immagine e Carosello. In precedenza, il testo non era associato alla casella di controllo a livello di programmazione, pertanto gli utenti non potevano ascoltare le istruzioni. Un attributo `aria-describedby` collega ora ogni casella di controllo alla relativa descrizione. (SITES-25364)
* Gli assistenti vocali ora annunciano quale pulsante Formati di paragrafo è attivo nell’Editor Rich Text. In precedenza, la selezione di un&#39;opzione dall&#39;elenco non forniva alla tecnologia per l&#39;accessibilità alcuna indicazione sulla scelta corrente. Il pulsante attivo ora contiene `aria-current="true"` e l&#39;opzione Target collegamento ipertestuale attivo contiene `aria-selected="true"`. (SITES-25367)
* I pulsanti Ordina nell’intestazione della tabella della Vista a elenco della console Sites soddisfano ora il requisito di contrasto 3:1 delle linee guida WCAG 1.4.11. In precedenza, le icone grigio chiaro mostravano un rapporto di 1,5:1 sullo sfondo dell’intestazione. Il colore più scuro dell’icona rende i pulsanti visibili agli autori con disabilità visive. (SITES-25372)
* La scheda Assets nella barra laterale dell’Editor pagina non viene più ricaricata quando lo stato attivo si sposta sul campo Filtro. In precedenza, quando si selezionava il campo vuoto, veniva attivato un ricaricamento e gli assistenti vocali annunciavano ogni volta un messaggio di caricamento. La scheda ora viene ricaricata solo dopo aver modificato il valore del filtro e aver premuto Invio. (SITES-25377)
* L’icona campione selezionata nella finestra modale Annotation soddisfa ora il requisito di contrasto WCAG 1.4.11 di 3:1. In precedenza, il segno di spunta bianco mostrava un rapporto di appena 1,58:1 sui campioni di colore giallo, arancione e verde. L’icona aggiornata fornisce agli autori con disabilità visive un chiaro indicatore. (SITES-25523)
* L’elenco Componenti nel pannello laterale dell’Editor pagina non è più attivo dalla tastiera. Gli utenti che utilizzano la tastiera selezionano e spostano i componenti con i controlli nella finestra del contenuto, pertanto l’elenco dei pannelli laterali ha ripetuto la funzione. Una nota sotto il filtro del componente indica agli utenti della tastiera dove trovare i controlli. (SITES-40752)


#### Interfaccia utente amministratore{#sites-adminui-6526}


#### Interfaccia classica{#sites-classicui-6526}

* Gli autori possono attivare nuovamente le pagine nella console Sites dell&#39;interfaccia classica (`siteadmin.html`). In precedenza, il pulsante Attiva pagina mostrava un’icona di selezione &quot;Caricamento&quot; a tempo indefinito e non attivava mai la replica, perché uno script di tracciamento non riuscito arrestava il gestore di clic. Il gestore di clic ora viene eseguito senza errori e completa l’attivazione. (SITES-52165)
* Il codice della lingua indonesiana viene ora visualizzato come ID nelle proprietà della copia in lingua. In precedenza, la barra Riferimenti mostrava il codice legacy IN per le pagine sotto la directory principale della lingua indonesiana. L’aggiornamento del bundle cq-wcm-core corregge il valore, in modo che il codice corrisponda allo standard ISO. (SITES-4491)

<!--
#### Component Console{#sites-component-console-6526}



#### [!DNL Content Fragments]{#sites-contentfragments-6526}



#### [!DNL Content Fragments] - Admin{#sites-admin-6526}
-->


#### [!DNL Content Fragments] - Editor frammento{#sites-fragments-editor-6526}

* Il pulsante Modifica frammento di contenuto viene visualizzato immediatamente per ogni riferimento a più campi nell’editor frammento di contenuto. In precedenza, il pulsante rimaneva nascosto fino a quando gli autori non salvavano il frammento principale e non faceva nulla dopo aver aperto il browser Percorsi. L’editor ora crea l’elenco delle azioni al primo rendering, in modo che gli autori aprano i frammenti di riferimento senza passaggi aggiuntivi. (SITES-43733)

* I caratteri cinesi, giapponesi e coreani non vengono più visualizzati in corsivo nel segnaposto della finestra di dialogo Crea frammento di contenuto. In precedenza, lo stile corsivo veniva applicato ai caratteri CJK in **Assets** > **File**, rendendo difficile la lettura del testo. Gli stili aggiornati ignorano il corsivo per le lingue CJK. (SITES-43548)
* L’editor del frammento di contenuto convalida correttamente i campi dopo l’aggiornamento dell’interfaccia utente Granite. Una recente modifica dell’interfaccia utente di Granite ha causato una regressione, pertanto le librerie client dell’editor non corrispondono più al nuovo comportamento di convalida. Le librerie e i test adattati risolvono la mancata corrispondenza. (SITES-46650)


#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6526}

* Le query GraphQL sui frammenti di contenuto ora riconoscono i riferimenti RemoteRef a Dynamic Media con OpenAPI Assets. In precedenza, le query non riuscivano con un &quot;Errore di convalida query persistente&quot; e non restituivano dati sulle risorse quando AEM 6.5 Sites utilizzava AEM as a Cloud Service Assets. Le risposte ora includono l’ID dell’archivio e l’ID della risorsa, in modo che i clienti possano creare gli URL di consegna. (SITES-48507)

* Le istanze di pubblicazione rimangono reattive durante il traffico GraphQL intenso. Blocca il conflitto in `GraphQLServiceImpl` thread di elaborazione delle richieste ritardati ai metodi dello schema, rallentando le richieste e richiedendo riavvii. La sincronizzazione migliorata risolve il problema delle prestazioni e mantiene la disponibilità dei siti e delle app mobili. (SITES-48699)

* Il messaggio sulla pagina GraphQL Endpoints rimane localizzato dopo il ricaricamento della pagina. In precedenza, al momento della creazione e dell’eliminazione degli endpoint, nella tua lingua veniva visualizzato il messaggio &quot;Nessun endpoint trovato&quot;, ma dopo un ricaricamento veniva ripristinato l’inglese. La pagina ora carica la stringa tradotta a ogni visita. (SITES-43586)


<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6526}
-->


#### [!DNL Content Fragments] - Modelli e Editor modelli{#sites-models-model-editor-6526}

* Le miniature per i modelli per frammenti di contenuto vengono visualizzate in **Strumenti** > **Generale** > **Modelli per frammenti di contenuto** quando il nome della configurazione contiene caratteri localizzati, ad esempio &quot;español テスト&quot;. In precedenza, la miniatura caricata non veniva visualizzata perché i caratteri causavano un errore nel percorso. La gestione aggiornata codifica correttamente il nome. (SITES-39242)

* La stringa Etichetta campo nell’area di lavoro dell’Editor modello per frammenti di contenuto ora viene visualizzata nella lingua dell’utente. In precedenza, l’etichetta rimaneva in inglese dopo che gli autori avevano trascinato un componente sull’area di lavoro, e tradotto solo dopo aver salvato e riaperto il modello. L’etichetta ora si traduce immediatamente, corrispondente al pannello Proprietà. (SITES-45383)


<!--
#### [!DNL Content Fragments] - REST API{#sites-restapi-6526}

#### ContextHub{#sites-contexthub-6526}
-->


#### Back-end core{#sites-core-backend-6526}

* L’attivazione pianificata della pagina tramite l’ora di attivazione viene ora eseguita solo quando necessario. `OnOffTriggerProcessor` ha attivato in precedenza la replica e l&#39;annullamento della validità della cache troppo spesso, costringendo gli autori a ripubblicare il contenuto manualmente. La correzione backported elimina l’elaborazione non necessaria e ripristina la pubblicazione pianificata affidabile. (SITES-48483)

* Il caricamento dei file funziona per le risorse remote da Gestione risorse di nuova generazione in un campo multiplo. In precedenza, il caricamento non riusciva quando gli autori sceglievano una risorsa remota per un campo all’interno di un campo multiplo. L’aggiornamento dei Componenti core ripristina il flusso di caricamento, in modo che il campo accetti la risorsa. (SITES-44266)


#### Componenti core{#sites-core-components-6526}

* Il selettore risorse remote mantiene separata l’immagine di ogni elemento con più campi. In precedenza, quando si selezionava un’immagine in un elemento con più campi, questa veniva applicata a tutti gli altri elementi e il riferimento della risorsa remota non veniva salvato. Ogni elemento ora contiene la propria selezione e il riferimento persiste dopo il salvataggio della finestra di dialogo. (SITES-42376)

* Questa versione include correzioni backported per Commerce, Componenti core, Componenti di base (legacy), Launches e Live Copy MSM. Le correzioni riguardano vulnerabilità di sicurezza, violazioni cross-site scripting (XSS), comportamento di caricamento dei file e comportamento Live Copy. I backport consentono di allineare AEM 6.5 e AEM 6.5 LTS alle correzioni fornite in precedenza in AEM as a Cloud Service. (SITES-43738)


<!--
#### Campaign integration{#sites-campaign-integration-6526}

#### ContentHub {#sites-contenthub-6526}

#### Crosswalk {#sites-crosswalk-6526}

#### Experience Fragments{#sites-experiencefragments-6526}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-6526}
-->


#### Headless - Amministratore {#sites-headless-admin-6526}

Miglioramento: la vista Anteprima nell’amministratore headless ora passa il percorso della variante selezionata al componente di anteprima. Questa modifica garantisce che le anteprime di frammenti di contenuto con più varianti caricino il contenuto dalla variante corretta. L&#39;array `draftFragmentIds` include il parametro di variante. (SITES-42714)


#### Lanci{#sites-launches-6526}

* Le voci della timeline per i lanci promossi ora vengono visualizzate nella lingua dell’utente. In precedenza, le stringhe &quot;Created version of&quot; (Versione creata di) e &quot;before promotion launch&quot; (Prima di promuovere il lancio) rimanevano in inglese dopo che gli autori avevano promosso un lancio e aperto la Timeline per il sito in Sites. Le risorse aggiornate forniscono le traduzioni in tutte le lingue. (SITES-13389)
* Il segnaposto Seleziona percorso di Launch Source nel pannello dei filtri Launches viene visualizzato completamente. In precedenza, il testo veniva tagliato nelle interfacce localizzate, come francese, italiano e portoghese, perché non rientrava nel campo. Il layout aggiornato mostra il segnaposto completo. (SITES-42792)
* La colonna Data attivazione in Strumenti > Siti > Lanci non mostra più AM o PM nelle lingue tedesca, francese, spagnola, italiana, portoghese brasiliana e cinese tradizionale. In precedenza, la colonna utilizzava un formato di 12 ore che non corrispondeva a tali impostazioni internazionali. Nella colonna viene ora visualizzato il formato 24 ore. (SITES-43178)


<!--
#### Link Checker{#sites-link-checker-6526}
-->


#### Localizzazione{#sites-localization-6526}

* Le stringhe nelle pagine dei report di stato in **Strumenti** > **Operazioni** vengono ora visualizzate nella lingua dell&#39;utente. In precedenza, i messaggi relativi a Percorso di ricerca delle risorse, Manutenzione, Coda di replica, Errori di registro, Bundle attivi e Prestazioni richieste rimanevano in lingua inglese. Le risorse i18n aggiornate forniscono le traduzioni e un file di fallback mantiene le stringhe disponibili. (NPR-44279)

* Il messaggio di errore &quot;Le impostazioni del percorso JSON vengono ignorate quando è selezionata l&#39;opzione &#39;Aggiungi manualmente&#39;&quot; ora viene visualizzato nella lingua dell&#39;utente nella console **Strumenti** > **Assets** > **Schemi di metadati**. In precedenza, il messaggio rimaneva in inglese dopo che gli autori avevano aggiunto un elemento a discesa, avevano selezionato Aggiungi tramite percorso JSON e avevano scelto Aggiungi manualmente. Le risorse aggiornate forniscono le traduzioni. (ASSETS-31575)
* La stringa &quot;innalzato di livello&quot; in **Assets** > **Gestisci** tag ora viene visualizzata nella lingua dell&#39;utente. In precedenza, la stringa rimaneva in inglese quando si passava il cursore sopra uno smart tag dopo aver selezionato Promuovi. Le risorse aggiornate forniscono la traduzione in tutte le lingue. (ASSETS-36070)
* L&#39;etichetta del pulsante Aggiungi non si sovrappone più al pulsante in **Proprietà cartella** > **Contributo risorsa**. In precedenza, il testo si scontrava con il pulsante nelle interfacce tedesca, italiana e portoghese brasiliana dopo aver creato una cartella con l’impostazione &quot;Contributo risorse&quot;. Gli stili aggiornati offrono alle etichette tradotte più a lungo spazio sufficiente. (ASSETS-36746)
* I titoli delle colonne nella Vista a elenco di Assets ora vengono visualizzati orizzontalmente nell’interfaccia giapponese. In precedenza, i titoli venivano visualizzati in verticale nella Vista a elenco in **Assets** > **File** e nella vista a schede dell&#39;editor frammenti di contenuto. Il pacchetto `cq-dam-content` aggiornato corregge la direzione del testo.(ASSETS-43105)
* Nella vista a colonne di Assets, ora nella lingua dell’utente viene visualizzato lo stato di pubblicazione &quot;Pianificato per un momento successivo&quot;. In precedenza, la stringa rimaneva in inglese dopo che gli autori avevano selezionato una risorsa, scelto **Gestisci pubblicazione**, selezionato l&#39;opzione **Più tardi**, aggiunto una data e pubblicato. Il pacchetto `cq-dam-content` aggiornato fornisce le traduzioni in tutte le lingue. (ASSETS-43307)
* Le stringhe nella scheda **Configurazione tag avanzati** vengono ora visualizzate completamente per il francese e il portoghese brasiliano. In precedenza, il testo veniva tagliato dopo aver fatto clic su **Crea** in **Strumenti** > **Servizi cloud** > **Tag avanzati**. Per leggere il testo senza una descrizione, utilizza l’aggiornamento CSS che fornisce spazio sufficiente. (ASSETS-68045)
* La stringa &quot;Predicato proprietà valore percorso multiplo&quot; nella barra di ricerca di amministrazione di Assets ora viene visualizzata nella lingua dell’utente. In precedenza, la stringa rimaneva in inglese quando gli amministratori modificavano il modulo di ricerca in **Strumenti** > **Generale** > **Cerca** moduli e trascinavano il predicato nel modulo. Il pacchetto `cq-dam-content` aggiornato fornisce le traduzioni.(CQ-4336103)
* Le etichette Aria nella vista Progetti ora vengono visualizzate nella lingua dell’utente. In precedenza, il pulsante Azioni su ogni sezione del progetto non aveva un nome accessibile e l’azione Configura sezione utilizzava un’etichetta inglese hardcoded mentre le etichette di pari livello erano localizzate. Lo script di riquadro aggiornato fornisce un’etichetta localizzata per entrambe le azioni. (CQ-4352359)
* Ora le raccolte avanzate con caratteri cinesi, giapponesi o coreani nel nome vengono salvate correttamente. In precedenza, il salvataggio di una raccolta da **Assets** > **Files** > **Filter** non era riuscito con &quot;Save Search Failed - Invalid request, duplicate collection not allowed&quot; (Salvataggio della ricerca non riuscito - Richiesta non valida, raccolta duplicata non consentita) quando il nome conteneva caratteri CJK. Il controllo dei duplicati ora confronta i titoli delle raccolte anziché i nomi dei nodi, in modo che le raccolte con titoli CJK diversi non entrino più in conflitto. (GRANITE-62592)
* Il menu a discesa Paese in **Sicurezza** > **Utenti** > **Crea** ora ordina alfabeticamente i nomi nella lingua dell&#39;utente. In precedenza, l’elenco elencava i nomi ordinati in inglese mentre mostrava i nomi localizzati, pertanto i paesi risultavano fuori ordine in lingue come il giapponese. Il bundle `com.adobe.granite.security.content` aggiornato viene ordinato in base alle regole che supportano le impostazioni locali. (GRANITE-67789)
* La liberatoria sull&#39;attività di manutenzione del Registro di controllo in **Strumenti** > **Operazioni** > **Manutenzione** viene ora visualizzata nella lingua dell&#39;utente. In precedenza, l’avviso relativo all’eliminazione del registro di audit e ai requisiti di conformità rimaneva in inglese dopo che gli utenti avevano fatto clic sull’icona della liberatoria nella finestra Manutenzione settimanale. Le risorse aggiornate forniscono la traduzione in tutte le lingue. (NPR-44189)
* I nomi delle autorizzazioni in **Sicurezza** > **Autorizzazioni** > **Visualizzazione di controllo** vengono ora visualizzati nella lingua dell&#39;utente. In precedenza, i nomi apparivano in inglese perché mancavano le traduzioni. Il bundle `com.adobe.granite.platform.i18n` aggiornato li fornisce. (NPR-44477)
* La finestra di dialogo Verifica stato in **Sicurezza** > **Configurazioni Adobe IMS** viene ora visualizzata nella lingua dell&#39;utente. In precedenza, la finestra di dialogo mostrava stringhe inglesi nelle interfacce localizzate perché mancavano le traduzioni. Il bundle `com.adobe.granite.platform.i18n` aggiornato li fornisce. (NPR-44479)
* Le stringhe nello strumento Diagnostica sincronizzazione utenti in **Strumenti** > **Operazioni** > **Diagnosi** vengono ora visualizzate nella lingua dell&#39;utente. In precedenza, lo strumento mostrava testo inglese nelle interfacce localizzate. Il bundle `com.adobe.granite.platform.i18n` aggiornato fornisce le traduzioni. (NPR-44481)
* I flussi di configurazione ora mostrano messaggi di errore di facile utilizzo nella lingua dell’utente. Precedentemente, errori nelle pagine di configurazione di AEM generavano testo tecnico o non tradotto. Il bundle `com.adobe.granite.ui.content` aggiornato gestisce gli errori e fornisce messaggi localizzati. (NPR-44840)
* Il messaggio di errore visualizzato quando si modificano le proprietà di un gruppo eliminato in **Sicurezza** > **Gruppi** viene ora visualizzato nella lingua dell&#39;utente. In precedenza, il messaggio rimaneva in inglese per le interfacce localizzate. Il bundle `com.adobe.granite.security.content` aggiornato fornisce le traduzioni. (NPR-44841)
* Il messaggio di errore &quot;Si è verificato un errore durante il salvataggio delle modifiche nel gruppo!&quot; ora viene visualizzato nella lingua dell&#39;utente nella console **Sicurezza** > **Gruppi** > **Modifica gruppo**. In precedenza, il messaggio rimaneva in inglese per le interfacce localizzate. Il bundle `com.adobe.granite.security.content` aggiornato fornisce le traduzioni. (NPR-44842)
* I caratteri cinesi, giapponesi e coreani non vengono più visualizzati in corsivo nel messaggio di errore relativo all’icona Posta in arrivo. In precedenza, lo stile corsivo distorceva i caratteri e rendeva il testo più difficile da leggere. Il bundle `com.adobe.granite.ui.coralui3` aggiornato rimuove lo stile di tali lingue. (NPR-44843)
* I numeri in **Operazioni** > **Monitoraggio** ora seguono il formato locale dell&#39;utente. In precedenza, la pagina mostrava numeri in un formato fisso indipendentemente dalla lingua dell’interfaccia. Il bundle `com.adobe.granite.monitoring.dashboard` aggiornato applica i separatori e il formato corretti. (NPR-44844)
* Nella scheda Spiega query è ora visibile lo strumento Query Builder Debugger. nella lingua dell’utente. In precedenza, il testo del collegamento era mancante nelle interfacce localizzate perché la stringa non era esternalizzata. Il bundle `com.adobe.granite.monitoring.dashboard` aggiornato lo ripristina. (NPR-44845)
* Il testo nella finestra di dialogo dello strumento Query Builder Debugger viene ora visualizzato nella lingua dell&#39;utente nella scheda Spiega query. In precedenza, diverse stringhe rimanevano in inglese perché non erano esternalizzate. Il bundle `cq-platform-content` aggiornato fornisce le traduzioni. (NPR-44846)
* Il testo nella pagina Risultato del controllo di coerenza ora viene visualizzato nella lingua dell’utente. In precedenza, diverse stringhe apparivano in inglese perché non erano esternalizzate. Il bundle `com.adobe.granite.operations.ui.core` aggiornato fornisce le traduzioni. (NPR-44847)
* Il Grafico di monitoraggio ora visualizza le etichette dei mesi e delle settimane nella lingua dell&#39;utente. In precedenza, le etichette erano hardcoded in inglese, pertanto il grafico ignorava le impostazioni locali dell’interfaccia. Il bundle `com.adobe.granite.monitoring.dashboard` aggiornato esternalizza le stringhe e ora vengono visualizzate le traduzioni. (NPR-44848)
* Il menu a discesa Paese in **Sicurezza** > **Utenti** > **Crea** ora ordina correttamente le voci. In precedenza, per alcune lingue i nomi dei paesi localizzati apparivano in ordine errato. Il bundle `com.adobe.granite.security.content` aggiornato applica l&#39;ordinamento in base alle impostazioni locali. (NPR-44942)
* Le descrizioni comandi nella finestra di dialogo del componente Pulsante vengono ora visualizzate nella lingua dell’utente. In precedenza, il testo delle informazioni per i campi Testo pulsante, Collegamento, Icona, HTML ID e `aria-label` rimaneva in inglese anche se le stringhe erano presenti nel servizio di localizzazione. Il dizionario aggiornato fornisce le traduzioni in tutte le lingue supportate. (SITES-7579)
* Le descrizioni nella sezione Proprietà del componente Elenco frammenti di contenuto vengono ora visualizzate nella lingua dell’utente. In precedenza, il testo delle informazioni per i campi Modello per frammento di contenuto, Tag, Numero massimo di elementi, Percorso principale, Ordinamento e Ordina per rimaneva in inglese. Il dizionario aggiornato fornisce le traduzioni per tutte le lingue supportate. (SITES-14969)
* I collegamenti della Guida per i Componenti core nell’Editor modelli ora consentono di accedere alle pagine localizzate della documentazione. In precedenza, selezionando Aiuto nella finestra di dialogo di configurazione del componente, veniva aperta la pagina Inglese indipendentemente dalla lingua dell’interfaccia. Gli URL aggiornati ora indirizzano gli utenti alla pagina per la lingua. (SITES-15058)
* Le descrizioni comandi delle informazioni nella finestra di dialogo Frammento di contenuto vengono ora visualizzate nella lingua dell’utente. In precedenza, il testo della descrizione comando per le modalità Elemento di testo singolo e Più elementi e per il percorso Frammento di contenuto rimaneva in inglese. Un dizionario aggiornato fornisce traduzioni per tutte le lingue. (SITES-17333)
* I messaggi di errore nell’editor dei criteri dei componenti dell’Editor modelli ora vengono visualizzati nella lingua dell’utente. In precedenza, i messaggi &quot;La risorsa {} non è modificabile&quot; e &quot;Impossibile creare un nodo in&quot; rimanevano in inglese quando gli autori modificavano un criterio per un componente o ne creavano uno nuovo. Le risorse aggiornate forniscono traduzioni per tutte le lingue supportate. (SITES-17475)
* Nella scheda Assets dell’Editor pagina ora viene visualizzata una stringa tradotta nel menu a discesa Seleziona componenti, dopo aver scelto Paragrafi dal menu a discesa Immagini. In precedenza, la stringa &quot;OTHER&quot; appariva in inglese perché mancava nelle risorse di localizzazione. Il dizionario aggiornato fornisce la traduzione in tutte le lingue. (SITES-21481)
* Le descrizioni comandi nella finestra di dialogo Configura componente Editor pagina non mostrano più un&#39;interruzione di riga aggiuntiva. In precedenza, le descrizioni dei componenti, come PDF Viewer e Progress Bar, venivano racchiuse in modo errato in diverse lingue. Ora le descrizioni comandi vengono racchiuse correttamente e la sillabazione delle parole funziona come previsto. (SITES-38567)
* La descrizione comando &quot;per uscire dall’editor di testo premi il tasto ESC&quot; viene ora visualizzata nella lingua dell’utente nella finestra di dialogo di configurazione del componente Testo. In precedenza, la stringa veniva visualizzata in inglese perché mancava nelle risorse di localizzazione. La descrizione comando ora si traduce in tutte le lingue. (SITES-43186)
* L&#39;etichetta STRUCTURE nell&#39;Editor modelli ora viene visualizzata nella lingua dell&#39;utente. In precedenza, l’etichetta rimaneva in inglese quando gli autori aprivano un modello di modulo adattivo, perché la stringa non era presente nelle risorse di localizzazione. L&#39;etichetta ora si traduce in tutte le lingue. (SITES-43599)


#### MSM - Live Copy{#sites-msm-live-copies-6526}

* La finestra di dialogo Rollout MSM carica nuovamente l’elenco Live Copy dopo un aggiornamento. In precedenza, un `NullPointerException` in `AsyncOperationServlet.doGet` ha interrotto la finestra di dialogo su un dispositivo di rotazione, pertanto gli autori non sono riusciti a selezionare le impostazioni locali di destinazione o ad avviare il rollout. Un bundle `com.adobe.granite.jobs.async` aggiornato gestisce i dati del processo mancanti e completa la richiesta. (SITES-43116)
* Il rollout dalla barra degli strumenti modificabile in una pagina blueprint funziona di nuovo. Azione della barra degli strumenti non riuscita con &quot;Impossibile leggere le proprietà di non definito (lettura di &#39;doRollout&#39;)&quot; perché la libreria client `MSM.Rollout` non è stata caricata. La pagina aggiornata carica ora la libreria, quindi inizia il processo di rollout e le modifiche raggiungono le Live Copy. (SITES-46052)

* La disattivazione batch di una pagina blueprint e delle relative pagine figlie non invia più eventi di rollout duplicati. Quando hai disattivato un elemento padre e i relativi elementi secondari in una richiesta, il sistema di replica ha emesso cinque eventi invece di tre e ogni pagina figlio è stata sottoposta a rollout due volte. La deduplicazione nel gestore di rollout ora invia un rollout per pagina, quindi le Live Copy non ricevono pacchetti ridondanti. (SITES-44988)


#### Editor pagina{#sites-pageeditor-6526}

* Lo stile selezionato rimane evidenziato nella finestra di dialogo di selezione dello stile Editor pagina dopo lo scorrimento dell&#39;elenco. In precedenza, uno stile veniva evidenziato quando lo si selezionava, ma l&#39;evidenziazione svaniva quando si faceva clic sulla barra di scorrimento. Questa regressione è iniziata dopo SP22 e la finestra di dialogo ora mantiene visibile lo stato selezionato. (SITES-30874)

* Gli autori possono modificare le pagine in modalità Layout quando i componenti principali e secondari definiscono punti di interruzione reattivi diversi. La funzione getResponsiveCssClasses non è riuscita in precedenza con un TypeError sui componenti che hanno omesso la larghezza di cq:responsive/telefono. Ora la funzione torna ai valori disponibili e continua il rendering. (SITES-46681)
* I rapporti di ritaglio personalizzati ora vengono caricati in modalità di modifica in linea ibrida per i componenti con più destinazioni di rilascio delle immagini. In precedenza, l’Editor immagini inizializzava un ipeConfig generico per tutte le destinazioni di rilascio, quindi mostrava solo le proporzioni predefinite e ignorava le proporzioni di ciascuna destinazione. L’editor ora legge la configurazione della destinazione di rilascio selezionata e il ritaglio viene applicato sia nella vista in linea che nella vista a schermo intero. (SITES-45771)
* Premendo Backspace nell’Editor Rich Text non vengono aggiunti al testo stili inline aggiuntivi. Un cliente ha segnalato che la rimozione di un’interruzione di riga dopo il testo in grassetto ha aggiunto style=&quot;font-size: 0.8125rem; background-color: transparent;&quot; al tag in grassetto. Il test sul service pack più recente non è riuscito a riprodurre il comportamento, pertanto non è stata necessaria alcuna modifica. (SITES-15883)


<!--
#### Replication{#sites-replication-6526}
-->


#### Editor Rich Text{#sites-rte-6526}

* I pulsanti della barra degli strumenti dell’Editor Rich Text funzionano in modalità Visualizzazione reattiva e Layout. In precedenza, i pulsanti venivano evidenziati quando si faceva clic su di essi, ma la selezione rimaneva invariata e non veniva aperta alcuna finestra di dialogo. Lo script dell’editor aggiornato applica la formattazione, che corrisponde al comportamento in modalità Modifica. (SITES-44233)
* Gli autori possono aggiungere simboli di valuta e di marchio ai componenti Testo senza perderli. Il plug-in Caratteri speciali (Special Characters) ha inserito i simboli, ma questi vengono visualizzati come spazi sia nell&#39;editor che nell&#39;output pubblicato. La gestione corretta esegue il rendering di ogni simbolo come inserito. (SITES-46532)
* L’icona Schermo intero nella barra degli strumenti dell’Editor Rich Text espande nuovamente l’editor. In precedenza, facendo clic sull’icona nel componente Testo core non veniva eseguita alcuna operazione e le dimensioni dell’editor rimanevano invariate. Gli autori ora dispongono di un’area di lavoro specifica per i contenuti in formato esteso, sia nella modifica in linea che nella modifica tramite finestra di dialogo. (SITES-46396)


#### Interfaccia utente amministratore sito{#sites-admin-ui-6526}

Se si ripristina una versione precedente di una risorsa, la miniatura della scheda viene aggiornata. Una modifica della codifica URL nella libreria client Timeline ha causato una mancata corrispondenza del percorso, pertanto la ricerca della scheda non è riuscita e la miniatura è rimasta obsoleta. L’aggiornamento viene ripristinato in base ai percorsi codificati e non elaborati. (SITES-46590)

<!--
#### Universal editor {#sites-universal-editor-6526}
-->

#### Estensioni flusso di lavoro {#sites-workflow-extensions-6526}

Visualizza payload ora apre l’editor di pacchetti dell’interfaccia utente touch per i flussi di lavoro che Gestisci pubblicazione viene avviato per più pagine. In precedenza, l’azione apriva l’editor di pacchetti dell’interfaccia classica obsoleto, anche se gli autori avevano avviato il flusso di lavoro nell’interfaccia touch. Gli autori ora esaminano il payload senza uscire dall’interfaccia utente touch. (SITES-40928)


### [!DNL Assets] {#assets-6526}

* Miglioramento: AEM Assets 6.5 include il supporto per la conformità Coalition for Content Provenance and Authenticity (C2PA) per i contenuti di intelligenza artificiale generativi. Il flusso di lavoro Aggiorna risorsa rileva le credenziali C2PA, estrae i metadati e firma le rappresentazioni rigenerate dal flusso di lavoro. La firma viene eseguita localmente in ogni istanza di AEM, pertanto i clienti non hanno bisogno di un’infrastruttura di firma dedicata. (ASSETS-75868)

* Miglioramento della documentazione: la nuova documentazione pubblica spiega come personalizzare la pipeline di elaborazione delle risorse mantenendo la conformità C2PA. La documentazione illustra come posizionare il passaggio Rileva credenziali C2PA prima dei passaggi di rendering e come la firma viene eseguita localmente in ogni istanza di AEM. La documentazione indica anche la limitazione sull’infrastruttura di firma dedicata o di proprietà del cliente. (ASSETS-76100)
* Il menu a discesa Aiuto nell’intestazione della shell ora rimane aperto quando passi il cursore del mouse sui relativi collegamenti negli ambienti AEM 6.5 SP26. In precedenza, il menu a discesa si chiudeva quando il puntatore veniva inserito nell’elenco, pertanto gli autori non potevano fare clic sui collegamenti alla documentazione, alla community o al supporto. Il bundle `com.adobe.granite.ui.content` aggiornato posticipa il controllo dello stato attivo, quindi il menu si chiude solo quando lo stato attivo esce davvero. (ASSETS-65676)

<!--
#### [!DNL Dynamic Media]{#assets-dm-6526}
-->

### [!DNL Forms]{#forms-6526}

* Nuova funzione: Supporto per i tag di accessibilità negli elenchi in formato Rich Text. In precedenza, i tag elenco venivano visualizzati nella struttura dei tag di accessibilità solo quando il modello seguiva una struttura specifica. La richiesta è stata chiusa come duplicato di un ticket correlato che fornisce la funzione. (LC-3923202)


<!--
#### Forms JEE {#forms-jee-6526}

#### Forms Designer {#forms-designer-6526}
-->


### Foundation {#foundation-6526}

* La stringa &quot;Paese&quot; nella finestra di dialogo **Sicurezza** > **Utenti** > **Crea** utente viene ora visualizzata nella lingua dell&#39;utente. In precedenza, l’etichetta rimaneva in inglese per le interfacce localizzate. Il bundle `com.adobe.granite.security.content` aggiornato fornisce le traduzioni. (NPR-43882)
* Il menu a discesa Aiuto nell’intestazione della shell ora rimane aperto quando passi il cursore del mouse sui relativi collegamenti negli ambienti AEM 6.5 SP26. In precedenza, il menu a discesa si chiudeva quando il puntatore veniva inserito nell’elenco, pertanto gli autori non potevano fare clic sui collegamenti alla documentazione, alla community o al supporto. Il bundle `com.adobe.granite.ui.content` aggiornato posticipa il controllo dello stato attivo, quindi il menu si chiude solo quando lo stato attivo esce davvero. (NPR-44686)
* Miglioramento: la query `HtmlLibraryManagerImpl` ora include un tag di tipo nodo in modo che la query utilizzi sempre l&#39;indice previsto. Il servizio registra inoltre un errore quando non trova librerie client, avvisando gli amministratori del problema. L&#39;aggiornamento esegue il bump della versione del bundle `com.adobe.granite.clientlibs` nel service pack. (NPR-44698)


<!--
#### Apache Felix {#foundation-apachefelix-6526}
-->


#### Autenticazione {#foundation-authentication-6526}

Salva e chiudi nell’editor utente ora ritorna ai risultati della ricerca corrente. In precedenza, dopo aver cercato un secondo utente in Omnisearch, aver modificato le proprietà e aver fatto clic su Salva e chiudi, la pagina apriva le proprietà del primo utente. Lo script UserProperties.js aggiornato ripristina la navigazione prevista. (NPR-44774)

<!--
#### Campaign{#foundation-campaign-6526}

#### Cloud Services{#foundation-cloudservices-6526}

#### Communities {#foundation-communities-6526}

#### Content distribution{#foundation-content-distribution-6526}

#### Adobe CRX {#foundation-crx-6526}
-->


#### Granite{#foundation-granite-6526}

* Ora il segnaposto &quot;Modello per frammenti di contenuto&quot; nel filtro di Assets Omnisearch viene visualizzato completamente. In precedenza, il testo veniva tagliato dopo essere passati ad Assets, dopo aver fatto clic sull’icona Filtri o Ricerca e aver espanso il campo Modello per frammenti di contenuto. Lo stile aggiornato offre al segnaposto spazio sufficiente. (GRANITE-54387)
* Il menu a discesa della Guida nell&#39;intestazione della shell ora rimane aperto quando si sposta il puntatore sui relativi collegamenti. In precedenza, il menu a discesa si chiudeva non appena il puntatore entrava nell’elenco dei collegamenti per la documentazione, la community e il supporto, rendendo i collegamenti irraggiungibili con il mouse. Il gestore di messa a fuoco ora rimanda il controllo al fotogramma di animazione successivo, quindi il passaggio del mouse non conta più come elemento attivo che esce dal menu. (GRANITE-70978)

<!--
#### Jetty{#foundation-jetty-6526}
-->

#### Integrazioni Launch{#foundation-launch-integrations-6526}

Miglioramento: l’integrazione di Adobe Analytics con Adobe Experience Manager Launch utilizza l’API Analytics 2.0. L’API di Analytics 1.4 raggiunge la fine del ciclo di vita il 31 agosto 2026. La migrazione mantiene il reporting e il funzionamento delle integrazioni Launch dopo tale data. (CQ-4365074, CQ-4365080)

<!--
#### Localization{#foundation-localization-6526}

#### Oak {#foundation-oak-6526}
-->

#### Platform{#foundation-platform-6526}

* Il collegamento Aiuto nel piè di pagina della pagina di accesso di AEM ora apre una pagina di lavoro. In precedenza, il collegamento puntava a un URL marketing.adobe.com che non esiste più. La configurazione del piè di pagina ora utilizza l&#39;URL [documentazione di Adobe Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager). (NPR-44388)
* Miglioramento: una richiesta del cliente ha richiesto l’API del grafico Microsoft come alternativa a SMTP quando AEM invia un’e-mail. Il ticket è stato risolto come duplicato, perché un altro ticket implementa già il flusso API di Graph. SMTP con OAuth 2.0 rimane disponibile per i clienti che devono abbandonare l’autenticazione di base SMTP. (GRANITE-57478)

* Le stringhe nella finestra di dialogo Autorizzazioni effettive ora vengono allineate correttamente nel browser **Strumenti** > **Generale** > **Configurazione**. In precedenza, una stringa veniva visualizzata fuori linea dopo aver selezionato una cartella, fatto clic su Proprietà e su Autorizzazioni effettive. Le regole di layout aggiornate ripristinano l’allineamento. (CQ-4359166)


#### Progetti {#foundation-projects-6526}

Ora viene visualizzata la stringa &quot;Seleziona directory principale&quot; nella finestra di dialogo Seleziona dizionario i18n. In precedenza, il testo veniva tagliato in diverse interfacce localizzate dopo la creazione di un progetto di traduzione e l’aggiunta di un dizionario i18n. Il pacchetto `cq-projects-translation-content` aggiornato fornisce alla stringa spazio sufficiente. (CQ-4355405)

<!--
#### Security{#foundation-security-6526}

#### Sling{#foundation-sling-6526}

#### SPA editor {#foundation-spa-editor-6526}
-->


#### Traduzione{#foundation-translation-6526}

Le opzioni di stile per il componente Elenco ora vengono visualizzate nella lingua dell’utente. In precedenza, stringhe come Blocca e Griglia rimanevano in inglese nel menu Stili dopo che gli autori avevano aggiunto il componente Elenco a un frammento di esperienza. Le risorse aggiornate forniscono le traduzioni, incluse le interfacce Coreano, Cinese semplificato e Cinese tradizionale. (CQ-4349666)

<!--
#### User interface{#foundation-ui-6526}

#### WCM{#foundation-wcm-6526}
-->

#### Flusso di lavoro{#foundation-workflow-6526}

Miglioramento: l’Editor pagina per l’interfaccia utente touch ora esegue il rendering della struttura del contenuto e supporta la modifica dei componenti Definizione risorsa nelle pagine dei pacchetti del flusso di lavoro. In precedenza, le pagine in `/etc/workflow/packages/` create da **Gestisci pubblicazione** > **Pubblica più tardi** non mostravano alcuna struttura contenuto nel pannello sinistro e gli autori non potevano modificare i componenti Definizione risorsa. Gli approvatori ora esaminano le pagine e le risorse all’interno di un payload del flusso di lavoro nell’interfaccia utente touch, in base al comportamento dell’interfaccia classica. (GRANITE-65620)

## Installa [!DNL Experience Manager] 6.5.26.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.26.0 richiede [!DNL Experience Manager] 6.5. Per istruzioni dettagliate, consulta la [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md). <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del Service Pack è disponibile in Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip).
* In una distribuzione con MongoDB e più istanze, installare [!DNL Experience Manager] 6.5.26.0 in una delle istanze di authoring utilizzando Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe consiglia di non rimuovere o disinstallare il pacchetto [!DNL Experience Manager] 6.5.26.0. Per eseguire il rollback, se necessario, creare un backup di `crx-repository` prima di installare il pacchetto. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Installare il Service Pack in [!DNL Experience Manager] 6.5{#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). Adobe consiglia di riavviare il sistema se il tempo di attività corrente di un’istanza è elevato.

1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup dell&#39;istanza [!DNL Experience Manager].

1. Scarica il Service Pack da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, vedere [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Selezionare il pacchetto, quindi selezionare **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l’istanza dopo l’installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l’istanza. Vedi [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Talvolta la finestra di dialogo nell’interfaccia utente di Gestione pacchetti si chiude durante l’installazione del Service Pack. Adobe consiglia di attendere che i registri di errore non vengano più modificati prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle di aggiornamento prima di confermare che l’installazione è andata a buon fine. Questo problema si verifica nel browser [!DNL Safari] ma può verificarsi occasionalmente in qualsiasi browser.

**Installazione automatica**

Per installare [!DNL Experience Manager] 6.5.26.0 è possibile utilizzare due metodi diversi.<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto nella cartella `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza l&#39;API HTTP [da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzare `cmd=install&recursive=true` per installare i pacchetti nidificati.

>[!NOTE]
>
>Experience Manager 6.5.26.0 non supporta l&#39;installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalida l&#39;installazione**

Per le piattaforme certificate per l&#39;utilizzo di questa versione, vedere i [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager (6.5.26.0)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tutti i bundle OSGi sono **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** nella console OSGi (usa la console Web: `/system/console/bundles`).

1. La versione del bundle OSGi `org.apache.jackrabbit.oak-core` è 1.22.20 o successiva (utilizzare la console Web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Installa Service Pack per [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Per istruzioni sull&#39;installazione del Service Pack in Experience Manager Forms, vedere [Istruzioni di installazione del Service Pack di Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funzione Forms adattivo, disponibile in [QuickStart per AEM 6.5](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), è progettata esclusivamente a scopo di esplorazione e valutazione. Per l’utilizzo in produzione, è essenziale ottenere una licenza valida per AEM Forms, in quanto la funzionalità Adaptive Forms richiede una licenza appropriata.

### Installare il pacchetto di indice GraphQL per i frammenti di contenuto Experience Manager{#install-aem-graphql-index-add-on-package}

I clienti che utilizzano GraphQL devono installare il [Frammento di contenuto Experience Manager con pacchetto indice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Questo consente di aggiungere la definizione dell’indice richiesta in base alle funzioni utilizzate.

Se non si installa questo pacchetto, si verificano query GraphQL lente o non riuscite.

>[!NOTE]
>
>Installare il pacchetto una sola volta per istanza; non è necessario reinstallarlo con ogni Service Pack.

### UberJar{#uber-jar}

UberJar per [!DNL Experience Manager] 6.5.26.0 è disponibile nel [archivio centrale Maven](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.26/). <!-- CHECK FOR UPDATE EACH NEW RELEASE FROM MADHULIKA SINGH -->

Per utilizzare UberJar in un progetto Maven, vedi [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includi nel POM del progetto la seguente dipendenza: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.26</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell&#39;archivio centrale di Maven anziché nell&#39;archivio pubblico Maven di Adobe (`repo.adobe.com`). Il file UberJar principale è stato rinominato in `uber-jar-<version>.jar`. Non esiste alcun `classifier`, con `apis` come valore, per il tag `dependency`.



## Funzioni obsolete e rimosse{#removed-deprecated-features}

Consulta [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md) per un elenco dettagliato di tutte le funzioni obsolete o rimosse per AEM 6.5.

### Supporto ai frammenti di contenuto nell’API REST di AEM Assets {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 fornisce OpenAPI moderne per la gestione dei modelli e frammenti di contenuto, pertanto gli endpoint precedenti per il supporto dei frammenti di contenuto nell’API REST di AEM Assets sono ora obsoleti.

Adobe intende mantenere questi endpoint meno recenti disponibili fino a un annuncio sulla fine del ciclo di vita. Adobe non pianifica ulteriori miglioramenti per gli endpoint obsoleti.

### Editor di SPA {#spa-editor}

[L&#39;editor SPA](/help/sites-developing/spa-overview.md) è stato dichiarato obsoleto per i nuovi progetti a partire dalla versione 6.5.25 di AEM 6.5. L’editor SPA rimane supportato per i progetti esistenti, ma non deve essere utilizzato per i nuovi progetti.

Gli editor preferiti per la gestione dei contenuti headless in AEM sono ora:

* [Editor universale](/help/sites-developing/universal-editor/introduction.md) per la modifica visiva.
* [Editor frammenti di contenuto](/help/sites-developing/universal-editor/introduction.md) per la modifica basata su modulo.

## Problemi noti{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

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
     Le nuove cartelle per `cache` e `diff-cache` vengono create automaticamente e non si verifica più un&#39;eccezione relativa a `mvstore` in `error.log`.

* Aggiorna le query GraphQL che hanno utilizzato un nome API personalizzato per il modello di contenuto in modo da utilizzare il nome predefinito del modello di contenuto.

* Una query GraphQL utilizza l&#39;indice `damAssetLucene` invece dell&#39;indice `fragments`. Questa azione genera query GraphQL non riuscite o che richiedono molto tempo per essere eseguite.

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

  Dopo questi passaggi, le query GraphQL vengono eseguite con una velocità migliorata.

* Quando si tenta di spostare, eliminare o pubblicare frammenti di contenuto, siti o pagine, si verifica un problema durante il recupero dei riferimenti ai frammenti di contenuto. La query in background non riesce; la funzionalità non funziona.
Per garantire il corretto funzionamento, è necessario aggiungere le seguenti proprietà al nodo di definizione dell&#39;indice `/oak:index/damAssetLucene` (non è richiesta alcuna reindicizzazione):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Se si aggiorna l&#39;istanza di [!DNL Experience Manager] dalla versione 6.5.0 alla versione 6.5.4 al Service Pack più recente in Java™ 11, vengono visualizzate `RRD4JReporter` eccezioni nel file `error.log`. Per interrompere le eccezioni, riavviare l&#39;istanza di [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Gli utenti possono rinominare una cartella in [!DNL Assets] e pubblicarla in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene ripubblicata.

* Durante l&#39;installazione di [!DNL Experience Manager] 6.5.x.x vengono visualizzati i seguenti errori e messaggi di avviso:
  * &quot;Quando l&#39;integrazione Adobe Target è configurata in [!DNL Experience Manager] utilizzando l&#39;API Target Standard (autenticazione IMS), l&#39;esportazione di frammenti di esperienza in Target genera la creazione di tipi di offerta errati. Invece del tipo &quot;Frammento di esperienza&quot;/sorgente &quot;Adobe Experience Manager&quot;, Target crea diverse offerte con il tipo &quot;HTML&quot;/sorgente &quot;Adobe Target Classic&quot;.
  * `com.adobe.granite.maintenance.impl.TaskScheduler`: nessuna finestra di manutenzione trovata in `granite/operations/maintenance`.
  * La convalida lato server di Moduli adattivi non riesce quando vengono utilizzate funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
  * `com.adobe.granite.maintenance.impl.TaskScheduler`: nessuna finestra di manutenzione trovata in `granite/operations/maintenance`.
  * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner Shoppable.
  * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro per l&#39;annullamento della registrazione.

* A partire da AEM 6.5.15, il motore JavaScript Rhino fornito dal bundle `org.apache.servicemix.bundles.rhino` ha un nuovo comportamento di posizionamento. Gli script che utilizzano la modalità rigorosa (`use strict;`) devono dichiarare le variabili corrette. In caso contrario, non vengono eseguiti e finiscono per generare un errore di runtime.

* Se si installa il contenuto standard correlato ai tag tramite un pacchetto di aggiornamento ufficiale, la proprietà Languages del nodo `/content/cq:tags` viene ripristinata sul valore predefinito. Questa azione è valida per Service Pack, Service Pack di sicurezza, Feature Pack estesi, Feature Pack cumulativi, patch e così via. Pertanto, è necessario aggiungerlo alle proprietà prima dell’installazione.

### Problema noto per AEM Sites {#known-issues-aem-sites-6526}

* **Problema noto con un hotfix disponibile per AEM Foundation**

  Dopo l&#39;aggiornamento da un service pack precedente ad Experience Manager 6.5.26.0, l&#39;ordinamento della versione del bundle CRXDE Lite può impedire ad Experience Manager di selezionare il bundle desiderato. Per correggere l&#39;ordinamento delle versioni, installare Service Pack 26, quindi scaricare e installare l&#39;aggiornamento rapido [`CRXDE Lite hotfix GRANITE-76725`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq660%2Fhotfixes%2Fgranite-76725%2Fcq-6.5.26-hotfix-GRANITE-76725-1.0.zip) da Software Distribution. L’aggiornamento rapido è di sola versione. Non contiene modifiche di codice o funzionali. (GRANITE-76725)

* Frammenti di contenuto-Anteprima non riuscita a causa della protezione DoS per una grande struttura ad albero di frammenti. Vedi l&#39;articolo [KB sulle opzioni di configurazione predefinite di GraphQL Query Executor](https://experienceleague.adobe.com/it/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemi noti per AEM Forms {#known-issues-aem-forms-6526}

* Quando un modulo contenente un campo **File allegato** che utilizza `bindref` viene inviato a un flusso di lavoro di AEM con un passaggio **Assegna attività**, gli allegati non vengono visualizzati. Di conseguenza, non vengono visualizzate quando l&#39;attività viene aperta dalla cartella Posta in arrivo. I file vengono salvati correttamente nell’archivio, ma l’interfaccia utente del passaggio Assegna attività non riesce a visualizzare gli allegati. (FORMS-23722)

* Quando un PDF con firma digitale viene allegato a un’attività in AEM Forms JEE Workspace, il caricamento rimane bloccato nello stato di caricamento o non riesce con un errore &quot;File non valido&quot;. Di conseguenza, non è possibile aggiungere all&#39;attività allegati PDF firmati di dimensioni maggiori. Questo problema è stato risolto in una versione successiva. Per un hotfix sulla versione, contatta il supporto Adobe. (FORMS-28517)

#### Problemi noti con gli hotfix disponibili {#aem-forms-issues-with-hotfixes}

Nei seguenti problemi è disponibile un hotfix per il download e l’installazione. Puoi [scaricare e installare l&#39;Hotfix](/help/release-notes/aem-forms-hotfix.md) per risolvere questi problemi:

* Dopo aver installato AEM Forms JEE Service Pack 21 (6.5.21.0), se trovi voci duplicate dei file jar Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` nella cartella `<AEM_Forms_Installation>/lib/caching/lib`, effettua le seguenti operazioni per risolvere il problema (FORMS-14926):

  1. Fermate i localizzatori, se sono in esecuzione.
  1. Arresta il server AEM.
  1. Passare a `<AEM_Forms_Installation>/lib/caching/lib`.
  1. Rimuovere tutti i file patch Geode ad eccezione di `geode-*-1.15.1.2.jar`. Verificare che siano presenti solo i file jar Geode con `version 1.15.1.2`.
  1. Apri il prompt dei comandi in modalità di amministrazione.
  1. Installare la patch Geode utilizzando il file `geode-*-1.15.1.2.jar`.

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

I seguenti file zip contengono i documenti di testo che elencano i bundle OSGi e i pacchetti di contenuti inclusi in questa versione di [!DNL Experience Manager] 6.5 Service Pack:

* [Elenco dei bundle OSGi inclusi in Experience Manager 6.5.26.0](/help/release-notes/assets/65260-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.26.0](/help/release-notes/assets/65260-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## Siti web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se fai parte della clientela e necessiti dell’accesso, contatta il responsabile dell’account Adobe.

* [Scarica il prodotto all’indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* Contatta l’[Assistenza Clienti di Adobe](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina prodotto](https://business.adobe.com/it/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/it/docs/experience-manager-65)
>* [Iscriviti agli aggiornamenti dei prodotti con priorità Adobe](https://www.adobe.com/subscription/priority-product-update.html)




