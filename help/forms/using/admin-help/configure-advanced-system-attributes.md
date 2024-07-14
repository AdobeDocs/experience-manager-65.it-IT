---
title: Configurare attributi di sistema avanzati
description: Utilizzare la pagina Configura attributi di sistema avanzati per modificare alcune impostazioni nel file di configurazione senza dover esportare, modificare e importare il file.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Configurare attributi di sistema avanzati {#configure-advanced-system-attributes}

Utilizzare la pagina Configura attributi di sistema avanzati per modificare alcune impostazioni nel file di configurazione senza dover esportare, modificare e importare il file. (Vedere [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. Nella console di amministrazione, fare clic su **[!UICONTROL Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati]**.
1. (Facoltativo) Modificate uno dei seguenti attributi di sessione:

   **Limite timeout sessione (minuti):** il tempo, in minuti, trascorso il quale un utente viene automaticamente disconnesso dal sistema. Per impostazione predefinita, l’AEM forma componenti come Workbench che si interrompe dopo due ore, indipendentemente dall’attività o dall’inattività, e l’utente deve effettuare di nuovo l’accesso. I valori validi sono compresi tra `1` e `1440`. Il valore predefinito è `120` (2 ore). Questa impostazione aggiorna la chiave di ingresso `SAML/Producer/assertionValidityInMinutes` nel file di configurazione.

   >[!NOTE]
   >
   >Non impostare il limite di timeout sessione al di sotto di 10 minuti perché il sistema potrebbe non comportarsi correttamente. Il valore consigliato è 10-120 (minuti).

   **Soglia asserzione (secondi):** un tempo di buffer per compensare i ritardi dovuti alle differenze di tempo del sistema tra i server applicazioni AEM forms in un cluster. I moduli AEM retrodatano il tempo di accesso di un utente in base al tempo (in secondi) specificato in questa proprietà. I valori validi sono compresi tra `0` e `3600`. Il valore predefinito è `60`. Questa impostazione aggiorna la chiave di ingresso `SAML/Producer/assertionThresholdInSeconds` nel file di configurazione.

   **Rinnovi consentiti massimi di un&#39;asserzione:** il numero massimo di volte in cui è possibile rinnovare in modo trasparente una sessione utente senza richiedere l&#39;accesso. I valori validi sono compresi tra `0` e `9999`. Il valore `0` indica che le asserzioni non vengono rinnovate. Il valore predefinito è 10. Questa impostazione aggiorna la chiave di ingresso `SAML/Producer/maxAssertionRenewalCount` nel file di configurazione.

1. (Facoltativo) Modificare uno dei seguenti attributi di sincronizzazione delle directory:

   **Registrazione statistiche di sincronizzazione:** Specifica se Gestione utenti registra statistiche dettagliate durante il processo di sincronizzazione. (Vedi [Attiva o disattiva la registrazione dettagliata durante la sincronizzazione](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **Espressione Cron Finisher Sincronizzazione:** Intervallo di tentativi di sincronizzazione non riusciti da parte di Gestione utenti. (Vedere [Configurare l&#39;opzione di esecuzione di un nuovo tentativo di sincronizzazione della directory](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option).)

   **Timeout blocco processo cluster in minuti:** utilizzato in ambienti cluster. Se la sincronizzazione su un nodo ha esito negativo e il blocco del cluster non viene rilasciato, questo valore specifica il numero di minuti di attesa di un altro nodo prima dell&#39;acquisizione forzata del blocco. Il valore predefinito è `15` minuti. I valori validi sono compresi tra `1` e `1440` minuti.

1. (Facoltativo) Modificare i seguenti attributi e quindi fare clic su **[!UICONTROL OK]**:

   **Controllo eventi di User Manager:** Selezionare questa opzione per abilitare il controllo degli eventi di sincronizzazione delle directory e degli eventi di autenticazione, quali esito positivo, errore e blocco. Per impostazione predefinita, questa opzione è selezionata solo se è stato installato un componente che richiede il controllo, ad esempio Rights Management. Questa impostazione aggiorna la chiave di ingresso `APSAuditService` nel file di configurazione.

   **Creazione automatica gruppo dinamico:** consente la creazione automatica di gruppi dinamici basati sui domini e-mail. (Vedi [Creare un gruppo dinamico](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group).)

È inoltre possibile ripristinare le impostazioni originali di Gestione utenti facendo clic su Ricarica.
