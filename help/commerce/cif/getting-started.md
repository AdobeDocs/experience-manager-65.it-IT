---
title: Guida introduttiva a Contenuto AEM e Commerce
description: Scopri come distribuire un progetto AEM Content and Commerce .
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
source-git-commit: 61b8d0bf960bd03a19d22061f3c897a56259dd24
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 5%

---

# Guida introduttiva a Contenuto AEM e Commerce {#start}

Per iniziare a utilizzare AEM contenuti e Commerce, è necessario installare il componente aggiuntivo Contenuto AEM e Commerce per AEM 6.5.

## Requisiti software minimi

[È necessario AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 o successivo.

## Onboarding {#onboarding}

L’onboarding per AEM contenuto e commerce è un processo in due fasi:

1. Installare il componente aggiuntivo Contenuto AEM e Commerce per AEM 6.5

2. Connetti AEM con la tua soluzione commerce

### Installare il componente aggiuntivo Contenuto AEM e Commerce per AEM 6.5 {#install-add-on}

Scarica e installa il componente aggiuntivo AEM Commerce per AEM 6.5 dal portale [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) .

Avvia e installa il Service Pack AEM 6.5 richiesto. È consigliabile installare l’ultimo service pack disponibile.

>[!NOTE]
>
>Questo verrà fatto dal CSE per i clienti di AEM Managed Service.

### Connetti AEM al tuo Commerce System {#connect}

AEM può essere collegato a qualsiasi sistema commerce con un endpoint GraphQL accessibile per AEM. Questi endpoint sono solitamente disponibili pubblicamente oppure possono essere collegati tramite VPN privata o connessioni locali a seconda della configurazione del singolo progetto.

Facoltativamente, è possibile fornire l’intestazione di autenticazione per utilizzare funzionalità CIF aggiuntive che richiedono l’autenticazione.

I progetti generati da [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) e da [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) che è già incluso nella [configurazione predefinita](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) devono essere regolati.

Sostituisci il valore di `url` in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con l’endpoint GraphQL del sistema commerce. Questa configurazione può essere effettuata tramite la console OSGI o distribuendo la configurazione OSGI tramite il progetto. Sono supportate configurazioni diverse per i sistemi di staging e produzione utilizzando diverse modalità di esecuzione AEM.

I componenti core AEM Content and Commerce e CIF utilizzano sia connessioni lato server che lato client AEM. I componenti core CIF lato client e gli strumenti di creazione di componenti aggiuntivi CIF si connettono per impostazione predefinita a `/api/graphql`. Se necessario, è possibile regolarlo tramite la configurazione del Cloud Service CIF (vedi di seguito).

Il componente aggiuntivo CIF fornisce un servlet proxy GraphQL in `/api/graphql` che può essere utilizzato facoltativamente per [sviluppo locale](develop.md). Per le distribuzioni di produzione si consiglia vivamente di impostare un proxy inverso per l’endpoint GraphQL di e-commerce tramite il Dispatcher AEM o su altri livelli di rete (come CDN).

## Configurazione di store e cataloghi {#catalog}

Il componente aggiuntivo e i [componenti core CIF](https://github.com/adobe/aem-core-cif-components) possono essere utilizzati su più strutture di siti AEM connesse a diversi store di e-commerce (o viste store e così via). Per impostazione predefinita, il componente aggiuntivo CIF viene distribuito con una configurazione predefinita che si collega allo store e al catalogo predefiniti di Adobe Commerce (Magento).

Questa configurazione può essere regolata per il progetto tramite la configurazione del Cloud Service CIF, come descritto di seguito:

1. In AEM vai a Strumenti -> Cloud Services -> Configurazione CIF

2. Seleziona la configurazione di e-commerce da modificare

3. Apri le proprietà di configurazione tramite la barra delle azioni

![Configurazione dei Cloud Services CIF](/help/commerce/cif/assets/cif-cloud-service-config.png)

È possibile configurare le seguenti proprietà:

- Client GraphQL: seleziona il client GraphQL configurato per la comunicazione back-end Commerce. In genere questo dovrebbe rimanere il valore predefinito.
- Visualizzazione archivio: l&#39;identificatore della vista archivio (Magento). Se questo campo viene lasciato vuoto, verrà utilizzata la visualizzazione archivio predefinita.
- Percorso proxy GraphQL: percorso URL del proxy GraphQL in AEM per le richieste proxy all’endpoint GraphQL di back-end per e-commerce.
   >[!NOTE]
   >
   > Nella maggior parte delle impostazioni il valore predefinito `/api/graphql` non deve essere modificato. Solo la configurazione avanzata che non utilizza il proxy GraphQL fornito dovrebbe modificare questa impostazione.
- Abilita supporto UID catalogo : abilita il supporto per UID invece di ID nelle chiamate GraphQL di back-end per e-commerce.
   >[!NOTE]
   >
   > Il supporto per gli UID è stato introdotto in Adobe Commerce (Magento) 2.4.2. Abilitare questa opzione solo se il backend commerce supporta uno schema GraphQL della versione 2.4.2 o successiva.
- Identificatore della categoria principale del catalogo: l&#39;identificatore (UID o ID) della directory principale del catalogo store
   >[!CAUTION]
   >
   > A partire dalla versione 2.0.0 dei componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. Se il progetto utilizza i componenti core CIF versione 2.0.0, è necessario abilitare il supporto per gli UID del catalogo e utilizzare un UID di categoria valido come &quot;Identificatore di categoria principale del catalogo&quot;.

La configurazione mostrata sopra è di riferimento. I progetti devono fornire le proprie configurazioni.

Per configurazioni più complesse che utilizzano più strutture di siti AEM combinate con diversi cataloghi di e-commerce, consulta l’ esercitazione [Configurazione di più store di Commerce](configuring/multi-store-setup.md) .

## Risorse aggiuntive {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Configurazione di Commerce Multi-Store](configuring/multi-store-setup.md)
