---
title: Creazione e configurazione di gruppi
seo-title: Creating and configuring groups
description: Scopri come creare gruppi manualmente o dinamicamente, modificare un gruppo, visualizzare i dettagli relativi a un gruppo o eliminare un gruppo.
seo-description: Learn how to create groups manually or dynamically, edit a group, view details about a group, or delete a group.
uuid: 8532d72b-270a-4fcf-b7a5-56fca979a5fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2058b501-65ce-4ad3-8e1b-b2eab896f70f
exl-id: 72edd8d1-8573-4942-8ced-1a100af58d78
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# Creazione e configurazione di gruppi{#creating-and-configuring-groups}

La creazione di gruppi di utenti consente di assegnare ruoli al gruppo anziché a singoli utenti.

Sono disponibili due diversi tipi di gruppi. Puoi creare manualmente un gruppo e aggiungervi utenti e altri gruppi. È inoltre possibile creare gruppi dinamici che includono automaticamente tutti gli utenti che soddisfano un set specifico di regole.

Gli utenti possono riscontrare un tempo di risposta più lento se appartengono a molti gruppi (ad esempio, 500 o più) o se i gruppi sono profondamente nidificati (ad esempio, 30 livelli). Se si verifica questo problema, è possibile configurare AEM moduli per preacquisire informazioni da determinati domini. (Vedi [Configurare AEM moduli per la preacquisizione delle informazioni di dominio](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information).)

## Creare manualmente un gruppo {#create-a-group-manually}

Quando crei manualmente un gruppo, puoi aggiungergli utenti e altri gruppi e assegnare ruoli al gruppo. È inoltre possibile associare il gruppo a un gruppo principale.

Se utilizzi Content Services (obsoleto), puoi selezionare l’opzione Seleziona questa opzione per inviare utenti e gruppi in provider di archiviazione principale esterni registrati nella pagina Gestione dominio per inviare in push le informazioni per i nuovi utenti o gruppi creati in Content Services (obsoleto).

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi, quindi fai clic su Nuovo gruppo.
1. Completare la sezione Impostazioni generali e fare clic su Avanti. Nome canonico e Nome gruppo sono attributi obbligatori.

   Il Nome canonico è un identificatore univoco per il gruppo. Ogni gruppo e utente in un dominio deve avere un nome canonico univoco. Selezionare la casella di controllo System Generated (Generazione sistema) per consentire a User Management di assegnare un valore univoco oppure deselezionare la casella di controllo e specificare un valore personalizzato per il Canonical Name (Nome canonico).

   Evita di utilizzare caratteri di sottolineatura (_) nei nomi canonici, ad esempio `sample_group`. Quando cerchi gruppi basati sul loro nome canonico, quelli contenenti caratteri di sottolineatura non vengono restituiti.

1. Per aggiungere utenti e gruppi a questo nuovo gruppo, fare clic su Trova utenti/gruppi ed effettuare le seguenti operazioni:

   * Nella casella Trova digitare i criteri di ricerca.
   * Nell’elenco In, selezionare Utenti, Gruppi o Utenti e gruppi.
   * Nell’elenco Uso, selezionare Nome, E-mail o ID utente.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare e fare clic su Trova.
   * Nei risultati della ricerca, selezionare le caselle di controllo relative agli utenti e ai gruppi da aggiungere a questo nuovo gruppo e fare clic su OK.

1. Fai clic su Avanti.
1. Per aggiungere il nuovo gruppo ad altri gruppi esistenti, fare clic su Trova gruppi ed eseguire le operazioni seguenti:

   * Nella casella Trova digitare i criteri di ricerca.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare e fare clic su Trova.
   * Nei risultati della ricerca, selezionare le caselle di controllo relative ai gruppi a cui appartiene il nuovo gruppo e fare clic su OK.

1. Fai clic su Avanti.
1. Per assegnare ruoli al gruppo, fare clic su Trova ruoli, selezionare le caselle di controllo relative a ciascun ruolo da assegnare al gruppo e fare clic su OK. Gli utenti del gruppo ereditano i ruoli assegnati a livello di gruppo.
1. Fare clic su Fine.

## Creare un gruppo dinamico {#create-a-dynamic-group}

In un gruppo dinamico, non selezioni singolarmente gli utenti che appartengono al gruppo. Al contrario, si specifica un set di regole e tutti gli utenti che soddisfano tali regole vengono aggiunti automaticamente al gruppo dinamico.

Utilizzare uno dei due modi seguenti per creare gruppi dinamici:

* Abilita la creazione automatica di gruppi dinamici basati sui domini e-mail, ad esempio @adobe.com. Quando si attiva questa funzione, Gestione utente crea un gruppo dinamico per ogni dominio e-mail univoco nel database dei moduli di AEM. Utilizza un’espressione cron per specificare la frequenza con cui User Management cerca nel database dei moduli AEM i nuovi domini e-mail. Questi gruppi dinamici vengono aggiunti al dominio locale DefaultDom e si chiamano &quot;Tutti gli utenti con un *`[email domain]`* ID posta.&quot;
* Crea un gruppo dinamico in base a criteri specifici, compresi il dominio e-mail, la descrizione, il nome canonico e il nome di dominio dell’utente. Per appartenere al gruppo dinamico, un utente deve soddisfare tutti i criteri specificati. Per impostare una condizione &quot;o&quot;, crea due gruppi dinamici separati e aggiungili a un gruppo locale. Ad esempio, utilizza questo approccio per creare un gruppo di utenti che appartengono al dominio e-mail @adobe.com o il cui nome canonico contiene ou=adobe.com. Tuttavia, gli utenti non devono necessariamente soddisfare entrambe le condizioni.

Un gruppo dinamico contiene solo utenti. Non può contenere altri gruppi. Tuttavia, un gruppo dinamico può appartenere a un gruppo padre.

### Crea automaticamente gruppi dinamici in base ai domini di posta elettronica {#automatically-create-dynamic-groups-based-on-email-domains}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati.
1. In Creazione automatica del gruppo dinamico, selezionare la casella di controllo.
1. Specifica quando User Manager controlla i nuovi domini e-mail. Questa ora deve essere successiva al tempo di sincronizzazione del dominio, perché la creazione di gruppi dinamici è logica solo se la sincronizzazione del dominio è completata.

   * Per abilitare la sincronizzazione automatica su base giornaliera, digitare l&#39;ora nel formato 24 ore nella casella Generato giornaliero a. Quando salvi le impostazioni, questo valore viene convertito in un’espressione cron, visualizzata nella casella seguente.
   * Per pianificare la sincronizzazione in un giorno specifico della settimana o del mese o in un mese particolare, selezionare il tipo di espressione cron appropriato nella casella. Il valore predefinito è `0 00 4 ? * *`(che significa controllare alle 4 del mattino ogni giorno).

      L&#39;utilizzo dell&#39;espressione cron si basa sul sistema di programmazione dei processi open source Quartz, versione 1.4.0.

1. Fai clic su Salva.

### Creare un gruppo dinamico in base a criteri specifici {#create-a-dynamic-group-based-on-specified-criteria}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Fare clic su Nuovo gruppo dinamico.
1. Completa la sezione Impostazioni generali . Nome gruppo è un attributo obbligatorio. Puoi assegnare il gruppo a qualsiasi dominio configurato.
1. In Criteri di gruppo dinamici, specifica uno o più attributi utilizzati per compilare il gruppo dinamico.

   >[!NOTE]
   >
   >Gli attributi Email, Description e Canonical Name fanno distinzione tra maiuscole e minuscole quando si utilizza l’operatore Uguale a . Non sono sensibili all’uso di maiuscole e minuscole con gli operatori Starts With, Ends With o Contains .

   **E-mail:** Dominio e-mail dell’utente, ad esempio `@adobe.com`.

   **Descrizione:** Descrizione dell’utente, ad esempio &quot;Informatista&quot;

   **Nome canonico:** Nome canonico dell’utente, ad esempio `ou=adobe.com`

   **Nome di dominio:** Il nome del dominio a cui appartiene l&#39;utente, ad esempio `DefaultDom`. L’attributo Nome di dominio distingue tra maiuscole e minuscole quando si utilizza l’operatore Contains . Non distingue tra maiuscole e minuscole per gli operatori Starts With, Ends With o Equals.

1. Fai clic su Prova. In una pagina di test vengono visualizzati i primi 200 utenti che soddisfano i criteri definiti. Fai clic su Chiudi.
1. Se il test ha restituito i risultati previsti, fare clic su Avanti. In caso contrario, modifica i criteri del gruppo dinamico ed effettua di nuovo il test.
1. Per aggiungere il gruppo dinamico a un gruppo padre, fare clic su Trova gruppi ed eseguire le operazioni seguenti:

   * Nella casella Trova digitare i criteri di ricerca.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare e fare clic su Trova.
   * Nei risultati della ricerca, selezionare le caselle di controllo relative ai gruppi a cui appartiene il gruppo dinamico e fare clic su OK.

1. Fai clic su Avanti.
1. Per assegnare ruoli al gruppo dinamico, fare clic su Trova ruoli, selezionare le caselle di controllo relative a ciascun ruolo da assegnare al gruppo, quindi fare clic su OK. Gli utenti del gruppo ereditano i ruoli assegnati a livello di gruppo.
1. Fare clic su Fine.

## Visualizzare i dettagli di un gruppo {#view-details-about-a-group}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Nell&#39;elenco In, selezionare Gruppo, quindi fare clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. Per ordinare l’elenco, fai clic su una delle intestazioni di colonna.
1. Fai clic sul nome del gruppo di cui visualizzare i dettagli. Viene visualizzata la pagina Dettagli gruppo.
1. Per visualizzare i membri diretti del gruppo, fare clic su Entità figlio.

## Modificare un gruppo {#edit-a-group}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Per trovare il gruppo da modificare, eseguire le operazioni seguenti:

   * Nella casella Trova digitare i criteri di ricerca.
   * Nell’elenco Utilizzo, selezionare Nome o E-mail.
   * Nell’elenco In, selezionare Gruppi.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare e fare clic su Trova.
   * Nei risultati della ricerca, fai clic sul nome del gruppo da modificare.

1. Nella scheda Dettagli modificare le impostazioni generali e fare clic su Salva.
1. Per modificare i gruppi associati, fare clic sulla scheda Gruppi padre ed eseguire le operazioni seguenti:

   * Per trovare i gruppi da aggiungere all’associazione, fare clic su Trova gruppi e completare le informazioni di ricerca.
   * Per aggiungere gruppi, selezionare la casella di controllo relativa ai gruppi da aggiungere, fare clic su OK e quindi su Salva.
   * Per eliminare un gruppo associato, selezionare la casella di controllo relativa al gruppo da eliminare, fare clic su Elimina, fare clic su OK e quindi su Salva.

1. Per modificare gli utenti e i gruppi del gruppo, fare clic sulla scheda Entità figlio ed eseguire le operazioni seguenti:

   * Per trovare utenti e gruppi da aggiungere, fare clic su Trova utenti/gruppi e completare le informazioni di ricerca.
   * Per aggiungere un utente o un gruppo, selezionare la casella di controllo relativa all&#39;utente o al gruppo, fare clic su OK e quindi su Salva.
   * Per eliminare un utente o un gruppo, selezionare la casella di controllo relativa all&#39;utente o al gruppo, fare clic su Elimina, fare clic su OK e quindi su Salva.

1. Per modificare le assegnazioni di ruolo, fare clic sulla scheda Assegnazioni ruolo ed eseguire le operazioni seguenti:

   * Per trovare i ruoli da assegnare al gruppo, fare clic su Trova ruoli.
   * Per aggiungere un ruolo, selezionare la casella di controllo relativa al ruolo, fare clic su OK e quindi su Salva.
   * Per annullare l’assegnazione di un ruolo, selezionare la casella di controllo relativa al ruolo, fare clic su Annulla assegnazione, quindi fare clic su Salva.

## Eliminare un gruppo {#delete-a-group}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Selezionare Gruppi dall&#39;elenco Trova, quindi fare clic su Trova.
1. Selezionare la casella di controllo relativa al gruppo da eliminare, fare clic su Elimina, quindi su OK.
