---
title: Gruppi community
seo-title: Gruppi community
description: Creazione di gruppi community
seo-description: Creazione di gruppi community
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
translation-type: tm+mt
source-git-commit: 6337a57ea12f1e026f6c754a083307ce018a1c13
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---


# Gruppi community {#community-groups}

La funzione per i gruppi della community è la possibilità per una sottocomunità di essere creata in modo dinamico all&#39;interno di un sito della community da utenti autorizzati (membri della community e autori) dagli ambienti di pubblicazione e authoring.

Questa capacità è presente quando la funzione [](/help/communities/functions.md#groups-function) dei gruppi è presente nella struttura del sito [](/help/communities/sites-console.md) community.

Un modello [di gruppo](/help/communities/tools-groups.md) community fornisce la progettazione della pagina di gruppo community quando un gruppo community viene creato in modo dinamico.

Uno o più modelli di gruppo vengono selezionati per la funzione dei gruppi quando la funzione viene aggiunta alla struttura di un sito community o a un modello di sito community. Questo elenco di modelli di gruppo viene presentato al membro o all&#39;autore che crea in modo dinamico un nuovo gruppo dall&#39;interno del sito della community.

## Creating a New Group {#creating-a-new-group}

La capacità di creare un nuovo gruppo di community si basa sull&#39;esistenza di un sito community che include la funzione dei gruppi, come quella creata con il Modello [del sito di](/help/communities/sites.md)riferimento.

Gli esempi seguenti utilizzano il sito della community creato a partire da `Reference Site Template` come descritto in [Guida introduttiva  esercitazione AEM Communities](/help/communities/getting-started.md) .

Pagina che viene caricata al momento della pubblicazione quando è selezionata la voce di menu **Gruppi** :

![nuovo gruppo](assets/new-group.png)

Quando selezionate l’icona **Nuovo gruppo** , si apre una finestra di dialogo di modifica.

Nella scheda **Impostazioni** , sono disponibili le funzioni di base del gruppo:

![group-settings](assets/group-settings.png)

* **Nome gruppo**

   Titolo del gruppo da visualizzare sul sito della community.

* **Descrizione**

   Una descrizione del gruppo da visualizzare sul sito della community.

* **Invita**

   Un elenco di membri da invitare a far parte del gruppo. La ricerca di tipo &quot;Type-ahead&quot; fornirà suggerimenti da invitare da parte dei membri della community.

* **Nome URL del gruppo**

   Nome della pagina del gruppo che diventa parte dell’URL.

* **Apri gruppo**

   La selezione `Open Group` indica che un visitatore anonimo può visualizzare il contenuto e ne deseleziona `Member Only Group`.

* **Gruppo per soli membri**

   La selezione `Member Only Group` indica che solo i membri del gruppo possono visualizzare il contenuto e ne deseleziona `Open Group`.

Nella scheda **Modello** è possibile selezionare dall&#39;elenco dei modelli di gruppo community specificati quando la funzione dei gruppi è stata inclusa nella struttura del sito community o in un modello di sito community.

![group-template](assets/group-template.png)

Nella scheda **Immagine** è possibile caricare un&#39;immagine da visualizzare per il gruppo nella pagina Gruppi del sito della community. Il foglio di stile predefinito ridimensiona l&#39;immagine a 170 x 90 pixel.

![group-image](assets/group-image.png)

Selezionando il pulsante **Crea gruppo** , le pagine del gruppo vengono create in base al modello scelto e viene creato un gruppo di utenti per l’iscrizione. La pagina Gruppi verrà aggiornata per mostrare la nuova sub-community.

Ad esempio, la pagina Gruppi con una nuova sottocomunità denominata &quot;Focus Group&quot;, per la quale è stata caricata una miniatura di immagine, verrà visualizzata come segue (ancora con accesso come amministratore di gruppo community):

![group-page](assets/group-page.png)

Quando si seleziona il `Focus Group` collegamento, nel browser viene aperta la pagina Gruppo di interesse, con un aspetto iniziale basato sul modello scelto, e un sottomenu che si trova sotto il menu del sito della community principale:

![open-group-page](assets/open-group-page.png)

### Community Group Member List Component {#community-group-member-list-component}

Il `Community Group Member List` componente è destinato agli sviluppatori di modelli di gruppo.

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Community Group Essentials](/help/communities/essentials-groups.md) per gli sviluppatori.

Per altre informazioni relative ai gruppi della community, visita [Gestione di utenti e gruppi](/help/communities/users.md)di utenti.
