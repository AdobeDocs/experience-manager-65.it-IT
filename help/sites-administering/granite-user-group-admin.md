---
title: Operazioni Granite - Amministrazione di utenti e gruppi
seo-title: Operazioni Granite - Amministrazione di utenti e gruppi
description: Scopri l’amministrazione di utenti e gruppi Granite.
seo-description: Scopri l’amministrazione di utenti e gruppi Granite.
uuid: 7b6b7767-712c-4cc8-8d90-36f26280d6e3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 95ab2e54-0f8d-49e0-ad20-774875f6f80a
exl-id: f3477d21-7e9a-4588-94e8-496bc42434a8
feature: Sicurezza
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 5%

---

# Operazioni Granite - Amministrazione di utenti e gruppi{#granite-operations-user-and-group-administration}

Poiché Granite incorpora l&#39;implementazione CRX Repository della specifica API JCR, dispone di una propria amministrazione di utenti e gruppi.

Questi account sono la base sottostante degli account [AEM](/help/sites-administering/security.md) e tutte le modifiche apportate all&#39;account con l&#39;amministrazione Granite verranno applicate se/quando gli account sono accessibili dalla [console Utenti AEM](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) (ad esempio `http://localhost:4502/useradmin`). Dalla console Utenti AEM puoi anche gestire i privilegi e altre specifiche AEM.

Le console di amministrazione di utenti e gruppi Granite sono disponibili nella console **[Strumenti](/help/sites-administering/tools-consoles.md)** dell’interfaccia touch:

![chlimage_1-72](assets/chlimage_1-72a.png)

Se si sceglie **Utenti** o **Gruppi** dalla console Strumenti, verrà aperta la console appropriata. In entrambi i casi puoi intervenire utilizzando la casella di selezione e quindi le azioni dalla barra degli strumenti, oppure aprendo i dettagli dell’account tramite il collegamento in **Nome**.

* [Amministrazione utente](#user-administration)

   ![chlimage_1-73](assets/chlimage_1-73a.png)

   La console **Utenti** elenca:

   * nome utente
   * nome di accesso utente (nome account)
   * qualsiasi titolo assegnato al conto

* [Amministrazione dei gruppi](#group-administration)

   ![chlimage_1-74](assets/chlimage_1-74a.png)

   La console **Gruppi** elenca:

   * il nome del gruppo
   * la descrizione del gruppo
   * il numero di utenti/gruppi nel gruppo

## Amministrazione utente {#user-administration}

### Aggiunta di un nuovo utente {#adding-a-new-user}

1. Utilizza l&#39;icona **Aggiungi utente**:

   ![](do-not-localize/chlimage_1-1.png)

1. Viene aperto il modulo **Crea utente** :

   ![chlimage_1-75](assets/chlimage_1-75a.png)

   Qui puoi inserire i dettagli utente dell’account (la maggior parte sono standard e esplicativi):

   * **ID**

      Questa è l&#39;identificazione univoca per l&#39;account utente. È obbligatorio e non può contenere spazi.

   * **Indirizzo e-mail**
   * **Password**

      Una password è obbligatoria.

   * **Ripeti password**

      Questo è obbligatorio in quanto è necessario per la conferma della password.

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

      * ****
StatoÈ possibile contrassegnare l’account come 
**** attiva o  **inattiva**.
   * **Foto**

      Qui puoi caricare una foto da usare come avatar.

      Tipi di file accettati: `.jpg .png .tif .gif`

      Dimensione preferita: `240x240px`

   * **Aggiungi utente a gruppi**

      Utilizza il menu a discesa di selezione per selezionare i gruppi di cui l’utente deve essere membro. Una volta selezionato, utilizza il nome **X** per deselezionare prima di salvare.

   * **Gruppi**

      Elenco dei gruppi di cui l&#39;utente è attualmente membro. Usa il nome **X** per deselezionare prima di salvare.


1. Quando hai definito l&#39;account utente, utilizza:

   * **** Annulla per interrompere la registrazione.
   * **** Salva per completare la registrazione. La creazione dell’account utente verrà confermata con un messaggio.

### Modifica di un utente esistente {#editing-an-existing-user}

1. Accedi ai dettagli utente dal collegamento sotto il nome utente nella console Utenti.

1. È ora possibile modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user).

1. Accedi ai dettagli utente dal collegamento sotto il nome utente nella console Utenti.

1. È ora possibile modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user).

### Modifica della password per un utente esistente {#changing-the-password-for-an-existing-user}

1. Accedi ai dettagli utente dal collegamento sotto il nome utente nella console Utenti.

1. È ora possibile modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user). Alla voce **Impostazioni account** è presente un collegamento per **Cambia password**.

   ![chlimage_1-76](assets/chlimage_1-76a.png)

1. Viene aperta la finestra di dialogo **Cambia password** . Immetti e digita nuovamente la nuova password insieme alla tua password. Utilizza **OK** per confermare le modifiche.

   ![chlimage_1-77](assets/chlimage_1-77a.png)

   Viene visualizzato un messaggio di conferma della modifica della password.

### Assegnazione gruppo rapido {#quick-group-assignment}

1. Utilizza la casella di controllo per contrassegnare uno o più utenti.
1. Utilizza l&#39;icona **Gruppi**:

   ![](do-not-localize/chlimage_1-2.png)

   Per aprire il menu a discesa di selezione del gruppo:

   ![chlimage_1-78](assets/chlimage_1-78a.png)

1. Nella casella di selezione puoi selezionare o deselezionare i gruppi a cui deve appartenere l’account utente.

1. Quando hai assegnato o non assegnato, i gruppi vengono utilizzati come richiesto:

   * **** Annulla per interrompere le modifiche
   * **** Salva per confermare le modifiche

### Eliminazione dei dettagli utente esistenti {#deleting-existing-user-details}

1. Utilizza la casella di controllo per contrassegnare uno o più utenti.
1. Utilizza l&#39;icona **Elimina** per eliminare i dettagli utente:

   ![](do-not-localize/chlimage_1-3.png)

1. Ti verrà chiesto di confermare l’eliminazione, quindi un messaggio confermerà che l’eliminazione effettiva è avvenuta.

## Amministrazione dei gruppi {#group-administration}

### Aggiunta di un nuovo gruppo {#adding-a-new-group}

1. Utilizzate l’icona Aggiungi gruppo :

   ![](do-not-localize/chlimage_1-4.png)

1. Viene aperto il modulo **Crea gruppo** :

   ![chlimage_1-79](assets/chlimage_1-79a.png)

   Qui puoi inserire i dettagli del gruppo:

   * **ID**

      Identificatore univoco del gruppo. Questo è obbligatorio e non può contenere spazi.

   * **Nome**

      Nome del gruppo; viene visualizzato nella console Gruppi .

   * **Descrizione**

      Descrizione del gruppo.

   * **Aggiungi membri al gruppo**

      Utilizza il menu a discesa di selezione per selezionare gli utenti da aggiungere al gruppo. Una volta selezionato, utilizza il nome **X** per deselezionare prima di salvare.

   * **Membri del gruppo**

      Elenco di utenti nel gruppo. Usa il nome **X** per deselezionare prima di salvare.

1. Una volta definito il gruppo, utilizza:

   * **** Annulla per interrompere la registrazione.
   * **** Salva per completare la registrazione. La creazione del gruppo verrà confermata con un messaggio.

### Modifica di un gruppo esistente {#editing-an-existing-group}

1. Accedi ai dettagli del gruppo dal collegamento sotto il nome del gruppo nella console Gruppi.

1. Ora puoi modificare e salvare i dettagli come in [Aggiunta di un nuovo gruppo](#adding-a-new-group).

### Copia di un gruppo esistente {#copying-an-existing-group}

1. Utilizza la casella di controllo per contrassegnare un gruppo.
1. Utilizza l&#39;icona **Copia** per copiare i dettagli del gruppo:

   ![](do-not-localize/chlimage_1-5.png)

1. Verrà aperto il modulo **Modifica impostazioni gruppo** .

   L&#39;ID gruppo sarà lo stesso dell&#39;originale, ma con il prefisso `Copy of`. È necessario modificarlo in quanto l’ID non può contenere spazi. Tutti gli altri dettagli saranno uguali all&#39;originale.

   Ora puoi modificare e salvare i dettagli come in [Aggiunta di un nuovo gruppo](#adding-a-new-group).

### Eliminazione di un gruppo esistente {#deleting-an-existing-group}

1. Utilizza la casella di controllo per contrassegnare uno o più gruppi.
1. Utilizza l&#39;icona **Elimina** per eliminare i dettagli del gruppo:

   ![](do-not-localize/chlimage_1-6.png)

1. Ti verrà chiesto di confermare l’eliminazione, quindi un messaggio confermerà che l’eliminazione effettiva è avvenuta.
