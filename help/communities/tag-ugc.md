---
title: Assegnazione di tag ai contenuti generati dagli utenti
description: L'assegnazione di tag a contenuti generati dagli utenti (UGC, User Generated Content) è il modo in cui i membri della community possono aiutare gli altri membri a cercare contenuti
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 3%

---

# Assegnazione di tag ai contenuti generati dagli utenti {#tagging-user-generated-content}

## Panoramica {#overview}

L&#39;assegnazione di tag a contenuti generati dagli utenti (UGC, User-Generated Content) è il mezzo tramite il quale i membri della community possono aiutare gli altri membri a cercare contenuti.

In genere, i tag vengono applicati dagli autori e dagli amministratori nell’ambiente di authoring. L’assegnazione tag UGC è univoca in quanto i tag UGC vengono applicati dai membri della community nell’ambiente di pubblicazione.

Gli spazi dei nomi e le tassonomie dei tag sono gli stessi per entrambe le applicazioni.

## Funzioni community {#communities-features}

Le funzioni di AEM Communities che possono essere configurate per consentire l’assegnazione tag sono:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Libreria file](file-library.md)
* [Forum](forum.md#configuretheaddedforum)
* [Domande e risposte](working-with-qna.md)

## Amministrazione dei tag {#administering-tags}

Consulta [Amministrazione dei tag](../../help/sites-administering/tags.md#tagging-console) per creare e gestire gli spazi dei nomi e le tassonomie dei tag.

Consulta [Nozioni di base sui tag](tag.md) per informazioni sugli sviluppatori.

Consulta [Utilizzo di Tag cloud per social network](tagcloud.md) per aggiungere un componente Cloud di tag per social network a una pagina per facilitare la ricerca di contenuti UGC pubblicati utilizzando i tag applicati.

### Autorizzazioni tag {#tag-permissions}

Le autorizzazioni predefinite sono impostate per non consentire agli spazi dei nomi dei tag di essere letti da tutti gli utenti nell’ambiente di pubblicazione.

Poiché i tag vengono applicati a UGC nell’ambiente di pubblicazione, è necessario abilitare l’autorizzazione di lettura per i membri della community affinché possano selezionare i tag da applicare.

Consulta [Impostazione delle autorizzazioni dei tag](../../help/sites-administering/tags.md#setting-tag-permissions).

Di seguito viene illustrato come viene visualizzato in CRXDE quando un amministratore applica le autorizzazioni di lettura a `/etc/tag/discussions` per il gruppo `Community Engage Members`.

![autorizzazioni tag](assets/tag-permissions.png)
