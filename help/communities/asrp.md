---
title: ASRP - Fornitore di risorse di storage Adobe
seo-title: ASRP - Fornitore di risorse di storage Adobe
description: Configurare AEM Communities per utilizzare un database relazionale come store comune
seo-description: Configurare AEM Communities per utilizzare un database relazionale come store comune
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf

---


# ASRP - Fornitore di risorse di storage Adobe {#asrp-adobe-storage-resource-provider}

## Informazioni su ASRP {#about-asrp}

Quando AEM Communities è configurato per utilizzare ASRP come store comune, il contenuto generato dall&#39;utente (UGC) è accessibile da tutte le istanze di creazione e pubblicazione senza la necessità di eseguire la sincronizzazione e la replica.

Vedere anche [Caratteristiche delle opzioni](/help/communities/working-with-srp.md#characteristics-of-srp-options) SRP e topologie [](/help/communities/topologies.md)consigliate.

## Requisiti {#requirements}

Per l’utilizzo di ASRP è necessaria una licenza aggiuntiva.

Per configurare il sito AEM Communities per l&#39;utilizzo di ASRP per UGC, contatta il rappresentante commerciale di riferimento per:

* URL del centro dati (indirizzo dell’endpoint ASRP)
* Chiave consumer
* Chiave segreta
* ID suite di rapporti

Le chiavi consumer e secret sono condivise tra tutte le suite di rapporti per una società. Esiste una suite di rapporti per tenant.

## Configurazione {#configuration}

### Seleziona ASRP {#select-asrp}

La console [Configurazione](/help/communities/srp-config.md) storage consente di selezionare la configurazione di storage predefinita, che identifica l&#39;implementazione di SRP da utilizzare.

**Nell&#39;istanza di AEM Author:**

* Dalla navigazione globale, andate a **[UIControl Tools > Communities > Storage Configuration]** (Strumenti di controllo UIControl) e selezionate **[UIControl Adobe Storage Resource Provider (ASRP)]**.

![chlimage_1-30](assets/chlimage_1-30.png)

Le seguenti informazioni vengono dal processo di provisioning:

* **URL** centro dati: Estrai per selezionare il centro dati di produzione identificato dal tuo rappresentante commerciale.
* **Suite** di rapporti predefinita: Immettete il nome della suite di rapporti predefinita.
* **Chiave** consumer: Immettete il codice &quot;consumer key&quot;.
* **Segreto**: Immettete il segreto.
* Seleziona **Invia**.

Preparate le istanze di pubblicazione:

* [Replicare la chiave di crittografia](#replicate-the-crypto-key)
* [Replica della configurazione](#publishing-the-configuration)

Dopo aver inviato la configurazione, verificare la connessione:

* Selezionate **Verifica configurazione**.

   Per ogni istanza di creazione e pubblicazione, verificare la connessione al centro dati dalla console Configurazione archiviazione.

* Assicurati che gli URL del sito per i dati del profilo siano instradabili dal centro dati tramite l&#39; [esternalizzazione dei collegamenti](#externalize-links).

### Replicare la chiave Crypto {#replicate-the-crypto-key}

La Chiave Consumatore e la Chiave Segreta sono crittografate. Affinché le chiavi siano crittografate/decrittografate correttamente, la chiave Granite Crypto principale deve essere la stessa in tutte le istanze di AEM.

Seguite le istruzioni riportate in [Replica della chiave](/help/communities/deploy-communities.md#replicate-the-crypto-key)di crittografia.

### Collegamenti esternalizzati {#externalize-links}

Per i collegamenti corretti alle immagini del profilo e del profilo, accertatevi di [configurare correttamente Link Externalizer](/help/sites-developing/externalizer.md).

Accertatevi di impostare i domini come URL che possono essere indirizzati dall’URL del centro dati (endpoint ASRP).

### Sincronizzazione tempo {#time-synchronization}

Affinché l&#39;autenticazione con l&#39;endpoint ASRP abbia esito positivo, i computer che eseguono le community AEM ospitate devono essere sincronizzati in base al tempo, ad esempio con il protocollo NTP ( [Network Time Protocol)](https://www.ntp.org/).

### Pubblicazione della configurazione {#publishing-the-configuration}

L’ASRP deve essere identificato come store comune in tutte le istanze di creazione e pubblicazione.

Per rendere disponibile la stessa configurazione nell’ambiente di pubblicazione:

Nell&#39;istanza di AEM Author:

* Dal menu principale, **[UIControl Tools > Operations > Replication]**.
* Seleziona **Attiva albero**
* **Percorso** iniziale: individuare `/etc/socialconfig/srpc/`
* Deseleziona **solo modifica**
* Seleziona **attiva**

## Aggiornamento da AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Se abilitate ASRP su un sito community pubblicato, tutti gli UGC già memorizzati in [JCR](/help/communities/jsrp.md) non sono più visibili, in quanto non è disponibile la sincronizzazione dei dati tra l&#39;archiviazione locale e l&#39;archiviazione cloud.

**`AEM Communities Extension`** è stato introdotto in precedenza nelle social community di AEM 6.0 come servizio cloud. A partire da AEM 6.1 Communities, non è necessaria alcuna configurazione cloud. È sufficiente selezionare ASRP dalla console [di configurazione](/help/communities/srp-config.md)dello storage.

A causa della nuova struttura di storage, è necessario seguire le istruzioni di [aggiornamento](/help/communities/upgrade.md#adobe-cloud-storage) quando si esegue l&#39;aggiornamento dalle social community alle community.

## Gestione dei dati utente {#managing-user-data}

Per informazioni sugli *utenti*, i profili ** utente e i gruppi *di* utenti, spesso inseriti nell’ambiente di pubblicazione, visita

* [Sincronizzazione utente](/help/communities/sync.md)
* [Gestione di utenti e gruppi di utenti](/help/communities/users.md)

## Risoluzione dei problemi {#troubleshooting}

### UGC scompare dopo l&#39;aggiornamento {#ugc-disappears-after-upgrade}

Se esegui l’aggiornamento da un sito della community social network AEM 6.0 esistente, assicurati di seguire le istruzioni [di](/help/communities/upgrade.md#adobe-cloud-storage)aggiornamento. In caso contrario, UGC non funzionerà più.

### Errori di autenticazione {#authentication-errors}

Se ricevete errori di autenticazione rispetto all’URL del datacenter e il file di registro degli errori AEM contiene messaggi sulle marche temporali non aggiornate, verificate che la sincronizzazione dell’ora sia in corso.

Utilizzate uno strumento come il protocollo NTP ( [Network Time Protocol)](https://www.ntp.org/) per sincronizzare ora tutti i server di creazione e pubblicazione AEM.

### Il nuovo contenuto non viene visualizzato nelle ricerche {#new-content-does-not-appear-in-searches}

L&#39;infrastruttura di storage cloud Adobe utilizza *la coerenza* finale per raggiungere gli obiettivi di scalabilità e prestazioni. Per questo motivo, il nuovo contenuto non è immediatamente disponibile e la sua visualizzazione nei risultati della ricerca richiede alcuni secondi.

Mentre viene monitorato l’intervallo che influisce sull’eventuale coerenza, contattate il rappresentante commerciale di riferimento se le ricerche richiedono più di pochi secondi per visualizzare il nuovo contenuto.

### UGC non visibile nell’ASRP {#ugc-not-visible-in-asrp}

Verificate che l&#39;ASRP sia stato configurato come fornitore predefinito, verificando la configurazione dell&#39;opzione di archiviazione. Per impostazione predefinita, il provider delle risorse di storage è JSRP, non ASRP.

Su tutte le istanze di AEM di creazione e pubblicazione, rivisitate la console Configurazione archiviazione o controllate l&#39;archivio AEM.

In JCR, se [/etc/socialconfig](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* Non contiene un nodo [srpc](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , significa che il provider di archiviazione è JSRP.
* Se il nodo srpc esiste e contiene la configurazione [](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)predefinita del nodo, le proprietà della configurazione predefinita definiscono ASRP come provider predefinito.

