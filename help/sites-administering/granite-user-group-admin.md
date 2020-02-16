---
title: Operazioni Granite - Amministrazione utente e gruppo
seo-title: Operazioni Granite - Amministrazione utente e gruppo
description: Ulteriori informazioni sull'amministrazione di utenti e gruppi Granite.
seo-description: Ulteriori informazioni sull'amministrazione di utenti e gruppi Granite.
uuid: 7b6b7767-712c-4cc8-8d90-36f26280d6e3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 95ab2e54-0f8d-49e0-ad20-774875f6f80a
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2

---


# Operazioni Granite - Amministrazione utente e gruppo{#granite-operations-user-and-group-administration}

Poiché Granite incorpora l&#39;implementazione del repository CRX della specifica API JCR, ha una propria amministrazione utente e di gruppo.

Questi account sono alla base degli account [](/help/sites-administering/security.md) AEM e tutte le modifiche apportate agli account con l&#39;amministrazione Granite si rifletteranno se/quando gli account sono accessibili dalla console [Utenti di](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) AEM (ad esempio `http://localhost:4502/useradmin`). Dalla console Utenti di AEM è inoltre possibile gestire i privilegi e altre specifiche di AEM.

Le console di amministrazione Granite per utenti e gruppi sono disponibili nella console **[Strumenti](/help/sites-administering/tools-consoles.md)**dell’interfaccia touch:

![chlimage_1-72](assets/chlimage_1-72a.png)

Scegliendo **Utenti** o **Gruppi** dalla console Strumenti si aprirà la console appropriata. In entrambi i casi è possibile intervenire utilizzando la casella di controllo e quindi le azioni dalla barra degli strumenti, oppure aprendo i dettagli dell&#39;account tramite il collegamento in **Nome**.

* [Amministrazione utente](#user-administration)

   ![chlimage_1-73](assets/chlimage_1-73a.png)

   Nella console **Utenti** sono elencati i seguenti elementi:

   * il nome utente
   * il nome di login utente (nome account)
   * qualsiasi titolo al quale è stato assegnato il conto

* [Amministrazione gruppo](#group-administration)

   ![chlimage_1-74](assets/chlimage_1-74a.png)

   Nella console **Gruppi** sono elencati i seguenti elementi:

   * il nome del gruppo
   * la descrizione del gruppo
   * il numero di utenti/gruppi nel gruppo

## Amministrazione utente {#user-administration}

### Aggiunta di un nuovo utente {#adding-a-new-user}

1. Utilizzate l&#39;icona **Aggiungi utente** :

   ![](do-not-localize/chlimage_1-1.png)

1. Viene aperto il modulo **Crea utente** :

   ![chlimage_1-75](assets/chlimage_1-75a.png)

   Qui potete inserire i dettagli utente per l&#39;account (la maggior parte sono standard e auto-esplicativi):

   * **ID**

      Si tratta dell&#39;identificazione univoca per l&#39;account utente. È obbligatorio e non può contenere spazi.

   * **Indirizzo e-mail**
   * **Password**

      Una password è obbligatoria.

   * **Ripeti password**

      Questo è obbligatorio in quanto è richiesto per la conferma della password.

   * **Nome**
   * **Cognome**
   * **Numero telefono**
   * **Qualifica**
   * **Via**
   * **Mobile**
   * **Città**
   * **Codice di avviamento postale**
   * **Paese**
   * **Stadio**
   * **Titolo**
   * **Genere**
   * **Informazioni su**
   * **Impostazioni account**

      * **Stato**&#x200B;È possibile contrassegnare l&#39;account come **attivo** o **inattivo**.
   * **Foto**

      Qui puoi caricare una foto da usare come avatar.

      Tipi di file accettati: `.jpg .png .tif .gif`

      Dimensioni preferite: `240x240px`

   * **Aggiungi utente a gruppi**

      Utilizzate l&#39;elenco a discesa di selezione per selezionare i gruppi di cui l&#39;utente deve essere membro. Una volta selezionata questa opzione, utilizzare la **X** con il nome per deselezionare la casella prima di salvare.

   * **Gruppi**

      Elenco di gruppi di cui l&#39;utente è attualmente membro. Per deselezionare la **X** in base al nome, prima di salvare.


1. Una volta definito l&#39;account utente, utilizzate:

   * **Annulla** per interrompere la registrazione.
   * **Salva** per completare la registrazione. La creazione dell&#39;account utente verrà confermata con un messaggio.

### Modifica di un utente esistente {#editing-an-existing-user}

1. Accedete ai dettagli utente dal collegamento situato sotto il nome utente nella console Utenti.

1. Ora potete modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user).

1. Accedete ai dettagli utente dal collegamento situato sotto il nome utente nella console Utenti.

1. Ora potete modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user).

### Modifica della password per un utente esistente {#changing-the-password-for-an-existing-user}

1. Accedete ai dettagli utente dal collegamento situato sotto il nome utente nella console Utenti.

1. Ora potete modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user). In Impostazioni **** account è presente un collegamento per **cambiare la password**.

   ![chlimage_1-76](assets/chlimage_1-76a.png)

1. Viene visualizzata la finestra di dialogo **Cambia password** . Immettete e digitate nuovamente la nuova password, insieme alla password. Utilizzare **OK** per confermare le modifiche.

   ![chlimage_1-77](assets/chlimage_1-77a.png)

   Viene visualizzato un messaggio di conferma della modifica della password.

### Assegnazione gruppo rapido {#quick-group-assignment}

1. Usate la casella di controllo per contrassegnare uno o più utenti.
1. Use the **Groups** icon:

   ![](do-not-localize/chlimage_1-2.png)

   Per aprire il menu a discesa di selezione del gruppo:

   ![chlimage_1-78](assets/chlimage_1-78a.png)

1. Nella casella di selezione potete selezionare o deselezionare i gruppi a cui appartiene l&#39;account utente.

1. Quando avete assegnato o meno i gruppi, come necessario, utilizzate:

   * **Annulla** per interrompere le modifiche
   * **Salva** per confermare le modifiche

### Eliminazione dei dettagli utente esistenti {#deleting-existing-user-details}

1. Usate la casella di controllo per contrassegnare uno o più utenti.
1. Usate l’icona **Elimina** per eliminare i dettagli utente:

   ![](do-not-localize/chlimage_1-3.png)

1. Vi verrà chiesto di confermare l&#39;eliminazione, quindi un messaggio confermerà che l&#39;eliminazione effettiva è avvenuta.

## Amministrazione gruppo {#group-administration}

### Aggiunta di un nuovo gruppo {#adding-a-new-group}

1. Utilizzate l’icona Aggiungi gruppo:

   ![](do-not-localize/chlimage_1-4.png)

1. Viene aperto il modulo **Crea gruppo** :

   ![chlimage_1-79](assets/chlimage_1-79a.png)

   Qui potete inserire i dettagli del gruppo:

   * **ID**

      Identificatore univoco per il gruppo. Questo è obbligatorio e non può contenere spazi.

   * **Nome**

      Un nome per il gruppo; verrà visualizzata nella console Gruppi.

   * **Descrizione**

       Descrizione del gruppo.

   * **Aggiungi membri al gruppo**

      Utilizzate il menu a discesa di selezione per selezionare gli utenti da aggiungere al gruppo. Una volta selezionata questa opzione, utilizzare la **X** con il nome per deselezionare la casella prima di salvare.

   * **Membri del gruppo**

      Elenco di utenti nel gruppo. Per deselezionare la **X** in base al nome, prima di salvare.

1. Una volta definito il gruppo, utilizzate:

   * **Annulla** per interrompere la registrazione.
   * **Salva** per completare la registrazione. La creazione del gruppo verrà confermata con un messaggio.

### Modifica di un gruppo esistente {#editing-an-existing-group}

1. Accedete ai dettagli del gruppo dal collegamento situato sotto il nome del gruppo nella console Gruppi.

1. Ora potete modificare e salvare i dettagli come in [Aggiunta di un nuovo gruppo](#adding-a-new-group).

### Copia di un gruppo esistente {#copying-an-existing-group}

1. Usate la casella di controllo per contrassegnare un gruppo.
1. Usate l’icona **Copia** per copiare i dettagli del gruppo:

   ![](do-not-localize/chlimage_1-5.png)

1. Viene aperto il modulo **Edit Group Settings (Modifica impostazioni** gruppo).

   L&#39;ID gruppo sarà uguale all&#39;ID originale, ma con il prefisso `Copy of`. È necessario modificarlo perché l’ID non può contenere spazi. Tutti gli altri dettagli saranno uguali all&#39;originale.

   Ora potete modificare e salvare i dettagli come in [Aggiunta di un nuovo gruppo](#adding-a-new-group).

### Eliminazione di un gruppo esistente {#deleting-an-existing-group}

1. Usate la casella di controllo per contrassegnare uno o più gruppi.
1. Usate l’icona **Elimina** per eliminare i dettagli del gruppo:

   ![](do-not-localize/chlimage_1-6.png)

1. Vi verrà chiesto di confermare l&#39;eliminazione, quindi un messaggio confermerà che l&#39;eliminazione effettiva è avvenuta.

