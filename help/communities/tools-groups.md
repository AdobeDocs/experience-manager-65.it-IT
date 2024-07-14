---
title: Modelli per gruppi
description: Scopri come accedere alla console Modelli di gruppo per un set di pagine e funzionalità collegate a un sito community.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# Modelli per gruppi {#group-templates}

La console Modelli gruppo è simile alla console [Modelli sito](/help/communities/sites.md). Entrambi sono blueprint per un set di pagine e funzionalità precollegate che costituiscono un sito della community. La differenza sta nel fatto che un modello di sito è per la community principale e un modello di gruppo è per un gruppo community, una sottocommunity nidificata all’interno della community principale.

Un gruppo community viene incorporato in un modello di sito includendo la funzione [Groups](/help/communities/functions.md#groups-function) (che non può essere la prima o l&#39;unica funzione nel modello).

A partire da Communities [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack), è possibile nidificare i gruppi includendo la funzione Groups all&#39;interno di un modello di gruppo.

Quando si esegue un&#39;azione per creare un gruppo community, viene selezionato il modello (struttura) del gruppo. La selezione dipende dalla configurazione della funzione Gruppi quando viene aggiunta al sito o al modello di gruppo.

>[!NOTE]
>
>Le console per la creazione di [siti community](/help/communities/sites-console.md), [modelli di siti community](/help/communities/sites.md), [modelli di gruppi community](/help/communities/tools-groups.md) e [funzioni community](/help/communities/functions.md) sono utilizzabili solo nell&#39;ambiente di authoring.

## Console Modelli per gruppi {#group-templates-console}

Per raggiungere la console dei modelli di gruppo nell’ambiente di authoring AEM:

* Seleziona **strumenti | Community | Modelli di gruppo,** dalla navigazione globale.

Questa console visualizza i modelli da cui è possibile creare un [sito community](/help/communities/sites-console.md) e consente la creazione di nuovi modelli di gruppo.

![Modello per gruppi community](assets/groups-template.png)

## Crea modello gruppo {#create-group-template}

Per iniziare a creare un modello di gruppo, selezionare `Create`.

Viene visualizzato il pannello Editor sito, che contiene tre pannelli secondari:

### Informazioni di base {#basic-info}

![site-basic-info](assets/site-basic-info.png)

Nel pannello Informazioni di base, vengono configurati un nome, una descrizione e se il modello è abilitato o disabilitato:

* **Nome nuovo modello gruppo**

  ID del nome del modello.

* **Descrizione**

  Descrizione del modello.

* **Disabilitato/Abilitato**

  Un interruttore che controlla se il modello è referenziabile.

#### Miniatura  {#thumbnail}

![miniatura-sito](assets/site-thumbnail.png)

(Facoltativo) Fai clic sull&#39;icona Carica immagine per visualizzare una miniatura con il Nome e la Descrizione ai creatori di siti della community.

#### Struttura {#structure}

>[!CAUTION]
>
>Se si lavora con AEM 6.1 Communities FP4 o versioni precedenti, non aggiungere una funzione di gruppo a un modello di gruppo.
>
>La funzionalità dei gruppi nidificati è disponibile a partire da Communities [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Non è ancora consentito aggiungere una funzione Gruppi come prima o unica funzione in un modello.

![Editor modelli di gruppo](assets/template-editor.png)

Per aggiungere funzioni di community, trascinare il puntatore del mouse dal lato destro a quello sinistro nell&#39;ordine in cui devono essere visualizzati i collegamenti del menu del sito. Gli stili vengono applicati al modello durante la creazione del sito.

Ad esempio, se desideri un forum, trascina la funzione forum dalla libreria e rilasciala sotto al generatore di modelli. Questo determina l’apertura della finestra di dialogo per la configurazione del forum. Per informazioni sulle finestre di dialogo di configurazione, vedere la [console delle funzioni](/help/communities/functions.md).

Continuare a trascinare tutte le altre funzioni community desiderate per un sito (gruppo) di comunità secondaria basato su questo modello.

![trascina funzioni](assets/dragfunctions.png)

Una volta eliminate e configurate tutte le funzioni desiderate nell&#39;area del generatore di modelli, seleziona **Salva** nell&#39;angolo superiore destro.

## Modifica modello gruppo {#edit-group-template}

Quando si visualizzano i gruppi community nella [console Modelli gruppo](#group-templates-console) principale, è possibile selezionare un modello di gruppo esistente da modificare.

La modifica di un modello di gruppo non influisce sui siti community già creati dal modello. È invece possibile [modificare direttamente la struttura di un sito community](/help/communities/sites-console.md#modify-structure).

Questo processo fornisce gli stessi pannelli di [creazione di un modello di gruppo](#create-group-template).
