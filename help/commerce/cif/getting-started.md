---
title: Guida introduttiva a AEM Content and Commerce
description: Scopri come distribuire un progetto di contenuti e commerce AEM.
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 6%

---

# Guida introduttiva a AEM Content and Commerce {#start}

Per iniziare a utilizzare i contenuti e il commercio dell’AEM, è necessario installare il componente aggiuntivo Contenuto e commercio dell’AEM per AEM 6.5.

## Requisiti minimi del software

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html) 7 o versione successiva.

## Onboarding {#onboarding}

L’onboarding per i contenuti e il commercio dell’AEM è un processo in due fasi:

1. Installare il componente aggiuntivo AEM Content and Commerce per AEM 6.5

2. Collegare l’AEM alla soluzione commerce

### Installare il componente aggiuntivo AEM Content and Commerce per AEM 6.5 {#install-add-on}

Scarica e installa il componente aggiuntivo AEM Commerce per AEM 6.5 da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html) portale.

Avviare e installare il Service Pack di AEM 6.5 richiesto. È consigliabile installare l&#39;ultimo service pack disponibile.

>[!NOTE]
>
>Ciò sarà effettuato dal CSE per i clienti di servizi gestiti AEM.

### Collegare AEM al sistema Commerce {#connect}

L&#39;AEM può essere connesso a qualsiasi sistema commerciale che abbia un endpoint GraphQL accessibile per l&#39;AEM. Questi endpoint sono solitamente disponibili pubblicamente o possono essere collegati tramite VPN private o connessioni locali a seconda della configurazione del singolo progetto.

In alternativa, è possibile fornire l’intestazione di autenticazione per utilizzare funzioni CIF aggiuntive che richiedono l’autenticazione.

Progetti generati da [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype)e [Negozio di riferimento AEM Venia](https://github.com/adobe/aem-cif-guides-venia) che è già incluso nel [configurazione predefinita](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) deve essere regolato.

Sostituisci il valore di `url` in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con l’endpoint GraphQL del sistema commerce. Questa configurazione può essere eseguita tramite la console OSGI o distribuendo la configurazione OSGI tramite il progetto. Sono supportate diverse configurazioni per i sistemi di staging e produzione utilizzando diverse modalità di esecuzione dell’AEM.

Il componente aggiuntivo AEM Content and Commerce e i componenti core CIF utilizzano connessioni lato server e client dell’AEM. I componenti core CIF lato client e gli strumenti di authoring del componente aggiuntivo CIF si connettono per impostazione predefinita a `/api/graphql`. Se necessario, questo può essere regolato tramite la configurazione del Cloud Service CIF (vedi sotto).

Il componente aggiuntivo CIF fornisce un servlet proxy di GraphQL all&#39;indirizzo `/api/graphql` che possono essere facoltativamente utilizzati per [sviluppo locale](develop.md). Per le distribuzioni in produzione, si consiglia vivamente di impostare un proxy inverso all’endpoint commerce GraphQL tramite il Dispatcher dell’AEM o ad altri livelli di rete (come CDN).

## Configurazione di store e cataloghi {#catalog}

Il componente aggiuntivo e [Componenti core CIF](https://github.com/adobe/aem-core-cif-components) può essere utilizzato su più strutture di siti AEM collegate a diversi store commerciali (o viste store, ecc.). Per impostazione predefinita, il componente aggiuntivo CIF viene distribuito con una configurazione predefinita che si connette all’archivio e al catalogo predefiniti di Adobe Commerce.

Questa configurazione può essere regolata per il progetto tramite la configurazione di Cloud Service CIF, come segue:

1. In AEM vai a Strumenti -> Cloud Services -> Configurazione CIF.

2. Seleziona la configurazione commerce da modificare

3. Apri le proprietà di configurazione tramite la barra delle azioni

![Configurazione Cloud Services CIF](/help/commerce/cif/assets/cif-cloud-service-config.png)

È possibile configurare le seguenti proprietà:

- Client GraphQL: seleziona il client GraphQL configurato per la comunicazione back-end commerce. In genere, questa impostazione deve rimanere quella predefinita.
- Visualizzazione store: l&#39;identificatore della visualizzazione store. Se vuota, verrà utilizzata la vista archivio predefinita.
- Percorso proxy GraphQL: il percorso URL che il proxy GraphQL dell’AEM utilizza per inoltrare le richieste all’endpoint GraphQL backend di Commerce.

   >[!NOTE]
   >
   >Nella maggior parte delle impostazioni il valore predefinito `/api/graphql` non deve essere modificato. Questa impostazione può essere modificata solo da una configurazione avanzata che non utilizza il proxy GraphQL fornito.

- Abilita supporto UID catalogo: abilita il supporto per UID invece dell’ID nelle chiamate GraphQL di back-end per e-commerce.

   >[!NOTE]
   >
   >Il supporto per gli UID è stato introdotto in Adobe Commerce 2.4.2. Abilita questa opzione solo se il backend di e-commerce supporta uno schema GraphQL della versione 2.4.2 o successiva.

- Identificatore categoria radice catalogo: l’identificatore (UID o ID) della radice del catalogo dell’archivio

   >[!CAUTION]
   >
   >A partire dalla versione 2.0.0 dei componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. Se il progetto utilizza i componenti core CIF versione 2.0.0, devi abilitare il supporto UID del catalogo e utilizzare un UID di categoria valido come &quot;Identificatore della categoria principale del catalogo&quot;.

La configurazione mostrata sopra è a scopo di riferimento. I progetti devono fornire le proprie configurazioni.

Per configurazioni più complesse che utilizzano più strutture di siti AEM combinate con diversi cataloghi di e-commerce, vedi [Configurazione di più store di Commerce](configuring/multi-store-setup.md) esercitazione.

## Risorse aggiuntive {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Configurazione di più store di Commerce](configuring/multi-store-setup.md)
