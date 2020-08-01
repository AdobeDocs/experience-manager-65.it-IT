---
title: Organizzazione delle risorse digitali
description: Organizzate le risorse digitali, le immagini, i file, le cartelle e così via utilizzando  Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 1%

---


# Organizzazione delle risorse digitali {#organize-digital-assets}

Tutte le risorse digitali, i metadati e il contenuto di documenti Microsoft Office e PDF vengono estratti e resi ricercabili. La ricerca consente un filtraggio sofisticato delle risorse e rispetta pienamente le autorizzazioni corrette. I metadati sono descritti dettagliatamente nei metadati in Digital Asset Management.

[!DNL Experience Manager Assets] supporta diversi modi di organizzare i contenuti. È possibile organizzarle in modo gerarchico utilizzando le cartelle oppure in modo non ordinato e ad hoc, utilizzando ad esempio i tag . Gli utenti possono modificare i tag nell’Editor risorse DAM in cui vengono visualizzate le risorse secondarie, le rappresentazioni e i metadati.

## Organizzare le risorse nelle cartelle {#organize-using-folders}

Il modo più semplice per organizzare le risorse è salvarle in cartelle. È analogo all&#39;organizzazione di file in cartelle nel nostro file system locale. Per ulteriori informazioni su come creare e gestire le cartelle, consultate [Gestire le risorse](managing-assets-touch-ui.md). Il modo in cui denominate file e cartelle, come vengono disposte le sottocartelle e come vengono gestiti i file all’interno di tali cartelle possono avere un impatto significativo sulla modalità di elaborazione delle risorse. Utilizzando strategie di denominazione di file e cartelle coerenti e appropriate, oltre a buone pratiche in materia di metadati, potete sfruttare al meglio il vostro archivio delle risorse digitali.

* Nella maggior parte dei casi, l’archivio delle risorse digitali è in continua crescita. Pertanto, è importante formalizzare l’utilizzo dei metadati, la struttura delle cartelle e la denominazione dei file all’inizio del ciclo di creazione dei contenuti.
* Utilizzate le cartelle solo per imporre una struttura di memorizzazione coerente alle risorse digitali. Questa coerenza consente di elaborare e gestire meglio le risorse. Ad esempio, le risorse inserite nei seguenti tipi di cartelle possono essere utili per utilizzare [i profili appropriati per l’elaborazione](processing-profiles.md)delle risorse:

   * **Cartelle** di sviluppo: contiene le risorse digitali su cui state lavorando.
   * **Cartelle** client: contiene risorse digitali basate su client o nomi di progetti.
   * **Cartelle** principali: contiene risorse digitali originali.
   * **Cartelle** di rendering: contiene rappresentazioni e copie delle risorse digitali originali.
   * **Cartelle** Dimensione file: contiene risorse digitali basate su file di piccole, medie o grandi dimensioni.
   * **Gestione delle cartelle**: contiene risorse digitali pronte per la pubblicazione live sul sito Web.
   * **Cartelle** di tipo MIME: contiene risorse digitali specifiche per tipi MIME quali immagini, documenti e contenuti multimediali.
   * **Archivia cartelle**: contiene risorse digitali ritirate.
   * **Cartelle** basate su data: contiene risorse digitali in base a una data di creazione o all’ultima data di modifica.

* Create una directory di cartelle che probabilmente non verrà modificata in modo che qualsiasi personalizzazione o automazione continui a funzionare. Ad esempio, i profili di elaborazione assegnati continuano a funzionare.
* Se una risorsa è già pubblicata, potete spostarla [!DNL Experience Manager] in un’altra cartella e ripubblicarla dalla nuova posizione, il percorso originale della risorsa pubblicata sarà ancora disponibile, insieme alla nuova risorsa pubblicata. La risorsa pubblicata originale, tuttavia, viene *perduta* [!DNL Experience Manager] e non può essere annullata dalla pubblicazione. Di conseguenza, si consiglia di annullare la pubblicazione di una risorsa e spostarla in un’altra cartella.

## Organizzare le risorse tramite i tag {#use-tags-to-organize-assets}

Utilizzando i tag come metadati potete facilmente cercare le risorse, creare raccolte utilizzando i risultati di ricerca, migliorare la classificazione delle ricerche per alcune risorse e sfruttare gli algoritmi AI di  Adobe Sensei per l&#39;individuazione delle risorse.

[!DNL Adobe Experience Manager Assets] utilizza un algoritmo di autoapprendimento per creare tag altamente descrittivi che consentono di trovare la risorsa giusta con pochi clic. I tag intelligenti utilizzano  Adobe Sensei, il nostro framework di machine learning e intelligenza artificiale, che può essere addestrato a riconoscere e applicare sia tag standard che specifici per il business alle immagini. I tag avanzati possono inoltre identificare contenuti, singole parole o frasi e applicare automaticamente tag descrittivi alle risorse

Per ulteriori informazioni, consultate i seguenti articoli:

* [Informazioni sui tag in  Experience Manager](/help/sites-authoring/tags.md)
* [Modificare i metadati delle risorse](meta-edit.md)
* [Tag avanzati migliorati nelle risorse](enhanced-smart-tags.md)

## Organizzare come raccolte {#organize-as-collections}

Con le raccolte di risorse in [!DNL Experience Manager Assets], potete semplificare la possibilità di creare, modificare e condividere risorse tra gli utenti. Create diversi tipi di raccolte in base al modo in cui le utilizzate, comprese le raccolte che contengono un elenco di riferimento statico di risorse, cartelle e raccolte, nonché le raccolte che richiamano risorse in base ai criteri di ricerca.  Potete anche creare raccolte con risorse da posizioni diverse e condividerle con più utenti con diversi livelli di accesso, visualizzazione e modifica dei privilegi.

Per ulteriori informazioni, vedete [Gestione delle raccolte](managing-collections-touch-ui.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organizzare le risorse per utilizzare i profili {#organize-to-use-profiles}

Un profilo di elaborazione contiene [!DNL Assets] comandi di elaborazione applicabili alle risorse che vengono caricate in cartelle predefinite. I profili vengono utilizzati per automatizzare l’elaborazione del contenuto di una cartella o di risorse appena caricate. Potete sfruttare i profili per organizzare meglio le risorse.

La standardizzazione dell’utilizzo dei metadati, della denominazione dei file e della struttura delle cartelle garantisce che, con la crescita del pool di risorse digitali, i profili di elaborazione possano essere applicati alle cartelle con maggiore precisione e coerenza.

>[!MORELIKETHIS]
>
>* [Profili per elaborare metadati, immagini e video](processing-profiles.md).
>* [Profili metadati](metadata-profiles.md).
>* [Profili](video-profiles.md)video.
>* [Profili](image-profiles.md)immagine Dynamic Media.

