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

La console Modelli gruppo è simile alla console Modelli [](/help/communities/sites.md) sito. Entrambi sono blueprint per un set di pagine e funzionalità precablate che formano un sito community. La differenza è che un modello di sito è per la comunità principale e un modello di gruppo è per un gruppo di community, una sottocomunità nidificata all&#39;interno della comunità principale.

Un gruppo community è incorporato in un modello di sito includendo la funzione [](/help/communities/functions.md#groups-function) Gruppi (che non può essere né la prima né la sola funzione nel modello).

Nel [Feature Pack 1](/help/communities/deploy-communities.md#latestfeaturepack)di Communities, è possibile nidificare i gruppi includendo la funzione Gruppi in un modello di gruppo.

Nel momento in cui viene eseguita un&#39;azione per creare un nuovo gruppo community, viene selezionato il modello (struttura) del gruppo. La selezione dipende dalla configurazione della funzione Gruppi al momento dell&#39;aggiunta al modello di sito o di gruppo.

>[!NOTE]
>
>Le console per la creazione di siti [](/help/communities/sites-console.md)community, modelli [di siti](/help/communities/sites.md)community, modelli [di gruppi](/help/communities/tools-groups.md) community e funzioni [](/help/communities/functions.md) community sono utilizzabili solo nell’ambiente di authoring.

## Console Modelli per gruppi {#group-templates-console}

Per accedere alla console dei modelli di gruppi nell’ambiente AEM Author:

* Seleziona **strumenti | Community | Modelli di gruppo,** dalla navigazione globale.

Questa console visualizza i modelli da cui è possibile creare un sito [](/help/communities/sites-console.md) community e consente di creare nuovi modelli di gruppo.

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
>La funzione dei gruppi nidificati è disponibile a partire da Community [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Non è ancora consentito aggiungere una funzione Groups come prima o unica funzione in un modello.

![Editor modelli di gruppo](assets/template-editor.png)

Per aggiungere funzioni per la community, trascinate dal lato destro a sinistra nell&#39;ordine in cui dovrebbero essere visualizzati i collegamenti del menu del sito. Gli stili verranno applicati al modello durante la creazione del sito.

Ad esempio, se desiderate un forum, trascinate la funzione forum dalla libreria e rilasciatela sotto il generatore di modelli. In questo modo si aprirà la finestra di dialogo di configurazione del forum. Per informazioni sulle finestre di dialogo di configurazione, vedere la console [](/help/communities/functions.md) delle funzioni.

Continuate a trascinare qualsiasi altra funzione della community desiderata per un sito della community secondaria (gruppo) basato su questo modello.

![funzioni di trascinamento](assets/dragfunctions.png)

Una volta che tutte le funzioni desiderate sono state rilasciate nell&#39;area del generatore di modelli e configurate, selezionate **Salva** nell&#39;angolo superiore destro.

##  Modifica modello gruppo{#edit-group-template}

Quando visualizzate gruppi di community nella console [Modelli](#group-templates-console)gruppo principale, è possibile selezionare un modello di gruppo esistente da modificare.

La modifica di un modello di gruppo non ha effetto sui siti community già creati dal modello. È possibile [modificare direttamente la struttura di un sito](/help/communities/sites-console.md#modify-structure)community.

Questo processo fornisce gli stessi pannelli utilizzati per [creare un modello](#create-group-template)di gruppo.
