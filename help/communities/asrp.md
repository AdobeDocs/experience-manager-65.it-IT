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

Vedi anche [Caratteristiche delle opzioni SRP](/help/communities/working-with-srp.md#characteristics-of-srp-options) e [Topologie consigliate](/help/communities/topologies.md).

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

Il [Console di configurazione archiviazione](/help/communities/srp-config.md) consente di selezionare la configurazione di archiviazione predefinita, che identifica l&#39;implementazione di SRP da utilizzare.

**Sull’istanza dell’autore AEM:**

* Dalla navigazione globale, accedi a **[!UICONTROL Strumenti > Community > Configurazione archiviazione]** e seleziona **[!UICONTROL Provider risorsa di archiviazione Adobe (ASRP)]**.

![asrp-default](assets/asrp-default.png)

Le seguenti informazioni provengono dal processo di provisioning:

* **URL del datacenter**: consente di selezionare il data center di produzione identificato dal rappresentante del tuo account.
* **Suite di rapporti predefinita**: immetti il nome della suite di rapporti predefinita.
* **Chiave consumer**: immetti la chiave consumer.
* **Segreto**: inserisci il segreto.
* Seleziona **Invia**.

Prepara le istanze di pubblicazione:

* [Replica la chiave di crittografia](#replicate-the-crypto-key)
* [Replica la configurazione](#publishing-the-configuration)

Dopo aver inviato la configurazione, verifica la connessione:

* Seleziona **Prova configurazione**.

  Per ogni istanza di authoring e pubblicazione, verifica la connessione al centro dati dalla console Configurazione di archiviazione.

* Verificare che gli URL del sito per i dati del profilo siano instradabili dal datacenter [esternalizzazione dei collegamenti](#externalize-links).

### Replica la chiave di crittografia {#replicate-the-crypto-key}

La chiave consumer e la chiave segreta sono crittografate. Affinché le chiavi possano essere crittografate o decrittografate correttamente, la chiave primaria di Granite Crypto deve essere la stessa su tutte le istanze AEM.

Segui le istruzioni all’indirizzo [Replica la chiave di crittografia](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Esternalizzare i collegamenti {#externalize-links}

Per i collegamenti immagine profilo e profilo corretti, assicurati di [Configurare Link Externalizer](/help/sites-developing/externalizer.md).

Assicurarsi di impostare i domini come URL instradabili dall&#39;URL del data center (endpoint ASRP).

### Sincronizzazione ora {#time-synchronization}

Affinché l’autenticazione con l’endpoint ASRP abbia esito positivo, i computer che eseguono l’AEM Communities in hosting devono essere sincronizzati in base all’ora, ad esempio con [NTP (Network Time Protocol)](https://www.ntp.org/).

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
>Se abiliti ASRP in un sito community pubblicato, eventuali contenuti UGC già memorizzati in [JCR](/help/communities/jsrp.md) non è più visibile, in quanto non esiste alcuna sincronizzazione dei dati tra l’archiviazione on-premise e l’archiviazione cloud.

**`AEM Communities Extension`** è stato precedentemente introdotto in social community AEM 6.0 as a cloud service. A partire da AEM 6.1 Communities, non è necessaria alcuna configurazione cloud. È sufficiente selezionare ASRP dal menu [console di configurazione dello storage](/help/communities/srp-config.md).

A causa della nuova struttura di storage, è necessario seguire la [aggiornamento](/help/communities/upgrade.md#adobe-cloud-storage) istruzioni per l’aggiornamento da social community a Communities.

## Gestione dei dati utente {#managing-user-data}

Per informazioni su *utenti*, *profili utente* e *gruppi di utenti*, spesso immesso nell’ambiente di pubblicazione, visita

* [Sincronizzazione utente](/help/communities/sync.md)
* [Gestione di utenti e gruppi di utenti](/help/communities/users.md)

## Risoluzione dei problemi {#troubleshooting}

### UGC scompare dopo l’aggiornamento {#ugc-disappears-after-upgrade}

Se effettui l’aggiornamento da un sito della community social AEM 6.0 esistente, assicurati di seguire la [istruzioni di aggiornamento](/help/communities/upgrade.md#adobe-cloud-storage), altrimenti UGC sembra essere perso.

### Errori di autenticazione {#authentication-errors}

Se ricevi errori di autenticazione rispetto all’URL del centro dati e il file error.log dell’AEM contiene messaggi su marche temporali non aggiornate, verifica che la sincronizzazione dell’ora sia in corso.

Utilizza uno strumento come [NTP (Network Time Protocol)](https://www.ntp.org/) per sincronizzare ora tutti i server di creazione e pubblicazione AEM.

### Il nuovo contenuto non viene visualizzato nelle ricerche {#new-content-does-not-appear-in-searches}

L&#39;infrastruttura di storage cloud di Adobe utilizza *coerenza finale* per raggiungere gli obiettivi di scalabilità e prestazioni. Per questo motivo, i nuovi contenuti non sono immediatamente disponibili e la loro visualizzazione nei risultati di ricerca richiede diversi secondi.

Anche se l’intervallo che influisce sulla coerenza finale è monitorato, contatta il rappresentante del tuo account se la visualizzazione dei nuovi contenuti nelle ricerche richiede più di qualche secondo.

### UGC non visibile in ASRP {#ugc-not-visible-in-asrp}

Verificare che ASRP sia stato configurato come provider predefinito controllando la configurazione dell&#39;opzione di archiviazione. Per impostazione predefinita, il provider di risorse di archiviazione è JSRP, non ASRP.

Su tutte le istanze AEM di authoring e pubblicazione, visita nuovamente la console Configurazione di archiviazione o controlla l’archivio AEM.

In JCR, se [/conf/global/settings/Communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* Non contiene un [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp) significa che il provider di archiviazione è JSRP.
* Se il nodo srpc esiste e contiene [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) , le proprietà defaultconfiguration definiscono ASRP come provider predefinito.
