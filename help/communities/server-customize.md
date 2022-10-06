---
title: Personalizzazione lato server
seo-title: Server-side Customization
description: Personalizzazione lato server in AEM Communities
seo-description: Customizing server-side in AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# Personalizzazione lato server {#server-side-customization}

| **[⇐ funzioni di base](essentials.md)** | **[Informazioni sulla personalizzazione lato client](client-customize.md)** |
|---|---|
|  | **[Helpers Handlebars SCF](handlebars-helpers.md)** |

## API Java {#java-apis}

>[!NOTE]
>
>La posizione del pacchetto delle API di Communities è soggetta a modifiche durante l’aggiornamento da una versione principale a quella successiva.

### Interfaccia SocialComponent {#socialcomponent-interface}

I componenti social sono POJO che rappresentano una risorsa per una funzione di AEM Communities. Idealmente, ogni SocialComponent rappresenta un resourceType specifico con GETters esposti che forniscono i dati al client in modo che la risorsa sia correttamente rappresentata. Tutta la logica di business e di visualizzazione è racchiusa nel componente Social, incluse le informazioni sulla sessione del visitatore del sito, se necessario.

L’interfaccia definisce un set di base di GETters necessario per rappresentare una risorsa. Importante: l&#39;interfaccia specifica la mappa&lt;string object=&quot;&quot;> metodi getAsMap() e String toJSONString() necessari per eseguire il rendering dei modelli Handlebar ed esporre gli endpoint GET JSON per le risorse.

Tutte le classi SocialComponent devono implementare l&#39;interfaccia `com.adobe.cq.social.scf.SocialComponent`

### Interfaccia socialCollectionComponent {#socialcollectioncomponent-interface}

L’interfaccia SocialCollectionComponent estende l’interfaccia SocialComponent per rappresentare meglio le risorse che sono raccolte di altre risorse.

Tutte le classi SocialCollectionComponent devono implementare l&#39;interfaccia com.adobe.cq.sosocial.scf.SocialCollectionComponent

### Interfaccia SocialComponentFactory {#socialcomponentfactory-interface}

Una SocialComponentFactory (fabbrica) registra un SocialComponent con il framework. La fabbrica fornisce un mezzo per far sì che il framework sappia quali componenti social sono disponibili per un dato resourceType e la loro classificazione prioritaria quando vengono identificati più componenti social.

SocialComponentFactory è responsabile della creazione di un&#39;istanza del SocialComponent selezionato che consente di inserire tutte le dipendenze necessarie dal SocialComponent dalla fabbrica utilizzando le pratiche di ID.

SocialComponentFactory è un servizio OSGi e ha accesso ad altri servizi OSGi che possono essere passati a SocialComponent tramite un costruttore.

Tutte le classi SocialComponentFactory devono implementare l&#39;interfaccia `com.adobe.cq.social.scf.SocialComponentFactory`

L&#39;implementazione del metodo SocialComponentFactory.getPriority() deve restituire il valore più alto affinché la fabbrica sia utilizzata per la risorsaType specificata come restituita da getResourceType().

### Interfaccia SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (manager) gestisce tutti i SocialComponents registrati con il framework ed è responsabile della selezione di SocialComponentFactory da utilizzare per una determinata risorsa (resourceType). Se non vengono registrate fabbriche per un resourceType specifico, il manager restituirà una fabbrica con il super tipo più vicino per la risorsa specificata.

Un SocialComponentFactoryManager è un servizio OSGi e ha accesso ad altri servizi OSGi che possono essere passati a SocialComponent tramite un costruttore.

Un handle del servizio OSGi si ottiene richiamando `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Richieste POST {#http-api-post-requests}

#### Classe PostOperation {#postoperation-class}

Gli endpoint HTTP API POST sono classi PostOperation definite implementando `SlingPostOperation` interfaccia (pacchetto) `org.apache.sling.servlets.post`).

La `PostOperation` set di implementazione di endpoint `sling.post.operation` a un valore a cui l&#39;operazione risponderà. A questa classe di implementazione verranno delegate tutte le richieste POST con un parametro:operation impostato su tale valore.

La `PostOperation` richiama `SocialOperation` che esegue le azioni necessarie per l&#39;operazione.

La `PostOperation` riceve il risultato dalla `SocialOperation` e restituisce la risposta appropriata al client.

#### Classe SocialOperation {#socialoperation-class}

Ogni `SocialOperation` l&#39;endpoint estende la classe AbstractSocialOperation e sostituisce il metodo `performOperation()`. Questo metodo esegue tutte le azioni necessarie per completare l&#39;operazione e restituire un `SocialOperationResult` oppure genera un `OperationException`, nel qual caso viene restituito uno stato di errore HTTP con un messaggio, se disponibile, al posto del normale codice di risposta JSON o di stato HTTP riuscito.

Estensione `AbstractSocialOperation` consente il riutilizzo di `SocialComponents` per inviare risposte JSON.

#### Classe SocialOperationResult {#socialoperationresult-class}

La `SocialOperationResult` viene restituita come risultato della `SocialOperation` ed è composto da un `SocialComponent`, codice di stato HTTP e messaggio di stato HTTP.

La `SocialComponent` rappresenta la risorsa interessata dall&#39;operazione.

Per un’operazione Crea , la variabile `SocialComponent` incluso nel `SocialOperationResult` rappresenta la risorsa appena creata e, per un’operazione Update, rappresenta la risorsa modificata dall’operazione. No `SocialComponent` viene restituito per un&#39;operazione Delete.

I codici di stato HTTP utilizzati sono:

* 201 per le operazioni di creazione
* 200 per le operazioni di aggiornamento
* 204 per le operazioni di eliminazione

#### Classe OperationException {#operationexception-class}

Un `OperationExcepton` possono essere lanciati quando si esegue un&#39;operazione se la richiesta non è valida o si verifica un altro errore, ad esempio errori interni, valori di parametro non validi, autorizzazioni non corrette e così via. Un `OperationException` è composto da un codice di stato HTTP e un messaggio di errore, che vengono restituiti al client come risposta al `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

Il quadro della componente sociale raccomanda che la logica di business responsabile dell&#39;esecuzione dell&#39;operazione non sia implementata all&#39;interno `SocialOperation` , ma è stato delegato a un servizio OSGi. L&#39;utilizzo di un servizio OSGi per la logica di business consente a `SocialComponent`, agiti da un `SocialOperation` endpoint , da integrare con altro codice e con logica di business diversa applicata.

Tutto `OperationService` estensione delle classi `AbstractOperationService`, che consente estensioni aggiuntive che possono collegarsi all’operazione in esecuzione. Ogni operazione nel servizio è rappresentata da un `SocialOperation` classe. La `OperationExtensions` è possibile richiamare la classe durante l&#39;esecuzione dell&#39;operazione chiamando i metodi

* `performBeforeActions()`

   Consente pre-verifiche/pre-elaborazione e convalide
* `performAfterActions()`

   Consente un&#39;ulteriore modifica delle risorse o richiama eventi personalizzati, flussi di lavoro, ecc.

#### Classe OperationExtension {#operationextension-class}

`OperationExtension` le classi sono pezzi di codice personalizzati che possono essere inseriti in un&#39;operazione che consente la personalizzazione delle operazioni per soddisfare le esigenze aziendali. Gli utenti del componente possono aggiungere funzionalità in modo dinamico e incrementale al componente. Il modello di estensione/hook consente agli sviluppatori di concentrarsi esclusivamente sulle estensioni stesse e rimuove la necessità di copiare e sovrascrivere intere operazioni e componenti.

## Codice di esempio {#sample-code}

Il codice di esempio è disponibile nella variabile [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) archivio. Cerca progetti con prefisso `aem-communities` o `aem-scf`.

## Best practice   {#best-practices}

Visualizza la [Linee guida sulla codifica](code-guide.md) sezione per diverse linee guida per la codifica e best practice per gli sviluppatori AEM Communities.

Vedi anche [Provider di risorse di storage (SRP) per UGC](srp.md) per informazioni sull’accesso ai contenuti generati dagli utenti.

| **[⇐ funzioni di base](essentials.md)** | **[Informazioni sulla personalizzazione lato client](client-customize.md)** |
|---|---|
|  | **[Helpers Handlebars SCF](handlebars-helpers.md)** |
