---
title: Configurare gli attributi di sistema avanzati
seo-title: Configurare gli attributi di sistema avanzati
description: Utilizzare la pagina Configura attributi di sistema avanzati per modificare alcune impostazioni nel file di configurazione senza dover esportare, modificare e importare il file.
seo-description: Utilizzare la pagina Configura attributi di sistema avanzati per modificare alcune impostazioni nel file di configurazione senza dover esportare, modificare e importare il file.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurare gli attributi di sistema avanzati {#configure-advanced-system-attributes}

Utilizzare la pagina Configura attributi di sistema avanzati per modificare alcune impostazioni nel file di configurazione senza dover esportare, modificare e importare il file. Consultate [Importazione ed esportazione del file](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)di configurazione.

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Configurazione > Configura attributi]** di sistema avanzati.
1. (Facoltativo) Modificate i seguenti attributi di sessione:

   **** Limite timeout sessione (minuti): Il tempo, in minuti, prima che un utente venga automaticamente disconnesso dal sistema. Per impostazione predefinita, i componenti dei moduli AEM, come Workbench, scadono dopo due ore, indipendentemente dall&#39;attività o dall&#39;inattività, e l&#39;utente deve effettuare di nuovo l&#39;accesso. I valori validi sono `1` a `1440`. Il valore predefinito è `120` (2 ore). Questa impostazione aggiorna la chiave di `SAML/Producer/assertionValidityInMinutes` voce nel file di configurazione.

   >[!NOTE]
   >
   >Non impostare il limite di timeout della sessione inferiore a 10 minuti perché il sistema potrebbe non funzionare correttamente. Il valore consigliato è 10-120 (minuti).

   **** Soglia Di Asserzione (Secondi): Tempo di buffer per compensare i ritardi dovuti alle differenze di tempo del sistema tra i server applicazione dei moduli AEM in un cluster. I moduli AEM retrodatano il tempo di accesso di un utente per il tempo (in secondi) specificato in questa proprietà. I valori validi sono `0` a `3600`. Il valore predefinito è `60`. Questa impostazione aggiorna la chiave di `SAML/Producer/assertionThresholdInSeconds` voce nel file di configurazione.

   **** Rinnovi consentiti massimi di un&#39;asserzione: Il numero massimo di volte che una sessione utente può essere rinnovata in modo trasparente senza richiedere l&#39;accesso. I valori validi sono `0` a `9999`. Un valore `0` indica che le asserzioni non vengono rinnovate. Il valore predefinito è 10. Questa impostazione aggiorna la chiave di `SAML/Producer/maxAssertionRenewalCount` voce nel file di configurazione.

1. (Facoltativo) Modificate i seguenti attributi di sincronizzazione della directory:

   **** Registrazione delle statistiche di sincronizzazione: Specifica se Gestione utente registra le statistiche dettagliate durante il processo di sincronizzazione. (Vedete [Attivare o disattivare la registrazione dettagliata durante la sincronizzazione](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **** Espressione Cron Synch Finisher: L&#39;intervallo in cui i tentativi di gestione utenti non riuscivano a eseguire la sincronizzazione. Consultate [Configurare l’opzione](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)dei tentativi di sincronizzazione della directory.

   **** Timeout Blocco Processo Cluster In Minuti: Utilizzata in ambienti cluster. Se la sincronizzazione su un nodo ha esito negativo e il blocco del cluster non viene rilasciato, questo valore specifica il numero di minuti che un altro nodo attende prima di acquisire forzatamente il blocco. The default value is `15` minutes. I valori validi sono `1` espressi in `1440` minuti.

1. (Facoltativo) Modificate i seguenti attributi e fate clic su **[!UICONTROL OK]**:

   **** Controllo eventi di User Manager: Selezionate questa opzione per abilitare il controllo degli eventi di sincronizzazione della directory e degli eventi di autenticazione come l&#39;esito positivo, l&#39;errore e il blocco. Per impostazione predefinita, questa opzione è selezionata solo se avete installato un componente che richiede il controllo, ad esempio Rights Management. Questa impostazione aggiorna la chiave di `APSAuditService` voce nel file di configurazione.

   **** Creazione automatica del gruppo dinamico: Abilita la creazione automatica di gruppi dinamici basati sui domini e-mail. Consultate [Creare un gruppo](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)dinamico.

Potete anche ripristinare le impostazioni di gestione utenti originali facendo clic su Ricarica.
