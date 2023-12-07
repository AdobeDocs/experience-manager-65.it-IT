---
title: Creazione e configurazione di gruppi
description: Scopri come creare gruppi manualmente o dinamicamente, modificarli, visualizzarne i dettagli o eliminarli.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 72edd8d1-8573-4942-8ced-1a100af58d78
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# Creazione e configurazione di gruppi{#creating-and-configuring-groups}

La creazione di gruppi di utenti consente di assegnare ruoli al gruppo anziché ai singoli utenti.

Sono disponibili due diversi tipi di gruppi. Puoi creare manualmente un gruppo e aggiungervi utenti e altri gruppi. Puoi anche creare gruppi dinamici che includono automaticamente tutti gli utenti che soddisfano un set specificato di regole.

Gli utenti possono riscontrare un tempo di risposta più lento se appartengono a più gruppi (ad esempio, 500 o più) o se i gruppi sono nidificati in profondità (ad esempio, 30 livelli). Se riscontri questo problema, puoi configurare i moduli AEM per preacquisire le informazioni da determinati domini. (vedere [Configurare i moduli AEM per la preacquisizione delle informazioni sul dominio](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information).)

## Creare un gruppo manualmente {#create-a-group-manually}

Quando crei manualmente un gruppo, puoi aggiungervi utenti e altri gruppi e assegnare ruoli al gruppo. È inoltre possibile associare il gruppo a un gruppo padre.

Se si utilizza Content Services (obsoleto), è possibile selezionare l&#39;opzione Seleziona questa opzione per il push di utenti e gruppi in provider di archiviazione principali esterni registrati nella pagina Gestione dominio per inviare le informazioni per eventuali nuovi utenti o gruppi creati in Content Services (obsoleto).

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi, quindi fai clic su Nuovo gruppo.
1. Completare la sezione Impostazioni generali e fare clic su Avanti. Nome canonico e Nome gruppo sono attributi obbligatori.

   Il Nome canonico è un identificatore univoco del gruppo. Ogni gruppo e utente in un dominio deve avere un nome canonico univoco. Selezionare la casella di controllo Generato dal sistema per consentire a Gestione utenti di assegnare un valore univoco oppure deselezionare la casella di controllo e specificare un valore personalizzato per il Nome canonico.

   Evita di usare i caratteri di sottolineatura (_) nei nomi canonici, ad esempio, `sample_group`. Quando si cercano gruppi in base al nome canonico, quelli contenenti caratteri di sottolineatura non vengono restituiti.

1. Per aggiungere utenti e gruppi a questo nuovo gruppo, fare clic su Trova utenti/gruppi ed eseguire le operazioni seguenti:

   * Nella casella Trova digitare i criteri di ricerca.
   * Nell&#39;elenco In selezionare Utenti, Gruppi oppure Utenti e gruppi.
   * Nell’elenco Utilizzo, seleziona Nome, E-mail o ID utente.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare e fare clic su Trova.
   * Nei risultati della ricerca selezionare le caselle di controllo relative agli utenti e ai gruppi da aggiungere al nuovo gruppo e fare clic su OK.

1. Fai clic su Avanti.
1. Per aggiungere questo nuovo gruppo ad altri gruppi esistenti, fare clic su Trova gruppi ed eseguire le operazioni seguenti:

   * Nella casella Trova digitare i criteri di ricerca.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare e fare clic su Trova.
   * Nei risultati della ricerca selezionare le caselle di controllo relative ai gruppi a cui appartiene il nuovo gruppo e fare clic su OK.

1. Fai clic su Avanti.
1. Per assegnare ruoli al gruppo, fare clic su Trova ruoli, selezionare le caselle di controllo relative a ciascun ruolo da assegnare al gruppo e fare clic su OK. Gli utenti del gruppo ereditano i ruoli assegnati a livello di gruppo.
1. Fare clic su Fine.

## Creare un gruppo dinamico {#create-a-dynamic-group}

In un gruppo dinamico, non puoi selezionare singolarmente gli utenti che appartengono al gruppo. Viene invece specificato un set di regole e tutti gli utenti che soddisfano tali regole vengono aggiunti automaticamente al gruppo dinamico.

Per creare gruppi dinamici, potete utilizzare uno dei due modi seguenti:

* Abilita la creazione automatica di gruppi dinamici basati sui domini e-mail, ad esempio @adobe.com. Quando abiliti questa funzione, Gestione utenti crea un gruppo dinamico per ogni dominio e-mail univoco nel database dei moduli AEM. Utilizza un’espressione cron per specificare la frequenza con cui User Management cerca nuovi domini e-mail nel database dei moduli AEM. Questi gruppi dinamici vengono aggiunti al dominio locale DefaultDom e sono denominati &quot;All users with an *`[email domain]`* ID e-mail.&quot;
* Crea un gruppo dinamico in base a criteri specificati, tra cui il dominio e-mail, la descrizione, il nome canonico e il nome di dominio dell’utente. Per appartenere al gruppo dinamico, un utente deve soddisfare tutti i criteri specificati. Per impostare una condizione &quot;o&quot;, crea due gruppi dinamici separati e aggiungili entrambi a un gruppo locale. Ad esempio, utilizza questo approccio per creare un gruppo di utenti che appartengono al dominio e-mail @adobe.com o il cui nome canonico contiene ou=adobe.com. Tuttavia, gli utenti non devono necessariamente soddisfare entrambe le condizioni.

Un gruppo dinamico contiene solo utenti. Non può contenere altri gruppi. Tuttavia, un gruppo dinamico può appartenere a un gruppo padre.

### Crea automaticamente gruppi dinamici basati sui domini e-mail {#automatically-create-dynamic-groups-based-on-email-domains}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati.
1. In Creazione automatica gruppo dinamico selezionare la casella di controllo.
1. Specifica quando User Manager controlla la presenza di nuovi domini e-mail. L&#39;ora deve essere successiva all&#39;ora di sincronizzazione del dominio perché la creazione di gruppi dinamici è logica solo se la sincronizzazione del dominio è stata completata.

   * Per abilitare la sincronizzazione automatica su base giornaliera, digitare l&#39;ora nel formato di 24 ore nella casella Si verifica il giorno alle. Quando salvi le impostazioni, questo valore viene convertito in un’espressione cron, che viene visualizzata nella casella sottostante.
   * Per pianificare la sincronizzazione in un giorno specifico della settimana o del mese oppure in un mese specifico, selezionare la casella corrispondente all&#39;espressione cron desiderata. Il valore predefinito è `0 00 4 ? * *`(il che significa controllare alle 4 del mattino ogni giorno).

     L’utilizzo delle espressioni cron si basa sul sistema di pianificazione dei processi open source Quartz, versione 1.4.0.

1. Fai clic su Salva.

### Creare un gruppo dinamico in base a criteri specificati {#create-a-dynamic-group-based-on-specified-criteria}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Fare clic su Nuovo gruppo dinamico.
1. Compila la sezione Impostazioni generali. Nome gruppo è un attributo obbligatorio. Puoi assegnare il gruppo a qualsiasi dominio configurato.
1. In Criteri di gruppo dinamico (Dynamic Group Criteria), specificate uno o più attributi utilizzati per popolare il gruppo dinamico.

   >[!NOTE]
   >
   >Gli attributi E-mail, Descrizione e Nome canonico distinguono tra maiuscole e minuscole quando si utilizza l’operatore È uguale a. Per gli operatori Starts With, Ends With o Contains non viene fatta distinzione tra maiuscole e minuscole.

   **E-mail:** Dominio e-mail dell’utente, ad esempio `@adobe.com`.

   **Descrizione:** Descrizione dell’utente, ad esempio &quot;Computer Scientist&quot;

   **Nome canonico:** Nome canonico dell’utente, ad esempio `ou=adobe.com`

   **Nome dominio:** Il nome del dominio a cui appartiene l’utente, ad esempio `DefaultDom`. Quando si utilizza l’operatore Contains, l’attributo Domain Name distingue tra maiuscole e minuscole. Per gli operatori Starts With, Ends With o Equals non viene fatta distinzione tra maiuscole e minuscole.

1. Fai clic su Prova. In una pagina di prova vengono visualizzati i primi 200 utenti che soddisfano i criteri definiti. Fai clic su Chiudi.
1. Se il test ha restituito i risultati previsti, fare clic su Avanti. In caso contrario, modifica i criteri del gruppo dinamico e verifica di nuovo.
1. Per aggiungere il gruppo dinamico a un gruppo padre, fare clic su Trova gruppi ed eseguire le operazioni seguenti:

   * Nella casella Trova digitare i criteri di ricerca.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare e fare clic su Trova.
   * Nei risultati della ricerca selezionare le caselle di controllo relative ai gruppi a cui appartiene il gruppo dinamico e fare clic su OK.

1. Fai clic su Avanti.
1. Per assegnare ruoli al gruppo dinamico, fare clic su Trova ruoli, selezionare le caselle di controllo per ogni ruolo da assegnare al gruppo e quindi fare clic su OK. Gli utenti del gruppo ereditano i ruoli assegnati a livello di gruppo.
1. Fare clic su Fine.

## Visualizzare i dettagli su un gruppo {#view-details-about-a-group}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Nell&#39;elenco In selezionare Gruppo e quindi fare clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. È possibile ordinare l&#39;elenco facendo clic su una delle intestazioni di colonna.
1. Fare clic sul nome del gruppo per visualizzare i dettagli relativi a. Viene visualizzata la pagina Dettagli gruppo.
1. Per visualizzare i membri diretti del gruppo, fare clic su Entità figlio.

## Modificare un gruppo {#edit-a-group}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Per trovare il gruppo da modificare, eseguire le operazioni seguenti:

   * Nella casella Trova digitare i criteri di ricerca.
   * Nell’elenco Utilizzo, seleziona Nome o E-mail.
   * Nell&#39;elenco In selezionare Gruppi.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare e fare clic su Trova.
   * Nei risultati della ricerca, fare clic sul nome del gruppo da modificare.

1. Nella scheda Dettagli, modifica le impostazioni generali e fai clic su Salva.
1. Per modificare i gruppi associati, fare clic sulla scheda Gruppi padre ed eseguire le operazioni seguenti:

   * Per trovare i gruppi da aggiungere all&#39;associazione, fare clic su Trova gruppi e completare le informazioni di ricerca.
   * Per aggiungere gruppi, selezionare la casella di controllo relativa ai gruppi da aggiungere, fare clic su OK e quindi su Salva.
   * Per eliminare un gruppo associato, selezionare la casella di controllo relativa al gruppo da eliminare, fare clic su Elimina, scegliere OK e quindi fare clic su Salva.

1. Per modificare gli utenti e i gruppi del gruppo, fare clic sulla scheda Entità figlio ed eseguire le operazioni seguenti:

   * Per trovare utenti e gruppi da aggiungere, fare clic su Trova utenti/gruppi e completare le informazioni di ricerca.
   * Per aggiungere un utente o un gruppo, selezionare la casella di controllo relativa all&#39;utente o al gruppo, fare clic su OK e quindi su Salva.
   * Per eliminare un utente o un gruppo, selezionare la casella di controllo relativa all&#39;utente o al gruppo, fare clic su Elimina, scegliere OK e quindi fare clic su Salva.

1. Per modificare le assegnazioni di ruolo, fare clic sulla scheda Assegnazioni ruolo ed eseguire le operazioni seguenti:

   * Per trovare i ruoli da assegnare al gruppo, fare clic su Trova ruoli.
   * Per aggiungere un ruolo, selezionare la casella di controllo relativa al ruolo, fare clic su OK e quindi su Salva.
   * Per annullare l&#39;assegnazione di un ruolo, selezionare la casella di controllo relativa al ruolo, fare clic su Annulla assegnazione e quindi su Salva.

## Eliminare un gruppo {#delete-a-group}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Nell&#39;elenco Trova selezionare Gruppi e quindi fare clic su Trova.
1. Selezionare la casella di controllo del gruppo da eliminare, fare clic su Elimina e quindi su OK.
