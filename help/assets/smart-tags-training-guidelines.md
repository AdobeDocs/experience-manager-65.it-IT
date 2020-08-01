---
title: Linee guida sulla formazione per Smart Content Service
description: Formazione del servizio  Adobe Sensei AI per l'applicazione di smart tag alle risorse
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 11%

---


# Linee guida sulla formazione per Smart Content Service {#smart-content-service-training-guidelines}

Per poter etichettare efficacemente le immagini del tuo marchio, Smart Content Service richiede che le immagini di formazione siano conformi a determinate linee guida.

## Orientamenti per la formazione {#guidelines-for-training}

Per risultati ottimali, le immagini del set di formazione devono essere conformi alle seguenti linee guida:

**Quantity and size (Quantità e dimensioni)**: almeno 30 immagini per tag. Almeno 500 pixel sul lato più lungo.

**Coerenza**: Le immagini di un tag devono essere visivamente simili.

Ad esempio, non è consigliabile assegnare a tutte queste immagini il tag `my-party` (per la formazione) perché non sono visivamente simili.

![Immagini illustrative per esemplificare le linee guida per la formazione](/help/assets/assets/do-not-localize/coherence.png)

**Copertura**: Dovrebbe esserci una varietà sufficiente nelle immagini della formazione. L&#39;idea è quella di fornire alcuni esempi, ma abbastanza diversi, in modo che  Experience Manager impari a concentrarsi sulle cose giuste. Se applicate lo stesso tag a immagini visivamente diverse, includete almeno cinque esempi di ciascun tipo.

Ad esempio, per il tag *model-down-pose*, includete più immagini di formazione simili all’immagine evidenziata di seguito per il servizio, in modo da identificare immagini simili con maggiore precisione durante l’assegnazione dei tag.

![Immagini illustrative per esemplificare le linee guida per la formazione](/help/assets/assets/do-not-localize/coverage_1.png)

**Distrazione/ostruzione**: Il servizio si allena meglio sulle immagini con meno distrazioni (sfondi visibili, accompagnamento indipendenti, come oggetti/persone con il soggetto principale).

Ad esempio, per il tag *casual-shoe*, la seconda immagine non è un buon candidato per l&#39;addestramento.

![Immagini illustrative per esemplificare le linee guida per la formazione](/help/assets/assets/do-not-localize/distraction.png)

**Completeness (Completezza):** se un’immagine è idonea per più tag, aggiungi tutti i tag applicabili prima di includere l’immagine nella formazione. Ad esempio, per tag quali `raincoat` e `model-side-view`, aggiungi entrambi i tag alla risorsa idonea prima di includerla nella formazione.

![Immagini illustrative per esemplificare le linee guida per la formazione](/help/assets/assets/do-not-localize/completeness.png)

## Limitazioni  {#limitations}

Gli smart tag avanzati si basano su modelli di apprendimento delle immagini e dei relativi tag. Questi modelli non sempre sono perfetti per identificare i tag. La versione corrente di Smart Content Service presenta i seguenti limiti:

* Incapacità di riconoscere sottili differenze nelle immagini. Ad esempio, camicie sottili o regolari.
* Impossibile identificare i tag in base a piccoli pattern/parti di un’immagine. Ad esempio, i logo delle T-shirt.
* I tag sono supportati nelle impostazioni internazionali [!DNL Experience Manager] supportate in. Per un elenco delle lingue, consultate [Note](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html)sulla versione di Smart Content Services.

Per cercare risorse con tag avanzati (regolari o avanzati), usate la ricerca [!DNL Assets] Omnisearch (ricerca full-text). Non esiste un predicato di ricerca separato per gli smart tag.

>[!NOTE]
>
>La capacità di Smart Content Service di formare i tag e applicarli ad altre immagini dipende dalla qualità delle immagini utilizzate per la formazione. Per risultati ottimali,  Adobe consiglia di usare immagini visivamente simili per formare il servizio per ciascun tag.
