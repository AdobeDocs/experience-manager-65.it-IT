---
title: Personalizzazione lato server
description: Scopri come personalizzare lato server in Adobe Experience Manager Communities.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# Personalizzazione lato server {#server-side-customization}

| **[⇐ caratteristiche di base](essentials.md)** | **[Personalizzazione lato client ⇒](client-customize.md)** |
|---|---|
|   | **[Helper Handlebars SCF ⇒](handlebars-helpers.md)** |

## API Java™ {#java-apis}

>[!NOTE]
>
>La posizione del pacchetto delle API Communities è soggetta a modifiche durante l’aggiornamento da una versione principale alla successiva.

### Interfaccia SocialComponent {#socialcomponent-interface}

I SocialComponents sono POJO che rappresentano una risorsa per una funzione di AEM Communities. Idealmente, ogni SocialComponent rappresenta un resourceType specifico con GETters esposti che forniscono dati al client in modo che la risorsa sia rappresentata accuratamente. Tutta la logica di business e di visualizzazione è incapsulata in SocialComponent, incluse le informazioni sulla sessione del visitatore del sito, se necessario.

L’interfaccia definisce un set di base di GETter necessari per rappresentare una risorsa. È importante sottolineare che l’interfaccia stabilisce i metodi Map&lt;String, Object> getAsMap() e String toJSONString() necessari per eseguire il rendering dei modelli Handlebars ed esporre gli endpoint JSON di GET per le risorse.

Tutte le classi SocialComponent devono implementare l&#39;interfaccia `com.adobe.cq.social.scf.SocialComponent`

### Interfaccia SocialCollectionComponent {#socialcollectioncomponent-interface}

L’interfaccia SocialCollectionComponent estende l’interfaccia SocialComponent per rappresentare meglio le risorse che sono insiemi di altre risorse.

Tutte le classi SocialCollectionComponent devono implementare l&#39;interfaccia com.adobe.cq.social.scf.SocialCollectionComponent

### Interfaccia SocialComponentFactory {#socialcomponentfactory-interface}

Un SocialComponentFactory (factory) registra un SocialComponent con il framework. La fabbrica fornisce un mezzo per consentire al framework di sapere quali componenti social sono disponibili per un dato resourceType e la loro classificazione di priorità quando vengono identificati più componenti social.

Un SocialComponentFactory è responsabile della creazione di un&#39;istanza del SocialComponent selezionato che consente di inserire tutte le dipendenze necessarie dal SocialComponent dalla factory utilizzando le procedure DI.

SocialComponentFactory è un servizio OSGi e ha accesso ad altri servizi OSGi che possono essere passati a SocialComponent tramite un costruttore.

Tutte le classi SocialComponentFactory devono implementare l&#39;interfaccia `com.adobe.cq.social.scf.SocialComponentFactory`

Un&#39;implementazione del metodo SocialComponentFactory.getPriority() deve restituire il valore più alto per la factory da utilizzare per il resourceType specificato, come restituito da getResourceType().

### Interfaccia SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (manager) gestisce tutti i SocialComponents registrati con il framework ed è responsabile della selezione di SocialComponentFactory da utilizzare per una determinata risorsa (resourceType). Se non sono registrate fabbriche per un resourceType specifico, il manager restituisce una fabbrica con il super type più vicino per la risorsa specificata.

SocialComponentFactoryManager è un servizio OSGi e ha accesso ad altri servizi OSGi che possono essere passati a SocialComponent tramite un costruttore.

Ottenuto un handle per il servizio OSGi richiamando `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Richieste POST {#http-api-post-requests}

#### Classe PostOperation {#postoperation-class}

Gli endpoint POST API HTTP sono classi PostOperation definite implementando l&#39;interfaccia `SlingPostOperation` (pacchetto `org.apache.sling.servlets.post`).

L&#39;implementazione dell&#39;endpoint `PostOperation` imposta `sling.post.operation` su un valore al quale risponde l&#39;operazione. Tutte le richieste POST con il parametro:operation impostato su tale valore sono delegate a questa classe di implementazione.

`PostOperation` richiama `SocialOperation` che esegue le azioni necessarie per l&#39;operazione.

`PostOperation` riceve il risultato da `SocialOperation` e restituisce la risposta appropriata al client.

#### Classe SocialOperation {#socialoperation-class}

Ogni endpoint `SocialOperation` estende la classe AbstractSocialOperation e sostituisce il metodo `performOperation()`. Questo metodo esegue tutte le azioni necessarie per completare l&#39;operazione e restituire `SocialOperationResult` oppure generare `OperationException`. In questo caso, al posto della normale risposta JSON o del codice di stato HTTP di successo viene restituito uno stato di errore HTTP con un messaggio, se disponibile.

L&#39;estensione di `AbstractSocialOperation` consente di riutilizzare `SocialComponents` per inviare risposte JSON.

#### Classe SocialOperationResult {#socialoperationresult-class}

La classe `SocialOperationResult` viene restituita come risultato di `SocialOperation` ed è composta da un `SocialComponent`, un codice di stato HTTP e un messaggio di stato HTTP.

`SocialComponent` rappresenta la risorsa interessata dall&#39;operazione.

Per un&#39;operazione Create, `SocialComponent` incluso in `SocialOperationResult` rappresenta la risorsa creata e per un&#39;operazione Update rappresenta la risorsa modificata dall&#39;operazione. Nessun `SocialComponent` restituito per un&#39;operazione di eliminazione.

I codici di stato HTTP utilizzati sono:

* 201 per operazioni di creazione
* 200 per le operazioni di aggiornamento
* 204 per le operazioni di eliminazione

#### Classe OperationException {#operationexception-class}

Viene generato un `OperationExcepton` quando si esegue un&#39;operazione se la richiesta non è valida o si verifica un altro errore. Ad esempio, errori interni, valori di parametro non validi o autorizzazioni non corrette. Un `OperationException` è composto da un codice di stato HTTP e da un messaggio di errore, che vengono restituiti al client come risposta a `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

Il framework del componente social consiglia di non implementare la regola business responsabile dell&#39;esecuzione dell&#39;operazione nella classe `SocialOperation`, ma di delegarla a un servizio OSGi. L&#39;utilizzo di un servizio OSGi per la logica di business consente a un `SocialComponent`, gestito da un endpoint `SocialOperation`, di essere integrato con altro codice e di applicare una logica di business diversa.

Tutte le classi `OperationService` estendono `AbstractOperationService`, consentendo estensioni aggiuntive che possono connettersi all&#39;operazione in esecuzione. Ogni operazione nel servizio è rappresentata da una classe `SocialOperation`. La classe `OperationExtensions` può essere richiamata durante l&#39;esecuzione dell&#39;operazione chiamando i metodi

* `performBeforeActions()`

  Consente pre-controlli/pre-elaborazione e convalide
* `performAfterActions()`

  Consente di modificare ulteriormente le risorse o richiamare eventi personalizzati, flussi di lavoro e così via.

#### Classe OperationExtension {#operationextension-class}

Le classi `OperationExtension` sono parti di codice personalizzate che possono essere inserite in un&#39;operazione che consente di personalizzare le operazioni in base alle esigenze aziendali. I consumatori del componente possono aggiungere funzionalità al componente in modo dinamico e incrementale. Il pattern di estensione/hook consente agli sviluppatori di concentrarsi esclusivamente sulle estensioni stesse e elimina la necessità di copiare e sovrascrivere intere operazioni e componenti.

## Codice di esempio {#sample-code}

Il codice di esempio è disponibile nell&#39;archivio [Adobe Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud). Cerca i progetti con prefisso `aem-communities` o `aem-scf`.

## Best practice {#best-practices}

Consulta la sezione [Linee guida per la codifica](code-guide.md) per scoprire varie linee guida per la codifica e best practice per gli sviluppatori di AEM Communities.

Per informazioni sull&#39;accesso ai contenuti generati dall&#39;utente, vedere anche [Provider risorse di archiviazione (SRP) per UGC](srp.md).

| **[⇐ caratteristiche di base](essentials.md)** | **[Personalizzazione lato client ⇒](client-customize.md)** |
|---|---|
|   | **[Helper Handlebars SCF ⇒](handlebars-helpers.md)** |
