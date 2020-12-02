---
title: Flussi di lavoro Forms incentrati su OSGi | Gestione dei dati utente
seo-title: Flussi di lavoro Forms incentrati su OSGi | Gestione dei dati utente
description: Flussi di lavoro Forms incentrati su OSGi | Gestione dei dati utente
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---


# Flussi di lavoro Forms incentrati su OSGi | Gestione dei dati utente {#forms-centric-workflows-on-osgi-handling-user-data}

I flussi di AEM Forms consentono di automatizzare i processi aziendali Forms incentrati sul mondo reale. I flussi di lavoro sono composti da una serie di passaggi eseguiti in un ordine specificato nel modello di flusso di lavoro associato. Ogni passaggio esegue un’azione specifica, ad esempio l’assegnazione di un’attività a un utente o l’invio di un messaggio e-mail. I flussi di lavoro possono interagire con le risorse presenti nell’archivio, negli account utente e nei servizi. Pertanto, i flussi di lavoro possono coordinare attività complesse che coinvolgono qualsiasi aspetto del Experience Manager .

È possibile avviare o avviare un flusso di lavoro incentrato sui moduli tramite uno dei seguenti metodi:

* Invio di un&#39;applicazione dalla AEM Posta in arrivo
* Invio di un&#39;applicazione dall&#39;app AEM [!DNL Forms]
* Invio di un modulo adattivo
* Utilizzo di una cartella esaminata
* Invio di una comunicazione interattiva o di una lettera

Per ulteriori informazioni sui flussi di lavoro e sulle funzionalità di AEM incentrati su Forms, vedi [Flusso di lavoro basato su Forms su OSGi](/help/forms/using/aem-forms-workflow.md).

## Archivio dati utente {#user-data-and-data-stores}

Quando un flusso di lavoro viene attivato, viene generato automaticamente un payload per l’istanza del flusso di lavoro. A ogni istanza del flusso di lavoro viene assegnato un ID istanza univoco e un ID payload associato. Il payload contiene le posizioni dell&#39;archivio per i dati utente e del modulo associati a un&#39;istanza del flusso di lavoro. Inoltre, le bozze e i dati della cronologia per un&#39;istanza del flusso di lavoro vengono memorizzati anche nell&#39;archivio AEM.

Le posizioni predefinite dell&#39;archivio in cui risiedono payload, bozze e cronologia di un&#39;istanza del flusso di lavoro sono le seguenti:

>[!NOTE]
>
>È possibile configurare posizioni diverse per memorizzare i dati di payload, bozza e cronologia durante la creazione di un flusso di lavoro o un&#39;applicazione. Per identificare le posizioni in cui un flusso di lavoro o un&#39;applicazione ha memorizzato i dati, controlla il flusso di lavoro.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>Istanza flusso di lavoro <br /></strong></td>
   <td>/var/workflow/instance/[server_id]/&lt;data&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instance/[server_id]/[data]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>Payload</strong></td>
   <td>/var/fd/dashboard/payload/[server_id]/[data]/<br /> [payload-id]/</td>
   <td>/etc/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>Bozze</strong></td>
   <td>/var/fd/dashboard/instance/[server_id]/<br /> [data]/[workflow-instance]/draft/[workitem]/</td>
   <td>/etc/fd/dashboard/instance/[server_id]/<br /> [data]/[workflow-instance]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>Storia</strong></td>
   <td>/var/fd/dashboard/instance/[server_id]/<br /> [data]/[workflow_instance]/history/</td>
   <td>/etc/fd/dashboard/instance/[server_id]/<br /> [data]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## Accesso ed eliminazione dei dati utente {#access-and-delete-user-data}

Potete accedere ed eliminare i dati utente da un’istanza di workflow nella directory archivio. A tal fine, è necessario conoscere l&#39;ID istanza dell&#39;istanza del flusso di lavoro associata all&#39;utente. Potete trovare l&#39;ID di istanza di un&#39;istanza del flusso di lavoro utilizzando il nome utente dell&#39;utente che ha avviato l&#39;istanza del flusso di lavoro o che è l&#39;assegnatario corrente dell&#39;istanza del flusso di lavoro.

Tuttavia, non è possibile identificare i flussi di lavoro associati a un iniziatore oppure i risultati potrebbero essere ambigui nei seguenti scenari:

* **Flusso di lavoro avviato tramite una cartella** controllata: Impossibile identificare un&#39;istanza del flusso di lavoro utilizzando il relativo iniziatore se il flusso di lavoro viene attivato da una cartella esaminata. In questo caso, le informazioni utente sono codificate nei dati memorizzati.
* **Flusso di lavoro avviato dall’istanza** pubblica AEM: Tutte le istanze del flusso di lavoro vengono create utilizzando un utente di servizio quando moduli adattivi, comunicazioni interattive o lettere vengono inviate dall’istanza di AEM pubblicazione. In questi casi, il nome utente dell’utente connesso non viene acquisito nei dati dell’istanza del flusso di lavoro.

### Accesso ai dati utente {#access}

Per identificare e accedere ai dati utente memorizzati per un&#39;istanza di workflow, effettua le seguenti operazioni:

1. AEM&#39;istanza di creazione, andare su `https://'[server]:[port]'/crx/de` e passare a **[!UICONTROL Strumenti > Query]**.

   Selezionare **[!UICONTROL SQL2]** dal menu a discesa **[!UICONTROL Type]**.

1. A seconda delle informazioni disponibili, eseguite una delle seguenti query:

   * Esegui quanto segue se l&#39;iniziatore del flusso di lavoro è noto:

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * Esegui quanto segue se l&#39;utente i cui dati si trovano sono l&#39;assegnatario del flusso di lavoro corrente:

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   La query restituisce la posizione di tutte le istanze del flusso di lavoro per l&#39;iniziatore del flusso di lavoro specificato o per l&#39;assegnatario del flusso di lavoro corrente.

   Ad esempio, la seguente query restituisce due percorsi di istanze del flusso di lavoro dal nodo `/var/workflow/instances` il cui iniziatore del flusso di lavoro è `srose`.

   ![workflow-instance](assets/workflow-instance.png)

1. Passare a un percorso di istanza del flusso di lavoro restituito dalla query. La proprietà status visualizza lo stato corrente dell&#39;istanza del flusso di lavoro.

   ![stato](assets/status.png)

1. Nel nodo dell&#39;istanza del flusso di lavoro, andate a `data/payload/`. La proprietà `path` memorizza il percorso del payload per l&#39;istanza del flusso di lavoro. È possibile accedere al percorso per accedere ai dati memorizzati nel payload.

   ![percorso di payload](assets/payload-path.png)

1. Andate alle posizioni per le bozze e la cronologia per l&#39;istanza del flusso di lavoro.

   Esempio:

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. Ripetere i passaggi da 3 a 5 per tutte le istanze del flusso di lavoro restituite dalla query al punto 2.

   >[!NOTE]
   >
   >AEM [!DNL Forms] l&#39;app memorizza anche i dati in modalità offline. È possibile che i dati per un&#39;istanza di flusso di lavoro siano memorizzati localmente su singoli dispositivi e vengano inviati al server [!DNL Forms] quando l&#39;app si sincronizza con il server.

### Elimina dati utente {#delete-user-data}

È necessario essere un amministratore AEM per eliminare i dati utente dalle istanze del flusso di lavoro, eseguendo la procedura seguente:

1. Seguite le istruzioni riportate in [Accedere ai dati utente](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access) e prendete nota di quanto segue:

   * Percorsi alle istanze del flusso di lavoro associate all&#39;utente
   * Stato delle istanze del flusso di lavoro
   * Percorsi ai payload per le istanze del flusso di lavoro
   * Percorsi alle bozze e alla cronologia per le istanze del flusso di lavoro

1. Eseguire questo passaggio per le istanze del flusso di lavoro nello stato **ESECUZIONE**, **SOSPENSO** o **STALE**:

   1. Andate a `https://'[server]:[port]'/aem/start.html` ed effettuate l&#39;accesso con le credenziali di amministratore.
   1. Passa a **[!UICONTROL Strumenti > Flusso di lavoro> Istanze]**.
   1. Selezionate le istanze del flusso di lavoro rilevanti per l&#39;utente e toccate **[!UICONTROL Termina]** per terminare le istanze in esecuzione.

      Per ulteriori informazioni sull&#39;utilizzo delle istanze del flusso di lavoro, vedere [Amministrazione delle istanze del flusso di lavoro](/help/sites-administering/workflows-administering.md).

1. Passate alla console [!DNL CRXDE Lite], individuate il percorso di payload per un&#39;istanza del flusso di lavoro ed eliminate il nodo `payload`.
1. Andate al percorso delle bozze per un&#39;istanza del flusso di lavoro ed eliminate il nodo `draft`.
1. Andate al percorso della cronologia per un&#39;istanza del flusso di lavoro ed eliminate il nodo `history`.
1. Andate al percorso dell&#39;istanza del flusso di lavoro per un&#39;istanza del flusso di lavoro ed eliminate il nodo `[workflow-instance-ID]` per il flusso di lavoro.

   >[!NOTE]
   >
   >Eliminando il nodo di istanza del flusso di lavoro, verrà rimossa l’istanza del flusso di lavoro per tutti i partecipanti al flusso di lavoro.

1. Ripetete i passaggi da 2 a 6 per tutte le istanze del flusso di lavoro identificate per un utente.
1. Identificare ed eliminare i dati bozza e invio offline dalla casella in uscita AEM [!DNL Forms] app dei partecipanti al flusso di lavoro per evitare l&#39;invio al server.

Potete inoltre utilizzare le API per accedere e rimuovere nodi e proprietà. Per ulteriori informazioni, consulta i seguenti documenti.

* [Come accedere a AEM JCR a livello di programmazione](/help/sites-developing/access-jcr.md)
* [Rimozione di nodi e proprietà](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [Riferimento API](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)

