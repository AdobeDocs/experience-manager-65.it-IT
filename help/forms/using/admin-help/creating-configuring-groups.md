---
title: Creazione e configurazione dei gruppi
description: Scopri come creare gruppi manualmente o in modo dinamico, modificarli, visualizzarne i dettagli o eliminarli.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 72edd8d1-8573-4942-8ced-1a100af58d78
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1585'
ht-degree: 100%

---

# Creazione e configurazione dei gruppi{#creating-and-configuring-groups}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

La creazione di gruppi di utenti consente di assegnare ruoli al gruppo anziché ai singoli utenti.

Sono disponibili due diversi tipi di gruppi. Puoi creare manualmente un gruppo e aggiungervi utenti e altri gruppi. Puoi anche creare gruppi dinamici che includono automaticamente tutti gli utenti che soddisfano un set specifico di regole.

Gli utenti possono riscontrare un tempo di risposta più lento se appartengono a più gruppi (ad esempio, 500 o più) o se i gruppi sono profondamente nidificati (ad esempio, 30 livelli). Se si verifica questo problema, puoi configurare AEM Forms per precaricare le informazioni da determinati domini. Consulta [Configurare AEM Forms per precaricare le informazioni sul dominio](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information).

## Creare un gruppo manualmente {#create-a-group-manually}

Quando crei manualmente un gruppo, puoi aggiungervi utenti e altri gruppi e assegnare ruoli al gruppo. Puoi inoltre associare il gruppo a un gruppo principale.

Se utilizzi Content Services (obsoleto), puoi selezionare l’opzione “Seleziona questa opzione per inviare utenti e gruppi a provider di archiviazione principali esterni registrati” nella pagina Gestione dominio per inviare le informazioni per eventuali nuovi utenti o gruppi creati in Content Services (obsoleto).

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi, quindi fai clic su Nuovo gruppo.
1. Completa la sezione Impostazioni generali e fai clic su Avanti. Nome canonico e Nome gruppo sono attributi obbligatori.

   Il Nome canonico è un identificatore univoco del gruppo. Ogni gruppo e utente in un dominio deve avere un nome canonico univoco. Seleziona la casella di controllo Generato dal sistema per consentire a Gestione utenti di assegnare un valore univoco oppure deseleziona la casella di controllo e specifica un valore personalizzato per il Nome canonico.

   Evita di utilizzare caratteri di sottolineatura (_) nei nomi canonici, ad esempio `sample_group`. Quando cerchi gruppi in base al nome canonico, quelli contenenti caratteri di sottolineatura non vengono restituiti.

1. Per aggiungere utenti e gruppi a questo nuovo gruppo, fai clic su Trova utenti/gruppi ed esegui le operazioni seguenti:

   * Nella casella Trova, digita i criteri di ricerca.
   * Nell’elenco In seleziona Utenti, Gruppi oppure Utenti e gruppi.
   * Nell’elenco Utilizzo, seleziona Nome, E-mail o ID utente.
   * Seleziona il dominio, il numero di elementi da visualizzare e fai clic su Trova.
   * Nei risultati della ricerca seleziona le caselle di controllo relative agli utenti e ai gruppi da aggiungere a questo nuovo gruppo e fai clic su OK.

1. Fai clic su Avanti.
1. Per aggiungere questo nuovo gruppo ad altri gruppi esistenti, fai clic su Trova gruppi ed esegui le operazioni seguenti:

   * Nella casella Trova, digita i criteri di ricerca.
   * Seleziona il dominio, il numero di elementi da visualizzare e fai clic su Trova.
   * Nei risultati della ricerca seleziona le caselle di controllo relative ai gruppi a cui appartiene il nuovo gruppo e fai clic su OK.

1. Fai clic su Avanti.
1. Per assegnare ruoli al gruppo, fai clic su Trova ruoli, seleziona le caselle di controllo relative a ciascun ruolo da assegnare al gruppo e fai clic su OK. Gli utenti del gruppo ereditano i ruoli assegnati a livello di gruppo.
1. Fai clic su Fine.

## Crea un gruppo dinamico {#create-a-dynamic-group}

In un gruppo dinamico, non puoi selezionare singolarmente gli utenti che appartengono al gruppo. Viene invece specificato un set di regole e tutti gli utenti che soddisfano tali regole vengono aggiunti automaticamente al gruppo dinamico.

Per creare gruppi dinamici, puoi utilizzare uno dei due metodi seguenti:

* Abilita la creazione automatica di gruppi dinamici basati sui domini e-mail, ad esempio @adobe.com. Quando abiliti questa funzione, Gestione utenti crea un gruppo dinamico per ogni dominio e-mail univoco nel database di AEM Forms. Utilizza un’espressione cron per specificare la frequenza con cui Gestione utenti cerca nuovi domini e-mail nel database di AEM Forms. Questi gruppi dinamici vengono aggiunti al dominio locale DefaultDom e sono denominati &quot;Tutti gli utenti con un ID di posta *`[email domain]`*&quot;.
* Crea un gruppo dinamico in base a criteri specificati, tra cui il dominio e-mail, la descrizione, il nome canonico e il nome di dominio dell’utente. Per appartenere al gruppo dinamico, un utente deve soddisfare tutti i criteri specificati. Per impostare una condizione &quot;o&quot;, crea due gruppi dinamici separati e aggiungili entrambi a un gruppo locale. Ad esempio, utilizza questo approccio per creare un gruppo di utenti che appartengono al dominio e-mail @adobe.com o il cui nome canonico contiene ou=adobe.com. Tuttavia, gli utenti non devono necessariamente soddisfare entrambe le condizioni.

Un gruppo dinamico contiene solo utenti. Non può contenere altri gruppi. Tuttavia, un gruppo dinamico può appartenere a un gruppo principale.

### Crea automaticamente gruppi dinamici basati sui domini e-mail {#automatically-create-dynamic-groups-based-on-email-domains}

1. Fai clic su Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati.
1. In Creazione automatica gruppo dinamico, seleziona la casella di controllo.
1. Specifica quando Gestione utenti controlla la presenza di nuovi domini e-mail. L’ora deve essere successiva all’ora di sincronizzazione del dominio perché la creazione di gruppi dinamici è logica solo se la sincronizzazione del dominio è stata completata.

   * Per abilitare la sincronizzazione automatica su base giornaliera, digitare l’ora nel formato di 24 ore nella casella Si verifica il giorno alle. Quando salvi le impostazioni, questo valore viene convertito in un’espressione cron, che viene visualizzata nella casella sottostante.
   * Per pianificare la sincronizzazione in un giorno specifico della settimana o del mese oppure in un mese specifico, selezionare la casella corrispondente all’espressione cron desiderata. Il valore predefinito è `0 00 4 ? * *`, che significa: verifica alle 4 del mattino ogni giorno.

     L’utilizzo dell’espressione Cron si basa sul sistema di pianificazione dei processi open source Quartz, versione 1.4.0.

1. Fai clic su Salva.

### Crea un gruppo dinamico in base a criteri specificati {#create-a-dynamic-group-based-on-specified-criteria}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Fai clic su Nuovo gruppo dinamico.
1. Compila la sezione Impostazioni generali. Nome gruppo è un attributo obbligatorio. Puoi assegnare il gruppo a qualsiasi dominio configurato.
1. In Criteri di gruppo dinamico, specifica uno o più attributi utilizzati per compilare il gruppo dinamico.

   >[!NOTE]
   >
   >Gli attributi E-mail, Descrizione e Nome canonico distinguono tra maiuscole e minuscole quando utilizzi l’operatore È uguale a. Per gli operatori Inizia con, Termina con o Contiene non viene fatta distinzione tra maiuscole e minuscole.

   **E-mail:** dominio e-mail dell’utente, ad esempio `@adobe.com`.

   **Descrizione:** descrizione utente, ad esempio &quot;Computer Scientist&quot;

   **Nome canonico:** nome canonico dell’utente, ad esempio `ou=adobe.com`

   **Nome dominio:** nome del dominio a cui appartiene l’utente, ad esempio `DefaultDom`. Quando utilizzi l’operatore Contiene, l’attributo Nome dominio distingue tra maiuscole e minuscole. Per gli operatori Inizia con, Termina con o Equivale a non viene fatta distinzione tra maiuscole e minuscole.

1. Fai clic su Test. In una pagina di test vengono visualizzati i primi 200 utenti che soddisfano i criteri definiti. Fai clic su Chiudi.
1. Se il test ha restituito i risultati previsti, fai clic su Avanti. In caso contrario, modifica i criteri del gruppo dinamico ed esegui nuovamente il test.
1. Per aggiungere il gruppo dinamico a un gruppo principale, fai clic su Trova gruppi ed esegui le operazioni seguenti:

   * Nella casella Trova, digita i criteri di ricerca.
   * Seleziona il dominio, il numero di elementi da visualizzare e fai clic su Trova.
   * Nei risultati della ricerca, seleziona le caselle di controllo relative ai gruppi a cui appartiene il gruppo dinamico e fai clic su OK.

1. Fai clic su Avanti.
1. Per assegnare ruoli al gruppo dinamico, fai clic su Trova ruoli, seleziona le caselle di controllo per ogni ruolo da assegnare al gruppo e quindi fai clic su OK. Gli utenti del gruppo ereditano i ruoli assegnati a livello di gruppo.
1. Fai clic su Fine.

## Visualizzare i dettagli su un gruppo {#view-details-about-a-group}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Nell’elenco In, seleziona Gruppo e quindi fai clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. Puoi ordinare l’elenco facendo clic su una delle intestazioni di colonna.
1. Fai clic sul nome del gruppo per visualizzare i relativi dettagli. Viene visualizzata la pagina Dettagli gruppo.
1. Per visualizzare i membri diretti del gruppo, fai clic su Entità principali secondarie.

## Modificare un gruppo {#edit-a-group}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Per trovare il gruppo da modificare, esegui le attività seguenti:

   * Nella casella Trova, digita i criteri di ricerca.
   * Nell’elenco Utilizzo, seleziona Nome o E-mail.
   * Nell’elenco In, seleziona Gruppi.
   * Seleziona il dominio, il numero di elementi da visualizzare e fai clic su Trova.
   * Nei risultati della ricerca, fai clic sul nome del gruppo da modificare.

1. Nella scheda Dettagli, modifica le impostazioni generali e fai clic su Salva.
1. Per modificare i gruppi associati, fai clic sulla scheda Gruppi principali ed esegui le attività seguenti:

   * Per trovare i gruppi da aggiungere all’associazione, fai clic su Trova gruppi e completa le informazioni di ricerca.
   * Per aggiungere gruppi, seleziona la casella di controllo relativa ai gruppi da aggiungere, fai clic su OK, quindi su Salva.
   * Per eliminare un gruppo associato, seleziona la casella di controllo relativa al gruppo da eliminare, fai clic su Elimina, seleziona OK, quindi fai clic su Salva.

1. Per modificare gli utenti e i gruppi del gruppo, fai clic sulla scheda Entità principali secondarie ed esegui le attività seguenti:

   * Per trovare utenti e gruppi da aggiungere, fai clic su Trova utenti/gruppi e completa le informazioni di ricerca.
   * Per aggiungere un utente o un gruppo, seleziona la casella di controllo relativa all’utente o al gruppo, fai clic su OK, quindi su Salva.
   * Per eliminare un utente o un gruppo, seleziona la casella di controllo relativa all’utente o al gruppo, fai clic su Elimina, seleziona OK, quindi fai clic su Salva.

1. Per modificare le assegnazioni dei ruoli, fai clic sulla scheda Assegnazioni ruolo ed esegui le attività seguenti:

   * Per trovare i ruoli da assegnare al gruppo, fai clic su Trova ruoli.
   * Per aggiungere un ruolo, seleziona la casella di controllo relativa al ruolo, fai clic su OK, quindi su Salva.
   * Per annullare l’assegnazione di un ruolo, seleziona la casella di controllo relativa al ruolo, fai clic su Annulla assegnazione, quindi su Salva.

## Eliminare un gruppo {#delete-a-group}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Nell’elenco Trova seleziona Gruppi, quindi fai clic su Trova.
1. Seleziona la casella di controllo del gruppo da eliminare, fai clic su Elimina, quindi su OK.
