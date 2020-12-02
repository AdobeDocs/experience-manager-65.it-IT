---
title: Console Badge
seo-title: Console Badge
description: La console dei badge delle community consente di aggiungere dei simboli personalizzati che possono essere visualizzati per i membri al momento della loro acquisizione (assegnazione) o di un ruolo specifico nella comunità (assegnazione)
seo-description: La console dei badge delle community consente di aggiungere dei simboli personalizzati che possono essere visualizzati per i membri al momento della loro acquisizione (assegnazione) o di un ruolo specifico nella comunità (assegnazione)
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
translation-type: tm+mt
source-git-commit: 548e19b0fc76ede8685ea938ed871fbdc8c3858f
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---


# Console Badge {#badges-console}

## Informazioni sui simboli {#about-badges}

La console Community Badges consente di aggiungere distintivi personalizzati che possono essere visualizzati per un membro quando guadagnato (assegnato) o assume un ruolo specifico nella comunità (assegnato).

### Visibilità del badge {#badge-visibility}

Attualmente, i simboli assegnati a un membro della comunità o assegnati a un membro della stessa verranno visualizzati insieme al nome e all&#39;avatar nei seguenti percorsi:

* Profili
* [Forum](/help/communities/forum.md)
* [D/R](/help/communities/working-with-qna.md)
* [Leaderboards](/help/communities/enabling-leaderboard.md)
* [Ideazione](/help/communities/ideation-feature.md)

Nell’ambiente di authoring, passate alla console Badge:

* Dalla navigazione globale: **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Badge]**

In questa console vengono visualizzati i simboli attualmente disponibili e dai quali è possibile aggiungere nuovi simboli.

![badges-homepage](assets/badges-homepage.png)

## Crea badge {#create-badge}

Un contrassegno viene creato caricando un’immagine di dimensioni appropriate (72 dpi con un’altezza compresa tra 26 e 32 pixel) e fornendo un nome. L&#39;immagine del contrassegno viene memorizzata nella directory archivio in `/libs/settings/community/badging/images` e replicata automaticamente nell&#39;ambiente di pubblicazione.

Se l&#39;ambiente di pubblicazione è una farm di editori, è necessario configurare [sincronizzazione utente](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Carica immagine**

   (*Richiesto*) Un&#39;immagine con un contrassegno di 32 x 32 pixel a 72 dpi consigliati in formato JPEG o PNG.

* **Nome**

   (*Obbligatorio*) Il nome del contrassegno. È il nome predefinito `Display Name` e il nome del nodo del repository. Se `Name` non è un nome di nodo del repository valido, verrà modificato.

* **Nome visualizzato**

   (*Facoltativo*) Nome da visualizzare per il contrassegno nell&#39;interfaccia utente. Il valore predefinito è il testo inalterato immesso per il simbolo `Name`.

* **Descrizione**

   (*Facoltativo*) Una descrizione per il contrassegno.

## Informazioni aggiuntive {#additional-information}

Per informazioni dettagliate sulla configurazione delle regole di punteggio e contrassegno, vedere [Punteggio e Badge](/help/communities/implementing-scoring.md).

Per gestire i simboli per i membri, vedere [Console Membri](/help/communities/members.md).
