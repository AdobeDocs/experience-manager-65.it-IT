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

Sovrapponi il sistema di commenti con una versione personalizzata copiando il numero minimo di file necessari da `/libs` in `/apps` e modificandoli in `/apps`.

>[!CAUTION]
>
>Il contenuto della cartella /libs non viene mai modificato perché eventuali reinstallazioni o aggiornamenti potrebbero eliminare o sostituire la cartella /libs mentre il contenuto della cartella /apps viene lasciato invariato.

Se si utilizza [CRXDE Liti](../../help/sites-developing/developing-with-crxde-lite.md) in un&#39;istanza Autore, iniziare creando un percorso nella cartella /apps identico al percorso dei componenti sovrapposti nella cartella /libs.

Il percorso da duplicare è:

* `/libs/social/commons/components/hbs/comments/comment`

Alcuni nodi nel percorso sono cartelle e altri componenti.

1. Passa a [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Crea `/apps/social` (se non esiste già)
   * Seleziona nodo `/apps`
   * **[!UICONTROL Crea > Cartella]**
      * Immettere il nome: `social`
1. Seleziona nodo `social`
   * **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**
      * Immettere il nome: `commons`
1. Seleziona nodo `commons`
   * **[!UICONTROL Crea > Cartella]**
      * Immettere il nome: `components`
1. Seleziona nodo `components`
   * **[!UICONTROL Crea > Cartella]**.
      * Immettere il nome: `hbs`
1. Seleziona nodo `hbs`
   * **[!UICONTROL Crea]** > **[!UICONTROL Crea componente]**
      * Immetti etichetta: `comments`
      * Immetti titolo: `Comments`
      * Immetti la descrizione: `List of comments without showing avatars`
      * Super Type: `social/commons/components/comments`
      * Immetti gruppo: `Communities`
      * Fai clic su **[!UICONTROL Avanti]** fino a **[!UICONTROL OK]**
1. Seleziona nodo `comments`

   * **[!UICONTROL Crea]** > **[!UICONTROL Crea componente]**

      * Immetti etichetta: `comment`
      * Immetti titolo: `Comment`
      * Immetti la descrizione: `A comment instance without avatars`
      * Super Type: `social/commons/components/comments/comment`
      * Immetti gruppo: `.hidden`
      * Fai clic su **[!UICONTROL Avanti]** fino a **[!UICONTROL OK]**
   * Seleziona **[!UICONTROL Salva tutto]**
1. Elimina `comments.jsp` predefinito
   * Seleziona nodo `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Seleziona **[!UICONTROL Elimina]**
1. Elimina il commento predefinito.jsp
   * seleziona nodo `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Seleziona **[!UICONTROL Elimina]**
   * Seleziona **[!UICONTROL Salva tutto]**

>[!NOTE]
>
>Per mantenere la catena di ereditarietà, `Super Type` (proprietà `sling:resourceSuperType`) dei componenti di sovrapposizione sono impostati sullo stesso valore di `Super Type` dei componenti sovrapposti, in questo caso:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

`Type` (proprietà `sling:resourceType`) della sovrapposizione deve essere un riferimento autonomo relativo in modo che qualsiasi contenuto non trovato in /apps venga quindi cercato in /libs.
* Nome: `sling:resourceType`
* Tipo: `String`
* Valore: `social/commons/components/hbs/comments`

1. Seleziona `[+] Add` verde
   * Nome: `sling:resourceType`
   * Tipo: `String`
   * Valore: `social/commons/components/hbs/comments/comment`
1. Seleziona `[+] Add` verde
   * Seleziona **[!UICONTROL Salva tutto]**

![create-nodes](assets/create-nodes.png)
