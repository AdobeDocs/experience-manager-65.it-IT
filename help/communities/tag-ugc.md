---
title: Assegnazione tag ai contenuti generati dagli utenti
seo-title: Assegnazione tag ai contenuti generati dagli utenti
description: Assegnazione di tag ai contenuti generati dagli utenti (UGC, User-Generated Content) è il modo in cui i membri della community possono aiutare gli altri membri a cercare contenuti
seo-description: Assegnazione di tag ai contenuti generati dagli utenti (UGC, User-Generated Content) è il modo in cui i membri della community possono aiutare gli altri membri a cercare contenuti
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 3%

---

# Assegnazione tag ai contenuti generati dagli utenti {#tagging-user-generated-content}

## Panoramica {#overview}

L’assegnazione tag al contenuto generato dall’utente (UGC) è il mezzo con cui i membri della community possono aiutare gli altri membri a cercare contenuti.

In genere, i tag vengono applicati dagli autori e dagli amministratori nell’ambiente di authoring. L’assegnazione tag UGC è univoca in quanto i tag UGC vengono applicati dai membri della community nell’ambiente di pubblicazione.

I namespace e le tassonomie dei tag sono gli stessi per entrambe le applicazioni.

## Funzioni di Communities {#communities-features}

Le funzioni di AEM Communities che possono essere configurate per consentire l’assegnazione di tag sono:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Libreria file](file-library.md)
* [Forum](forum.md#configuretheaddedforum)
* [Domande e risposte](working-with-qna.md)

## Amministrazione dei tag {#administering-tags}

Per creare e gestire i namespace e le tassonomie dei tag, consulta [Amministrazione dei tag](../../help/sites-administering/tags.md#tagging-console) .

Per informazioni sugli sviluppatori, consulta [Tag Essentials](tag.md) .

Consulta [Utilizzo di Social Tag Cloud](tagcloud.md) per aggiungere un componente Social Tag Cloud a una pagina per facilitare la ricerca di contenuti generati dagli utenti pubblicati utilizzando i tag applicati.

### Autorizzazioni di tag {#tag-permissions}

Le autorizzazioni predefinite sono impostate per non consentire a tutti gli utenti dell’ambiente di pubblicazione di leggere i namespace dei tag.

Poiché i tag vengono applicati a UGC nell’ambiente di pubblicazione, è necessario abilitare l’autorizzazione di lettura per i membri della community affinché possano selezionare i tag da applicare.

Consulta [Impostazione delle autorizzazioni dei tag](../../help/sites-administering/tags.md#setting-tag-permissions).

Di seguito viene illustrato come viene visualizzato in CRXDE quando un amministratore applica le autorizzazioni di lettura a `/etc/tag/discussions` per il gruppo `Community Engage Members`.

![tag-permissions](assets/tag-permissions.png)
