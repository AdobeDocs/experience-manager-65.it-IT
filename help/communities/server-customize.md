---
title: Personalizzazione lato server
seo-title: Personalizzazione lato server
description: Personalizzazione lato server in AEM Communities
seo-description: Personalizzazione lato server in AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

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

I componenti social sono POJO che rappresentano una risorsa per una funzione di AEM Communities. Idealmente, ogni SocialComponent rappresenta uno specifico resourceType con GETters esposti che forniscono i dati al client in modo che la risorsa sia correttamente rappresentata. Tutta la logica di business e di visualizzazione è racchiusa in SocialComponent, incluse le informazioni sulla sessione del visitatore del sito, se necessario.

L&#39;interfaccia definisce un set base di GETters necessari per rappresentare una risorsa. L&#39;interfaccia specifica i metodi Map&lt;String, Object> getAsMap() e String toJSONString() necessari per eseguire il rendering dei modelli Handlebars ed esporre gli endpoint GET JSON per le risorse.

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

Gli endpoint POST API HTTP sono classi PostOperation definite implementando l&#39; `SlingPostOperation` interfaccia (pacchetto `org.apache.sling.servlets.post`).

L&#39;implementazione dell&#39; `PostOperation` endpoint viene impostata `sling.post.operation` su un valore a cui l&#39;operazione risponderà. Tutte le richieste POST con un parametro:operation impostato su tale valore verranno delegate a questa classe di implementazione.

Viene `PostOperation` richiamata la `SocialOperation` quale esegue le azioni necessarie per l&#39;operazione.

Il `PostOperation` destinatario riceve il risultato dal `SocialOperation` e restituisce la risposta appropriata al client.

#### Classe SocialOperation {#socialoperation-class}

Ogni `SocialOperation` endpoint estende la classe AbstractSocialOperation e sostituisce il metodo `performOperation()`. Questo metodo esegue tutte le azioni necessarie per completare l&#39;operazione e restituire un errore `SocialOperationResult` o generare un errore `OperationException`, nel qual caso viene restituito uno stato di errore HTTP con un messaggio, se disponibile, al posto del normale codice di risposta JSON o di stato HTTP riuscito.

L’estensione `AbstractSocialOperation` consente il riutilizzo dell’invio di risposte `SocialComponents` JSON.

#### Classe SocialOperationResult {#socialoperationresult-class}

La `SocialOperationResult` classe viene restituita come risultato dell&#39;evento `SocialOperation` ed è composta da un codice di stato `SocialComponent`, HTTP e messaggio di stato HTTP.

Rappresenta `SocialComponent` la risorsa interessata dall&#39;operazione.

Per un&#39;operazione di creazione, l&#39; `SocialComponent` elemento incluso nel `SocialOperationResult` rappresenta la risorsa appena creata e, per un&#39;operazione di aggiornamento, rappresenta la risorsa modificata dall&#39;operazione. Non `SocialComponent` viene restituito alcun valore per un&#39;operazione Delete.

I codici di stato HTTP di successo utilizzati sono:

* 201 per le operazioni di creazione
* 200 per le operazioni di aggiornamento
* 204 per le operazioni Elimina

#### Classe OperationException {#operationexception-class}

Se la richiesta non è valida o si verifica un altro errore, `OperationExcepton` è possibile generare un messaggio di errore durante l&#39;esecuzione di un&#39;operazione, ad esempio errori interni, valori errati dei parametri, autorizzazioni non corrette e così via. Un messaggio `OperationException` è composto da un codice di stato HTTP e un messaggio di errore, che vengono restituiti al client come risposta al `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

Il framework dei componenti sociali raccomanda che la logica aziendale responsabile dell&#39;esecuzione dell&#39;operazione non sia implementata all&#39;interno della `SocialOperation` classe, ma delegata a un servizio OSGi. L&#39;utilizzo di un servizio OSGi per la business logic consente a un `SocialComponent`, agendo in base a un `SocialOperation` endpoint, di essere integrato con altro codice e di applicare diverse logiche aziendali.

Tutte `OperationService` le classi si estendono `AbstractOperationService`, consentendo ulteriori estensioni che possono collegarsi all&#39;operazione in corso. Ogni operazione nel servizio è rappresentata da una `SocialOperation` classe. La `OperationExtensions` classe può essere invocata durante l&#39;esecuzione dell&#39;operazione chiamando i metodi

* `performBeforeActions()`

   Consente pre-verifiche/pre-elaborazione e convalide
* `performAfterActions()`

   Consente di modificare ulteriormente le risorse o richiamare eventi personalizzati, flussi di lavoro ecc.

#### Classe OperationExtension {#operationextension-class}

`OperationExtension` le classi sono pezzi di codice personalizzati che possono essere inseriti in un&#39;operazione che consente la personalizzazione delle operazioni per soddisfare le esigenze aziendali. Gli utenti del componente possono aggiungere al componente in modo dinamico e incrementale funzionalità. Il pattern di estensione/gancio consente agli sviluppatori di concentrarsi esclusivamente sulle estensioni stesse e elimina la necessità di copiare e sovrascrivere intere operazioni e componenti.

## Codice di esempio {#sample-code}

Il codice di esempio è disponibile nell’archivio GitHub [di](https://github.com/Adobe-Marketing-Cloud) Adobe Marketing Cloud. Cercare progetti con un prefisso `aem-communities` o `aem-scf`.

## Best practice   {#best-practices}

Consultate la sezione Linee guida [per la](code-guide.md) codifica per diverse linee guida e best practice per gli sviluppatori di AEM Communities.

Per informazioni sull&#39;accesso ai contenuti generati dall&#39;utente, consultate anche [Storage Resource Provider (SRP) per UGC](srp.md) .

| **[⇐ Funzioni Essenziali](essentials.md)** | **[Personalizzazione lato client ⇒](client-customize.md)** |
|---|---|
|  | **[Helper manubrio SCF](handlebars-helpers.md)** |

