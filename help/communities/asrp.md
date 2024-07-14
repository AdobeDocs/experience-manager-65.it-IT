---
title: ASRP - Provider risorsa di archiviazione Adobe
description: Impostare AEM Communities per l'utilizzo di un database relazionale come archivio comune
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# ASRP - Provider risorsa di archiviazione Adobe {#asrp-adobe-storage-resource-provider}

## Informazioni su ASRP {#about-asrp}

Quando AEM Communities è configurato per utilizzare ASRP come archivio comune, i contenuti generati dagli utenti (UGC, User Generated Content) sono accessibili da tutte le istanze di authoring e pubblicazione senza la necessità di sincronizzazione o replica.

Vedi anche [Caratteristiche delle opzioni SRP](/help/communities/working-with-srp.md#characteristics-of-srp-options) e [topologie consigliate](/help/communities/topologies.md).

## Requisiti {#requirements}

È necessaria una licenza aggiuntiva per l&#39;utilizzo di ASRP.

Per configurare il sito AEM Communities per l’utilizzo di ASRP per UGC, contatta il rappresentante del tuo account per:

* URL del datacenter (indirizzo dell&#39;endpoint ASRP)
* Chiave consumer
* Chiave segreta
* ID suite di rapporti

Le chiavi consumer e segrete vengono condivise in tutte le suite di rapporti per un’azienda. Esiste una suite di rapporti per tenant.

## Configurazione {#configuration}

### Seleziona ASRP {#select-asrp}

La [console Configurazione archiviazione](/help/communities/srp-config.md) consente di selezionare la configurazione di archiviazione predefinita, che identifica l&#39;implementazione di SRP da utilizzare.

**Sull&#39;istanza di creazione AEM:**

* Dalla navigazione globale, passare a **[!UICONTROL Strumenti > Community > Configurazione archiviazione]** e selezionare **[!UICONTROL Provider risorse di archiviazione Adobe (ASRP)]**.

![asrp-default](assets/asrp-default.png)

Le seguenti informazioni provengono dal processo di provisioning:

* **URL datacenter**: pull-down per selezionare il datacenter di produzione identificato dal rappresentante dell&#39;account.
* **Suite di rapporti predefinita**: immetti il nome della suite di rapporti predefinita.
* **Chiave consumer**: immettere la chiave consumer.
* **Segreto**: immetti il segreto.
* Seleziona **Invia**.

Prepara le istanze di pubblicazione:

* [Replica la chiave di crittografia](#replicate-the-crypto-key)
* [Replica la configurazione](#publishing-the-configuration)

Dopo aver inviato la configurazione, verifica la connessione:

* Seleziona **Prova configurazione**.

  Per ogni istanza di authoring e pubblicazione, verifica la connessione al centro dati dalla console Configurazione di archiviazione.

* Verificare che gli URL del sito per i dati del profilo siano instradabili dal datacenter mediante [esternalizzazione dei collegamenti](#externalize-links).

### Replica la chiave di crittografia {#replicate-the-crypto-key}

La chiave consumer e la chiave segreta sono crittografate. Affinché le chiavi possano essere crittografate o decrittografate correttamente, la chiave primaria di Granite Crypto deve essere la stessa su tutte le istanze AEM.

Segui le istruzioni in [Replica la chiave di crittografia](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Esternalizzare i collegamenti {#externalize-links}

Per i collegamenti immagine profilo e profilo corretti, assicurati di [configurare correttamente Link Externalizer](/help/sites-developing/externalizer.md).

Assicurarsi di impostare i domini come URL instradabili dall&#39;URL del data center (endpoint ASRP).

### Sincronizzazione ora {#time-synchronization}

Affinché l&#39;autenticazione con l&#39;endpoint ASRP abbia esito positivo, è necessario che i computer che eseguono l&#39;AEM Communities ospitato siano sincronizzati in base all&#39;ora, ad esempio con il [protocollo NTP (Network Time Protocol)](https://www.ntp.org/).

### Pubblicazione della configurazione {#publishing-the-configuration}

ASRP deve essere identificato come archivio comune su tutte le istanze di authoring e pubblicazione.

Per rendere disponibile la configurazione identica nell’ambiente di pubblicazione:

Sull’istanza dell’autore AEM:

* Passa dal menu principale a **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]**
* Seleziona **Attiva albero**
* **Percorso iniziale**: passa a `/conf/global/settings/communities/srpc/`
* Deseleziona **Solo Modificato**
* Seleziona **Attiva**

## Aggiornamento da AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Se si abilita ASRP in un sito community pubblicato, qualsiasi UGC già archiviato in [JCR](/help/communities/jsrp.md) non sarà più visibile, in quanto non esiste alcuna sincronizzazione dei dati tra l&#39;archiviazione locale e l&#39;archiviazione cloud.

**`AEM Communities Extension`** è stato introdotto in precedenza nelle social community AEM 6.0 come servizio cloud. A partire da AEM 6.1 Communities, non è necessaria alcuna configurazione cloud. È sufficiente selezionare ASRP dalla [console di configurazione di archiviazione](/help/communities/srp-config.md).

A causa della nuova struttura di archiviazione, è necessario seguire le istruzioni [aggiorna](/help/communities/upgrade.md#adobe-cloud-storage) durante l&#39;aggiornamento da Social community a Communities.

## Gestione dei dati utente {#managing-user-data}

Per informazioni relative a *utenti*, *profili utente* e *gruppi di utenti*, spesso immessi nell&#39;ambiente di pubblicazione, visitare

* [Sincronizzazione utente](/help/communities/sync.md)
* [Gestione di utenti e gruppi di utenti](/help/communities/users.md)

## Risoluzione dei problemi {#troubleshooting}

### UGC scompare dopo l’aggiornamento {#ugc-disappears-after-upgrade}

Se si esegue l&#39;aggiornamento da un sito di social community AEM 6.0 esistente, seguire le [istruzioni di aggiornamento](/help/communities/upgrade.md#adobe-cloud-storage), altrimenti UGC andrà perso.

### Errori di autenticazione {#authentication-errors}

Se ricevi errori di autenticazione rispetto all’URL del centro dati e il file error.log dell’AEM contiene messaggi su marche temporali non aggiornate, verifica che la sincronizzazione dell’ora sia in corso.

Utilizzare uno strumento come [Network Time Protocol (NTP)](https://www.ntp.org/) per sincronizzare in tempo tutti i server di creazione e pubblicazione AEM.

### Il nuovo contenuto non viene visualizzato nelle ricerche {#new-content-does-not-appear-in-searches}

L&#39;infrastruttura di archiviazione cloud Adobe utilizza *coerenza finale* per raggiungere gli obiettivi di scalabilità e prestazioni. Per questo motivo, i nuovi contenuti non sono immediatamente disponibili e la loro visualizzazione nei risultati di ricerca richiede diversi secondi.

Anche se l’intervallo che influisce sulla coerenza finale è monitorato, contatta il rappresentante del tuo account se la visualizzazione dei nuovi contenuti nelle ricerche richiede più di qualche secondo.

### UGC non visibile in ASRP {#ugc-not-visible-in-asrp}

Verificare che ASRP sia stato configurato come provider predefinito controllando la configurazione dell&#39;opzione di archiviazione. Per impostazione predefinita, il provider di risorse di archiviazione è JSRP, non ASRP.

Su tutte le istanze AEM di authoring e pubblicazione, visita nuovamente la console Configurazione di archiviazione o controlla l’archivio AEM.

In JCR, se [/conf/global/settings/Communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* Non contiene un nodo [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp). Il provider di archiviazione è JSRP.
* Se il nodo srpc esiste e contiene il nodo [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration), le proprietà di default configuration definiscono ASRP come provider predefinito.
