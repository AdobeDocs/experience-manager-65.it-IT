---
title: Personalizzazione lato server
seo-title: Personalizzazione lato server
description: Personalizzazione lato server in  AEM Communities
seo-description: Personalizzazione lato server in  AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---


# Personalizzazione lato server {#server-side-customization}

| **[⇐ Funzioni Essenziali](essentials.md)** | **[Personalizzazione lato client ⇒](client-customize.md)** |
|---|---|
|  | **[Helper manubrio SCF](handlebars-helpers.md)** |

## API Java {#java-apis}

>[!NOTE]
>
>La posizione del pacchetto delle API Community è soggetta a modifiche quando si esegue l&#39;aggiornamento da una versione principale a quella successiva.

### Interfaccia SocialComponent {#socialcomponent-interface}

I componenti social sono POJO che rappresentano una risorsa per una funzione AEM Communities . Idealmente, ogni SocialComponent rappresenta uno specifico resourceType con GETters esposti che forniscono i dati al client in modo che la risorsa sia correttamente rappresentata. Tutta la logica di business e di visualizzazione è racchiusa in SocialComponent, incluse le informazioni sulla sessione del visitatore del sito, se necessario.

L&#39;interfaccia definisce un set base di GETters necessari per rappresentare una risorsa. È importante notare che l&#39;interfaccia specifica i metodi Map&lt;String, Object> getAsMap() e String toJSONString() necessari per eseguire il rendering dei modelli Handlebars ed esporre gli endpoint JSON GET per le risorse.

Tutte le classi SocialComponent devono implementare l&#39;interfaccia `com.adobe.cq.social.scf.SocialComponent`

### Interfaccia SocialCollectionComponent {#socialcollectioncomponent-interface}

L&#39;interfaccia SocialCollectionComponent estende l&#39;interfaccia SocialComponent per rappresentare meglio le risorse che sono raccolte di altre risorse.

Tutte le classi SocialCollectionComponent devono implementare l&#39;interfaccia com.adobe.cq.social.scf.SocialCollectionComponent

### Interfaccia SocialComponentFactory {#socialcomponentfactory-interface}

Un SocialComponentFactory (factory) registra un SocialComponent con il framework. La fabbrica fornisce un mezzo per far sapere al framework quali SocialComponents sono disponibili per un dato resourceType e la loro classificazione di priorità quando vengono identificati più SocialComponents.

SocialComponentFactory è responsabile della creazione di un&#39;istanza del SocialComponent selezionato che consente di inserire tutte le dipendenze necessarie dal SocialComponent dalla fabbrica utilizzando le procedure DI.

SocialComponentFactory è un servizio OSGi e ha accesso ad altri servizi OSGi che possono essere passati a SocialComponent tramite un costruttore.

Tutte le classi SocialComponentFactory devono implementare l&#39;interfaccia `com.adobe.cq.social.scf.SocialComponentFactory`

L&#39;implementazione del metodo SocialComponentFactory.getPriority() deve restituire il valore più alto affinché la fabbrica venga utilizzata per il resourceType specificato come restituito da getResourceType().

### Interfaccia SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (manager) gestisce tutti i SocialComponents registrati con il framework ed è responsabile della selezione di SocialComponentFactory da utilizzare per una determinata risorsa (resourceType). Se non sono registrate fabbriche per uno specifico resourceType, il manager restituirà una fabbrica con il super type più vicino per la risorsa specificata.

Un SocialComponentFactoryManager è un servizio OSGi e ha accesso ad altri servizi OSGi che possono essere passati a SocialComponent tramite un costruttore.

Un handle per il servizio OSGi viene ottenuto richiamando `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Richieste POST {#http-api-post-requests}

#### Classe PostOperation {#postoperation-class}

Gli endpoint POST API HTTP sono classi PostOperation definite implementando l&#39;interfaccia `SlingPostOperation` (pacchetto `org.apache.sling.servlets.post`).

L&#39;implementazione dell&#39;endpoint `PostOperation` imposta `sling.post.operation` su un valore a cui l&#39;operazione risponderà. Tutte le richieste di POST con un parametro:operation impostato su tale valore verranno delegate a questa classe di implementazione.

L&#39;elemento `PostOperation` richiama l&#39;elemento `SocialOperation` che esegue le azioni necessarie per l&#39;operazione.

Il `PostOperation` riceve il risultato dal `SocialOperation` e restituisce la risposta appropriata al client.

#### Classe SocialOperation {#socialoperation-class}

Ogni endpoint `SocialOperation` estende la classe AbstractSocialOperation e sostituisce il metodo `performOperation()`. Questo metodo esegue tutte le azioni necessarie per completare l&#39;operazione e restituire un `SocialOperationResult` oppure generare un `OperationException`, nel qual caso viene restituito uno stato di errore HTTP con un messaggio, se disponibile, al posto del normale codice di risposta JSON o di stato HTTP riuscito.

L&#39;estensione di `AbstractSocialOperation` consente il riutilizzo di `SocialComponents` per inviare risposte JSON.

#### Classe SocialOperationResult {#socialoperationresult-class}

La classe `SocialOperationResult` viene restituita come risultato di `SocialOperation` ed è composta da un `SocialComponent`, da un codice di stato HTTP e da un messaggio di stato HTTP.

L&#39;elemento `SocialComponent` rappresenta la risorsa interessata dall&#39;operazione.

Per un&#39;operazione di creazione, la `SocialComponent` inclusa nella `SocialOperationResult` rappresenta la risorsa appena creata e, per un&#39;operazione di aggiornamento, rappresenta la risorsa modificata dall&#39;operazione. Per un&#39;operazione di eliminazione non viene restituito nessun `SocialComponent`.

I codici di stato HTTP di successo utilizzati sono:

* 201 per le operazioni di creazione
* 200 per le operazioni di aggiornamento
* 204 per le operazioni Elimina

#### Classe OperationException {#operationexception-class}

Durante l&#39;esecuzione di un&#39;operazione è possibile generare un `OperationExcepton` se la richiesta non è valida o si verifica un altro errore, ad esempio errori interni, valori errati dei parametri, autorizzazioni non corrette e così via. Un `OperationException` è composto da un codice di stato HTTP e un messaggio di errore, che vengono restituiti al client come risposta al `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

Il framework dei componenti social consiglia di non implementare la logica di business responsabile dell&#39;esecuzione dell&#39;operazione all&#39;interno della classe `SocialOperation`, ma di delegarla a un servizio OSGi. L&#39;utilizzo di un servizio OSGi per la logica aziendale consente di integrare un `SocialComponent`, basato su un endpoint `SocialOperation` con un altro codice e applicare una logica aziendale diversa.

Tutte le classi `OperationService` estendono `AbstractOperationService`, consentendo estensioni aggiuntive che possono collegarsi all&#39;operazione in corso. Ogni operazione nel servizio è rappresentata da una classe `SocialOperation`. La classe `OperationExtensions` può essere richiamata durante l&#39;esecuzione dell&#39;operazione chiamando i metodi

* `performBeforeActions()`

   Consente pre-verifiche/pre-elaborazione e convalide
* `performAfterActions()`

   Consente di modificare ulteriormente le risorse o richiamare eventi personalizzati, flussi di lavoro ecc.

#### Classe OperationExtension {#operationextension-class}

`OperationExtension` le classi sono pezzi di codice personalizzati che possono essere inseriti in un&#39;operazione che consente la personalizzazione delle operazioni per soddisfare le esigenze aziendali. Gli utenti del componente possono aggiungere al componente in modo dinamico e incrementale funzionalità. Il pattern di estensione/gancio consente agli sviluppatori di concentrarsi esclusivamente sulle estensioni stesse e elimina la necessità di copiare e sovrascrivere intere operazioni e componenti.

## Codice di esempio {#sample-code}

Il codice di esempio è disponibile nell&#39;archivio [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud). Cercare progetti con il prefisso `aem-communities` o `aem-scf`.

## Best practice   {#best-practices}

Per informazioni su diverse linee guida di codifica e best practice per  sviluppatori AEM Communities, vedere la sezione [Linee guida di codifica](code-guide.md).

Vedere anche [Storage Resource Provider (SRP) per UGC](srp.md) per informazioni sull&#39;accesso ai contenuti generati dall&#39;utente.

| **[⇐ Funzioni Essenziali](essentials.md)** | **[Personalizzazione lato client ⇒](client-customize.md)** |
|---|---|
|  | **[Helper manubrio SCF](handlebars-helpers.md)** |

