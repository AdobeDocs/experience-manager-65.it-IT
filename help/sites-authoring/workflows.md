---
title: Utilizzo dei flussi di lavoro
seo-title: Working with Workflows
description: I flussi di lavoro in AEM consentono di automatizzare le serie di passaggi che vengono eseguite su una pagina o su una risorsa.
seo-description: Workflows in AEM allow you to automate a series of steps that are performed on a page or asset.
uuid: c4442d2a-c6b0-49d4-a1ce-384017c45bf0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 7cb99618-d903-4cfb-b0d9-b23d189f6e78
exl-id: 7383d590-c6b7-440a-a33d-196dce9736ef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 100%

---

# Utilizzo dei flussi di lavoro{#working-with-workflows}

I flussi di lavoro in AEM consentono di automatizzare le serie di passaggi che vengono eseguite su una (o più) pagine e/o risorse.

Ad esempio, per la pubblicazione, un editor deve rivedere il contenuto prima che l’amministratore del sito attivi la pagina. Un flusso di lavoro che automatizza questo esempio avvisa ogni partecipante quando è il momento di eseguire il lavoro richiesto:

1. L’autore applica il flusso di lavoro alla pagina.
1. L’editor riceve una richiesta di lavoro per esaminare il contenuto della pagina. Al termine, indica che il lavoro richiesto è stato completato.
1. L’amministratore del sito riceve quindi una richiesta di lavoro per l’attivazione della pagina. Al termine, indica che il lavoro richiesto è stato completato.

In genere:

* Gli autori dei contenuti applicano i flussi di lavoro alle pagine e partecipano ai flussi di lavoro.
* I flussi di lavoro utilizzati sono specifici per i processi aziendali dell’organizzazione.

Le pagine seguenti trattano:

* [Applicazione dei flussi di lavoro alle pagine](/help/sites-authoring/workflows-applying.md)
* [Partecipazione ai flussi di lavoro](/help/sites-authoring/workflows-participating.md)
