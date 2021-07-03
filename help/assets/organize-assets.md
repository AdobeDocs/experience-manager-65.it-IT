---
title: Organizzazione delle risorse digitali
description: Organizza le risorse digitali, le immagini, i file, le cartelle e così via utilizzando Experience Manager.
contentOwner: AG
role: User
feature: Gestione risorse,Ricerca
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# Organizzazione delle risorse digitali {#organize-digital-assets}

Tutte le risorse digitali, i metadati e il contenuto di Microsoft Office e i documenti PDF vengono estratti e resi ricercabili. La ricerca consente un filtraggio sofisticato delle risorse e rispetta completamente le autorizzazioni appropriate. I metadati sono descritti in dettaglio nei metadati di Digital Asset Management.

[!DNL Experience Manager Assets] supporta diversi modi per organizzare i contenuti. È possibile organizzarle in modo gerarchico utilizzando le cartelle oppure in modo non ordinato e ad hoc, utilizzando ad esempio i tag. Gli utenti possono modificare i tag nell’editor risorse DAM in cui vengono visualizzate risorse secondarie, rappresentazioni e metadati.

## Organizzare le risorse nelle cartelle {#organize-using-folders}

Il modo più semplice per organizzare le risorse è salvarle nelle cartelle. È simile all&#39;organizzazione di file in cartelle nel nostro filesystem locale. Per ulteriori informazioni su come creare e gestire le cartelle, consulta [Gestire le risorse](manage-assets.md). Le modalità di denominazione di file e cartelle, di organizzazione delle sottocartelle e di gestione dei file in queste cartelle possono avere un impatto significativo sulle modalità di elaborazione di tali risorse. Utilizzando strategie di denominazione dei file e delle cartelle coerenti e appropriate, oltre a buone pratiche in materia di metadati, puoi sfruttare al massimo l’archivio delle risorse digitali.

* Nella maggior parte dei casi, l’archivio delle risorse digitali è sempre in crescita. Pertanto, è importante formalizzare l’uso dei metadati, la struttura delle cartelle e la denominazione dei file all’inizio del ciclo di creazione dei contenuti.
* Utilizza solo le cartelle per imporre una struttura di archiviazione coerente per le risorse digitali. Questa coerenza consente di elaborare e gestire meglio le risorse. Ad esempio, le risorse inserite nei seguenti tipi di cartelle possono essere utili per utilizzare profili [appropriati da utilizzare per l’elaborazione delle risorse](processing-profiles.md):

   * **Cartelle** di sviluppo: contiene risorse digitali su cui stai lavorando.
   * **Cartelle** client: contiene risorse digitali basate su client o nomi di progetto.
   * **Cartelle** principali: contiene risorse digitali originali di origine.
   * **Cartelle** di rendering: contiene rappresentazioni e copie delle risorse digitali originali di origine.
   * **Cartelle** dimensioni file: contiene risorse digitali basate su file di piccole, medie o grandi dimensioni.
   * **Cartelle** di staging: contiene risorse digitali pronte per la pubblicazione live sul sito web.
   * **Cartelle** di tipo MIME: contiene risorse digitali specifiche per i tipi MIME come immagini, documenti e elementi multimediali.
   * **Archivia cartelle**: contiene risorse digitali in pensione.
   * **Cartelle** basate su data: contiene risorse digitali in base a una data di creazione o a un’ultima data di modifica.

* Crea una directory di cartelle che non è probabile modificare in modo che qualsiasi personalizzazione o automazione continui a funzionare. Ad esempio, i profili di elaborazione assegnati continuano a funzionare.
* Se una risorsa è già stata pubblicata, utilizza [!DNL Experience Manager] per spostare la risorsa in un’altra cartella e ripubblicarla dalla nuova posizione, la posizione originale della risorsa pubblicata è ancora disponibile, insieme alla nuova risorsa pubblicata. La risorsa pubblicata originale, tuttavia, è *persa* in [!DNL Experience Manager] e non può essere annullata dalla pubblicazione. Di conseguenza, come best practice, prima annulla la pubblicazione di una risorsa e poi spostala in un’altra cartella.

## Organizzare le risorse utilizzando i tag {#use-tags-to-organize-assets}

Utilizzando i tag come metadati, puoi facilmente cercare le risorse, creare raccolte utilizzando i risultati della ricerca, aumentare la classificazione della ricerca per alcune risorse e sfruttare gli algoritmi AI di Adobe Sensei per l’individuazione delle risorse.

[!DNL Adobe Experience Manager Assets] utilizza un algoritmo di apprendimento automatico per creare tag altamente descrittivi che consentono di trovare la risorsa giusta in pochi clic. L’assegnazione tag avanzati utilizza Adobe Sensei, il nostro framework di intelligenza artificiale e apprendimento automatico, che può essere addestrato a riconoscere e applicare tag standard e specifici per il business alle immagini. I tag avanzati possono inoltre identificare contenuti, singole parole o frasi e applicare automaticamente tag descrittivi alle risorse

Per ulteriori informazioni, consulta i seguenti articoli:

* [Informazioni sui tag in Experience Manager](/help/sites-authoring/tags.md)
* [Modificare i metadati delle risorse](metadata.md)
* [Tag avanzati migliorati nelle risorse](enhanced-smart-tags.md)

## Organizza come raccolte {#organize-as-collections}

Con le raccolte di risorse in [!DNL Experience Manager Assets] puoi semplificare la possibilità di creare, modificare e condividere risorse tra gli utenti. Crea diversi tipi di raccolte in base al modo in cui le utilizzi, incluse le raccolte che contengono un elenco di riferimento statico di risorse, cartelle e raccolte, nonché le raccolte che richiamano le risorse in base ai criteri di ricerca.  Puoi anche creare raccolte con risorse da posizioni diverse e condividerle con più utenti con diversi livelli di accesso, visualizzazione e modifica.

Per ulteriori informazioni, consulta [gestire le raccolte](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organizzare le risorse per utilizzare i profili {#organize-to-use-profiles}

Un profilo di elaborazione contiene [!DNL Assets] comandi di elaborazione applicabili alle risorse caricate in cartelle predefinite. I profili vengono utilizzati per automatizzare l’elaborazione del contenuto di una cartella o di risorse appena caricate. Puoi sfruttare i profili per organizzare meglio le risorse.

La standardizzazione dell’utilizzo dei metadati, della denominazione dei file e della struttura delle cartelle consente di applicare profili di elaborazione alle cartelle con maggiore precisione e coerenza man mano che cresce il pool di risorse digitali.

>[!MORELIKETHIS]
>
>* [Profili per elaborare metadati, immagini e video](processing-profiles.md).
>* [Profili metadati](/help/assets/metadata-config.md#metadata-profiles).
>* [Profili video](video-profiles.md).
>* [Profili immagine di Dynamic Media](image-profiles.md).

