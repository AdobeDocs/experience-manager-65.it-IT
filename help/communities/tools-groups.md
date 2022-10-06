---
title: Modelli per gruppi
seo-title: Group Templates
description: Come accedere alla console Modelli di gruppo
seo-description: How to access the Group Templates console
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# Modelli per gruppi {#group-templates}

La console Modelli di gruppo è simile alla [Modelli di sito](/help/communities/sites.md) console. Entrambe sono blueprint per un set di pagine e funzionalità precablate che formano un sito community. La differenza consiste nel fatto che un modello di sito è per la comunità principale e un modello di gruppo è per un gruppo community, una sottocomunità nidificata all’interno della comunità principale.

Un gruppo community viene incorporato in un modello di sito includendo [Funzione Groups](/help/communities/functions.md#groups-function) (che non può essere la prima funzione o l&#39;unica funzione nel modello).

A livello di Comunità [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack), è possibile nidificare i gruppi includendo la funzione Groups all’interno di un modello di gruppo.

Nel momento in cui viene intrapresa un&#39;azione per creare un nuovo gruppo community, viene selezionato il modello (struttura) del gruppo. La selezione dipende dalla configurazione della funzione Groups (Gruppi) quando viene aggiunta al modello di sito o di gruppo.

>[!NOTE]
>
>Le console per la creazione di [siti della community](/help/communities/sites-console.md), [modelli di sito community](/help/communities/sites.md), [modelli di gruppo community](/help/communities/tools-groups.md) e [funzioni della community](/help/communities/functions.md) sono utilizzabili solo nell’ambiente di authoring.

## Console Modelli di gruppo {#group-templates-console}

Per raggiungere la console dei modelli di gruppi nell’ambiente di authoring di AEM:

* Seleziona **Strumenti | Comunità | Modelli di gruppo,** dalla navigazione globale.

In questa console vengono visualizzati i modelli da cui viene [sito della community](/help/communities/sites-console.md) può essere creato e consente di creare nuovi modelli di gruppo.

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

Ad esempio, se desideri un forum, trascina la funzione forum dalla libreria e rilascia sotto il generatore di modelli. In questo modo si aprirà la finestra di dialogo di configurazione del forum. Consulta la sezione [console funzioni](/help/communities/functions.md) per informazioni sulle finestre di dialogo di configurazione.

Continua a trascinare e rilasciare tutte le altre funzioni della community desiderate per un sito della sottocommunity (gruppo) basato su questo modello.

![trascinare le funzioni](assets/dragfunctions.png)

Una volta che tutte le funzioni desiderate sono state rilasciate nell&#39;area del generatore di modelli e configurate, seleziona **Salva** nell&#39;angolo in alto a destra.

##  Modifica modello gruppo {#edit-group-template}

Quando visualizzi gruppi della community nella pagina principale [Console Modelli di gruppo](#group-templates-console), è possibile selezionare un modello di gruppo esistente da modificare.

La modifica di un modello di gruppo non influisce sui siti della community già creati dal modello. È possibile [modificare un sito community](/help/communities/sites-console.md#modify-structure)La struttura invece.

Questo processo fornisce gli stessi pannelli di [creazione di un modello di gruppo](#create-group-template).
