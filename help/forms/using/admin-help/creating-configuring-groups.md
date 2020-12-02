---
title: Creazione e configurazione di gruppi
seo-title: Creazione e configurazione di gruppi
description: Scoprite come creare gruppi manualmente o dinamicamente, modificare un gruppo, visualizzare i dettagli di un gruppo o eliminare un gruppo.
seo-description: Scoprite come creare gruppi manualmente o dinamicamente, modificare un gruppo, visualizzare i dettagli di un gruppo o eliminare un gruppo.
uuid: 8532d72b-270a-4fcf-b7a5-56fca979a5fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2058b501-65ce-4ad3-8e1b-b2eab896f70f
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 0%

---


# Creazione e configurazione di gruppi{#creating-and-configuring-groups}

La creazione di gruppi di utenti consente di assegnare i ruoli al gruppo anziché ai singoli utenti.

Sono disponibili due diversi tipi di gruppi. Potete creare manualmente un gruppo e aggiungervi utenti e altri gruppi. Potete anche creare gruppi dinamici che includono automaticamente tutti gli utenti che soddisfano un set specifico di regole.

Gli utenti potrebbero riscontrare un tempo di risposta più lento se appartengono a molti gruppi (ad esempio, 500 o più) o se i gruppi sono nidificati in profondità (ad esempio, 30 livelli). Se si verifica questo problema, è possibile configurare AEM moduli per preacquisire informazioni da alcuni domini. (Vedere [Configurare AEM moduli per la preacquisizione delle informazioni sul dominio](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information).)

## Creare manualmente un gruppo {#create-a-group-manually}

Quando create manualmente un gruppo, potete aggiungervi utenti e altri gruppi e assegnare ruoli al gruppo. Potete anche associare il gruppo a un gruppo principale.

Se si utilizza Content Services (obsoleto), è possibile selezionare l&#39;opzione Seleziona questa opzione per inviare utenti e gruppi nei provider di archiviazione principale esterni registrati nella pagina Gestione dominio per inviare le informazioni a tutti i nuovi utenti o gruppi creati in Content Services (obsoleto).

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Utenti e gruppi, quindi fate clic su Nuovo gruppo.
1. Completate la sezione Impostazioni generali e fate clic su Avanti. Nome canonico e Nome gruppo sono attributi obbligatori.

   Il Nome canonico è un identificatore univoco per il gruppo. Ogni gruppo e utente in un dominio deve avere un nome canonico univoco. Selezionate la casella di controllo Sistema generato per consentire a Gestione utente di assegnare un valore univoco, oppure deselezionate la casella di controllo e specificate un valore personalizzato per il Nome canonico.

   Evitare di utilizzare caratteri di sottolineatura (_) nei nomi canonici, ad esempio `sample_group`. Quando cercate dei gruppi in base al nome canonico, quelli che contengono caratteri di sottolineatura non vengono restituiti.

1. Per aggiungere utenti e gruppi a questo nuovo gruppo, fate clic su Trova utenti/gruppi ed effettuate le seguenti operazioni:

   * Nella casella Trova, digitate i criteri di ricerca.
   * Nell&#39;elenco In, selezionare Utenti, Gruppi o Utenti e Gruppi.
   * Nell&#39;elenco Utilizzo, selezionare Nome, E-mail o ID utente.
   * Selezionate il dominio, selezionate il numero di elementi da visualizzare e fate clic su Trova.
   * Nei risultati della ricerca, selezionate le caselle di controllo per gli utenti e i gruppi da aggiungere a questo nuovo gruppo e fate clic su OK.

1. Fai clic su Avanti.
1. Per aggiungere il nuovo gruppo ad altri gruppi esistenti, fate clic su Trova gruppi ed effettuate le seguenti operazioni:

   * Nella casella Trova, digitate i criteri di ricerca.
   * Selezionate il dominio, selezionate il numero di elementi da visualizzare e fate clic su Trova.
   * Nei risultati della ricerca, selezionate le caselle di controllo relative ai gruppi a cui appartiene il nuovo gruppo e fate clic su OK.

1. Fai clic su Avanti.
1. Per assegnare i ruoli al gruppo, fate clic su Trova ruoli, selezionate le caselle di controllo per ciascun ruolo da assegnare al gruppo e fate clic su OK. Gli utenti del gruppo ereditano i ruoli assegnati a livello di gruppo.
1. Fare clic su Fine.

## Creare un gruppo dinamico {#create-a-dynamic-group}

In un gruppo dinamico, non selezionate singolarmente gli utenti che appartengono al gruppo. Al contrario, specificate un set di regole e tutti gli utenti che soddisfano tali regole vengono automaticamente aggiunti al gruppo dinamico.

Utilizzate uno dei due modi seguenti per creare gruppi dinamici:

* Abilita la creazione automatica di gruppi dinamici basati su domini e-mail, ad esempio @adobe.com. Quando si attiva questa funzione, Gestione utente crea un gruppo dinamico per ciascun dominio e-mail univoco nel database dei moduli AEM. Utilizzare un&#39;espressione cron per specificare la frequenza con cui la Gestione utente cerca nel database dei moduli AEM nuovi domini e-mail. Questi gruppi dinamici vengono aggiunti al dominio locale DefaultDom e sono denominati &quot;Tutti gli utenti con un ID di posta *`[email domain]`*.&quot;
* Create un gruppo dinamico basato su criteri specifici, inclusi il dominio e-mail dell&#39;utente, la descrizione, il nome canonico e il nome di dominio. Per appartenere al gruppo dinamico, un utente deve soddisfare tutti i criteri specificati. Per impostare una condizione &quot;OR&quot;, create due gruppi dinamici distinti e aggiungeteli entrambi a un gruppo locale. Ad esempio, utilizzate questo approccio per creare un gruppo di utenti che appartengono al dominio e-mail @adobe.com o il cui nome canonico contiene ou=adobe.com. Tuttavia, gli utenti non devono necessariamente soddisfare entrambe le condizioni.

Un gruppo dinamico contiene solo utenti. Non può contenere altri gruppi. Tuttavia, un gruppo dinamico può appartenere a un gruppo principale.

### Crea automaticamente gruppi dinamici basati su domini di posta elettronica {#automatically-create-dynamic-groups-based-on-email-domains}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati.
1. In Creazione automatica del gruppo dinamico, selezionate la casella di controllo.
1. Specificate quando User Manager verifica la presenza di nuovi domini e-mail. Questa ora deve essere successiva all’ora di sincronizzazione del dominio, perché la creazione di gruppi dinamici è logica solo se la sincronizzazione del dominio è completata.

   * Per abilitare la sincronizzazione automatica su base giornaliera, digitare l&#39;ora nel formato 24 ore nella casella Verifica giorno a. Quando salvate le impostazioni, questo valore viene convertito in un&#39;espressione cron, visualizzata nella casella seguente.
   * Per pianificare la sincronizzazione in un giorno particolare della settimana o del mese, oppure in un mese particolare, selezionare la relativa espressione cron nella casella. Il valore predefinito è `0 00 4 ? * *`(che significa check at 4 A.M. ogni giorno).

      L&#39;utilizzo dell&#39;espressione cron si basa sul sistema di programmazione dei processi open source Quartz, versione 1.4.0.

1. Fate clic su Salva.

### Creare un gruppo dinamico basato su criteri specifici {#create-a-dynamic-group-based-on-specified-criteria}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Fate clic su Nuovo gruppo dinamico.
1. Completate la sezione Impostazioni generali. Nome gruppo è un attributo obbligatorio. Potete assegnare il gruppo a qualsiasi dominio configurato.
1. In Criteri di gruppo dinamici, specificate uno o più attributi utilizzati per compilare il gruppo dinamico.

   >[!NOTE]
   >
   >Gli attributi E-mail, Descrizione e Nome canonico fanno distinzione tra maiuscole e minuscole quando si utilizza l&#39;operatore Uguale a. Non viene fatta distinzione tra maiuscole e minuscole con gli operatori Inizia con, Termina con o Contiene.

   **E-mail:dominio e-mail dell’** utente, ad esempio  `@adobe.com`.

   **Descrizione:descrizione** dell&#39;utente, ad esempio &quot;Computer Scientist&quot;

   **Nome canonico:nome canonico** dell&#39;utente, ad esempio  `ou=adobe.com`

   **Nome dominio:** il nome del dominio a cui appartiene l&#39;utente, ad esempio  `DefaultDom`. L&#39;attributo Nome dominio distingue tra maiuscole e minuscole quando si utilizza l&#39;operatore Contiene. Non fa distinzione tra maiuscole e minuscole con gli operatori Inizia con, Termina con o È uguale a.

1. Fate clic su Test. Una pagina di test mostra i primi 200 utenti che soddisfano i criteri definiti. Fai clic su Chiudi.
1. Se il test ha restituito i risultati previsti, fare clic su Avanti. In caso contrario, modificate i criteri del gruppo dinamico e ripetete il test.
1. Per aggiungere il gruppo dinamico a un gruppo principale, fate clic su Trova gruppi ed effettuate le seguenti operazioni:

   * Nella casella Trova, digitate i criteri di ricerca.
   * Selezionate il dominio, selezionate il numero di elementi da visualizzare e fate clic su Trova.
   * Nei risultati della ricerca, selezionate le caselle di controllo relative ai gruppi a cui appartiene il gruppo dinamico e fate clic su OK.

1. Fai clic su Avanti.
1. Per assegnare i ruoli al gruppo dinamico, fate clic su Trova ruoli, selezionate le caselle di controllo per ciascun ruolo da assegnare al gruppo, quindi fate clic su OK. Gli utenti del gruppo ereditano i ruoli assegnati a livello di gruppo.
1. Fare clic su Fine.

## Visualizza dettagli su un gruppo {#view-details-about-a-group}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Nell&#39;elenco In, selezionare Gruppo, quindi fare clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. Potete ordinare l’elenco facendo clic su una delle intestazioni di colonna.
1. Fate clic sul nome del gruppo per visualizzare i dettagli. Viene visualizzata la pagina Dettagli gruppo.
1. Per visualizzare i membri diretti del gruppo, fate clic su Entità figlio.

## Modificare un gruppo {#edit-a-group}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Per trovare il gruppo da modificare, effettuate le seguenti operazioni:

   * Nella casella Trova, digitate i criteri di ricerca.
   * Nell&#39;elenco Uso, selezionare Nome o E-mail.
   * Nell&#39;elenco In, selezionare Gruppi.
   * Selezionate il dominio, selezionate il numero di elementi da visualizzare e fate clic su Trova.
   * Nei risultati della ricerca, fate clic sul nome del gruppo da modificare.

1. Nella scheda Dettagli, modificate le impostazioni generali e fate clic su Salva.
1. Per modificare i gruppi associati, fare clic sulla scheda Gruppi padre ed eseguire le operazioni seguenti:

   * Per trovare i gruppi da aggiungere all&#39;associazione, fate clic su Trova gruppi e completate le informazioni di ricerca.
   * Per aggiungere gruppi, selezionate la casella di controllo relativa ai gruppi da aggiungere, fate clic su OK, quindi su Salva.
   * Per eliminare un gruppo associato, selezionate la casella di controllo relativa al gruppo da eliminare, fate clic su Elimina, quindi su OK e quindi su Salva.

1. Per modificare gli utenti e i gruppi del gruppo, fate clic sulla scheda Entità figlio ed effettuate le seguenti operazioni:

   * Per trovare utenti e gruppi da aggiungere, fate clic su Trova utenti/gruppi e completate le informazioni di ricerca.
   * Per aggiungere un utente o un gruppo, selezionate la casella di controllo per l’utente o il gruppo, fate clic su OK, quindi su Salva.
   * Per eliminare un utente o un gruppo, selezionate la casella di controllo dell’utente o del gruppo, fate clic su Elimina, quindi su OK e infine su Salva.

1. Per modificare le assegnazioni dei ruoli, fare clic sulla scheda Assegnazioni ruoli ed effettuare le seguenti operazioni:

   * Per trovare i ruoli da assegnare al gruppo, fate clic su Trova ruoli.
   * Per aggiungere un ruolo, selezionate la casella di controllo relativa al ruolo, fate clic su OK, quindi su Salva.
   * Per annullare l’assegnazione di un ruolo, selezionare la casella di controllo relativa al ruolo, fare clic su Annulla assegnazione e quindi su Salva.

## Eliminare un gruppo {#delete-a-group}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Nell’elenco Trova, selezionare Gruppi, quindi fare clic su Trova.
1. Selezionate la casella di controllo relativa al gruppo da eliminare, fate clic su Elimina, quindi su OK.

