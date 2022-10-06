---
title: Configurare attributi di sistema avanzati
seo-title: Configure advanced system attributes
description: Utilizzare la pagina Configura attributi di sistema avanzati per modificare alcune impostazioni nel file di configurazione senza la necessità di esportare, modificare e importare il file.
seo-description: Use the Configure Advanced System Attributes page to modify certain settings in the configuration file without the need to export, edit, and import the file.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---

# Configurare attributi di sistema avanzati {#configure-advanced-system-attributes}

Utilizzare la pagina Configura attributi di sistema avanzati per modificare alcune impostazioni nel file di configurazione senza la necessità di esportare, modificare e importare il file. (Vedi [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati]**.
1. (Facoltativo) Modifica uno dei seguenti attributi di sessione:

   **Limite Di Timeout Della Sessione (Minuti):** Il tempo, in minuti, prima che un utente venga automaticamente disconnesso dal sistema. Per impostazione predefinita, AEM componenti dei moduli, come Workbench scadono dopo due ore, indipendentemente dall’attività o dall’inattività, e l’utente deve effettuare di nuovo l’accesso. I valori validi sono `1` a `1440`. Il valore predefinito è `120` (2 ore). Questa impostazione aggiorna `SAML/Producer/assertionValidityInMinutes` chiave di ingresso nel file di configurazione.

   >[!NOTE]
   >
   >Non impostare il limite di timeout della sessione inferiore a 10 minuti perché il sistema potrebbe non funzionare correttamente. Il valore consigliato è 10-120 (minuti).

   **Soglia di asserzione (secondi):** Tempo di buffer per l&#39;offset dei ritardi dovuti alle differenze di tempo del sistema tra i server applicazioni AEM forms in un cluster. AEM forms retrodaterà il tempo di accesso di un utente per il tempo (in secondi) specificato in questa proprietà. I valori validi sono `0` a `3600`. Il valore predefinito è `60`. Questa impostazione aggiorna `SAML/Producer/assertionThresholdInSeconds` chiave di ingresso nel file di configurazione.

   **Rinnovi massimi consentiti di un&#39;asserzione:** Il numero massimo di volte in cui la sessione di un utente può essere rinnovata in modo trasparente senza richiedere l&#39;accesso. I valori validi sono `0` a `9999`. Un valore di `0` significa che le affermazioni non vengono rinnovate. Il valore predefinito è 10. Questa impostazione aggiorna `SAML/Producer/maxAssertionRenewalCount` chiave di ingresso nel file di configurazione.

1. (Facoltativo) Modifica uno dei seguenti attributi di sincronizzazione della directory:

   **Registrazione statistiche di sincronizzazione:** Specifica se la Gestione utente registra le statistiche dettagliate durante il processo di sincronizzazione. (Vedi [Attiva o disattiva la registrazione dettagliata durante la sincronizzazione](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **Espressione Cron Di Synch Finisher:** L&#39;intervallo a cui la gestione utente tenta di eseguire nuovamente le sincronizzazioni non riuscite. (Vedi [Configurare l’opzione di esecuzione di un nuovo tentativo di sincronizzazione della directory](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option).)

   **Timeout Blocco Processo Cluster In Minuti:** Utilizzato in ambienti cluster. Se la sincronizzazione su un nodo non riesce e il blocco del cluster non viene rilasciato, questo valore specifica il numero di minuti che un altro nodo attende prima di acquisire forzatamente il blocco. Il valore predefinito è `15` minuti. I valori validi sono `1` a `1440` minuti.

1. (Facoltativo) Modifica i seguenti attributi e fai clic su **[!UICONTROL OK]**:

   **Controllo eventi di User Manager:** Selezionare questa opzione per abilitare il controllo degli eventi di sincronizzazione della directory e degli eventi di autenticazione come successo, errore e blocco. Per impostazione predefinita, questa opzione non è selezionata a meno che non sia stato installato un componente che richiede il controllo, ad esempio Rights Management. Questa impostazione aggiorna `APSAuditService` chiave di ingresso nel file di configurazione.

   **Creazione automatica del gruppo dinamico:** Abilita la creazione automatica di gruppi dinamici basati sui domini e-mail. (Vedi [Creare un gruppo dinamico](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group).)

È inoltre possibile ripristinare le impostazioni di Gestione utente originali facendo clic su Ricarica.
