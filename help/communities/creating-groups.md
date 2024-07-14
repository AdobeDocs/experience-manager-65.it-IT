---
title: Gruppi community
description: Scopri in che modo la funzione Gruppi community consente di creare dinamicamente una sottocommunity all’interno di un sito community da parte di utenti autorizzati in Publish e Author.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Gruppi community {#community-groups}

La funzione Gruppi community consente la creazione dinamica di una sottocommunity all’interno di un sito community da parte di utenti autorizzati (membri e autori della community) dagli ambienti di pubblicazione e authoring.

Questa funzionalità è presente quando la funzione [gruppi](/help/communities/functions.md#groups-function) è presente nella struttura [sito community](/help/communities/sites-console.md).

Un [modello per gruppo community](/help/communities/tools-groups.md) fornisce la struttura della pagina del gruppo community quando un gruppo community viene creato in modo dinamico.

Uno o più modelli di gruppo vengono selezionati per la funzione gruppi quando la funzione viene aggiunta alla struttura di un sito community o a un modello di sito community. Questo elenco di modelli di gruppo viene presentato al membro o all&#39;autore che crea un gruppo in modo dinamico dall&#39;interno del sito community.

## Creazione di un nuovo gruppo {#creating-a-new-group}

La possibilità di creare un gruppo community si basa sull&#39;esistenza di un sito community che include la funzione dei gruppi, ad esempio uno creato dal [modello del sito di riferimento](/help/communities/sites.md).

Gli esempi seguenti utilizzano il sito community creato da `Reference Site Template` come descritto nell&#39;esercitazione [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md).

Questa è la pagina che viene caricata al momento della pubblicazione quando è selezionata la voce di menu **Gruppi**:

![nuovo-gruppo](assets/new-group.png)

Quando selezioni l&#39;icona **Nuovo gruppo**, viene visualizzata una finestra di dialogo di modifica.

Nella scheda **Impostazioni** sono disponibili le caratteristiche di base del gruppo:

![impostazioni-gruppo](assets/group-settings.png)

* **Nome gruppo**

  Titolo del gruppo che si desidera visualizzare nel sito della community. Evita di usare caratteri di sottolineatura (_) e parole chiave come risorse e configurazione nel nome del gruppo.

* **Descrizione**

  Descrizione del gruppo da visualizzare sul sito community.

* **Invita**

  Elenco di membri da invitare al gruppo. La ricerca del tipo di anticipo fornisce suggerimenti ai membri della community da invitare.

* **Nome URL gruppo**

  Il nome della pagina del gruppo che diventa parte dell’URL.

* **Apri gruppo**

  La selezione di `Open Group` indica che qualsiasi visitatore anonimo del sito può visualizzare il contenuto e deseleziona `Member Only Group`.

* **Gruppo per soli membri**

  La selezione di `Member Only Group` indica che solo i membri del gruppo possono visualizzare il contenuto e deseleziona `Open Group`.

Nella scheda **Modello** è possibile effettuare una selezione dall&#39;elenco dei modelli per gruppi community. Questi modelli sono stati specificati quando la funzione dei gruppi è stata inclusa nella struttura del sito community o in un modello di sito community.

![modello-gruppo](assets/group-template.png)

Nella scheda **Immagine** è possibile caricare un&#39;immagine da visualizzare per il gruppo nella pagina Gruppi del sito community. Il foglio di stile predefinito ridimensiona l&#39;immagine a 170 x 90 pixel.

![immagine-gruppo](assets/group-image.png)

Selezionando **Crea gruppo**, le pagine del gruppo vengono create in base al modello scelto, viene creato un gruppo di utenti per l&#39;appartenenza e la pagina Gruppi viene aggiornata per mostrare la nuova sottocomunità.

Ad esempio, la pagina Gruppi con una nuova sottocommunity denominata &quot;Gruppo attivo&quot;, per la quale è stata caricata una miniatura di immagine, viene visualizzata come segue (è ancora connesso come amministratore di un gruppo community):

![pagina-gruppo](assets/group-page.png)

Selezionando il collegamento `Focus Group` si apre la pagina Gruppo attivo nel browser, che ha un aspetto iniziale basato sul modello scelto e include un sottomenu sotto il menu del sito community principale:

![pagina-gruppo-aperto](assets/open-group-page.png)

### Componente elenco membri del gruppo community {#community-group-member-list-component}

Il componente `Community Group Member List` è destinato agli sviluppatori di modelli di gruppo.

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Community Group Essentials](/help/communities/essentials-groups.md) per sviluppatori.

Per altre informazioni relative ai gruppi community, visitare [Gestione di utenti e gruppi di utenti](/help/communities/users.md).
