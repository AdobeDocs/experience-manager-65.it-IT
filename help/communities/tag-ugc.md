---
title: Assegnazione di tag ai contenuti generati dall'utente
seo-title: Assegnazione di tag ai contenuti generati dall'utente
description: Assegnazione di tag ai contenuti generati dagli utenti (UGC, user generated content) è il modo in cui i membri della community possono aiutare altri membri a cercare contenuti
seo-description: Assegnazione di tag ai contenuti generati dagli utenti (UGC, user generated content) è il modo in cui i membri della community possono aiutare altri membri a cercare contenuti
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 3%

---


# Assegnazione tag a contenuto generato dall&#39;utente {#tagging-user-generated-content}

## Panoramica {#overview}

L’assegnazione di tag ai contenuti generati dall’utente (UGC) è il mezzo mediante il quale i membri della community possono facilitare la ricerca di contenuti da parte di altri membri.

In genere, i tag vengono applicati da autori e amministratori nell’ambiente di authoring. L’assegnazione di tag UGC è univoca in quanto i tag UGC vengono applicati dai membri della community nell’ambiente di pubblicazione.

Gli spazi dei nomi e le tassonomie dei tag sono gli stessi per entrambe le applicazioni.

## Caratteristiche delle community {#communities-features}

Le  funzioni AEM Communities che possono essere configurate per consentire l’assegnazione di tag sono:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Libreria file](file-library.md)
* [Forum](forum.md#configuretheaddedforum)
* [Domande e risposte](working-with-qna.md)

## Amministrazione dei tag {#administering-tags}

Per creare e gestire spazi dei nomi dei tag e tassonomie, vedere [Amministrazione dei tag](../../help/sites-administering/tags.md#tagging-console).

Per informazioni sugli sviluppatori, vedere [Tag Essentials](tag.md).

Consultate [Utilizzo di Social Tag Cloud](tagcloud.md) per aggiungere un componente Social Tag Cloud a una pagina per facilitare la ricerca di UGC pubblicate utilizzando i tag applicati.

### Autorizzazioni tag {#tag-permissions}

Le autorizzazioni predefinite sono impostate in modo da non consentire agli spazi dei nomi dei tag di essere letti da tutti gli utenti nell’ambiente di pubblicazione.

Poiché i tag vengono applicati a UGC nell’ambiente di pubblicazione, è necessario abilitare l’autorizzazione di lettura per i membri della community, affinché possano selezionare i tag da applicare.

Consultate [Impostazione delle autorizzazioni per i tag](../../help/sites-administering/tags.md#setting-tag-permissions).

Di seguito viene illustrato come viene visualizzato in CRXDE quando un amministratore applica le autorizzazioni di lettura a `/etc/tag/discussions` per il gruppo `Community Engage Members`.

![tag-permissions](assets/tag-permissions.png)

