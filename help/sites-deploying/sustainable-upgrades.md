---
title: Aggiornamenti sostenibili
description: Scopri gli aggiornamenti sostenibili in Adobe Experience Manager 6.4.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Aggiornamenti sostenibili{#sustainable-upgrades}

## Framework di personalizzazione {#customization-framework}

### Architettura (funzionale/infrastruttura/contenuto/applicazione)  {#architecture-functional-infrastructure-content-application}

La funzione framework di personalizzazione è progettata per contribuire a ridurre le violazioni in aree non estensibili del codice (come API) o del contenuto (come sovrapposizioni) che non sono compatibili con l’aggiornamento.

Sono disponibili due componenti del framework di personalizzazione: **API Surface** e **Content Classification**.

#### Superficie API {#api-surface}

Nelle versioni precedenti di Adobe Experience Manager (AEM), molte API sono state esposte tramite il file JAR di Uber. Alcune di queste API non erano destinate all’uso da parte dei clienti, ma sono state esposte per supportare la funzionalità AEM tra i bundle. In futuro, le API Java™ saranno contrassegnate come pubbliche o private per indicare ai clienti quali API sono sicure da utilizzare nel contesto degli aggiornamenti. Altre specifiche includono:

* Le API Java™ contrassegnate come `Public` possono essere utilizzate e utilizzate come riferimento dai bundle di implementazione personalizzati.

* Le API pubbliche sono compatibili con le versioni precedenti dell’installazione di un pacchetto di compatibilità.
* Il pacchetto di compatibilità contiene un file JAR Uber di compatibilità per garantire la compatibilità con le versioni precedenti
* Le API Java™ contrassegnate come `Private` devono essere utilizzate solo da bundle interni AEM, non da bundle personalizzati.

>[!NOTE]
>
>Il concetto di `Private` e `Public` in questo contesto non deve essere confuso con le nozioni Java™ di classi pubbliche e private.

![immagine2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### Classificazioni contenuto {#content-classifications}

L’AEM utilizza da tempo il principio delle sovrapposizioni e Sling Resource Merger per consentire ai clienti di estendere e personalizzare la funzionalità dell’AEM. Le funzionalità predefinite che alimentano le console e l&#39;interfaccia utente di AEM sono memorizzate in **/libs**. I clienti non devono mai modificare nulla sotto **/libs**, ma potrebbero aggiungere contenuto aggiuntivo sotto **/apps** per sovrapporre ed estendere la funzionalità definita in **/libs** (Per ulteriori informazioni, consulta Sviluppo con sovrapposizioni). Ciò causava ancora numerosi problemi durante l&#39;aggiornamento dell&#39;AEM poiché il contenuto in **/libs** poteva cambiare causando l&#39;interruzione della funzionalità di sovrapposizione in modi imprevisti. I clienti possono inoltre estendere i componenti AEM tramite l&#39;ereditarietà tramite `sling:resourceSuperType` o semplicemente fare riferimento a un componente in **/libs** direttamente tramite sling:resourceType. Problemi di aggiornamento simili potrebbero verificarsi con casi di utilizzo di riferimento e di sostituzione.

Per rendere più sicuro e semplice per i clienti capire quali aree di **/libs** sono sicure da utilizzare e sovrapporre il contenuto in **/libs** è stato classificato con i seguenti mixin:

* **Pubblico (granite:PublicArea)** - Definisce un nodo come pubblico in modo che possa essere sovrapposto, ereditato (`sling:resourceSuperType`) o utilizzato direttamente ( `sling:resourceType`). I nodi sotto /libs contrassegnati come pubblici possono essere aggiornati con l’aggiunta di un pacchetto di compatibilità. In generale, i clienti devono utilizzare solo nodi contrassegnati come pubblici.

* **Astratto (granite:AbstractArea)** - Definisce un nodo come astratto. I nodi possono essere sovrapposti o ereditati ( `sling:resourceSupertype`) ma non utilizzati direttamente ( `sling:resourceType`).

* **Finale (granite:FinalArea)** - Definisce un nodo come finale. I nodi classificati come finali idealmente non devono essere sovrapposti o ereditati. I nodi finali possono essere utilizzati direttamente tramite `sling:resourceType`. Per impostazione predefinita, i sottonodi sotto il nodo finale sono considerati interni.

* ***Interno (granite:InternalArea)*** *- *Definisce un nodo interno. I nodi classificati come interni idealmente non devono essere sovrapposti, ereditati o utilizzati direttamente. Questi nodi sono destinati solo alle funzionalità interne dell’AEM

* **Nessuna annotazione** - I nodi ereditano la classificazione in base alla gerarchia della struttura. La directory principale / è per impostazione predefinita Public. **Anche i nodi con un elemento padre classificato come Interno o Finale devono essere trattati come Interno.**

>[!NOTE]
>
>Questi criteri vengono applicati solo ai meccanismi basati su percorsi di ricerca Sling. Altre aree di **/libs** come una libreria lato client possono essere contrassegnate come `Internal`, ma possono ancora essere utilizzate con l&#39;inclusione clientlib standard. In questi casi è importante che il cliente continui a rispettare la classificazione interna.

#### Indicatori del tipo di contenuto CRXDE Lite {#crxde-lite-content-type-indicators}

I mixin applicati in CRXDE Lite mostrano i nodi di contenuto e gli alberi contrassegnati come `INTERNAL` in grigio. Per `FINAL`, solo l&#39;icona è oscurata. Anche i figli di questi nodi vengono visualizzati in grigio. La funzionalità Sovrapponi nodo è disabilitata in entrambi questi casi.

**Pubblico**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Finale**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**Interno**

![immagine2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Verifica stato contenuto**

>[!NOTE]
>
>A partire da AEM 6.5, Adobe consiglia di utilizzare il rilevatore pattern per rilevare le violazioni dell’accesso ai contenuti. I rapporti del rilevatore pattern sono più dettagliati, rilevano più problemi e riducono la probabilità di falsi positivi.
>
>Per ulteriori informazioni, vedere [Valutazione della complessità dell&#39;aggiornamento con il rilevatore pattern](/help/sites-deploying/pattern-detector.md).

L’AEM 6.5 viene fornito con un controllo di integrità per avvisare i clienti se il contenuto sovrapposto o di riferimento viene utilizzato in modo incoerente con la classificazione del contenuto.

Il **&#x200B; Sling/Granite Content Access Check** è un nuovo controllo di integrità che monitora l’archivio per verificare se il codice del cliente accede in modo errato ai nodi protetti in AEM.

Questa operazione esegue la scansione di **/apps** e in genere richiede diversi secondi.

Per accedere a questa nuova verifica stato, eseguire le operazioni seguenti:

1. Dalla schermata iniziale dell&#39;AEM, passa a **Strumenti > Operazioni > Rapporti stato**
1. Fai clic su **Controllo accesso a contenuti Sling/Granite**.

   ![schermata_shot_2017-12-14alle55648pm](assets/screen_shot_2017-12-14at55648pm.png)

Al termine dell’analisi, viene visualizzato un elenco di avvisi per informare l’utente finale del nodo protetto a cui si fa riferimento in modo errato:

![screenshot-2018-2-5healthReports](assets/screenshot-2018-2-5healthreports.png)

Dopo aver corretto le violazioni, torna allo stato verde:

![screenshot-2018-2-5healthreports-changes](assets/screenshot-2018-2-5healthreports-violations.png)

La verifica stato visualizza le informazioni raccolte da un servizio in background che controlla in modo asincrono ogni volta che viene utilizzato un tipo di risorsa o sovrapposizione in tutti i percorsi di ricerca Sling. Se i mixin di contenuto non vengono utilizzati correttamente, viene segnalata una violazione.
