---
title: Guida introduttiva ai contenuti di AEM e Commerce
description: Scopri come distribuire un progetto AEM Content and Commerce.
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 9%

---

# Guida introduttiva ai contenuti di AEM e Commerce {#start}

Per iniziare a utilizzare AEM Content e Commerce, è necessario installare AEM Content and Commerce Add-On for AEM 6.5.

## Requisiti minimi del software

[È richiesto AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html) 7 o versione successiva.

## Onboarding {#onboarding}

L’onboarding per AEM Content e Commerce è un processo in due fasi:

1. Installare il componente aggiuntivo AEM Content and Commerce per AEM 6.5

2. Collegare AEM alla soluzione commerce

### Installare il componente aggiuntivo AEM Content and Commerce per AEM 6.5 {#install-add-on}

Scarica e installa il componente aggiuntivo AEM Commerce per AEM 6.5 dal portale [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html).

Avvia e installa il Service Pack di AEM 6.5 richiesto. È consigliabile installare l&#39;ultimo service pack disponibile.

>[!NOTE]
>
>Questa operazione verrà eseguita dal CSE per i clienti di AEM Managed Service.

### Collegare AEM al sistema Commerce {#connect}

AEM può essere connesso a qualsiasi sistema commerce con un endpoint GraphQL accessibile per AEM. Questi endpoint sono solitamente disponibili pubblicamente o possono essere collegati tramite VPN private o connessioni locali a seconda della configurazione del singolo progetto.

In alternativa, è possibile fornire un’intestazione di autenticazione per utilizzare funzioni CIF aggiuntive che richiedono l’autenticazione.

I progetti generati da [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype) e [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) già inclusi nella [configurazione predefinita](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) devono essere regolati.

Sostituisci il valore di `url` in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con l&#39;endpoint GraphQL del tuo sistema commerce. Questa configurazione può essere eseguita tramite la console OSGI o distribuendo la configurazione OSGI tramite il progetto. Sono supportate diverse configurazioni per i sistemi di staging e produzione utilizzando diverse modalità di esecuzione di AEM.

I componenti aggiuntivi AEM Content and Commerce e CIF Core utilizzano connessioni lato server e client di AEM. Per impostazione predefinita, i componenti core CIF lato client e gli strumenti di creazione di componenti aggiuntivi CIF si connettono a `/api/graphql`. Se necessario, è possibile regolare questo valore tramite la configurazione di CIF Cloud Service (vedi di seguito).

Il componente aggiuntivo CIF fornisce un servlet proxy di GraphQL in `/api/graphql` che può essere utilizzato facoltativamente per [lo sviluppo locale](develop.md). Per le distribuzioni in produzione, si consiglia vivamente di impostare un proxy inverso all’endpoint commerce GraphQL tramite AEM Dispatcher o su altri livelli di rete (come CDN).

## Configurazione di store e cataloghi {#catalog}

Il componente aggiuntivo e i [componenti core CIF](https://github.com/adobe/aem-core-cif-components) possono essere utilizzati in più strutture del sito AEM connesse a diversi store commerce (o viste store, ecc.). Per impostazione predefinita, il componente aggiuntivo CIF viene distribuito con una configurazione predefinita che si connette all’archivio e al catalogo predefiniti di Adobe Commerce.

Questa configurazione può essere regolata per il progetto tramite la configurazione di CIF Cloud Service seguendo questi passaggi:

1. In AEM vai a Strumenti > Cloud Services > Configurazione CIF.

2. Seleziona la configurazione commerce da modificare

3. Apri le proprietà di configurazione tramite la barra delle azioni

![Configurazione servizi cloud CIF](/help/commerce/cif/assets/cif-cloud-service-config.png)

È possibile configurare le seguenti proprietà:

- Client GraphQL: seleziona il client GraphQL configurato per la comunicazione back-end commerce. In genere, questa impostazione deve rimanere quella predefinita.
- Visualizzazione store: l&#39;identificatore della visualizzazione store. Se vuota, viene utilizzata la visualizzazione predefinita dello store.
- Percorso proxy GraphQL: il percorso URL che il proxy GraphQL in AEM utilizza per inoltrare le richieste all’endpoint GraphQL back-end di commerce.

  >[!NOTE]
  >
  >Nella maggior parte delle impostazioni il valore predefinito `/api/graphql` non deve essere modificato. Questa impostazione può essere modificata solo da una configurazione avanzata che non utilizza il proxy GraphQL fornito.

- Abilita il supporto per Catalog UID: abilita il supporto per UID invece dell’ID nelle chiamate GraphQL back-end per e-commerce.

  >[!NOTE]
  >
  >Il supporto per gli UID è stato introdotto in Adobe Commerce 2.4.2. Abilita questa opzione solo se il backend di e-commerce supporta uno schema GraphQL della versione 2.4.2 o successiva.

- Identificatore categoria principale catalogo: l’identificatore (UID o ID) della directory principale del catalogo principale dello store

  >[!CAUTION]
  >
  >A partire dalla versione 2.0.0 dei Componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. Se il progetto utilizza i componenti core di CIF versione 2.0.0, devi abilitare il supporto per Catalog UID e utilizzare una categoria valida di UID come &quot;Identificatore categoria radice catalogo&quot;.

La configurazione mostrata sopra è a scopo di riferimento. I progetti devono fornire le proprie configurazioni.

Per impostazioni più complesse che utilizzano più strutture di siti AEM combinate con diversi cataloghi di e-commerce, vedere l&#39;esercitazione [Configurazione di più store di Commerce](configuring/multi-store-setup.md).

## Risorse aggiuntive {#additional-resources}

- [Archetipo di progetto AEM](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Configurazione di Commerce Multi-Store](configuring/multi-store-setup.md)
