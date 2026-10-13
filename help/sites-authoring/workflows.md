---
title: Utilizzare i flussi di lavoro
description: I flussi di lavoro in Adobe Experience Manager consentono di automatizzare una serie di passaggi eseguiti su una pagina o una risorsa.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 7383d590-c6b7-440a-a33d-196dce9736ef
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: f6a6f91a-8819-530a-8e7b-c50884a25aef
    internal-label: Workflow
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 74%
---
# Utilizzare i flussi di lavoro{#working-with-workflows}

I flussi di lavoro di AEM consentono di automatizzare una serie di passaggi eseguiti su (una o più) pagine e/o risorse.

Ad esempio, per la pubblicazione, un editor deve rivedere il contenuto prima che l’amministratore del sito attivi la pagina. Un flusso di lavoro che automatizza questo esempio avvisa ogni partecipante quando è il momento di eseguire il lavoro richiesto:

1. L’autore applica il flusso di lavoro alla pagina.
1. L’editor riceve un elemento di lavoro che indica che è necessario rivedere il contenuto della pagina. Al termine, sarà indicato che l’elemento di lavoro è stato completato.
1. L’amministratore del sito riceve quindi una richiesta di lavoro per l’attivazione della pagina. Al termine, sarà indicato che l’elemento di lavoro è stato completato.

In genere:

* Gli autori dei contenuti applicano i flussi di lavoro alle pagine e partecipano ai flussi di lavoro.
* I flussi di lavoro utilizzati sono specifici per i processi aziendali dell’organizzazione.

Le pagine seguenti trattano:

* [Applicazione dei flussi di lavoro alle pagine](/help/sites-authoring/workflows-applying.md)
* [Partecipazione ai flussi di lavoro](/help/sites-authoring/workflows-participating.md)
