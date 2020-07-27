---
title: Configurazione delle impostazioni del server
seo-title: Configurazione delle impostazioni del server
description: La pagina Impostazioni server consente di accedere alle impostazioni e-mail, notifica delle attività e notifica da parte dell’amministratore.
seo-description: La pagina Impostazioni server consente di accedere alle impostazioni e-mail, notifica delle attività e notifica da parte dell’amministratore.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2657'
ht-degree: 0%

---


# Configurazione delle impostazioni del server {#configuring-server-settings}

La pagina Impostazioni server consente di accedere alle varie impostazioni del flusso di lavoro dei moduli:

* **Impostazioni** e-mail che abilitano i messaggi e-mail in uscita, insieme alle impostazioni del server e-mail utilizzate per tali messaggi. (See [Configuring email settings](configuring-server-settings.md#configuring-email-settings).)
* **Impostazioni** di notifica delle attività che attivano, disattivano o modificano i messaggi inviati nelle notifiche e-mail agli utenti finali e ai gruppi in merito alle loro attività. Consultate [Configurazione delle notifiche per utenti e gruppi](configuring-server-settings.md#configuring-notifications-for-users-and-groups).
* **Impostazioni** di notifica dell&#39;amministratore che abilitano, disattivano o modificano i messaggi inviati nelle notifiche e-mail per le attività amministrative. Consultate [Configurazione delle notifiche per gli amministratori](configuring-server-settings.md#configuring-notifications-for-administrators).

## Configurazione delle impostazioni e-mail {#configuring-email-settings}

È possibile specificare un account e-mail per il server dei moduli tramite il quale inviare messaggi e-mail agli utenti e agli amministratori dei moduli AEM. Questi messaggi e-mail vengono utilizzati per informare e ricordare agli utenti le attività che devono completare, notificare all’utente le attività che hanno raggiunto una scadenza e notificare all’amministratore eventuali errori di processo che si verificano.

Per abilitare l&#39;invio di messaggi e-mail tra moduli AEM e utenti, configurate le impostazioni e-mail in uscita nella pagina Impostazioni e-mail. L&#39;e-mail in uscita deve utilizzare un server SMTP.

Per consentire ai moduli AEM di ricevere e gestire i messaggi e-mail in arrivo dagli utenti, create un endpoint e-mail per il servizio Attività completa. (vedere [Creare un endpoint e-mail per il servizio](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)Attività completa).

Se i vostri processi sono progettati e implementati senza richiedere e-mail, non dovete configurare alcuna opzione nella pagina Impostazioni e-mail.

### Configurare le impostazioni e-mail in uscita {#configure-outgoing-email-settings}

1. Nella console di amministrazione, fare clic su Servizi > flusso di lavoro moduli > Impostazioni server > Impostazioni e-mail.
1. Selezionate Abilita messaggi in uscita.
1. Nella casella Server SMTP, digitare il nome del server di posta elettronica o l&#39;indirizzo IP. Tutti i messaggi e-mail di notifica provenienti dal flusso di lavoro dei moduli vengono inviati da questo server e-mail.
1. Nelle caselle Nome utente e Password, digitare il nome di login e la password da utilizzare quando il server SMTP richiede l&#39;autenticazione. Lasciateli vuoti se è consentito l’accesso anonimo.
1. Nella casella Indirizzo e-mail, digitare l&#39;indirizzo e-mail da utilizzare come indirizzo di ritorno per i messaggi e-mail inviati dal flusso di lavoro del modulo.

   >[!NOTE]
   >
   >Se si utilizza Microsoft Exchange Server e l&#39;indirizzo e-mail è un indirizzo e-mail non valido, il server di Microsoft Exchange non invia un messaggio e-mail alle liste di distribuzione. Per risolvere il problema, selezionare l&#39;opzione **Abilita comunicazione** esterna separatamente per ogni elenco di distribuzione del server Microsoft Exchange.

1. Fate clic su Salva.

>[!NOTE]
>
>Se si immettono informazioni errate, è possibile fare clic su Annulla per tornare alla pagina visualizzata in precedenza.

### Configurazione dei modelli e-mail per l&#39;utilizzo di AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione dei moduli AEM.

Per impostazione predefinita, le e-mail inviate dai moduli AEM contengono collegamenti a (obsoleto per i moduli AEM su JEE) Flex Workspace. Puoi configurare i moduli AEM per l’invio di e-mail con collegamenti a AEM Forms Workspace. Per ulteriori informazioni sui vantaggi di AEM Forms Workspace (obsoleto per i moduli AEM su JEE) Flex Workspace, consulta [questo](/help/forms/using/features-html-workspace-available-flex.md) articolo.

1. Nella console di amministrazione, fare clic su Home > Servizi > Flusso di lavoro moduli > Impostazioni server > Notifiche attività.
1. Aprire il modello di assegnazione delle attività.
1. Impostate il modello nelle notifiche attività su quanto segue: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configurazione delle notifiche per utenti e gruppi {#configuring-notifications-for-users-and-groups}

Nella pagina Notifica attività è possibile configurare modelli che il flusso di lavoro dei moduli utilizzerà per generare le notifiche e-mail inviate a utenti e gruppi. È possibile personalizzare e formattare le notifiche utilizzando le variabili del flusso di lavoro dei moduli.

Puoi configurare i seguenti tipi di notifiche per utenti e gruppi:

* promemoria
* assegnazioni di task
* scadenze

Per generare le notifiche e-mail per un gruppo, specificate un indirizzo e-mail per il gruppo in Gestione utente. <!--Fix broken link See Setting up and organizing users -->Quando il flusso di lavoro dei moduli invia una notifica e-mail a un gruppo, ogni membro del gruppo con un indirizzo e-mail specificato riceve la notifica e-mail. Quando un membro del gruppo riceve una notifica e-mail e desidera richiedere l’attività, deve fare clic sul collegamento dell’attestazione nella notifica e-mail, che apre la pagina dei dettagli dell’attività in Workspace. Da qui, il membro può reclamare o reclamare e aprire l&#39;elemento di lavoro.

>[!NOTE]
>
>Flex Worksapce è obsoleto per la versione dei moduli AEM.

### Configurare i promemoria per utenti o gruppi {#configure-reminders-for-users-or-groups}

Potete inviare notifiche di promemoria all’utente o al gruppo assegnato quando si avvicina una scadenza per completare un’attività. Le regole per determinare esattamente quando viene inviata una notifica di promemoria sono determinate dallo sviluppatore del processo.

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Impostazioni server > Notifiche attività.
1. In Tipo di notifica, fate clic su Promemoria (per utenti) o su Gruppo - Promemoria (per gruppi).
1. Selezionate Abilita promemoria o Abilita gruppo - Promemoria.
1. (Solo notifiche utente) Per includere un allegato del modulo e dei relativi dati con il messaggio e-mail del promemoria, selezionare Includi dati del modulo.
1. Nella casella Oggetto, digitare il testo per l&#39;oggetto del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consultate [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica, digitate il testo per il corpo del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consultate [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell&#39;elenco Formato messaggio, selezionare il formato in cui viene inviato il messaggio e-mail, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, selezionate il formato di codifica da usare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fate clic su Salva.

### Configurare le notifiche di assegnazione delle attività per utenti o gruppi {#configure-task-assignment-notifications-for-users-or-groups}

È possibile inviare notifiche di assegnazione a un utente o a un gruppo al momento dell&#39;assegnazione di un&#39;attività.

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Impostazioni server > Notifiche attività.
1. In Tipo di notifica, fare clic su Assegnazione task per gli utenti o Gruppo - Assegnazione task per i gruppi.
1. Selezionare Abilita assegnazione task per gli utenti o Abilita gruppo - Assegnazione task per i gruppi.
1. (Solo notifiche utente) Per includere un allegato del modulo e dei relativi dati con il messaggio e-mail di assegnazione delle attività, selezionare Includi dati modulo.
1. Nella casella Oggetto, digitare il testo per l&#39;oggetto del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consultate [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica, digitate il testo per il corpo del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consultate [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell&#39;elenco Formato messaggio, selezionare il formato in cui viene inviato il messaggio e-mail, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, selezionate il formato di codifica da usare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fate clic su Salva.

### Configurare le notifiche di scadenza per gli utenti o i gruppi {#configure-deadline-notifications-for-users-or-groups}

È possibile inviare notifiche di scadenza a utenti e gruppi al termine della scadenza per l&#39;azione in base a un&#39;attività assegnata. Una notifica di scadenza è in genere informativa perché l&#39;utente non può più agire in base all&#39;attività assegnata.

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Impostazioni server > Notifiche attività.
1. In Tipo di notifica, fate clic su Scadenza (per utenti) o Raggruppa - Scadenza (per gruppi).
1. Selezionate Abilita scadenza o Abilita gruppo - Scadenza.
1. Nella casella Oggetto, digitare il testo per l&#39;oggetto del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consultate [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica, digitate il testo per il corpo del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consultate [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell&#39;elenco Formato messaggio, selezionare il formato in cui viene inviato il messaggio e-mail, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, selezionate il formato di codifica da usare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fate clic su Salva.

### Nascondere il tag NON DELETE per tutte le e-mail {#hide-the-do-not-delete-tag-for-all-emails}

Puoi configurare l’e-mail in modo che venga nascosta al tag di tracciamento NON DELETE in tutte le e-mail inviate in un processo incentrato sull’utente. Per informazioni dettagliate, consultate [Come nascondere il tag &#39;DO-NOT-DELETE&#39; con CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html)

## Configurazione delle notifiche per gli amministratori {#configuring-notifications-for-administrators}

È possibile configurare modelli che il flusso di lavoro dei moduli utilizzerà per generare le notifiche e-mail inviate agli amministratori.

Potete configurare i seguenti tipi di notifiche per gli amministratori:

* diramazione in stallo
* operazione in stallo

### Configurare le notifiche dei rami in stallo {#configure-stalled-branch-notifications}

Se un ramo si arresta (interrompe deliberatamente o a causa di un errore), puoi avere una notifica e-mail inviata a un amministratore o a un altro utente, che può quindi esaminare il problema.

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Impostazioni server > Notifiche per l’amministratore.
1. In Tipo di notifica, fare clic su Ramo bloccato.
1. Selezionare Abilita ramo bloccato.
1. Nella casella Indirizzo e-mail, digitate gli indirizzi degli utenti a cui inviare una notifica quando un ramo si ferma. Utilizzate il formato user@domain.com e separate ogni indirizzo con una virgola. In genere, questo indirizzo e-mail è destinato a un amministratore.
1. Nella casella Oggetto, digitare il testo per l&#39;oggetto del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consultate [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nella casella Modello notifica, digitate il testo per il corpo del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consultate [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Nell&#39;elenco Formato messaggio, selezionare il formato in cui viene inviato il messaggio e-mail, HTML o Testo. Il formato predefinito è HTML.
1. Nell’elenco Codifica e-mail, selezionate il formato di codifica da usare per il messaggio e-mail. Il valore predefinito è UTF-8, che la maggior parte degli utenti al di fuori del Giappone utilizza. Gli utenti in Giappone possono selezionare ISO2022-JP.
1. Fate clic su Salva.

### Configurare le notifiche delle operazioni bloccate {#configure-stalled-operation-notifications}

Se un&#39;operazione si arresta (interrompe deliberatamente o a causa di un errore), potete ricevere una notifica e-mail a un amministratore o a un altro utente, che può indagare sul problema.

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Impostazioni server > Notifiche per l’amministratore.
1. In Tipo di notifica, fare clic su Operazione bloccata.
1. Selezionate Abilita operazione bloccata.
1. Nella casella Indirizzi e-mail, digitate gli indirizzi degli utenti a cui inviare la notifica quando un&#39;operazione si arresta. Utilizzate il formato user@domain.com e separate ogni indirizzo con una virgola. In genere, questo indirizzo e-mail è destinato a un amministratore.
1. Nella casella Oggetto, digitare il testo per l&#39;oggetto del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consultate [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications)
1. Nella casella Modello notifica, digitate il testo per il corpo del messaggio e-mail. Questo campo è precompilato con testo predefinito. Per informazioni dettagliate sulla personalizzazione di questo campo, consultate [Personalizzazione del contenuto delle notifiche](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Fate clic su Salva.

## Personalizzazione del contenuto delle notifiche {#customizing-the-content-of-notifications}

Le pagine Notifiche attività e Notifiche amministratori forniscono diverse funzioni che consentono di personalizzare i messaggi di notifica:

* editor Rich Text
* selettore variabile
* Generazione URL

### Rich text editor {#rich-text-editor}

L’area Modello notifica è un editor Rich Text che consente di generare HTML per i messaggi di notifica e-mail. Contiene opzioni di formattazione di font e paragrafo, che si trovano sotto la casella Modello notifica. Le opzioni includono il tipo di font, la dimensione, lo stile e il colore, nonché l&#39;allineamento del paragrafo e gli elenchi puntati.

### Generazione URL {#url-generation}

Solo per le notifiche delle attività, il flusso di lavoro Forms include due configurazioni URL predefinite che è possibile trascinare dall&#39;elenco Generazione URL nella casella Modello di notifica e quindi personalizzare:

* OpenTask è disponibile per i tipi di notifica Promemoria e Assegnazione task. Questo URL fornisce un collegamento all’attività in Workspace, consentendo all’utente di accedere rapidamente all’attività dalla notifica e-mail. Quando trascinate l’URL OpenTask nella casella Modello di notifica, l’URL si presenta nel seguente formato:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask è disponibile per i tipi di notifica Gruppo - Promemoria e Gruppo - Assegnazione task. Questo URL fornisce un collegamento alla pagina dei dettagli dell’attività in Workspace, in cui l’utente può reclamare o reclamare e aprire l’elemento di lavoro. Quando si trascina l&#39;URL ClaimTask nella casella Modello di notifica, l&#39;URL è nel formato seguente:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Worksapce è obsoleto per la versione dei moduli AEM.

Se la soluzione viene distribuita in un ambiente cluster, sostituitela `@@notification-host@@` con l&#39;indirizzo del cluster.

`<`*PORT *`>`è il numero di porta del listener HTTP per il server applicazione. La porta listener HTTP predefinita per i server applicazione supportati è la seguente:

**JBoss:** 8080

**Oracle WebLogic Server:** 7001

**IBM WebSphere:** 9080

Affinché questi URL funzionino correttamente, sostituite `<`*PORT *`>`con il numero di porta appropriato per l&#39;ambiente.

>[!NOTE]
>
>Se si utilizza un&#39;applicazione Web personalizzata diversa da Forms per fornire agli utenti l&#39;accesso alle attività, è necessario utilizzare un formato URL appropriato per l&#39;applicazione personalizzata.

### Selettore variabile {#variable-picker}

L&#39;elenco Selettore variabile fornisce variabili utili che è possibile trascinare nelle caselle Oggetto o Modello di notifica. Quando si rilascia una variabile nelle caselle Oggetto o Modello di notifica, questa viene modificata nel nome effettivo della variabile del flusso di lavoro dei moduli con due simboli @ su entrambi i lati, ad esempio `@@taskid@@`.

Per promemoria, assegnazioni di attività e scadenze per utenti e gruppi, potete utilizzare le seguenti variabili nelle caselle Oggetto e Modello di notifica:

**descrizione** Il contenuto della proprietà Descrizione, come definito nel passaggio utente (punto iniziale, operazione Assegna attività o operazione Assegna più attività) del processo in Workbench.

**istruzioni** Il contenuto della proprietà Istruzioni attività, come definito nel passaggio utente del processo in Workbench.

**notification-host** Il nome host del server applicazione dei moduli AEM.

**process-name** Il nome del processo.

**operation-name** Il nome del passaggio.

**tascapola** L&#39;identificatore univoco per l&#39;attività corrente.

**azioni** Genera un elenco numerato di route valide (ad esempio, Approva, Rifiuta) su cui il destinatario può fare clic.

Inoltre, per i promemoria di gruppo, le assegnazioni di task di gruppo e le scadenze di gruppo, potete utilizzare anche:

**group-name** Il nome del gruppo a cui è assegnato l’elemento di lavoro.

>[!NOTE]
>
>Se una variabile non ha valore, non viene restituito nulla.

Per i rami in stallo, nelle caselle Oggetto e Modello di notifica è possibile utilizzare le seguenti variabili:

**branch-id** L&#39;identificatore del ramo.

**process-id** L’identificatore dell’istanza di processo.

**notification-host** Il nome host del server applicazione dei moduli AEM.

Per le operazioni in stallo, nelle caselle Oggetto e Modello di notifica è possibile utilizzare le seguenti variabili:

**action-id** L’identificatore dell’operazione.

**branch-id** L&#39;identificatore del ramo.

**process-id** L’identificatore dell’istanza di processo.

**notification-host** Il nome host del server applicazione dei moduli AEM.

### Utilizzo di una variabile nella casella Oggetto {#using-a-variable-in-the-subject-box}

Se si digita il testo seguente nella casella Oggetto per le notifiche Assegnazione task:

`Please complete task @@taskid@@`

L&#39;utente riceve un messaggio e-mail con il seguente oggetto se gli è stata assegnata l&#39;attività 376:

`Please complete task 376`

### Uso delle variabili nella casella Modello di notifica {#using-variables-in-the-notification-template-box}

Se si digita il testo seguente nella casella Modello di notifica per le notifiche per ramo bloccato:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

Se il numero del ramo è 4868 e il nome del server è `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configurazione delle connessioni di monitoraggio delle attività aziendali {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring, un modulo opzionale, offre una serie di dashboard operativi che offrono visibilità in tempo reale sulle operazioni e sugli indicatori di prestazioni chiave.

Nella pagina Impostazioni di configurazione BAM, impostare le connessioni al server che esegue BAM in modo che gli eventi relativi al processo possano essere tracciati e trasmessi a tale server.

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Impostazioni server > Impostazioni di configurazione BAM.
1. Nella casella Host BAM digitare il nome del server che esegue BAM. Il valore predefinito è localhost.
1. Nella casella Porta BAM digitare la porta da utilizzare per connettersi al server che esegue BAM. La porta BAM predefinita per JBoss è 8080, WebLogic è 7001 e WebSphere è 9080.
1. Nella casella Host server digitare il nome o l&#39;indirizzo IP del server dei moduli host. Il valore predefinito è localhost.
1. Nella casella Porta server, digitare il numero di porta utilizzato dal server dei moduli.
1. Nelle caselle Nome utente e Password digitare l&#39;ID utente e la password appropriati per accedere al server BAM. Il nome utente predefinito è CognosNowAdmin e la password predefinita è manager.
1. Fate clic su Salva.

