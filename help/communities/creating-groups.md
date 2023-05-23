---
title: Gruppi community
seo-title: Community Groups
description: Creazione di gruppi community
seo-description: Creating community groups
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%

---

# Gruppi community {#community-groups}

La funzione Gruppi community consente la creazione dinamica di una sottocommunity all’interno di un sito community da parte di utenti autorizzati (membri e autori della community) dagli ambienti di pubblicazione e authoring.

Questa funzionalità è presente quando [funzione gruppi](/help/communities/functions.md#groups-function) è presente in [sito community](/help/communities/sites-console.md) struttura.

A [modello per gruppo community](/help/communities/tools-groups.md) fornisce la struttura della pagina gruppo community quando un gruppo community viene creato in modo dinamico.

Uno o più modelli di gruppo vengono selezionati per la funzione gruppi quando la funzione viene aggiunta alla struttura di un sito community o a un modello di sito community. Questo elenco di modelli di gruppo viene presentato al membro o all&#39;autore che crea dinamicamente un nuovo gruppo dall&#39;interno del sito community.

## Creazione di un nuovo gruppo {#creating-a-new-group}

La possibilità di creare un nuovo gruppo community si basa sull&#39;esistenza di un sito community che include la funzione gruppi, ad esempio uno creato da [Modello di riferimento per sito](/help/communities/sites.md).

Gli esempi seguenti utilizzano il sito community creato da `Reference Site Template` come descritto nella [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md) esercitazione.

Questa è la pagina che viene caricata al momento della pubblicazione quando **Gruppi** voce di menu selezionata:

![new-group](assets/new-group.png)

Quando selezioni il **Nuovo gruppo** viene visualizzata una finestra di dialogo per la modifica.

Sotto **Impostazioni** , sono disponibili le funzioni di base del gruppo:

![group-settings](assets/group-settings.png)

* **Nome gruppo**

   Titolo del gruppo da visualizzare sul sito della community. Evita di usare caratteri di sottolineatura (_) e parole chiave come risorse e configurazione nel nome del gruppo.

* **Descrizione**

   Descrizione del gruppo da visualizzare sul sito community.

* **Invita**

   Elenco di membri da invitare a partecipare al gruppo. La ricerca del tipo di anticipo fornirà suggerimenti ai membri della community da invitare.

* **Nome URL del gruppo**

   Il nome della pagina del gruppo che diventa parte dell’URL.

* **Apri gruppo**

   Selezione `Open Group` indica che qualsiasi visitatore anonimo del sito può visualizzare il contenuto e deseleziona `Member Only Group`.

* **Gruppo per soli membri**

   Selezione `Member Only Group` indica che solo i membri del gruppo possono visualizzare il contenuto e deseleziona `Open Group`.

Sotto **Modello** scheda è la possibilità di selezionare dall&#39;elenco dei modelli di gruppo community specificati quando la funzione gruppi è stata inclusa nella struttura del sito community o in un modello di sito community.

![group-template](assets/group-template.png)

Sotto **Immagine** è la possibilità di caricare un&#39;immagine da visualizzare per il gruppo nella pagina Gruppi del sito community. Il foglio di stile predefinito ridimensiona l&#39;immagine a 170 x 90 pixel.

![immagine-gruppo](assets/group-image.png)

Selezionando **Crea gruppo** , le pagine del gruppo vengono create in base al modello scelto, viene creato un gruppo di utenti per l&#39;appartenenza e la pagina Gruppi viene aggiornata per mostrare la nuova sottocommunity.

Ad esempio, la pagina Gruppi con una nuova sottocommunity denominata &quot;Gruppo attivo&quot;, per la quale è stata caricata una miniatura di immagine, viene visualizzata come segue (è ancora connesso come amministratore di un gruppo community):

![group-page](assets/group-page.png)

Selezione del `Focus Group` Il collegamento consente di aprire la pagina Gruppo attivo nel browser, che ha un aspetto iniziale basato sul modello scelto e include un sottomenu nel menu del sito community principale:

![open-group-page](assets/open-group-page.png)

### Componente elenco membri del gruppo community {#community-group-member-list-component}

Il `Community Group Member List` Il componente è destinato agli sviluppatori di modelli di gruppo.

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Nozioni di base sul gruppo community](/help/communities/essentials-groups.md) pagina per sviluppatori.

Per altre informazioni relative ai gruppi della community, visita [Gestione di utenti e gruppi di utenti](/help/communities/users.md).
