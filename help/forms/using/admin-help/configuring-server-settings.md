---
title: Configurazione delle impostazioni del server
seo-title: Configuring Server Settings
description: La pagina Impostazioni server consente di accedere alle impostazioni di e-mail, notifica delle attività e notifica da parte dell’amministratore.
seo-description: The Server Settings page provides access to email, task notification and administrator notification settings.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '2625'
ht-degree: 0%

---

# Configurazione delle impostazioni del server {#configuring-server-settings}

La pagina Impostazioni server consente di accedere a varie impostazioni per il flusso di lavoro dei moduli:

* **Impostazioni e-mail** che abilitano i messaggi e-mail in uscita, insieme alle impostazioni del server e-mail utilizzate per tali messaggi. (Vedi [Configurazione delle impostazioni e-mail](configuring-server-settings.md#configuring-email-settings).)
* **Impostazioni di notifica attività** che attivano, disattivano o modificano i messaggi inviati nelle notifiche e-mail agli utenti e ai gruppi finali relativi alle loro attività. (Vedi [Configurazione delle notifiche per utenti e gruppi](configuring-server-settings.md#configuring-notifications-for-users-and-groups).)
* **Impostazioni delle notifiche dell&#39;amministratore** che consentono, disattivano o modificano i messaggi inviati nelle notifiche e-mail per le attività amministrative. (Vedi [Configurazione delle notifiche per gli amministratori](configuring-server-settings.md#configuring-notifications-for-administrators).)

## Configurazione delle impostazioni e-mail {#configuring-email-settings}

È possibile specificare un account e-mail per il server dei moduli, tramite il quale invia messaggi e-mail agli utenti e agli amministratori AEM moduli. Questi messaggi e-mail vengono utilizzati per informare e ricordare agli utenti le attività che devono completare, informare l’utente delle attività che hanno raggiunto una scadenza e segnalare all’amministratore eventuali errori di processo che si verificano.

Per abilitare l’invio di messaggi e-mail tra AEM moduli e utenti, configura le impostazioni e-mail in uscita nella pagina Impostazioni e-mail. L’e-mail in uscita deve utilizzare un server SMTP.

Per consentire AEM moduli di ricevere e gestire i messaggi e-mail in arrivo dagli utenti, creare un endpoint e-mail per il servizio Attività completa. (Vedi [Creare un endpoint e-mail per il servizio Attività completa](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)).

Se i tuoi processi sono progettati e implementati senza richiedere e-mail, non è necessario configurare alcuna delle opzioni nella pagina Impostazioni e-mail.

### Configurare le impostazioni e-mail in uscita {#configure-outgoing-email-settings}

1. Nella console di amministrazione, fai clic su Servizi > flusso di lavoro moduli > Impostazioni server > Impostazioni e-mail.
1. Selezionare Abilita messaggi in uscita.
1. Nella casella Server SMTP digitare il nome del server di posta elettronica o l&#39;indirizzo IP. Tutti i messaggi e-mail di notifica dal flusso di lavoro dei moduli vengono inviati da questo server e-mail.
1. Nelle caselle Nome utente e Password digitare il nome di accesso e la password da utilizzare quando il server SMTP richiede l’autenticazione. Lasciali vuoti se è consentito l’accesso anonimo.
1. Nella casella Indirizzo e-mail digitare l’indirizzo e-mail da utilizzare come indirizzo di ritorno per i messaggi e-mail inviati dal flusso di lavoro dei moduli.

   >[!NOTE]
   >
   >Se si utilizza Microsoft Exchange Server e l&#39;indirizzo e-mail è un indirizzo e-mail non valido, il server Microsoft Exchange non riesce a inviare un&#39;e-mail alle liste di distribuzione. Per risolvere il problema, seleziona la **Abilita comunicazione esterna** separatamente per ogni elenco di distribuzione sul server Microsoft Exchange.

1. Fai clic su Salva.

>[!NOTE]
>
>Se si immettono informazioni errate, è possibile fare clic su Annulla per tornare alla pagina visualizzata in precedenza.

### Configurazione dei modelli e-mail per l’utilizzo di AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM versione dei moduli.

Per impostazione predefinita, le e-mail inviate da AEM moduli contengono collegamenti a (obsoleto per i moduli AEM su JEE) Flex Workspace. È possibile configurare AEM moduli per l’invio di e-mail con collegamenti ad AEM Forms Workspace. Per ulteriori informazioni sui vantaggi di AEM Forms Workspace rispetto a (obsoleto per i moduli AEM su JEE) Flex Workspace, consulta [questo](/help/forms/using/features-html-workspace-available-flex.md) articolo.

1. Nella console di amministrazione, fai clic su Home > Servizi > flusso di lavoro moduli > Impostazioni server > Notifiche attività.
1. Aprire il modello di assegnazione delle attività.
1. Imposta il modello nelle notifiche delle attività come segue: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configurazione delle notifiche per utenti e gruppi {#configuring-notifications-for-users-and-groups}

Nella pagina Notifica attività è possibile configurare modelli che il flusso di lavoro dei moduli utilizzerà per generare le notifiche e-mail inviate a utenti e gruppi. Puoi personalizzare e formattare le notifiche utilizzando le variabili del flusso di lavoro dei moduli.

Puoi configurare i seguenti tipi di notifiche per utenti e gruppi:

* promemoria
* assegnazioni di task
* scadenze

Per generare notifiche e-mail per un gruppo, specifica un indirizzo e-mail per il gruppo in Gestione utente. <!--Fix broken link See Setting up and organizing users -->Quando il flusso di lavoro dei moduli invia una notifica e-mail a un gruppo, ogni membro del gruppo con un indirizzo e-mail specificato riceve la notifica e-mail. Quando un membro del gruppo riceve una notifica e-mail e desidera richiedere l’attività, deve fare clic sul collegamento di richiesta nella notifica e-mail, che apre la pagina dei dettagli dell’attività in Workspace. Da lì, il membro può reclamare o reclamare e aprire l&#39;elemento di lavoro.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM versione dei moduli.

### Configurare i promemoria per utenti o gruppi {#configure-reminders-for-users-or-groups}

È possibile inviare notifiche di promemoria all&#39;utente o al gruppo assegnato quando si avvicina una scadenza per completare un&#39;attività. Le regole per determinare esattamente quando viene inviata una notifica di promemoria sono determinate dallo sviluppatore del processo.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Impostazioni server > Notifiche attività.
1. In Tipo di notifica fare clic su Promemoria (per utenti) o su Promemoria gruppo (per gruppi).
1. Selezionare Abilita promemoria o Abilita gruppo - Promemoria.
1. (Solo notifiche utente) Per includere un allegato del modulo e dei relativi dati con il messaggio e-mail di promemoria, selezionare Includi dati modulo.
1. Nella casella Oggetto digitare il testo relativo all’oggetto del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello di notifica digitare il testo relativo al corpo del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell’elenco Formato messaggio, selezionare il formato in cui viene inviato il messaggio e-mail, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Configurare le notifiche di assegnazione delle attività per utenti o gruppi {#configure-task-assignment-notifications-for-users-or-groups}

È possibile inviare notifiche di assegnazione di attività a un utente o a un gruppo quando viene assegnata un&#39;attività.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Impostazioni server > Notifiche attività.
1. In Tipo di notifica fare clic su Assegnazione task per gli utenti o su Assegnazione gruppo - Task per i gruppi.
1. Selezionare Abilita assegnazione task per gli utenti o Attiva assegnazione gruppo - task per i gruppi.
1. (Solo notifiche utente) Per includere un allegato del modulo e dei relativi dati con il messaggio e-mail di assegnazione dell’attività, selezionare Includi dati modulo.
1. Nella casella Oggetto digitare il testo relativo all’oggetto del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello di notifica digitare il testo relativo al corpo del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell’elenco Formato messaggio, selezionare il formato in cui viene inviato il messaggio e-mail, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Configurare le notifiche di scadenza per utenti o gruppi {#configure-deadline-notifications-for-users-or-groups}

È possibile inviare notifiche di scadenza a utenti e gruppi quando la scadenza per agire in base a un&#39;attività assegnata è passata. Una notifica di scadenza è in genere informativa perché l’utente non può più agire in base all’attività assegnata.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Impostazioni server > Notifiche attività.
1. In Tipo di notifica fare clic su Scadenza (per gli utenti) o Scadenza gruppo (per i gruppi).
1. Selezionare Abilita scadenza o Abilita scadenza gruppo.
1. Nella casella Oggetto digitare il testo relativo all’oggetto del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello di notifica digitare il testo relativo al corpo del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell’elenco Formato messaggio, selezionare il formato in cui viene inviato il messaggio e-mail, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Nascondi il tag NON DELETE per tutte le e-mail {#hide-the-do-not-delete-tag-for-all-emails}

Puoi configurare l’e-mail in modo che si nasconda al tag di tracciamento NON DELETE in tutte le e-mail inviate in un processo incentrato sull’uomo.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## Configurazione delle notifiche per gli amministratori {#configuring-notifications-for-administrators}

Puoi configurare modelli che il flusso di lavoro dei moduli utilizzerà per generare le notifiche e-mail inviate agli amministratori.

Puoi configurare i seguenti tipi di notifiche per gli amministratori:

* ramo bloccato
* funzionamento in stallo

### Configurare le notifiche dei rami in stallo {#configure-stalled-branch-notifications}

Se un ramo si arresta (smette di procedere deliberatamente o a causa di un errore), puoi far inviare una notifica e-mail a un amministratore o a un altro utente, che può quindi indagare il problema.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Impostazioni server > Notifiche per l’amministratore.
1. In Tipo di notifica fare clic su Ramo bloccato.
1. Selezionare Abilita diramazione bloccata.
1. Nella casella Indirizzo e-mail, digitare gli indirizzi degli utenti da avvisare quando un ramo si arresta. Usa il formato user@domain.com e separa ogni indirizzo con una virgola. In genere, questo indirizzo e-mail è riservato a un amministratore.
1. Nella casella Oggetto digitare il testo relativo all’oggetto del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello di notifica digitare il testo relativo al corpo del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell’elenco Formato messaggio, selezionare il formato in cui viene inviato il messaggio e-mail, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, seleziona il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fai clic su Salva.

### Configurare le notifiche delle operazioni in stallo {#configure-stalled-operation-notifications}

Se un&#39;operazione si arresta (smette di procedere deliberatamente o a causa di un errore), puoi chiedere a un amministratore o a un altro utente di inviare una notifica e-mail per indagare sul problema.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Impostazioni server > Notifiche per l’amministratore.
1. In Tipo di notifica fare clic su Operazione bloccata.
1. Selezionare Abilita operazione bloccata.
1. Nella casella Indirizzi e-mail, digitare gli indirizzi degli utenti da avvisare quando un&#39;operazione si arresta. Usa il formato user@domain.com e separa ogni indirizzo con una virgola. In genere, questo indirizzo e-mail è riservato a un amministratore.
1. Nella casella Oggetto digitare il testo relativo all’oggetto del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications)
1. Nella casella Modello di notifica digitare il testo relativo al corpo del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consulta [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Fai clic su Salva.

## Personalizzazione del contenuto delle notifiche {#customizing-the-content-of-notifications}

Le pagine Notifiche attività e Notifiche per l’amministratore forniscono diverse funzioni che ti consentono di personalizzare i messaggi di notifica:

* editor Rich Text
* selettore variabile
* Generazione URL

### Editor Rich Text {#rich-text-editor}

L’area Modello notifiche è un editor Rich Text che consente di generare HTML per i messaggi di notifica e-mail. Fornisce opzioni di formattazione per i font e i paragrafi, disponibili sotto la casella Modello di notifica. Le opzioni disponibili sono tipo di font, dimensioni, stile e colore, allineamento del paragrafo e punti elenco.

### Generazione URL {#url-generation}

Solo per le notifiche delle attività, il flusso di lavoro Forms include due configurazioni URL predefinite che è possibile trascinare dall’elenco Generazione URL nella casella Modello di notifica e quindi personalizzare:

* OpenTask è disponibile per i tipi di notifica Promemoria e Assegnazione task. Questo URL fornisce un collegamento all’attività in Workspace, che consente all’utente di accedere rapidamente all’attività dalla notifica e-mail. Quando si trascina l&#39;URL OpenTask nella casella Modello di notifica, l&#39;URL si presenta nel seguente formato:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask è disponibile per i tipi di notifica Gruppo - Promemoria e Gruppo - Assegnazione task. Questo URL fornisce un collegamento alla pagina dei dettagli dell’attività in Workspace, in cui l’utente può reclamare o reclamare e aprire l’elemento di lavoro. Quando si trascina l&#39;URL dell&#39;attività di attestazione nella casella Modello di notifica, l&#39;URL si presenta nel formato seguente:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM versione dei moduli.

Se la soluzione viene distribuita in un ambiente cluster, sostituisci `@@notification-host@@` con l&#39;indirizzo del cluster.

`<`*PORTA* `>` è il numero di porta del listener HTTP per l&#39;application server. La porta del listener HTTP predefinita per i server applicazioni supportati è la seguente:

**JBoss:** 8080

**Server WebLogic Oracle:** 7001

**IBM WebSphere:** 9080

Affinché questi URL funzionino correttamente, sostituisci `<`*PORTA* `>` con il numero di porta appropriato per l&#39;ambiente.

>[!NOTE]
>
>Se utilizzi un’applicazione Web personalizzata diversa da Forms per fornire agli utenti l’accesso alle attività, devi invece utilizzare un formato URL appropriato per l’applicazione personalizzata.

### Selettore variabile {#variable-picker}

L’elenco Selezione variabili fornisce variabili utili che è possibile trascinare nelle caselle Oggetto o Modello di notifica. Quando si rilascia una variabile nelle caselle Oggetto o Modello di notifica, viene modificato il nome della variabile del flusso di lavoro dei moduli effettivi con due simboli @ su entrambi i lati, ad esempio: `@@taskid@@`.

Per promemoria, assegnazioni di attività e scadenze per utenti e gruppi, è possibile utilizzare le seguenti variabili nelle caselle Oggetto e Modello di notifica:

**descrizione** Contenuto della proprietà Description, come definito nel passaggio utente (punto iniziale, operazione Assegna attività o operazione Assegna più attività) del processo in Workbench.

**istruzioni** Contenuto della proprietà Istruzioni attività, come definito nel passaggio utente del processo in Workbench.

**notification-host** Il nome host del server dell&#39;applicazione AEM forms .

**nome del processo** Nome del processo.

**nome operativo** Nome del passaggio.

**asino** Identificatore univoco per l&#39;attività corrente.

**azioni** Genera un elenco numerato di percorsi validi (ad esempio Approva, Rifiuta) su cui il destinatario può fare clic.

Inoltre, per i promemoria di gruppo, le assegnazioni di task di gruppo e le scadenze di gruppo, è possibile utilizzare:

**nome gruppo** Nome del gruppo a cui viene assegnato l&#39;elemento di lavoro.

>[!NOTE]
>
>Se una variabile non ha alcun valore, non viene restituito nulla.

Per i rami bloccati, è possibile utilizzare le seguenti variabili nelle caselle Oggetto e Modello di notifica:

**branch-id** Identificatore del ramo.

**process-id** Identificatore dell&#39;istanza del processo.

**notification-host** Il nome host del server dell&#39;applicazione AEM forms .

Per le operazioni in stallo, è possibile utilizzare le seguenti variabili nelle caselle Oggetto e Modello di notifica:

**action-id** Identificatore dell&#39;operazione.

**branch-id** Identificatore del ramo.

**process-id** Identificatore dell&#39;istanza del processo.

**notification-host** Il nome host del server dell&#39;applicazione AEM forms .

### Uso di una variabile nella casella Oggetto {#using-a-variable-in-the-subject-box}

Se si digita il testo seguente nella casella Oggetto per le notifiche Assegnazione task:

`Please complete task @@taskid@@`

L’utente riceve un messaggio e-mail con l’oggetto seguente se gli è stato assegnato l’attività 376:

`Please complete task 376`

### Uso delle variabili nella casella Modello di notifica {#using-variables-in-the-notification-template-box}

Se si digita il testo seguente nella casella Modello di notifica per le notifiche di diramazione bloccata:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

L’amministratore riceve un messaggio e-mail contenente il seguente contenuto se il numero del ramo è 4868 e il nome del server è `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configurazione delle connessioni di monitoraggio delle attività aziendali {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring, un modulo opzionale, fornisce una serie di dashboard operativi che offrono visibilità in tempo reale nelle operazioni e negli indicatori di prestazioni chiave.

Nella pagina Impostazioni di configurazione BAM impostare le connessioni al server che esegue BAM in modo che gli eventi relativi al processo possano essere tracciati e trasmessi a tale server.

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro Forms > Impostazioni server > Impostazioni di configurazione BAM.
1. Nella casella Host BAM digitare il nome del server che esegue BAM. Il valore predefinito è localhost.
1. Nella casella Porta BAM digitare la porta da utilizzare per la connessione al server che esegue BAM. La porta BAM predefinita per JBoss è 8080, WebLogic è 7001 e WebSphere è 9080.
1. Nella casella Host server digitare il nome o l&#39;indirizzo IP del server dei moduli host. Il valore predefinito è localhost.
1. Nella casella Porta server digitare il numero di porta utilizzato dal server dei moduli.
1. Nelle caselle Nome utente e Password digitare l&#39;ID utente e la password appropriati per accedere al server BAM. Il nome utente predefinito è CognosNowAdmin e la password predefinita è manager.
1. Fai clic su Salva.
