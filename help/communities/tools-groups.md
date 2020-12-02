---
title: Modelli per gruppi
seo-title: Modelli per gruppi
description: Come accedere alla console Modelli gruppo
seo-description: Come accedere alla console Modelli gruppo
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 3%

---


# Modelli per gruppi {#group-templates}

La console Modelli gruppo è simile alla console [Modelli sito](/help/communities/sites.md). Entrambi sono blueprint per un set di pagine e funzionalità precablate che formano un sito community. La differenza è che un modello di sito è per la comunità principale e un modello di gruppo è per un gruppo di community, una sottocomunità nidificata all&#39;interno della comunità principale.

Un gruppo community è incorporato in un modello di sito includendo la funzione [Groups](/help/communities/functions.md#groups-function) (che non può essere né la prima né la sola funzione nel modello).

Per quanto riguarda Communities [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack), è possibile nidificare i gruppi includendo la funzione Groups all&#39;interno di un modello di gruppo.

Nel momento in cui viene eseguita un&#39;azione per creare un nuovo gruppo community, viene selezionato il modello (struttura) del gruppo. La selezione dipende dalla configurazione della funzione Gruppi al momento dell&#39;aggiunta al modello di sito o di gruppo.

>[!NOTE]
>
>Le console per la creazione di [siti community](/help/communities/sites-console.md), [modelli di siti community](/help/communities/sites.md), [modelli di gruppi community](/help/communities/tools-groups.md) e [funzioni community](/help/communities/functions.md) sono utilizzabili solo nell&#39;ambiente di authoring.

## Console Modelli gruppo {#group-templates-console}

Per accedere alla console dei modelli di gruppi nell’ambiente AEM Author:

* Selezionare **Strumenti | Community | Modelli di gruppo,** dalla navigazione globale.

Questa console visualizza i modelli da cui è possibile creare un [sito community](/help/communities/sites-console.md) e consente di creare nuovi modelli di gruppo.

![Modello per gruppi community](assets/groups-template.png)

## Crea modello gruppo {#create-group-template}

Per iniziare a creare un nuovo modello di gruppo, selezionate `Create`.

Viene visualizzato il pannello Editor sito che contiene 3 sottopannelli:

### Informazioni di base {#basic-info}

![site-basic-info](assets/site-basic-info.png)

Nel pannello Informazioni di base, un nome, una descrizione e se il modello è abilitato o disabilitato sono configurati:

* **Nome nuovo modello per gruppo**

   ID del nome del modello.

* **Descrizione**

   Descrizione del modello.

* **Disattivato/Abilitato**

   Un interruttore di attivazione/disattivazione che controlla se il modello è referenziabile.

#### Miniatura  {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

(Facoltativo) Selezionate l’icona Carica immagine per visualizzare una miniatura con il nome e la descrizione per i creatori dei siti della community.

#### Struttura {#structure}

>[!CAUTION]
>
>Se lavorate con AEM 6.1 Communities FP4 o versioni precedenti, non aggiungete una funzione di gruppo a un modello di gruppo.
>
>La funzione dei gruppi nidificati è disponibile a partire da Communities [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Non è ancora consentito aggiungere una funzione Groups come prima o unica funzione in un modello.

![Editor modelli di gruppo](assets/template-editor.png)

Per aggiungere funzioni per la community, trascinate dal lato destro a sinistra nell&#39;ordine in cui dovrebbero essere visualizzati i collegamenti del menu del sito. Gli stili verranno applicati al modello durante la creazione del sito.

Ad esempio, se desiderate un forum, trascinate la funzione forum dalla libreria e rilasciatela sotto il generatore di modelli. In questo modo si aprirà la finestra di dialogo di configurazione del forum. Per informazioni sulle finestre di dialogo di configurazione, vedere la [console delle funzioni](/help/communities/functions.md).

Continuate a trascinare qualsiasi altra funzione della community desiderata per un sito della community secondaria (gruppo) basato su questo modello.

![funzioni di trascinamento](assets/dragfunctions.png)

Una volta che tutte le funzioni desiderate sono state rilasciate nell&#39;area del generatore di modelli e configurate, selezionare **Save** nell&#39;angolo superiore destro.

##  Modifica modello gruppo{#edit-group-template}

Quando visualizzate i gruppi della community nella console principale [Modelli di gruppo](#group-templates-console), è possibile selezionare un modello di gruppo esistente da modificare.

La modifica di un modello di gruppo non ha effetto sui siti community già creati dal modello. È possibile [modificare direttamente la struttura di un sito della community ](/help/communities/sites-console.md#modify-structure).

Questo processo fornisce gli stessi pannelli di [creazione di un modello di gruppo](#create-group-template).
