---
title: Console badge
description: La console Badge community consente di aggiungere distintivi personalizzati che possono essere visualizzati dai membri quando ricevono (assegnati) o quando assumono un ruolo specifico nella community (assegnati)
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 4%

---

# Console badge {#badges-console}

## Informazioni sui badge {#about-badges}

La console Distintivi community consente di aggiungere distintivi personalizzati che possono essere visualizzati per un membro quando guadagnato (assegnato) o quando assume un ruolo specifico nella community (assegnato).

### Visibilità badge {#badge-visibility}

Attualmente, i badge che un membro della community ottiene, o a cui viene assegnato, vengono visualizzati insieme al nome e all’avatar nelle seguenti posizioni:

* Profili
* [Forum](/help/communities/forum.md)
* [D/R](/help/communities/working-with-qna.md)
* [Classifiche](/help/communities/enabling-leaderboard.md)
* [Ideazione](/help/communities/ideation-feature.md)

Nell’ambiente di authoring, accedi alla console Badge:

* Dalla navigazione globale: **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Distintivi]**

Questa console mostra i badge attualmente disponibili e da cui è possibile aggiungere nuovi badge.

![badges-homepage](assets/badges-homepage.png)

## Crea badge {#create-badge}

Un badge viene creato caricando un’immagine sufficientemente piccola (72 dpi, con un’altezza compresa tra 26 e 32 pixel) e fornendo un nome. L’immagine del badge viene memorizzata nell’archivio in `/libs/settings/community/badging/images` e viene replicato automaticamente nell’ambiente di pubblicazione.

Se l’ambiente di pubblicazione è una farm di editori, è necessario configurare [sincronizzazione utenti](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Carica immagine**

  (*Obbligatorio* a) Immagine badge con dimensioni consigliate di 32 x 32 pixel a 72 dpi in formato JPEG o PNG.

* **Nome**

  (*Obbligatorio*) Il nome del badge. È l&#39;impostazione predefinita `Display Name` e il nome del nodo dell’archivio. Se il `Name` non è un nome di nodo di archivio valido, è stato modificato.

* **Nome visualizzato**

  (*Facoltativo*) Nome da visualizzare per il badge nell’interfaccia utente. Il valore predefinito è il testo non modificato immesso per `Name`.

* **Descrizione**

  (*Facoltativo*) Descrizione del badge.

## Informazioni aggiuntive {#additional-information}

Per informazioni dettagliate sull’impostazione delle regole di punteggio e badge, consulta [Punteggio e distintivi](/help/communities/implementing-scoring.md).

Per gestire i badge per i membri, consulta [Console Membri](/help/communities/members.md).
