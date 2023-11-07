---
title: 'Operazioni Granite: amministrazione di utenti e gruppi'
seo-title: Granite Operations - User and Group Administration
description: Scopri l’amministrazione di utenti e gruppi Granite.
seo-description: Learn about Granite user and group administration.
uuid: 7b6b7767-712c-4cc8-8d90-36f26280d6e3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 95ab2e54-0f8d-49e0-ad20-774875f6f80a
exl-id: f3477d21-7e9a-4588-94e8-496bc42434a8
feature: Security
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 5%

---


# Operazioni Granite: amministrazione di utenti e gruppi{#granite-operations-user-and-group-administration}

Poiché Granite incorpora l’implementazione dell’archivio CRX della specifica API JCR, dispone di un’amministrazione autonoma di utenti e gruppi.

Questi conti sono alla base della [Conti AEM](/help/sites-administering/security.md) e le eventuali modifiche apportate all’account con l’amministrazione Granite verranno applicate se/quando gli account sono accessibili da [Console Utenti AEM](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) (ad esempio, `http://localhost:4502/useradmin`). Dalla console Utenti AEM puoi anche gestire i privilegi e altre specifiche AEM.

Le console di amministrazione di utenti e gruppi Granite sono entrambe disponibili dal **[Strumenti](/help/sites-administering/tools-consoles.md)** console dell’interfaccia touch:

![Console Strumenti](assets/chlimage_1-72a.png)

Scelta di **Utenti** o **Gruppi** dalla console Strumenti apre la console appropriata. In entrambi è possibile intervenire utilizzando la casella di selezione e quindi le azioni dalla barra degli strumenti, oppure aprendo i dettagli dell’account tramite il collegamento in **Nome**.

* [Amministrazione utente](#user-administration)

  ![chlimage_1-73](assets/chlimage_1-73a.png)

  Il **Utenti** elenchi console:

   * il nome utente
   * il nome di accesso dell’utente (nome account)
   * qualsiasi titolo assegnato all’account

* [Amministrazione gruppo](#group-administration)

  ![Console di gestione utenti](assets/chlimage_1-74a.png)

  Il **Gruppi** elenchi console:

   * il nome del gruppo
   * la descrizione del gruppo
   * il numero di utenti/gruppi nel gruppo

## Amministrazione utente {#user-administration}

### Aggiunta di un nuovo utente {#adding-a-new-user}

1. Utilizza il **Aggiungi utente** icona:

   ![Icona Aggiungi utente](do-not-localize/chlimage_1-1.png)

1. Il **Crea utente** aperture modulo:

   ![Modulo dettagli utente](assets/chlimage_1-75a.png)

   Qui puoi immettere i dettagli utente per l’account (la maggior parte sono standard e auto-esplicativi):

   * **ID**

     Identificazione univoca dell&#39;account utente. È obbligatorio e non può contenere spazi.

   * **Indirizzo e-mail**
   * **Password**

     La password è obbligatoria.

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
   * **Stato**
   * **Titolo**
   * **Genere**
   * **Informazioni su**
   * **Impostazioni account**

      * **Stato**
Puoi contrassegnare l’account come **attivo** o **inattivo**.

   * **Foto**

     Qui puoi caricare una foto da usare come avatar.

     Tipi di file accettati: `.jpg .png .tif .gif`

     Dimensione preferita: `240x240px`

   * **Aggiungi utente a gruppi**

     Utilizza il menu a discesa di selezione per selezionare i gruppi di cui l’utente deve essere membro. Una volta selezionata, utilizza **X** dal nome da deselezionare prima del salvataggio.

   * **Gruppi**

     Elenco di gruppi di cui l&#39;utente è attualmente membro. Utilizza il **X** dal nome da deselezionare prima del salvataggio.

1. Dopo aver definito l’account utente, utilizza:

   * **Annulla** per interrompere la registrazione.
   * **Salva** per completare la registrazione. La creazione dell’account utente verrà confermata con un messaggio.

### Modifica di un utente esistente {#editing-an-existing-user}

1. Accedi ai dettagli utente dal collegamento posto sotto il nome utente nella console Utenti.

1. Ora puoi modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user).

1. Accedi ai dettagli utente dal collegamento posto sotto il nome utente nella console Utenti.

1. Ora puoi modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user).

### Modifica della password per un utente esistente {#changing-the-password-for-an-existing-user}

1. Accedi ai dettagli utente dal collegamento posto sotto il nome utente nella console Utenti.

1. Ora puoi modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user). Sotto **Impostazioni account** esiste un collegamento per **Cambia password**.

   ![Finestra di dialogo Impostazioni account](assets/chlimage_1-76a.png)

1. Il **Cambia password** viene visualizzata una finestra di dialogo. Immettere e ridigitare la nuova password, insieme alla password. Utilizzare **OK** per confermare le modifiche.

   ![Finestra di dialogo Modifica password](assets/chlimage_1-77a.png)

   Un messaggio conferma che la password è stata cambiata.

### Assegnazione gruppo rapido {#quick-group-assignment}

1. Utilizza la casella di selezione per contrassegnare uno o più utenti.
1. Utilizza il **Gruppi** icona:

   ![Utilizzo dell’icona Gruppi](do-not-localize/chlimage_1-2.png)

   Per aprire il menu a discesa di selezione del gruppo:

   ![Selettore gruppi](assets/chlimage_1-78a.png)

1. Nella casella di selezione è possibile selezionare o deselezionare i gruppi a cui deve appartenere l&#39;account utente.

1. Quando hai assegnato, o non hai assegnato, i gruppi come richiesto, utilizza:

   * **Annulla** per interrompere le modifiche
   * **Salva** per confermare le modifiche

### Eliminazione dei dettagli utente esistenti {#deleting-existing-user-details}

1. Utilizza la casella di selezione per contrassegnare uno o più utenti.
1. Utilizza il **Elimina** icona per eliminare i dettagli utente:

   ![Elimina dettagli utente esistenti](do-not-localize/chlimage_1-3.png)

1. Ti verrà chiesto di confermare l’eliminazione, quindi un messaggio confermerà che l’effettiva eliminazione ha avuto luogo.

## Amministrazione gruppo {#group-administration}

### Aggiunta di un nuovo gruppo {#adding-a-new-group}

1. Utilizza l’icona Aggiungi gruppo:

   ![Aggiungi un nuovo gruppo](do-not-localize/chlimage_1-4.png)

1. Il **Crea gruppo** aperture modulo:

   ![Modulo Dettagli gruppo](assets/chlimage_1-79a.png)

   Qui puoi immettere i dettagli del gruppo:

   * **ID**

     Identificatore univoco del gruppo. Questo è obbligatorio e non può contenere spazi.

   * **Nome**

     Un nome per il gruppo; viene visualizzato nella console Gruppi.

   * **Descrizione**

     Descrizione del gruppo.

   * **Aggiungi membri al gruppo**

     Utilizza il menu a discesa di selezione per selezionare gli utenti da aggiungere al gruppo. Una volta selezionata, utilizza **X** dal nome da deselezionare prima del salvataggio.

   * **Membri del gruppo**

     Elenco di utenti del gruppo. Utilizza il **X** dal nome da deselezionare prima del salvataggio.

1. Dopo aver definito il gruppo, utilizzare:

   * **Annulla** per interrompere la registrazione.
   * **Salva** per completare la registrazione. La creazione del gruppo verrà confermata con un messaggio.

### Modifica di un gruppo esistente {#editing-an-existing-group}

1. Accedi ai dettagli del gruppo dal collegamento posto sotto il nome del gruppo nella console Gruppi.

1. Ora puoi modificare e salvare i dettagli come in [Aggiunta di un nuovo gruppo](#adding-a-new-group).

### Copia di un gruppo esistente {#copying-an-existing-group}

1. Utilizza la casella di selezione per contrassegnare un gruppo.
1. Utilizza il **Copia** icona per copiare i dettagli del gruppo:

   ![Copia un gruppo esistente](do-not-localize/chlimage_1-5.png)

1. Il **Modifica impostazioni gruppo** il modulo verrà aperto.

   L’ID gruppo sarà lo stesso dell’originale, ma con il prefisso `Copy of`. È necessario modificare questa impostazione perché l’ID non può contenere spazi. Tutti gli altri dettagli saranno gli stessi dell&#39;originale.

   Ora puoi modificare e salvare i dettagli come in [Aggiunta di un nuovo gruppo](#adding-a-new-group).

### Eliminazione di un gruppo esistente {#deleting-an-existing-group}

1. Utilizza la casella di selezione per contrassegnare uno o più gruppi.
1. Utilizza il **Elimina** per eliminare i dettagli del gruppo:

   ![Eliminazione di un gruppo esistente](do-not-localize/chlimage_1-6.png)

1. Ti verrà chiesto di confermare l’eliminazione, quindi un messaggio confermerà che l’effettiva eliminazione ha avuto luogo.
