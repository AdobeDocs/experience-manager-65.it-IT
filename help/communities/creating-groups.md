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

La funzione gruppi community consente a una sottocommunity di creare in modo dinamico all’interno di un sito community utenti autorizzati (membri della community e autori) dagli ambienti di pubblicazione e authoring.

Questa funzionalità è presente quando [funzione gruppi](/help/communities/functions.md#groups-function) è presente nel [sito della community](/help/communities/sites-console.md) struttura.

A [modello di gruppo community](/help/communities/tools-groups.md) fornisce la progettazione della pagina del gruppo community quando un gruppo community viene creato in modo dinamico.

Uno o più modelli di gruppo vengono selezionati per la funzione dei gruppi quando la funzione viene aggiunta alla struttura di un sito community o a un modello di sito community. Questo elenco di modelli di gruppo viene presentato al membro o all&#39;autore che crea in modo dinamico un nuovo gruppo dall&#39;interno del sito community.

## Creazione di un nuovo gruppo {#creating-a-new-group}

La capacità di creare un nuovo gruppo community si basa sull&#39;esistenza di un sito community che include la funzione dei gruppi, come quella creata dalla [Modello del sito di riferimento](/help/communities/sites.md).

Gli esempi che seguono utilizzano il sito della community creato dal `Reference Site Template` come descritto nel [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md) esercitazione.

Questa è la pagina che viene caricata al momento della pubblicazione **Gruppi** voce di menu selezionata:

![nuovo gruppo](assets/new-group.png)

Quando selezioni la **Nuovo gruppo** viene visualizzata una finestra di dialogo di modifica.

Sotto la **Impostazioni** fornisce le funzioni di base del gruppo:

![impostazioni gruppo](assets/group-settings.png)

* **Nome gruppo**

   Titolo del gruppo da visualizzare sul sito della community. Evita di usare caratteri di sottolineatura (_) e parole chiave come le risorse e la configurazione nel nome del gruppo.

* **Descrizione**

   Una descrizione del gruppo da visualizzare sul sito della community.

* **Invita**

   Un elenco di membri da invitare a far parte del gruppo. La ricerca di tipo &quot;type-ahead&quot; fornirà suggerimenti dei membri della community da invitare.

* **Nome URL del gruppo**

   Nome della pagina del gruppo che diventa parte dell’URL.

* **Apri gruppo**

   Selezione `Open Group` indica che un visitatore anonimo del sito può visualizzare il contenuto e deseleziona `Member Only Group`.

* **Gruppo per soli membri**

   Selezione `Member Only Group` indica che solo i membri del gruppo possono visualizzare il contenuto e deseleziona `Open Group`.

Sotto la **Modello** tab è la possibilità di selezionare dall&#39;elenco dei modelli di gruppo community specificati quando la funzione gruppi è stata inclusa nella struttura del sito community o in un modello di sito community.

![modello di gruppo](assets/group-template.png)

Sotto la **Immagine** tab è la capacità di caricare un&#39;immagine da visualizzare per il gruppo nella pagina Groups del sito community. Il foglio di stile predefinito ridimensiona l’immagine a 170 x 90 pixel.

![immagine di gruppo](assets/group-image.png)

Selezionando la **Crea gruppo** le pagine del gruppo vengono create in base al modello scelto e viene creato un gruppo di utenti per l’iscrizione. La pagina Gruppi verrà aggiornata per mostrare la nuova sottocomunità.

Ad esempio, la pagina Groups (Gruppi) con una nuova sottocommunity denominata &quot;Focus Group&quot;, per la quale è stata caricata una miniatura dell’immagine, verrà visualizzata come segue (ancora connesso come amministratore del gruppo community):

![pagina di gruppo](assets/group-page.png)

Selezione della `Focus Group` Il collegamento consente di aprire la pagina Gruppo di elementi attivi nel browser, che ha un aspetto iniziale basato sul modello scelto, e include un sottomenu nel menu del sito della community principale:

![open-group-page](assets/open-group-page.png)

### Componente elenco membri gruppo community {#community-group-member-list-component}

La `Community Group Member List` Il componente è destinato agli sviluppatori di modelli di gruppo.

### Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sui gruppi community](/help/communities/essentials-groups.md) per sviluppatori.

Per altre informazioni relative ai gruppi della community, visita [Gestione di utenti e gruppi di utenti](/help/communities/users.md).
