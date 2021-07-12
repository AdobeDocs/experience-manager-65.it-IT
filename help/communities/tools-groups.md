---
title: Modelli per gruppi
seo-title: Modelli per gruppi
description: Come accedere alla console Modelli di gruppo
seo-description: Come accedere alla console Modelli di gruppo
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Admin
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 3%

---


# Modelli per gruppi {#group-templates}

La console Modelli di gruppo è simile alla console [Modelli di sito](/help/communities/sites.md). Entrambe sono blueprint per un set di pagine e funzionalità precablate che formano un sito community. La differenza consiste nel fatto che un modello di sito è per la comunità principale e un modello di gruppo è per un gruppo community, una sottocomunità nidificata all’interno della comunità principale.

Un gruppo di community viene incorporato in un modello di sito includendo la [funzione Groups](/help/communities/functions.md#groups-function) (che non può essere la prima funzione o solo nel modello).

Per quanto riguarda Communities [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack), è possibile nidificare i gruppi includendo la funzione Groups all&#39;interno di un modello di gruppo.

Nel momento in cui viene intrapresa un&#39;azione per creare un nuovo gruppo community, viene selezionato il modello (struttura) del gruppo. La selezione dipende dalla configurazione della funzione Groups (Gruppi) quando viene aggiunta al modello di sito o di gruppo.

>[!NOTE]
>
>Le console per la creazione di [siti della community](/help/communities/sites-console.md), [modelli di sito della community](/help/communities/sites.md), [modelli di gruppo della community](/help/communities/tools-groups.md) e [funzioni della community](/help/communities/functions.md) sono utilizzabili solo nell’ambiente di authoring.

## Console Modelli di gruppo {#group-templates-console}

Per raggiungere la console dei modelli di gruppi nell’ambiente di authoring di AEM:

* Seleziona **Strumenti | Comunità | Modelli di gruppo,** dalla navigazione globale.

Questa console visualizza i modelli da cui è possibile creare un [sito community](/help/communities/sites-console.md) e consente di creare nuovi modelli di gruppo.

![Modello per gruppi community](assets/groups-template.png)

## Crea modello gruppo {#create-group-template}

Per iniziare a creare un nuovo modello di gruppo, seleziona `Create`.

Viene visualizzato il pannello Editor sito che contiene 3 pannelli secondari:

### Informazioni di base {#basic-info}

![site-basic-info](assets/site-basic-info.png)

Nel pannello Informazioni di base sono configurati un nome, una descrizione e se il modello è abilitato o disabilitato:

* **Nome nuovo modello per gruppo**

   ID del nome del modello.

* **Descrizione**

   Descrizione del modello.

* **Disabilitato/Abilitato**

   Un interruttore di attivazione che controlla se il modello è referenziabile.

#### Miniatura  {#thumbnail}

![miniatura del sito](assets/site-thumbnail.png)

(Facoltativo) Seleziona l’icona Carica immagine per visualizzare una miniatura insieme a Nome e Descrizione per i creatori dei siti della community.

#### Struttura {#structure}

>[!CAUTION]
>
>Se lavori con AEM 6.1 Communities FP4 o versioni precedenti, non aggiungere una funzione gruppi a un modello di gruppo.
>
>La funzione dei gruppi nidificati è disponibile a partire da Communities [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Non è ancora consentito aggiungere una funzione Groups come prima o unica funzione in un modello.

![Editor modelli di gruppo](assets/template-editor.png)

Per aggiungere funzioni di community, trascina da destra a sinistra nell’ordine in cui dovrebbero essere visualizzati i collegamenti al menu del sito. Gli stili verranno applicati al modello durante la creazione del sito.

Ad esempio, se desideri un forum, trascina la funzione forum dalla libreria e rilascia sotto il generatore di modelli. In questo modo si aprirà la finestra di dialogo di configurazione del forum. Per informazioni sulle finestre di dialogo di configurazione, consulta la [console funzioni](/help/communities/functions.md) .

Continua a trascinare e rilasciare tutte le altre funzioni della community desiderate per un sito della sottocommunity (gruppo) basato su questo modello.

![trascinare le funzioni](assets/dragfunctions.png)

Una volta che tutte le funzioni desiderate sono state rilasciate nell&#39;area del generatore di modelli e configurate, seleziona **Salva** nell&#39;angolo in alto a destra.

##  Modifica modello gruppo {#edit-group-template}

Quando visualizzi i gruppi della community nella console principale [Modelli di gruppo](#group-templates-console), è possibile selezionare un modello di gruppo esistente da modificare.

La modifica di un modello di gruppo non influisce sui siti della community già creati dal modello. È invece possibile modificare direttamente la struttura di un sito della community ](/help/communities/sites-console.md#modify-structure).[

Questo processo fornisce gli stessi pannelli di [creazione di un modello di gruppo](#create-group-template).
