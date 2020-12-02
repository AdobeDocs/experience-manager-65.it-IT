---
title: Integrazione con BrightEdge Content Optimizer
seo-title: Integrazione con BrightEdge Content Optimizer
description: Scoprite come integrare AEM con BrightEdge Content Optimizer.
seo-description: Scoprite come integrare AEM con BrightEdge Content Optimizer.
uuid: 7075dd3c-2fd6-4050-af1c-9b16ad4366ec
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: cf25c9a8-0555-4c67-8aa5-55984fd8d301
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---


# Integrazione con BrightEdge Content Optimizer{#integrating-with-brightedge-content-optimizer}

Crea una configurazione cloud BrightEdge in modo che AEM possa connettersi utilizzando le credenziali del tuo account BrightEdge. Potete creare più configurazioni se utilizzate più account.

Quando create la configurazione, specificate un titolo. Il titolo deve essere descrittivo in modo che gli utenti possano correlare la configurazione con l&#39;account BrightEdge. Quando un autore o un amministratore di pagina associa una pagina Web all’account BrightEdge, questo titolo viene presentato in un elenco a discesa.

1. Nella barra laterale, fate clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Fate clic sul collegamento visualizzato nella sezione BrightEdge Content Optimizer. La creazione o meno di una configurazione BrightEdge determina il testo del collegamento:

   * Configura ora: Questo collegamento viene visualizzato quando non è stata creata alcuna configurazione.
   * Mostra configurazioni: Questo collegamento viene visualizzato quando sono state create una o più configurazioni.

   ![chlimage_1-4](assets/chlimage_1-4a.png)

1. Se avete fatto clic su Mostra configurazioni, fate clic sul collegamento + accanto a Configurazioni disponibili.
1. Digitare un titolo per la configurazione. Facoltativamente, digitare un nome per il nodo utilizzato per memorizzare la configurazione nella directory archivio. Fai clic su Crea.
1. Nella finestra di dialogo Configurazione BrightEdge Content Optimizer, digitate il nome utente e la password dell&#39;account BrightEdge, quindi fate clic su OK.

## Modifica di una configurazione BrightEdge {#editing-a-brightedge-configuration}

Se necessario, modificate il nome utente e la password di una configurazione BrightEdge. Le modifiche interessano tutte le pagine che utilizzano la configurazione.

1. Nella barra laterale, fate clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nella sezione BrightEdge Content Optimizer, fate clic su Mostra configurazioni.

   ![chlimage_1-5](assets/chlimage_1-5a.png)

1. Fate clic sul nome della configurazione da modificare.
1. Fate clic su Modifica, modificate i valori delle proprietà, quindi fate clic su OK.

## Associazione di pagine a una configurazione BrightEdge {#associating-pages-with-a-brightedge-configuration}

Associate le pagine a una configurazione BrightEdge per inviare i dati di pagina al servizio BrightEdge per l&#39;analisi. Quando si associa una pagina a una configurazione, le pagine figlie ereditano l’associazione. In genere, si associa la pagina principale del sito in modo che i dati di tutte le pagine vengano inviati a BrightEdge.

1. Aprite la console Siti Web classici. ([http://localhost:4502/siteadmin#/content](http://localhost:4502/siteadmin#/content))
1. Nella struttura Siti Web selezionate la cartella o la pagina che contiene la pagina da associare alla configurazione BrightEdge.
1. Nell’elenco delle pagine, fare clic con il pulsante destro del mouse sulla pagina da configurare e fare clic su Proprietà.
1. Nella scheda Cloud Services, fate clic sul pulsante Aggiungi servizio, quindi nella finestra di dialogo Cloud Services selezionate BrightEdge Content Optimizer e fate clic su OK.
1. Nell&#39;elenco BrightEdge Content Optimizer, selezionare la configurazione BrightEdge da associare alla pagina, quindi fare clic su OK.

   ![chlimage_1-6](assets/chlimage_1-6a.png)

## Attivazione di una configurazione BrightEdge {#activating-a-brightedge-configuration}

Attivate una configurazione BrightEdge per replicarla nell’istanza di pubblicazione e per consentire alle pagine pubblicate di interagire con il servizio BrightEdge.

1. Nella barra laterale fate clic su Siti, quindi individuate e selezionate la pagina associata alla configurazione BrightEdge.
1. Tocca o fai clic sull’icona Pubblica, quindi fai clic o tocca Pubblica.

   ![chlimage_1-7](assets/chlimage_1-7a.png)

1. Nell&#39;elenco delle configurazioni visualizzate, accertatevi che la configurazione BrightEdge sia selezionata, quindi fate clic su Pubblica.

   ![chlimage_1-8](assets/chlimage_1-8a.png)

