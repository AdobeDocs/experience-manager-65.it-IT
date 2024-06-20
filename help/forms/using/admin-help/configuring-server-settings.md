---
title: Configurazione delle impostazioni del server
description: La pagina Impostazioni server consente di accedere alle impostazioni di notifica e-mail, attività e amministratore.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '2631'
ht-degree: 0%

---

# Configurazione delle impostazioni del server {#configuring-server-settings}

La pagina Impostazioni server consente di accedere a varie impostazioni per il flusso di lavoro dei moduli:

* **Impostazioni e-mail** che abilitano i messaggi e-mail in uscita, insieme alle impostazioni del server e-mail utilizzate per tali messaggi. (vedere [Configurazione delle impostazioni e-mail](configuring-server-settings.md#configuring-email-settings).)
* **Impostazioni notifica attività** che abilitano, disabilitano o modificano i messaggi inviati tramite notifiche e-mail a utenti e gruppi finali in relazione alle loro attività. (vedere [Configurazione delle notifiche per utenti e gruppi](configuring-server-settings.md#configuring-notifications-for-users-and-groups).)
* **Impostazioni delle notifiche per gli amministratori** che abilitano, disabilitano o modificano i messaggi inviati nelle notifiche e-mail per le attività amministrative. (vedere [Configurazione delle notifiche per gli amministratori](configuring-server-settings.md#configuring-notifications-for-administrators).)

## Configurazione delle impostazioni e-mail {#configuring-email-settings}

È possibile specificare un account di posta elettronica per Forms Server, tramite il quale inviare messaggi di posta elettronica agli utenti e agli amministratori di AEM Forms. Questi messaggi e-mail vengono utilizzati per notificare e ricordare agli utenti le attività che devono completare, notificare all’utente le attività che hanno raggiunto una scadenza e notificare all’amministratore eventuali errori di processo che si verificano.

Per abilitare l’invio di messaggi e-mail tra i moduli AEM e gli utenti, configura le impostazioni e-mail in uscita nella pagina Impostazioni e-mail. L&#39;e-mail in uscita deve utilizzare un server SMTP.

Per consentire ai moduli AEM di ricevere e gestire i messaggi e-mail in arrivo dagli utenti, creare un endpoint e-mail per il servizio Attività completa. (vedere [Creare un endpoint e-mail per il servizio Attività completa](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)).

Se i processi sono progettati e implementati senza richiedere l’invio di e-mail, non è necessario configurare alcuna delle opzioni nella pagina Impostazioni e-mail.

### Configurare le impostazioni e-mail in uscita {#configure-outgoing-email-settings}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro moduli > Impostazioni server > Impostazioni e-mail.
1. Selezionare Abilita messaggi in uscita.
1. Nella casella Server SMTP digitare il nome o l&#39;indirizzo IP del server di posta elettronica. Tutti i messaggi e-mail di notifica provenienti dal flusso di lavoro dei moduli vengono inviati da questo server e-mail.
1. Nelle caselle Nome utente e Password digitare il nome di accesso e la password da utilizzare quando il server SMTP richiede l&#39;autenticazione. Lasciale vuoto se è consentito l&#39;accesso anonimo.
1. Nella casella Indirizzo e-mail digitare l&#39;indirizzo e-mail da utilizzare come indirizzo di ritorno per i messaggi e-mail inviati da Forms Workflow.

   >[!NOTE]
   >
   >Se si utilizza Microsoft Exchange Server e l&#39;indirizzo e-mail è un indirizzo e-mail non valido, il server Microsoft Exchange non riesce a inviare un messaggio e-mail alle liste di distribuzione. Per risolvere il problema, selezionare **Abilita comunicazione esterna** separatamente per ogni lista di distribuzione sul server Microsoft Exchange.

1. Fai clic su Salva.

>[!NOTE]
>
>Se si immettono informazioni non corrette, è possibile fare clic su Annulla per tornare alla pagina visualizzata in precedenza.

### Configurazione dei modelli e-mail per l’utilizzo di AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione con moduli AEM.

Per impostazione predefinita, le e-mail inviate dai moduli AEM contengono collegamenti a (obsoleto per i moduli AEM su JEE) Flex Workspace. Puoi configurare i moduli AEM per inviare e-mail con collegamenti ad AEM Forms Workspace. Per ulteriori informazioni sui vantaggi di AEM Forms Workspace rispetto a (obsoleto per i moduli AEM su JEE) Flex Workspace, consulta [questo](/help/forms/using/features-html-workspace-available-flex.md) articolo.

1. Nella console di amministrazione, fai clic su Home > Servizi > Flusso di lavoro moduli > Impostazioni server > Notifiche attività.
1. Aprire il modello di assegnazione delle attività.
1. Nelle notifiche delle attività, imposta il modello come segue: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configurazione delle notifiche per utenti e gruppi {#configuring-notifications-for-users-and-groups}

Nella pagina Notifica attività è possibile configurare i modelli utilizzati dal flusso di lavoro dei moduli per generare le notifiche e-mail inviate a utenti e gruppi. È possibile personalizzare e formattare le notifiche utilizzando le variabili del flusso di lavoro dei moduli.

Puoi configurare i seguenti tipi di notifiche per utenti e gruppi:

* promemoria
* assegnazioni attività
* scadenze

Per generare notifiche e-mail per un gruppo, specifica un indirizzo e-mail per il gruppo in Gestione utente. <!--Fix broken link See Setting up and organizing users -->Quando il flusso di lavoro Forms invia una notifica e-mail a un gruppo, la notifica e-mail viene inviata a ogni membro del gruppo che ha un indirizzo e-mail specificato. Quando un membro del gruppo riceve una notifica e-mail e desidera richiedere l’attività, deve fare clic sul collegamento attestazione nella notifica e-mail, che apre la pagina dei dettagli dell’attività in Workspace. Da questo punto, il membro può richiedere o richiedere e aprire l&#39;elemento di lavoro.

>[!NOTE]
>
>Flex Workspace è obsoleto per il rilascio di moduli AEM.

### Configurare i promemoria per utenti o gruppi {#configure-reminders-for-users-or-groups}

È possibile inviare notifiche di promemoria all&#39;utente o al gruppo assegnato quando si avvicina una scadenza per il completamento di un&#39;attività. Le regole per determinare esattamente quando viene inviata una notifica di promemoria sono determinate dallo sviluppatore del processo.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Impostazioni server > Notifiche attività.
1. In Tipo notifica fare clic su Promemoria (per utenti) o Gruppo - Promemoria (per gruppi).
1. Selezionare Abilita promemoria o Abilita gruppo - Promemoria.
1. (Solo notifiche utente) Per includere un allegato del modulo e i relativi dati con il messaggio e-mail di promemoria, selezionare Includi dati modulo.
1. Nella casella Oggetto digitare il testo per la riga dell&#39;oggetto del messaggio di posta elettronica. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, vedi [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica digitare il testo del corpo del messaggio di posta elettronica. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, vedi [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell&#39;elenco Formato messaggio selezionare il formato di invio del messaggio di posta elettronica, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Configurare le notifiche di assegnazione delle attività per utenti o gruppi {#configure-task-assignment-notifications-for-users-or-groups}

È possibile inviare notifiche di assegnazione delle attività a un utente o a un gruppo quando viene assegnata un&#39;attività.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Impostazioni server > Notifiche attività.
1. In Tipo notifica fare clic su Assegnazione attività per utenti o su Gruppo - Assegnazione attività per gruppi.
1. Selezionare Abilita assegnazione attività per gli utenti o Abilita gruppo - Assegnazione attività per i gruppi.
1. (Solo notifiche utente) Per includere un allegato del modulo e i relativi dati con il messaggio e-mail di assegnazione delle attività, selezionare Includi dati modulo.
1. Nella casella Oggetto digitare il testo per la riga dell&#39;oggetto del messaggio di posta elettronica. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, vedi [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica digitare il testo del corpo del messaggio di posta elettronica. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, vedi [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell&#39;elenco Formato messaggio selezionare il formato di invio del messaggio di posta elettronica, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Configurare le notifiche di scadenza per utenti o gruppi {#configure-deadline-notifications-for-users-or-groups}

Puoi inviare notifiche di scadenza a utenti e gruppi una volta passata la scadenza per agire su un’attività assegnata. Una notifica di scadenza è in genere informativa perché l’utente non può più agire sull’attività assegnata.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Impostazioni server > Notifiche attività.
1. In Tipo di notifica, fai clic su Scadenza (per gli utenti) o Gruppo - Scadenza (per i gruppi).
1. Seleziona Abilita scadenza o Abilita gruppo - Scadenza.
1. Nella casella Oggetto digitare il testo per la riga dell&#39;oggetto del messaggio di posta elettronica. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, vedi [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica digitare il testo del corpo del messaggio di posta elettronica. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, vedi [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell&#39;elenco Formato messaggio selezionare il formato di invio del messaggio di posta elettronica, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Nascondi il tag DO NOT DELETE per tutte le e-mail {#hide-the-do-not-delete-tag-for-all-emails}

Puoi configurare l’e-mail in modo che venga nascosta al tag di tracciamento DO NOT DELETE in tutte le e-mail inviate con un processo incentrato sulla persona.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## Configurazione delle notifiche per gli amministratori {#configuring-notifications-for-administrators}

È possibile configurare i modelli utilizzati dal flusso di lavoro dei moduli per generare le notifiche e-mail inviate agli amministratori.

Puoi configurare i seguenti tipi di notifiche per gli amministratori:

* ramo bloccato
* operazione in stallo

### Configurare le notifiche di ramo bloccate {#configure-stalled-branch-notifications}

Se un ramo si arresta (smette di procedere deliberatamente o a causa di un errore), puoi inviare una notifica e-mail a un amministratore o a un altro utente, che può quindi indagare sul problema.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Impostazioni server > Notifiche per gli amministratori.
1. In Tipo notifica fare clic su Ramo bloccato.
1. Selezionare Abilita ramo bloccato.
1. Nella casella Indirizzo e-mail, digita gli indirizzi degli utenti a cui inviare una notifica quando un ramo si blocca. Utilizza il formato user@domain.com e separa ogni indirizzo con una virgola. In genere, questo indirizzo e-mail è per un amministratore.
1. Nella casella Oggetto digitare il testo per la riga dell&#39;oggetto del messaggio di posta elettronica. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, vedi [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica digitare il testo del corpo del messaggio di posta elettronica. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, vedi [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell&#39;elenco Formato messaggio selezionare il formato di invio del messaggio di posta elettronica, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Configurare le notifiche di operazioni bloccate {#configure-stalled-operation-notifications}

Se un&#39;operazione si arresta (interrompe l&#39;operazione deliberatamente o a causa di un errore), è possibile che venga inviata una notifica e-mail a un amministratore o a un altro utente, che può analizzare il problema.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro di Forms > Impostazioni server > Notifiche per gli amministratori.
1. In Tipo notifica fare clic su Operazione bloccata.
1. Selezionare Abilita operazione bloccata.
1. Nella casella Indirizzi e-mail digitare gli indirizzi degli utenti a cui inviare una notifica quando un&#39;operazione viene interrotta. Utilizza il formato user@domain.com e separa ogni indirizzo con una virgola. In genere, questo indirizzo e-mail è per un amministratore.
1. Nella casella Oggetto digitare il testo per la riga dell&#39;oggetto del messaggio di posta elettronica. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, vedi [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications)
1. Nella casella Modello notifica digitare il testo del corpo del messaggio di posta elettronica. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, vedi [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Fai clic su Salva.

## Personalizzazione del contenuto delle notifiche {#customizing-the-content-of-notifications}

Le pagine Notifiche attività e Notifiche amministratore offrono diverse funzioni che consentono di personalizzare i messaggi di notifica:

* editor rich text
* selettore variabili
* Generazione URL

### Editor Rich Text {#rich-text-editor}

L’area Modello notifica è un editor Rich Text che consente di generare HTML per i messaggi di notifica e-mail. Fornisce le opzioni di formattazione del carattere e del paragrafo che si trovano sotto la casella Modello di notifica. Le opzioni disponibili includono tipo di carattere, dimensioni, stile e colore, allineamento dei paragrafi e punti elenco.

### Generazione URL {#url-generation}

Solo per le notifiche di attività, il flusso di lavoro di Forms include due configurazioni di URL predefinite che è possibile trascinare dall&#39;elenco Generazione URL nella casella Modello di notifica e quindi personalizzare:

* OpenTask è disponibile per i tipi di notifica Promemoria e Assegnazione task. Questo URL fornisce un collegamento all’attività in Workspace, consentendo all’utente di accedere rapidamente all’attività dalla notifica e-mail. Quando si trascina l&#39;URL OpenTask nella casella Modello di notifica, l&#39;URL viene visualizzato nel formato seguente:

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask è disponibile per i tipi di notifica Gruppo - Promemoria e Gruppo - Assegnazione attività. Questo URL fornisce un collegamento alla pagina dei dettagli dell’attività in Workspace, in cui l’utente può inviare una richiesta di risarcimento o inoltrarla e aprire l’elemento di lavoro. Quando si trascina l&#39;URL ClaimTask nella casella Modello notifica, l&#39;URL viene visualizzato nel formato seguente:

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace è obsoleto per il rilascio di moduli AEM.

Se la soluzione viene distribuita in un ambiente cluster, sostituire `@@notification-host@@` con l&#39;indirizzo del cluster.

`<`*PORTA* `>` è il numero di porta del listener HTTP per il server applicazioni. La porta del listener HTTP predefinita per i server applicazioni supportati è la seguente:

**JBoss:** 8080

**Oracle di server WebLogic:** 7001

**IBM WebSphere:** 9080

Per far funzionare questi URL correttamente, sostituisci `<`*PORTA* `>` con il numero di porta appropriato per l’ambiente in uso.

>[!NOTE]
>
>Se utilizzi un’applicazione web personalizzata diversa da Forms per consentire agli utenti di accedere alle attività, devi utilizzare un formato URL appropriato per l’applicazione personalizzata.

### Selettore variabili {#variable-picker}

L&#39;elenco Selettore variabili fornisce variabili utili che è possibile trascinare nelle caselle Oggetto o Modello di notifica. Quando si rilascia una variabile nelle caselle Oggetto o Modello di notifica, questa viene modificata nel nome effettivo della variabile del flusso di lavoro dei moduli con due simboli @ su entrambi i lati, ad esempio `@@taskid@@`.

Per i promemoria, le assegnazioni di attività e le scadenze per utenti e gruppi, è possibile utilizzare le seguenti variabili nelle caselle Oggetto e Modello di notifica:

**descrizione** Contenuto della proprietà Description, come definito nel passaggio utente (punto iniziale, operazione Assegna task o operazione Assegna più task) del processo in Workbench.

**istruzioni** Contenuto della proprietà Istruzioni attività, come definito nel passaggio utente del processo in Workbench.

**notification-host** Il nome host del server applicazioni AEM forms.

**process-name** Nome del processo.

**operation-name** Nome del passaggio.

**taskid** Identificatore univoco dell&#39;attività corrente.

**azioni** Produce un elenco numerato di route valide (ad esempio, Approva, Rifiuta) su cui il destinatario può fare clic.

Inoltre, per i promemoria del gruppo, le assegnazioni delle attività del gruppo e le scadenze del gruppo, è possibile utilizzare anche:

**group-name** Nome del gruppo a cui è assegnato l&#39;elemento di lavoro.

>[!NOTE]
>
>Se una variabile non ha un valore, non viene restituito nulla.

Per i rami in stallo, è possibile utilizzare le seguenti variabili nelle caselle Oggetto e Modello di notifica:

**branch-id** Identificatore della filiale.

**process-id** Identificatore dell&#39;istanza del processo.

**notification-host** Il nome host del server applicazioni AEM forms.

Per le operazioni in stallo, è possibile utilizzare le seguenti variabili nelle caselle Oggetto e Modello di notifica:

**action-id** L’identificatore dell’operazione.

**branch-id** Identificatore della filiale.

**process-id** Identificatore dell&#39;istanza del processo.

**notification-host** Il nome host del server applicazioni AEM forms.

### Utilizzo di una variabile nella casella Oggetto {#using-a-variable-in-the-subject-box}

Se si digita il testo seguente nella casella Oggetto per le notifiche di assegnazione delle attività:

`Please complete task @@taskid@@`

L’utente riceve un messaggio e-mail con il seguente oggetto se gli è stata assegnata l’attività 376:

`Please complete task 376`

### Utilizzo delle variabili nella casella Modello di notifica {#using-variables-in-the-notification-template-box}

Se si digita il testo seguente nella casella Modello di notifica per le notifiche di diramazione bloccata:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

Se il numero di filiale è 4868 e il nome del server è `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configurazione delle connessioni di Business Activity Monitoring {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring, un modulo opzionale, fornisce una serie di dashboard operativi che forniscono visibilità in tempo reale sulle operazioni e sugli indicatori di prestazioni chiave.

Nella pagina Impostazioni configurazione BAM impostare le connessioni al server che esegue BAM in modo che gli eventi correlati al processo possano essere tracciati e trasmessi a tale server.

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro di Forms > Impostazioni server > Impostazioni configurazione BAM.
1. Nella casella Host BAM digitare il nome del server che esegue BAM. L&#39;impostazione predefinita è localhost.
1. Nella casella Porta BAM digitare la porta da utilizzare per la connessione al server che esegue BAM. La porta BAM predefinita per JBoss è 8080, WebLogic 7001 e WebSphere 9080.
1. Nella casella Host server digitare il nome o l&#39;indirizzo IP dell&#39;host Forms Server. Il valore predefinito è localhost.
1. Nella casella Porta server digitare il numero di porta utilizzato dal server Forms.
1. Nelle caselle Nome utente e Password digitare l&#39;ID utente e la password appropriati per accedere al server BAM. Il nome utente predefinito è CognosNowAdmin e la password predefinita è manager.
1. Fai clic su Salva.
