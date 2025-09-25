---
title: ' Configurazione delle impostazioni del server'
description: La pagina Impostazioni server consente di accedere alle impostazioni di notifica e-mail, attività e amministratore.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '2643'
ht-degree: 100%

---

# Configurazione delle impostazioni del server {#configuring-server-settings}

La pagina Impostazioni server consente di accedere a varie impostazioni per Forms Workflow:

* **Impostazioni e-mail** che abilitano i messaggi e-mail in uscita, insieme alle impostazioni del server e-mail utilizzate per tali messaggi. Consulta [Configurazione delle impostazioni e-mail](configuring-server-settings.md#configuring-email-settings).
* **Impostazioni notifica attività** che attivano, disabilitano o modificano i messaggi inviati tramite notifiche e-mail a utenti e gruppi finali in relazione alle loro attività. Consulta [Configurazione delle notifiche per utenti e gruppi](configuring-server-settings.md#configuring-notifications-for-users-and-groups).
* **Impostazioni notifiche amministratore** che attivano, disattivano o modificano i messaggi inviati nelle notifiche e-mail per le attività amministrative. Consulta [Configurazione delle notifiche per gli amministratori](configuring-server-settings.md#configuring-notifications-for-administrators).

## Configurazione delle impostazioni e-mail {#configuring-email-settings}

È possibile specificare un account di posta elettronica per il server Forms, tramite il quale inviare messaggi di posta elettronica agli utenti e agli amministratori di AEM Forms. Questi messaggi e-mail vengono utilizzati per notificare e ricordare agli utenti le attività che devono completare, notificare le attività che hanno raggiunto una scadenza e notificare all’amministratore eventuali errori di processo che si verificano.

Per abilitare l’invio di messaggi e-mail tra AEM Forms e gli utenti, configura le impostazioni e-mail in uscita nella pagina Impostazioni e-mail. L’e-mail in uscita deve utilizzare un server SMTP.

Per consentire ad AEM Forms di ricevere e gestire i messaggi e-mail in arrivo dagli utenti, è necessario creare un endpoint e-mail per il servizio Completa attività. Consulta [Creare un endpoint e-mail per il servizio Completa attività](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

Se i processi sono progettati e implementati senza richiedere l’invio di e-mail, non è necessario configurare alcuna delle opzioni nella pagina Impostazioni e-mail.

### Configurare le impostazioni delle e-mail in uscita {#configure-outgoing-email-settings}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Impostazioni server > Impostazioni e-mail.
1. Seleziona Abilita messaggi in uscita.
1. Nella casella Server SMTP, digita il nome o l’indirizzo IP del server di posta elettronica. Tutti i messaggi e-mail di notifica provenienti da Forms Workflow vengono inviati da questo server e-mail.
1. Nelle caselle Nome utente e Password, digita il nome di accesso e la password da utilizzare quando il server SMTP richiede l’autenticazione. Lasciale vuote se è consentito l’accesso anonimo.
1. Nella casella Indirizzo e-mail digita l’indirizzo e-mail da utilizzare come indirizzo di ritorno per i messaggi e-mail inviati da Forms Workflow.

   >[!NOTE]
   >
   >Se utilizzi Microsoft Exchange Server e l’indirizzo e-mail non è valido, il server Microsoft Exchange non riesce a inviare un messaggio e-mail agli elenchi di distribuzione. Per risolvere il problema, seleziona l’opzione **Abilita comunicazione esterna** separatamente per ciascuna lista di distribuzione nel server Microsoft Exchange.

1. Fai clic su Salva.

>[!NOTE]
>
>Se immetti informazioni non corrette, puoi fare clic su Annulla per tornare alla pagina visualizzata in precedenza.

### Configurazione dei modelli e-mail per l’utilizzo dell’area di lavoro di AEM Forms {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Per la versione di AEM Forms, l’area di lavoro flessibile è obsoleta.

Per impostazione predefinita, le e-mail inviate da AEM Forms contengono collegamenti all’area di lavoro flessibile (obsoleta per AEM Forms su JEE). Puoi configurare AEM Forms per l’invio di e-mail con collegamenti all’area di lavoro di AEM Forms. Per ulteriori informazioni sui vantaggi dell’area di lavoro di AEM Forms rispetto all’area di lavoro flessibile (obsoleta per AEM Forms su JEE), consulta [questo](/help/forms/using/features-html-workspace-available-flex.md) articolo.

1. Nella console di amministrazione, fai clic su Home > Servizi > Forms Workflow > Impostazioni server > Notifiche attività.
1. Apri il modello di assegnazione delle attività.
1. Imposta il modello nelle notifiche delle attività su: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configurazione delle notifiche per utenti e gruppi {#configuring-notifications-for-users-and-groups}

Nella pagina Notifica attività è possibile configurare i modelli utilizzati da Forms Workflow per generare le notifiche e-mail inviate a utenti e gruppi. È possibile personalizzare e formattare le notifiche utilizzando le variabili di Forms Workflow.

Per utenti e gruppi, puoi configurare le seguenti notifiche:

* promemoria
* assegnazioni attività
* scadenze

Per generare notifiche e-mail per un gruppo, specifica un indirizzo e-mail per il gruppo in Gestione utenti. <!--Fix broken link See Setting up and organizing users -->Quando Forms Workflow invia una notifica e-mail a un gruppo, ogni membro del gruppo che dispone di un indirizzo e-mail specificato la riceva. Quando un membro del gruppo riceve una notifica e-mail e desidera richiedere l’attività, deve fare clic sul relativo collegamento nella notifica e-mail, che apre la pagina dei dettagli dell’attività nell’area di lavoro. Da questo punto, il membro può effettuare una richiesta, oppure effettuare una richiesta e aprire l’elemento di lavoro.

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione di AEM Forms.

### Configurare i promemoria per utenti o gruppi {#configure-reminders-for-users-or-groups}

Quando si avvicina una scadenza per il completamento di un’attività, è possibile inviare notifiche di promemoria all’utente o al gruppo assegnato. Le regole per stabilire con esattezza quando viene inviata una notifica di promemoria sono determinate dallo sviluppatore del processo.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Impostazioni server > Notifiche attività.
1. In Tipo di notifica, fai clic su Promemoria (per utenti) o su Gruppo - Promemoria (per gruppi).
1. Seleziona Abilita promemoria o Abilita gruppo - Promemoria.
1. (Solo notifiche utente) Per includere come allegato il modulo e i relativi dati con il messaggio e-mail di promemoria, seleziona Includi dati modulo.
1. Nella casella Oggetto, digita il testo che desideri inserire come oggetto del messaggio e-mail. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica, digita il testo del corpo del messaggio e-mail. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell’elenco Formato messaggio, seleziona il formato in cui desideri che venga inviato il messaggio e-mail: HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti residenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Configurare le notifiche di assegnazione delle attività per utenti o gruppi {#configure-task-assignment-notifications-for-users-or-groups}

Quando a un utente o a un gruppo viene assegnata un’attività, è possibile inviare loro una notifica di assegnazione dell’attività.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Impostazioni server > Notifiche attività.
1. In Tipo di notifica, fai clic su Assegnazione attività (per singoli utenti) o su Gruppo - Assegnazione attività (per gruppi).
1. Selezionare Abilita Assegnazione attività per i singoli utenti o Abilita Gruppo - Assegnazione attività per i gruppi.
1. (Solo notifiche utente) Per includere come allegato il modulo e i relativi dati con il messaggio e-mail di assegnazione dell’attività, seleziona Includi dati modulo.
1. Nella casella Oggetto, digita il testo che desideri inserire come oggetto del messaggio e-mail. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica, digita il testo del corpo del messaggio e-mail. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell’elenco Formato messaggio, seleziona il formato in cui desideri che venga inviato il messaggio e-mail: HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti residenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Configurare le notifiche di scadenza per utenti o gruppi {#configure-deadline-notifications-for-users-or-groups}

Quando è trascorsa la scadenza per eseguire un’attività assegnata, è possibile inviare notifiche di scadenza a utenti e gruppi. Una notifica di scadenza è solitamente informativa perché l’utente non può più intervenire sull’attività assegnata.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Impostazioni server > Notifiche attività.
1. In Tipo di notifica, fai clic su Scadenza (per singoli utenti) o su Gruppo - Scadenza (per i gruppi).
1. Seleziona Abilita Scadenza o Abilita Gruppo - Scadenza.
1. Nella casella Oggetto, digita il testo che desideri inserire come oggetto del messaggio e-mail. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica, digita il testo del corpo del messaggio e-mail. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell’elenco Formato messaggio, seleziona il formato in cui desideri che venga inviato il messaggio e-mail: HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti residenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Nascondi il tag DO NOT DELETE per tutte le e-mail {#hide-the-do-not-delete-tag-for-all-emails}

Puoi configurare le e-mail in modo da nascondere il tag di tracciamento DO NOT DELETE in tutte le e-mail inviate in un processo incentrato sulla persona.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## Configurazione delle notifiche per gli amministratori {#configuring-notifications-for-administrators}

È possibile configurare i modelli utilizzati da Forms Workflow per generare le notifiche e-mail inviate agli amministratori.

Per gli amministratori, puoi configurare i seguenti tipi di notifiche:

* ramo bloccato
* operazione bloccata

### Configurare le notifiche di ramo bloccato {#configure-stalled-branch-notifications}

Se un ramo si blocca (si interrompe deliberatamente o a causa di un errore), è possibile fare in modo che venga inviata una notifica e-mail a un amministratore o a un altro utente, che potrà quindi indagare sul problema.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Impostazioni server > Notifiche amministratore.
1. In Tipo di notifica, fai clic su Ramo bloccato.
1. Seleziona Abilita Ramo bloccato.
1. Nella casella Indirizzo e-mail, digita gli indirizzi degli utenti a cui inviare una notifica quando si blocca un ramo. Utilizza il formato utente@dominio.com e separa ogni indirizzo con una virgola. In genere, questo indirizzo e-mail è per un amministratore.
1. Nella casella Oggetto, digita il testo che desideri inserire come oggetto del messaggio e-mail. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica, digita il testo del corpo del messaggio e-mail. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell’elenco Formato messaggio, seleziona il formato in cui desideri che venga inviato il messaggio e-mail: HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti residenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Configurare le notifiche di operazione bloccata {#configure-stalled-operation-notifications}

Se un’operazione si blocca (si interrompe deliberatamente o a causa di un errore), è possibile fare in modo che venga inviata una notifica e-mail a un amministratore o a un altro utente, che potrà indagare sul problema.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Impostazioni server > Notifiche amministratore.
1. In Tipo di notifica, fai clic su Operazione bloccata.
1. Seleziona Abilita Operazione bloccata.
1. Nella casella Indirizzi e-mail, digita gli indirizzi degli utenti a cui inviare una notifica quando si blocca un’operazione. Utilizza il formato utente@dominio.com e separa ogni indirizzo con una virgola. In genere, questo indirizzo e-mail è per un amministratore.
1. Nella casella Oggetto, digita il testo che desideri inserire come oggetto del messaggio e-mail. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications)
1. Nella casella Modello notifica, digita il testo del corpo del messaggio e-mail. Questo campo viene precompilato con il testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Fai clic su Salva.

## Personalizzazione del contenuto delle notifiche {#customizing-the-content-of-notifications}

Le pagine Notifiche attività e Notifiche amministratore offrono varie funzionalità che consentono di personalizzare i messaggi di notifica:

* editor rich text
* selettore variabili
* generazione di URL

### Editor rich text {#rich-text-editor}

L’area Modello notifica è un editor rich text che consente di generare HTML per i messaggi di notifica e-mail. Fornisce le opzioni di formattazione del carattere e del paragrafo che si trovano sotto la casella Modello notifica. Le opzioni disponibili includono tipo di carattere, dimensioni, stile e colore, allineamento dei paragrafi e punti elenco.

### generazione di URL {#url-generation}

Solo per le notifiche di attività, Forms Workflow include due configurazioni di URL predefinite che è possibile trascinare dall’elenco di generazione URL nella casella Modello notifica e quindi personalizzare:

* OpenTask è disponibile per i tipi di notifica Promemoria e Assegnazione attività. Questo URL fornisce un collegamento all’attività nell’area di lavoro, consentendo all’utente di accedere rapidamente all’attività dalla notifica e-mail. Trascinando l’URL di OpenTask nella casella Modello notifica, l’URL viene visualizzato nel formato seguente:

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask è disponibile per i tipi di notifica Gruppo - Promemoria e Gruppo - Assegnazione attività. Questo URL fornisce un collegamento alla pagina dei dettagli dell’attività nell’area di lavoro, in cui l’utente può effettuare una richiesta oppure effettuare una richiesta e aprire l’elemento di lavoro. Trascinando l’URL di ClaimTask nella casella Modello notifica, l’URL viene visualizzato nel formato seguente:

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione di AEM Forms.

Se la soluzione viene distribuita in un ambiente cluster, sostituire `@@notification-host@@` con l’indirizzo del cluster.

`<`*PORT* `>` è il numero di porta del listener HTTP per il server applicazioni. La porta del listener HTTP predefinita per i server applicazioni supportati è la seguente:

**JBoss:** 8080

**Oracle WebLogic Server:** 7001

**IBM WebSphere:** 9080

Per garantire il corretto funzionamento di questi URL, sostituisci `<`*PORT* `>` con il numero di porta appropriato per l’ambiente in uso.

>[!NOTE]
>
>Se utilizzi un’applicazione web personalizzata diversa da Forms per consentire agli utenti di accedere alle attività, devi utilizzare un formato URL appropriato per l’applicazione personalizzata.

### Selettore variabili {#variable-picker}

L’elenco Selettore variabili fornisce variabili utili che è possibile trascinare nelle caselle Oggetto o Modello di notifica. Quando rilasci una variabile nelle caselle Oggetto o Modello di notifica, questa viene modificata nel nome effettivo della variabile del flusso di lavoro dei moduli con due simboli @ su entrambi i lati, ad esempio `@@taskid@@`.

Per i promemoria, le assegnazioni di attività e le scadenze per utenti e gruppi, è possibile utilizzare le seguenti variabili nelle caselle Oggetto e Modello di notifica:

**descrizione** Il contenuto della proprietà Descrizione, come definito nel passaggio utente (punto iniziale, operazione Assegna attività o operazione Assegna più attività) del processo in Workbench.

**istruzioni** I contenuti della proprietà Istruzioni attività, come definiti nel passaggio utente del processo in Workbench.

**notification-host** Il nome host del server applicazioni AEM Forms.

**process-name** Il nome del processo.

**operation-name** Il nome del passaggio.

**taskid** L’identificatore univoco dell’attività corrente.

**azioni** Produce un elenco numerato di percorsi validi (ad esempio, Approva, Rifiuta) su cui il destinatario può fare clic.

Inoltre, per i promemoria del gruppo, le assegnazioni delle attività del gruppo e le scadenze del gruppo, è possibile utilizzare anche:

**nome-gruppo** Il nome del gruppo a cui è assegnato l’elemento di lavoro.

>[!NOTE]
>
>Se una variabile non ha un valore, non viene restituito nulla.

Per i rami bloccati, è possibile utilizzare le seguenti variabili nelle caselle Oggetto e Modello di notifica:

**branch-id** L’identificatore del ramo.

**process-id** L’identificatore dell’istanza del processo.

**notification-host** Il nome host del server applicazioni AEM Forms.

Per le operazioni bloccate, è possibile utilizzare le seguenti variabili nelle caselle Oggetto e Modello di notifica:

**action-id** L’identificatore dell’operazione.

**branch-id** L’identificatore del ramo.

**process-id** L’identificatore dell’istanza del processo.

**notification-host** Il nome host del server applicazioni AEM Forms.

### Utilizzo di una variabile nella casella Oggetto {#using-a-variable-in-the-subject-box}

Se digiti il testo seguente nella casella Oggetto per le notifiche di assegnazione delle attività:

`Please complete task @@taskid@@`

L’utente riceve un messaggio e-mail con il seguente oggetto se gli è stata assegnata l’attività 376:

`Please complete task 376`

### Utilizzo delle variabili nella casella Modello di notifica {#using-variables-in-the-notification-template-box}

Se digiti il testo seguente nella casella Modello di notifica per le notifiche di diramazione bloccata:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

L’amministratore riceve un messaggio di posta elettronica con il contenuto seguente se il numero di ramo è 4868 e il nome del server è `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configurazione delle connessioni di Business Activity Monitoring (monitoraggio dell’attività aziendale) {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring, un modulo opzionale, fornisce una serie di dashboard operative che forniscono visibilità in tempo reale sulle operazioni e sugli indicatori di prestazioni chiave.

Nella pagina Impostazioni configurazione BAM imposta le connessioni al server che esegue BAM in modo che gli eventi correlati al processo possano essere tracciati e trasmessi a tale server.

1. Nella console di amministrazione, fai clic su Servizi > Forms workflow > Impostazioni server > Impostazioni configurazione BAM.
1. Nella casella Host BAM digita il nome del server che esegue BAM. Il valore predefinito è localhost.
1. Nella casella Porta BAM digita la porta da utilizzare per la connessione al server che esegue BAM. La porta BAM predefinita per JBoss è 8080, per WebLogic 7001 e per WebSphere 9080.
1. Nella casella Host server digita il nome o l’indirizzo IP dell’host server Forms. Il valore predefinito è localhost.
1. Nella casella Porta server digita il numero di porta utilizzato dal server Forms.
1. Nelle caselle Nome utente e Password digita l’ID utente e la password appropriati per accedere al server BAM. Il nome utente predefinito è CognosNowAdmin e la password predefinita è manager.
1. Fai clic su Salva.
