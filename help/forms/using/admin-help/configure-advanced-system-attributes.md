---
title: Configurare gli attributi di sistema avanzati
seo-title: Configurare gli attributi di sistema avanzati
description: Utilizzare la pagina Configura attributi di sistema avanzati per modificare determinate impostazioni nel file di configurazione senza dover esportare, modificare e importare il file.
seo-description: Utilizzare la pagina Configura attributi di sistema avanzati per modificare determinate impostazioni nel file di configurazione senza dover esportare, modificare e importare il file.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---


# Configurare gli attributi di sistema avanzati {#configure-advanced-system-attributes}

Utilizzare la pagina Configura attributi di sistema avanzati per modificare determinate impostazioni nel file di configurazione senza dover esportare, modificare e importare il file. (Vedere [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati]**.
1. (Facoltativo) Modificate i seguenti attributi di sessione:

   **Limite timeout sessione (minuti):** il tempo, in minuti, prima che un utente venga automaticamente disconnesso dal sistema. Per impostazione predefinita, AEM componenti dei moduli come Workbench scadono dopo due ore, indipendentemente dall&#39;attività o dall&#39;inattività, e l&#39;utente deve eseguire di nuovo l&#39;accesso. I valori validi sono da `1` a `1440`. Il valore predefinito è `120` (2 ore). Questa impostazione aggiorna la chiave di voce `SAML/Producer/assertionValidityInMinutes` nel file di configurazione.

   >[!NOTE]
   >
   >Non impostare il limite di timeout della sessione inferiore a 10 minuti perché il sistema potrebbe non funzionare correttamente. Il valore consigliato è 10-120 (minuti).

   **Soglia di asserzione (secondi):** tempo del buffer per compensare i ritardi dovuti alle differenze di tempo del sistema tra AEM server applicazione dei moduli in un cluster. AEM form retrodaterà il tempo di accesso di un utente per il tempo (in secondi) specificato in questa proprietà. I valori validi sono da `0` a `3600`. Il valore predefinito è `60`. Questa impostazione aggiorna la chiave di voce `SAML/Producer/assertionThresholdInSeconds` nel file di configurazione.

   **Rinnovi consentiti massimi di un&#39;asserzione:** il numero massimo di volte in cui una sessione utente può essere rinnovata in modo trasparente senza richiedere l&#39;accesso. I valori validi sono da `0` a `9999`. Un valore di `0` indica che le asserzioni non vengono rinnovate. Il valore predefinito è 10. Questa impostazione aggiorna la chiave di voce `SAML/Producer/maxAssertionRenewalCount` nel file di configurazione.

1. (Facoltativo) Modificate i seguenti attributi di sincronizzazione della directory:

   **Registrazione delle statistiche di sincronizzazione:** specifica se Gestione utente registra statistiche dettagliate durante il processo di sincronizzazione. (Vedere [Attivare o disattivare la registrazione dettagliata durante la sincronizzazione](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **Espressione Cron Synch Finisher:** l&#39;intervallo con cui la gestione utente tenta di non riuscire a sincronizzare. (Vedere [Configurare l&#39;opzione dei tentativi di sincronizzazione della directory](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option).)

   **Timeout blocco processo cluster in minuti:** utilizzato in ambienti cluster. Se la sincronizzazione su un nodo ha esito negativo e il blocco del cluster non viene rilasciato, questo valore specifica il numero di minuti che un altro nodo attende prima di acquisire forzatamente il blocco. Il valore predefinito è `15` minuti. I valori validi sono compresi tra `1` e `1440` minuti.

1. (Facoltativo) Modificate i seguenti attributi e fate clic su **[!UICONTROL OK]**:

   **Controllo eventi di User Manager:** selezionate questa opzione per abilitare il controllo degli eventi di sincronizzazione della directory e degli eventi di autenticazione quali successo, errore e blocco. Per impostazione predefinita, questa opzione è selezionata solo se è stato installato un componente che richiede il controllo, ad esempio un Rights Management. Questa impostazione aggiorna la chiave di voce `APSAuditService` nel file di configurazione.

   **Creazione automatica di gruppi dinamici:** abilita la creazione automatica di gruppi dinamici basati sui domini e-mail. (Vedere [Creare un gruppo dinamico](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group).)

Potete anche ripristinare le impostazioni di gestione utenti originali facendo clic su Ricarica.
