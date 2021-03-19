---
title: Console dei badge
seo-title: Console dei badge
description: La console dei badge per le comunità consente di aggiungere badge personalizzati che possono essere visualizzati per i membri guadagnati (assegnati) o quando assumono un ruolo specifico nella comunità (assegnati)
seo-description: La console dei badge per le comunità consente di aggiungere badge personalizzati che possono essere visualizzati per i membri guadagnati (assegnati) o quando assumono un ruolo specifico nella comunità (assegnati)
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 4%

---


# Console Badge {#badges-console}

## Informazioni sui badge {#about-badges}

La console dei badge per le comunità consente di aggiungere badge personalizzati che possono essere visualizzati per un membro al momento della maturazione (assegnazione) o quando assume un ruolo specifico nella comunità (assegnazione).

### Visibilità del badge {#badge-visibility}

Attualmente, i badge che un membro della community guadagna o è assegnato verranno visualizzati insieme al suo nome e al suo avatar nelle seguenti posizioni:

* Profili
* [Forum](/help/communities/forum.md)
* [D/R](/help/communities/working-with-qna.md)
* [Leadership](/help/communities/enabling-leaderboard.md)
* [Ideazione](/help/communities/ideation-feature.md)

Nell’ambiente di authoring, passa alla console Badge :

* Dalla navigazione globale: **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Badge]**

In questa console vengono visualizzati i badge attualmente disponibili e da cui è possibile aggiungere nuovi badge.

![badges-homepage](assets/badges-homepage.png)

## Crea badge {#create-badge}

Un badge viene creato caricando un’immagine di dimensioni adeguate (72 dpi con un’altezza compresa tra 26 e 32 pixel) e specificando un nome. L’immagine del badge viene memorizzata nell’archivio in `/libs/settings/community/badging/images` e replicata automaticamente nell’ambiente di pubblicazione.

Se l&#39;ambiente di pubblicazione è una farm di editori, è necessario configurare [la sincronizzazione utente](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Carica immagine**

   (*Obbligatorio*) Un&#39;immagine di badge con dimensioni consigliate di 32 x 32 pixel a 72 dpi in formato JPEG o PNG.

* **Nome**

   (*Obbligatorio*) Il nome del badge. È il nome predefinito `Display Name` e il nome del nodo del repository. Se il `Name` non è un nome di nodo di archivio valido, verrà modificato.

* **Nome visualizzato**

   (*Facoltativo*) Nome da visualizzare per il badge nell&#39;interfaccia utente. Il valore predefinito è il testo non alterato immesso per `Name`.

* **Descrizione**

   (*Facoltativo*) Una descrizione del badge.

## Informazioni aggiuntive {#additional-information}

Per informazioni dettagliate sull’impostazione delle regole di punteggio e contrassegno, consulta [Punteggio e badge](/help/communities/implementing-scoring.md).

Per la gestione dei badge per i membri, vedere [Console membri](/help/communities/members.md).
