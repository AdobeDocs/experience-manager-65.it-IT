---
title: Aggiornamenti sostenibili
seo-title: Aggiornamenti sostenibili
description: Scopri gli aggiornamenti sostenibili in AEM 6.4.
seo-description: Scopri gli aggiornamenti sostenibili in AEM 6.4.
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# Aggiornamenti sostenibili{#sustainable-upgrades}

## Framework di personalizzazione {#customization-framework}

### Architettura (funzionalità/infrastruttura/contenuto/applicazione) {#architecture-functional-infrastructure-content-application}

La funzione Customization Framework consente di ridurre le violazioni nelle aree non estensibili del codice (come APIS) o del contenuto (come le sovrapposizioni) che non sono facili da aggiornare.

Esistono due componenti del framework di personalizzazione: **Superficie API** e **Classificazione contenuto**.

#### Superficie API {#api-surface}

Nelle versioni precedenti di AEM molte API erano esposte tramite Uber Jar. Alcune di queste API non erano destinate ai clienti, ma erano esposte al supporto AEM funzionalità tra i bundle. In futuro, le API Java saranno contrassegnate come Pubbliche o Private per indicare ai clienti quali API sono sicure da utilizzare nel contesto degli aggiornamenti. Altre specifiche includono:

* Le API Java contrassegnate come `Public` possono essere utilizzate e a cui fanno riferimento i bundle di implementazione personalizzati.

* Le API pubbliche saranno compatibili con l&#39;installazione di un pacchetto di compatibilità.
* Il pacchetto di compatibilità conterrà un Uber JAR compatibile per garantire la compatibilità con le versioni precedenti
* Le API Java contrassegnate come `Private` sono destinate ad essere utilizzate solo AEM bundle interni e non devono essere utilizzate da bundle personalizzati.

>[!NOTE]
>
>Il concetto di `Private` e `Public` in questo contesto non deve essere confuso con le nozioni Java delle classi pubbliche e private.

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### Classificazioni contenuto {#content-classifications}

AEM da tempo utilizza l’entità delle sovrapposizioni e Sling Resource Merger per consentire ai clienti di estendere e personalizzare AEM funzionalità. Le funzionalità predefinite per l&#39;utilizzo delle console AEM e dell&#39;interfaccia utente sono memorizzate in **/libs**. I clienti non devono mai modificare nulla sotto **/libs**, ma possono aggiungere contenuto aggiuntivo sotto **/apps** per sovrapporre ed estendere le funzionalità definite in **/libs** (per ulteriori informazioni, consultate Sviluppo con sovrapposizioni). Ciò causava ancora numerosi problemi durante l&#39;aggiornamento AEM come contenuto in **/libs**, causando possibili interruzioni impreviste della funzionalità di sovrapposizione. I clienti possono anche estendere AEM componenti attraverso l&#39;ereditarietà tramite `sling:resourceSuperType`, oppure fare semplicemente riferimento a un componente in **/libs** direttamente tramite sling:resourceType. Problemi simili di aggiornamento possono verificarsi con i casi di utilizzo di riferimento e ignorare.

Per rendere più sicuro e facile per i clienti capire quali aree di **/libs** sono sicure da utilizzare e sovrapporre il contenuto in **/libs** è stato classificato con i seguenti mixin:

* **Public (granite:PublicArea)**  - Definisce un nodo come pubblico in modo che possa essere sovrapposto, ereditato (  `sling:resourceSuperType`) o utilizzato direttamente (  `sling:resourceType`). I nodi sotto /libs contrassegnati come Pubblico saranno sicuri da aggiornare con l&#39;aggiunta di un pacchetto di compatibilità. In generale, i clienti devono solo sfruttare i nodi contrassegnati come Pubblico.

* **Abstract (granite:AbstractArea)**  - Definisce un nodo come astratto. I nodi possono essere sovrapposti o ereditati ( `sling:resourceSupertype`) ma non devono essere utilizzati direttamente ( `sling:resourceType`).

* **Final (granite:FinalArea)**  - Definisce un nodo come finale. I nodi classificati come finali idealmente non devono essere sovrapposti o ereditati. I nodi finali possono essere utilizzati direttamente tramite `sling:resourceType`. I sottonodi sotto il nodo finale sono considerati interni per impostazione predefinita.

* ***Internal (granite:InternalArea)*** *- *Definisce un nodo come interno. I nodi classificati come interni idealmente non devono essere sovrapposti, ereditati o utilizzati direttamente. Questi nodi sono destinati solo alla funzionalità interna di AEM

* **Nessuna annotazione** : i nodi ereditano la classificazione in base alla gerarchia ad albero. Per impostazione predefinita, / root è Pubblico. **Anche i nodi con un elemento padre classificato come interno o finale devono essere trattati come interni.**

>[!NOTE]
>
>Questi criteri vengono applicati solo ai meccanismi basati sul percorso di ricerca Sling. Altre aree di **/libs** come una libreria lato client possono essere contrassegnate come `Internal`, ma possono essere comunque utilizzate con l&#39;inclusione clientlib standard. È importante che un cliente continui a rispettare la classificazione interna in questi casi.

#### Indicatori del tipo di contenuto CRXDE Lite {#crxde-lite-content-type-indicators}

Le miscele applicate nei CRXDE Lite mostreranno nodi di contenuto e strutture ad albero contrassegnate come `INTERNAL` in grigio. Per `FINAL` solo l&#39;icona è disattivata. Anche gli elementi secondari di questi nodi risulteranno grigi. In entrambi i casi, la funzionalità Overlay Node (Nodo sovrapposizione) è disabilitata.

**Pubblico**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Finale**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**Interno**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Controllo integrità contenuto**

>[!NOTE]
>
>A AEM 6.5,  Adobe consiglia di utilizzare il Rilevatore pattern per rilevare le violazioni dell&#39;accesso ai contenuti. I report dei rilevatori di pattern sono più dettagliati, rilevano più problemi e riducono la probabilità di falsi positivi.
>
>Per ulteriori informazioni, vedere [Valutare la complessità dell&#39;aggiornamento con il rilevatore di pattern](/help/sites-deploying/pattern-detector.md).

AEM 6.5 invierà un controllo dello stato per avvisare i clienti se il contenuto sovrapposto o di riferimento viene utilizzato in modo non coerente con la classificazione del contenuto.

Il** Sling/Granite Content Access Check** è un nuovo controllo dello stato che controlla l&#39;archivio per verificare se il codice cliente accede in modo errato ai nodi protetti in AEM.

Questa operazione eseguirà la scansione di **/apps** e in genere richiede diversi secondi per essere completata.

Per accedere a questa nuova verifica dello stato di salute, è necessario effettuare le seguenti operazioni:

1. Dalla schermata iniziale AEM, passare a **Strumenti > Operazioni > Rapporti stato**
1. Fare clic su **Sling/Granite Content Access Check** come mostrato di seguito:

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

Al termine dell&#39;analisi, verrà visualizzato un elenco di avvisi che avvisano un utente finale del nodo protetto a cui viene fatto riferimento in modo non corretto:

![screenshot-2018-2-5Health Reports](assets/screenshot-2018-2-5healthreports.png)

Dopo aver riparato le violazioni, ritornerà allo stato verde:

![screenshot-2018-2-5Health Reports-Violazioni](assets/screenshot-2018-2-5healthreports-violations.png)

La verifica dello stato mostra le informazioni raccolte da un servizio in background che verifica in modo asincrono ogni volta che una sovrapposizione o un tipo di risorsa viene utilizzata in tutti i percorsi di ricerca Sling. Se le miscele di contenuto vengono utilizzate in modo errato, viene segnalata una violazione.
