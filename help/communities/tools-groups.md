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

La console Modelli di gruppo è simile alla [Modelli del sito](/help/communities/sites.md) console. Entrambi sono blueprint per un set di pagine e funzionalità precollegate che costituiscono un sito della community. La differenza sta nel fatto che un modello di sito è per la community principale e un modello di gruppo è per un gruppo community, una sottocommunity nidificata all’interno della community principale.

Un gruppo community viene incorporato in un modello di sito includendo [Funzione Gruppi](/help/communities/functions.md#groups-function) (che non può essere la prima o l&#39;unica funzione del modello).

A partire da Communities [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack), è possibile nidificare i gruppi includendo la funzione Gruppi all’interno di un modello di gruppo.

Quando si esegue un&#39;azione per creare un gruppo community, viene selezionato il modello (struttura) del gruppo. La selezione dipende dalla configurazione della funzione Gruppi quando viene aggiunta al sito o al modello di gruppo.

>[!NOTE]
>
>Le console per la creazione di [siti community](/help/communities/sites-console.md), [modelli per sito community](/help/communities/sites.md), [modelli per gruppi community](/help/communities/tools-groups.md), e [funzioni community](/help/communities/functions.md) devono essere utilizzati solo nell’ambiente di authoring.

## Console Modelli per gruppi {#group-templates-console}

Per raggiungere la console dei modelli di gruppo nell’ambiente di authoring AEM:

* Seleziona **Strumenti | Community | Modelli per gruppi,** dalla navigazione globale.

In questa console vengono visualizzati i modelli da cui [sito community](/help/communities/sites-console.md) può essere creato e consente di creare nuovi modelli di gruppo.

![Modello per gruppi community](assets/groups-template.png)

## Crea modello gruppo {#create-group-template}

Per iniziare a creare un modello di gruppo, seleziona `Create`.

Viene visualizzato il pannello Editor sito, che contiene tre pannelli secondari:

### Informazioni di base {#basic-info}

![site-basic-info](assets/site-basic-info.png)

Nel pannello Informazioni di base, vengono configurati un nome, una descrizione e se il modello è abilitato o disabilitato:

* **Nome nuovo modello gruppo**

  ID del nome del modello.

* **Descrizione**

  Descrizione del modello.

* **Disabilitato/abilitato**

  Un interruttore che controlla se il modello è referenziabile.

#### Miniatura  {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

(Facoltativo) Fai clic sull&#39;icona Carica immagine per visualizzare una miniatura con il Nome e la Descrizione ai creatori di siti della community.

#### Struttura {#structure}

>[!CAUTION]
>
>Se si lavora con AEM 6.1 Communities FP4 o versioni precedenti, non aggiungere una funzione di gruppo a un modello di gruppo.
>
>La funzione Gruppi nidificati è disponibile nelle community [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Non è ancora consentito aggiungere una funzione Gruppi come prima o unica funzione in un modello.

![Editor modelli per gruppi](assets/template-editor.png)

Per aggiungere funzioni di community, trascinare il puntatore del mouse dal lato destro a quello sinistro nell&#39;ordine in cui devono essere visualizzati i collegamenti del menu del sito. Gli stili vengono applicati al modello durante la creazione del sito.

Ad esempio, se desideri un forum, trascina la funzione forum dalla libreria e rilasciala sotto al generatore di modelli. Questo determina l’apertura della finestra di dialogo per la configurazione del forum. Consulta la [console funzioni](/help/communities/functions.md) per informazioni sulle finestre di dialogo di configurazione.

Continuare a trascinare tutte le altre funzioni community desiderate per un sito (gruppo) di comunità secondaria basato su questo modello.

![trascina funzioni](assets/dragfunctions.png)

Una volta rilasciate e configurate tutte le funzioni desiderate nell’area di creazione del modello, seleziona **Salva** nell’angolo superiore destro.

## Modifica modello gruppo {#edit-group-template}

Quando si visualizzano i gruppi della community nel [Console Modelli per gruppi](#group-templates-console), è possibile selezionare un modello di gruppo esistente da modificare.

La modifica di un modello di gruppo non influisce sui siti community già creati dal modello. È possibile eseguire direttamente [modificare un sito community](/help/communities/sites-console.md#modify-structure)La struttura di.

Questo processo fornisce gli stessi pannelli [creazione di un modello di gruppo](#create-group-template).
