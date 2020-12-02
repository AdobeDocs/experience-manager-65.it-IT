---
title: Crea nodi
seo-title: Crea nodi
description: Sovrapporre il sistema dei commenti
seo-description: Sovrapporre il sistema dei commenti
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 8%

---


# Crea nodi {#create-nodes}

Sovrapponete il sistema dei commenti a una versione personalizzata copiando il numero minimo di file necessari da `/libs` a `/apps` e modificandoli in `/apps`.

>[!CAUTION]
>
>Il contenuto della cartella /libs non viene mai modificato perché qualsiasi reinstallazione o aggiornamento potrebbe eliminare o sostituire la cartella /libs mentre il contenuto della cartella /apps non viene toccato.

L&#39;utilizzo di [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) in un&#39;istanza di creazione inizia dalla creazione di un percorso nella cartella /apps identico al percorso dei componenti sovrapposti nella cartella /libs.

Il percorso da duplicare è:

* `/libs/social/commons/components/hbs/comments/comment`

Alcuni nodi del percorso sono cartelle e alcuni sono componenti.

1. Passa a [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Crea `/apps/social` (se non esiste già)
   * Selezionare il nodo `/apps`
   * **[!UICONTROL Crea > Cartella...]**
      * Inserisci il nome: `social`
1. Selezionare il nodo `social`
   * **[!UICONTROL Crea]**  >  **[!UICONTROL Cartella...]**
      * Inserisci il nome: `commons`
1. Selezionare il nodo `commons`
   * **[!UICONTROL Crea > Cartella...]**
      * Inserisci il nome: `components`
1. Selezionare il nodo `components`
   * **[!UICONTROL Crea > Cartella..]**.
      * Inserisci il nome: `hbs`
1. Selezionare il nodo `hbs`
   * **[!UICONTROL Crea]**  >  **[!UICONTROL Crea componente...]**
      * Inserisci etichetta: `comments`
      * Immetti titolo: `Comments`
      * Inserire Descrizione: `List of comments without showing avatars`
      * Super Type: `social/commons/components/comments`
      * Inserisci gruppo: `Communities`
      * Fare clic su **[!UICONTROL Next]** fino a **[!UICONTROL OK]**
1. Selezionare il nodo `comments`

   * **[!UICONTROL Crea]**  >  **[!UICONTROL Crea componente...]**

      * Inserisci etichetta: `comment`
      * Immetti titolo: `Comment`
      * Inserire Descrizione: `A comment instance without avatars`
      * Super Type: `social/commons/components/comments/comment`
      * Inserisci gruppo: `.hidden`
      * Fare clic su **[!UICONTROL Next]** fino a **[!UICONTROL OK]**
   * Selezionare **[!UICONTROL Salva tutto]**
1. Elimina il valore predefinito `comments.jsp`
   * Selezionare il nodo `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Selezionare **[!UICONTROL Elimina]**
1. Elimina il commento predefinito.jsp
   * select node `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Selezionare **[!UICONTROL Elimina]**
   * Selezionare **[!UICONTROL Salva tutto]**

>[!NOTE]
>
>Per mantenere la catena di ereditarietà, la `Super Type` (proprietà `sling:resourceSuperType`) dei componenti della sovrapposizione è impostata sullo stesso valore della `Super Type` dei componenti sovrapposti, in questo caso:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


La proprietà `Type`(proprietà `sling:resourceType`) della sovrapposizione deve essere un riferimento autonomo relativo, in modo che qualsiasi contenuto non trovato in /apps venga ricercato in /libs.
* Nome: `sling:resourceType`
* Tipo: `String`
* Valore: `social/commons/components/hbs/comments`

1. Selezionare il verde `[+] Add`
   * Nome: `sling:resourceType`
   * Tipo: `String`
   * Valore: `social/commons/components/hbs/comments/comment`
1. Selezionare il verde `[+] Add`
   * Selezionare **[!UICONTROL Salva tutto]**

![create-nodes](assets/create-nodes.png)

