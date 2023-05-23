---
title: Aggiornamenti sostenibili
seo-title: Sustainable Upgrades
description: Scopri gli aggiornamenti sostenibili in AEM 6.4.
seo-description: Learn about sustainable upgrades in AEM 6.4.
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# Aggiornamenti sostenibili{#sustainable-upgrades}

## Framework di personalizzazione {#customization-framework}

### Architettura (funzionale/infrastruttura/contenuto/applicazione)  {#architecture-functional-infrastructure-content-application}

La funzione Framework di personalizzazione è progettata per contribuire a ridurre le violazioni in aree non estensibili del codice (come API) o del contenuto (come sovrapposizioni) che non sono compatibili con l’aggiornamento.

Esistono due componenti del framework di personalizzazione: **Superficie API** e **Classificazione dei contenuti**.

#### Superficie API {#api-surface}

Nelle versioni precedenti dell’AEM molte API sono state esposte tramite il file JAR di Uber. Alcune di queste API non erano destinate all’uso da parte dei clienti, ma sono state esposte per supportare la funzionalità AEM tra i bundle. In futuro, le API Java saranno contrassegnate come pubbliche o private per indicare ai clienti quali API sono sicure da utilizzare nel contesto degli aggiornamenti. Altre specifiche includono:

* API Java contrassegnate come `Public` possono essere utilizzati e utilizzati come riferimento dai bundle di implementazione personalizzati.

* Le API pubbliche saranno compatibili con le versioni precedenti, con l’installazione di un pacchetto di compatibilità.
* Il pacchetto di compatibilità conterrà un JAR Uber di compatibilità per garantire la compatibilità con le versioni precedenti
* API Java contrassegnate come `Private` sono destinati a essere utilizzati solo da bundle interni AEM e non devono essere utilizzati da bundle personalizzati.

>[!NOTE]
>
>Il concetto di `Private` e `Public` in questo contesto non va confuso con le nozioni Java di classi pubbliche e private.

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### Classificazioni contenuto {#content-classifications}

L’AEM utilizza da tempo il principio delle sovrapposizioni e Sling Resource Merger per consentire ai clienti di estendere e personalizzare la funzionalità dell’AEM. Le funzionalità predefinite che alimentano le console AEM e l’interfaccia utente sono memorizzate in **/libs**. I clienti non devono mai modificare nulla sotto **/libs** ma potrebbe aggiungere contenuto aggiuntivo sotto **/apps** per sovrapporre ed estendere la funzionalità definita in **/libs** Per ulteriori informazioni, consulta Sviluppo con sovrapposizioni. Questo causava ancora numerosi problemi durante l’aggiornamento dell’AEM come contenuto in **/libs** potrebbe cambiare causando un’interruzione imprevista della funzionalità di sovrapposizione. I clienti possono inoltre estendere i componenti AEM tramite l’ereditarietà tramite `sling:resourceSuperType`o semplicemente fare riferimento a un componente in **/libs** direttamente tramite sling:resourceType. Problemi di aggiornamento simili potrebbero verificarsi con casi di utilizzo di riferimento e di sostituzione.

Per rendere più sicuro e facile per i clienti capire quali aree **/libs** sono sicuri da usare e sovrapporre al contenuto in **/libs** è stato classificato con i seguenti mixin:

* **Pubblico (granite:PublicArea)** - Definisce un nodo come pubblico in modo che possa essere sovrapposto, ereditato ( `sling:resourceSuperType`) o utilizzato direttamente ( `sling:resourceType`). I nodi al di sotto di /libs contrassegnati come pubblici potranno essere aggiornati con l’aggiunta di un pacchetto di compatibilità. In generale, i clienti devono sfruttare solo i nodi contrassegnati come Pubblici.

* **Riassunto (granite:AbstractArea)** - Definisce un nodo come astratto. I nodi possono essere sovrapposti o ereditati ( `sling:resourceSupertype`) ma non deve essere utilizzato direttamente ( `sling:resourceType`).

* **Finale (granito:FinalArea)** - Definisce un nodo come finale. I nodi classificati come finali idealmente non devono essere sovrapposti o ereditati. I nodi finali possono essere utilizzati direttamente tramite `sling:resourceType`. Per impostazione predefinita, i sottonodi sotto il nodo finale sono considerati interni.

* ***Interno (granite:InternalArea)*** *- *Definisce un nodo interno. I nodi classificati come interni idealmente non devono essere sovrapposti, ereditati o utilizzati direttamente. Questi nodi sono destinati solo alle funzionalità interne dell’AEM

* **Nessuna annotazione** - I nodi ereditano la classificazione in base alla gerarchia della struttura. Per impostazione predefinita, la directory principale / è Public. **Anche i nodi con un elemento padre classificato come Interno o Finale devono essere trattati come Interno.**

>[!NOTE]
>
>Questi criteri vengono applicati solo ai meccanismi basati su percorsi di ricerca Sling. Altre aree di **/libs** come una libreria lato client può essere contrassegnata come `Internal`, ma può ancora essere utilizzato con l’inclusione clientlib standard. In questi casi è importante che il cliente continui a rispettare la classificazione interna.

#### Indicatori del tipo di contenuto CRXDE Lite {#crxde-lite-content-type-indicators}

I mixin applicati in CRXDE Lite mostreranno i nodi di contenuto e gli alberi contrassegnati come `INTERNAL` come disattivata. Per `FINAL` solo l’icona è disattivata. Anche gli elementi secondari di questi nodi verranno visualizzati in grigio. La funzionalità Sovrapponi nodo è disabilitata in entrambi questi casi.

**Pubblico**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Finale**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**Interno**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Verifica stato contenuto**

>[!NOTE]
>
>A partire da AEM 6.5, Adobe consiglia di utilizzare il rilevatore pattern per rilevare le violazioni dell’accesso ai contenuti. I rapporti del rilevatore pattern sono più dettagliati, rilevano più problemi e riducono la probabilità di falsi positivi.
>
>Per ulteriori informazioni, consulta [Valutazione della complessità dell’aggiornamento con il rilevatore pattern](/help/sites-deploying/pattern-detector.md).

AEM 6.5 viene fornito con un controllo di integrità per avvisare i clienti se il contenuto sovrapposto o di riferimento viene utilizzato in modo incoerente con la classificazione del contenuto.

Il** Sling/Granite Content Access Check** è un nuovo controllo di integrità che monitora l’archivio per verificare se il codice del cliente accede in modo errato ai nodi protetti in AEM.

Verrà eseguita la scansione **/apps** e in genere richiede diversi secondi.

Per accedere a questo nuovo controllo di integrità, è necessario effettuare le seguenti operazioni:

1. Dalla schermata iniziale dell’AEM, passa a **Strumenti > Operazioni > Rapporti stato**
1. Fai clic sul pulsante **Controllo dell’accesso ai contenuti Sling/Granite** come mostrato di seguito:

   ![screen_shot_2017-12-14alle55648pm](assets/screen_shot_2017-12-14at55648pm.png)

Al termine dell’analisi, verrà visualizzato un elenco di avvisi per avvisare l’utente finale del nodo protetto a cui si fa riferimento in modo errato:

![screenshot-2018-2-5health reports](assets/screenshot-2018-2-5healthreports.png)

Dopo aver risolto le violazioni, tornerà allo stato verde:

![screenshot-2018-2-5rapporti sanitari-violazioni](assets/screenshot-2018-2-5healthreports-violations.png)

La verifica stato visualizza le informazioni raccolte da un servizio in background che controlla in modo asincrono ogni volta che viene utilizzato un tipo di risorsa o sovrapposizione in tutti i percorsi di ricerca Sling. Se i mixin di contenuto non vengono utilizzati correttamente, viene segnalata una violazione.
