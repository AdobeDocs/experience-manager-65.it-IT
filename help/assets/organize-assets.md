---
title: Organizzazione delle risorse digitali
description: Organizza risorse digitali, immagini, file, cartelle e così via, utilizzando Experience Manager.
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
hide: true
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 2%

---

# Organizzazione delle risorse digitali {#organize-digital-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| Adobe Experience Manager (AEM) as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=en) |
| AEM 6.5 | Questo articolo |

Tutte le risorse digitali, i metadati e il contenuto dei documenti di Microsoft® Office e PDF vengono estratti e resi ricercabili. La ricerca consente di applicare filtri sofisticati alle risorse e rispetta appieno le autorizzazioni appropriate. I metadati sono descritti in dettaglio in Metadati in Gestione delle risorse digitali.

[!DNL Experience Manager Assets] supporta diversi modi di organizzare i contenuti. Puoi organizzarli in modo gerarchico utilizzando le cartelle oppure in modo non ordinato e ad hoc, utilizzando, ad esempio, i tag. Gli utenti possono modificare i tag nell’Editor risorse DAM in cui vengono visualizzate le risorse secondarie, le rappresentazioni e i metadati.

## Organizzare le risorse in cartelle {#organize-using-folders}

Il modo più semplice per organizzare le risorse è salvarle nelle cartelle. È simile all’organizzazione dei file nelle cartelle nel file system locale. Per ulteriori informazioni su come creare e gestire le cartelle, consulta [Gestione risorse](manage-assets.md). Il modo in cui denominate i file e le cartelle, organizzate le sottocartelle e gestite i file all’interno di queste cartelle può avere un impatto significativo sul modo in cui tali risorse vengono elaborate. Utilizzando strategie di denominazione di file e cartelle coerenti e appropriate, insieme a una buona pratica sui metadati, puoi sfruttare al massimo l’archivio delle risorse digitali.

* Di solito, l’archivio delle risorse digitali è sempre in crescita. Pertanto, è importante formalizzare l’uso dei metadati, la struttura delle cartelle e la denominazione dei file nelle prime fasi del ciclo di creazione dei contenuti.
* Utilizza le cartelle solo per imporre una struttura di archiviazione coerente per le risorse digitali. Questa coerenza aiuta il processo e gestisce meglio le risorse. Ad esempio, le risorse posizionate nei seguenti tipi di cartelle possono aiutarti a utilizzare le [profili da utilizzare per l’elaborazione delle risorse](processing-profiles.md):

   * **Cartelle di sviluppo**: contiene risorse digitali sulle quali stai lavorando.
   * **Cartelle client**: contiene risorse digitali basate sui client o i nomi dei progetti.
   * **Cartelle primarie**: contiene risorse digitali originali di origine.
   * **Cartelle di rappresentazione**: contiene copie trasformate e copie delle risorse digitali originali di origine.
   * **Cartelle dimensione file**: contiene risorse digitali basate su file di dimensioni piccole, medie o grandi.
   * **Cartelle di gestione temporanea**: contiene risorse digitali pronte per la pubblicazione live sul sito web.
   * **Cartelle di tipo MIME**: contiene risorse digitali specifiche per i tipi MIME, ad esempio immagini, documenti e file multimediali.
   * **Archiviare le cartelle**: contiene risorse digitali ritirate.
   * **Cartelle basate sulla data**: contiene risorse digitali basate su una data di creazione o su una data dell’ultima modifica.

* Crea una directory di cartelle che non dovrebbero essere modificate in modo che qualsiasi personalizzazione o automazione continui a funzionare. Ad esempio, i profili di elaborazione assegnati continuano a funzionare.
* Se una risorsa è già pubblicata, utilizza [!DNL Experience Manager] per spostare la risorsa in un’altra cartella e ripubblicarla dalla nuova posizione, rimane disponibile la posizione originale della risorsa pubblicata insieme alla risorsa appena ripubblicata. La risorsa pubblicata originale, tuttavia, è *perso* a [!DNL Experience Manager] e non può essere annullata. Pertanto, come best practice, devi prima annullare la pubblicazione di una risorsa e quindi spostarla in un’altra cartella.

## Organizzare le risorse utilizzando i tag {#use-tags-to-organize-assets}

Utilizzando i tag, come metadati, puoi facilmente cercare le risorse, creare raccolte utilizzando i risultati della ricerca, migliorare la classificazione delle ricerche per alcune risorse e utilizzare gli algoritmi di intelligenza artificiale di Adobe Sensei per l’individuazione delle risorse.

[!DNL Adobe Experience Manager Assets] utilizza un algoritmo di apprendimento automatico per creare tag altamente descrittivi che ti consentono di trovare la risorsa giusta con pochi clic. L’assegnazione tag avanzati utilizza Adobe Sensei, il framework di intelligenza artificiale e apprendimento automatico di Adobe, che può essere addestrato per riconoscere e applicare tag standard e specifici per l’azienda alle immagini. I tag avanzati possono inoltre identificare contenuti, singole parole o frasi e applicare automaticamente tag descrittivi alle risorse

Per ulteriori informazioni, consulta i seguenti articoli:

* [Informazioni sui tag in Experience Manager](/help/sites-authoring/tags.md)
* [Modificare i metadati delle risorse](metadata.md)
* [Tag avanzati migliorati in Assets](enhanced-smart-tags.md)

## Organizza come raccolte {#organize-as-collections}

Con raccolte di risorse in [!DNL Experience Manager Assets], è possibile semplificare la creazione, la modifica e la condivisione delle risorse tra gli utenti. Crea diversi tipi di raccolte in base al modo in cui le utilizzi, incluse le raccolte che contengono un elenco di riferimento statico di risorse, cartelle e raccolte e le raccolte che estraggono le risorse in base ai criteri di ricerca. Puoi anche creare raccolte con risorse da posizioni diverse e condividerle con più utenti con diversi livelli di accesso, visualizzazione e modifica dei privilegi.

Per ulteriori informazioni, consulta [gestire le raccolte](manage-collections.md).

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organizzare le risorse per utilizzare i profili {#organize-to-use-profiles}

Un profilo di elaborazione contiene [!DNL Assets] elaborazione dei comandi applicabili alle risorse caricate in cartelle predefinite. I profili vengono utilizzati per automatizzare l’elaborazione del contenuto di una cartella o delle risorse appena caricate. Puoi utilizzare i profili per organizzare meglio le risorse.

La standardizzazione dell’utilizzo dei metadati, della denominazione dei file e della struttura delle cartelle garantisce che, man mano che il pool di risorse digitali cresce, sia possibile applicare profili di elaborazione alle cartelle con maggiore precisione e coerenza.

>[!MORELIKETHIS]
>
>* [Profili per elaborare metadati, immagini e video](processing-profiles.md).
>* [Profili metadati](/help/assets/metadata-config.md#metadata-profiles).
>* [Profili video](video-profiles.md).
>* [Profili immagine Dynamic Medie](image-profiles.md).
