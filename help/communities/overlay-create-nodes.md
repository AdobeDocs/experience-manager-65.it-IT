---
title: Crea nodi
description: Scopri come sovrapporre il sistema di commenti con una versione personalizzata copiando il numero minimo di file necessari da /libs e modificandoli in /apps.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Crea nodi {#create-nodes}

Sovrapponi il sistema di commenti con una versione personalizzata copiando il numero minimo di file necessari da `/libs` in `/apps` e modificarli in `/apps`.

>[!CAUTION]
>
>Il contenuto della cartella /libs non viene mai modificato perché eventuali reinstallazioni o aggiornamenti potrebbero eliminare o sostituire la cartella /libs mentre il contenuto della cartella /apps viene lasciato invariato.

Utilizzo di [CRXDE Liti](../../help/sites-developing/developing-with-crxde-lite.md) in un’istanza Autore, inizia creando un percorso nella cartella /apps identico al percorso dei componenti sovrapposti nella cartella /libs.

Il percorso da duplicare è:

* `/libs/social/commons/components/hbs/comments/comment`

Alcuni nodi nel percorso sono cartelle e altri componenti.

1. Sfoglia per [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Crea `/apps/social` (se non esiste già)
   * Seleziona `/apps` nodo
   * **[!UICONTROL Crea > Cartella]**
      * Inserisci il nome: `social`
1. Seleziona `social` nodo
   * **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**
      * Inserisci il nome: `commons`
1. Seleziona `commons` nodo
   * **[!UICONTROL Crea > Cartella]**
      * Inserisci il nome: `components`
1. Seleziona `components` nodo
   * **[!UICONTROL Crea > Cartella]**.
      * Inserisci il nome: `hbs`
1. Seleziona `hbs` nodo
   * **[!UICONTROL Crea]** > **[!UICONTROL Crea componente]**
      * Immetti etichetta: `comments`
      * Inserisci il titolo: `Comments`
      * Immetti la descrizione: `List of comments without showing avatars`
      * Super Type: `social/commons/components/comments`
      * Immetti gruppo: `Communities`
      * Clic **[!UICONTROL Successivo]** fino a **[!UICONTROL OK]**
1. Seleziona `comments` nodo

   * **[!UICONTROL Crea]** > **[!UICONTROL Crea componente]**

      * Immetti etichetta: `comment`
      * Inserisci il titolo: `Comment`
      * Immetti la descrizione: `A comment instance without avatars`
      * Super Type: `social/commons/components/comments/comment`
      * Immetti gruppo: `.hidden`
      * Clic **[!UICONTROL Successivo]** fino a **[!UICONTROL OK]**
   * Seleziona **[!UICONTROL Salva tutto]**
1. Elimina il valore predefinito `comments.jsp`
   * Seleziona nodo `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Seleziona **[!UICONTROL Elimina]**
1. Elimina il commento predefinito.jsp
   * seleziona nodo `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Seleziona **[!UICONTROL Elimina]**
   * Seleziona **[!UICONTROL Salva tutto]**

>[!NOTE]
>
>Per mantenere la catena di ereditarietà, `Super Type` (proprietà `sling:resourceSuperType`) dei componenti di sovrapposizione sono impostati sullo stesso valore della `Super Type` dei componenti sovrapposti, in questo caso:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

La sovrapposizione è propria `Type`(proprietà `sling:resourceType`) deve essere un riferimento autonomo relativo in modo che qualsiasi contenuto non trovato in /apps venga quindi cercato in /libs.
* Nome: `sling:resourceType`
* Tipo: `String`
* Valore: `social/commons/components/hbs/comments`

1. Seleziona il verde `[+] Add`
   * Nome: `sling:resourceType`
   * Tipo: `String`
   * Valore: `social/commons/components/hbs/comments/comment`
1. Seleziona il verde `[+] Add`
   * Seleziona **[!UICONTROL Salva tutto]**

![create-nodes](assets/create-nodes.png)
