---
title: Post-elaborazione di lettere e comunicazioni interattive
seo-title: Post Processing of Letters
description: L’elaborazione post-elaborazione delle lettere in Gestione corrispondenza consente di creare processi post AEM e Forms, come la stampa e l’e-mail, e di integrarli con le lettere.
seo-description: Post Processing of Letters in Correspondence Management lets you create AEM and Forms post processes, such as print and email, and integrate them with your letters.
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
feature: Correspondence Management
exl-id: 91ee4422-99c1-4907-a507-5968c6984f28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# Post-elaborazione di lettere e comunicazioni interattive{#post-processing-of-letters-and-interactive-communications}

## Post-elaborazione {#post-processing}

Gli agenti possono associare ed eseguire flussi di lavoro di post-elaborazione su lettere e comunicazioni interattive. Il processo di post da eseguire può essere selezionato nella vista Proprietà del modello Lettera. È possibile impostare i processi post per inviare e-mail, stampare, fax o archiviare le lettere finali.

![Post-elaborazione](assets/ppoverview.png)

Per associare i processi post a lettere o comunicazioni interattive, è innanzitutto necessario impostare i processi post. È possibile eseguire due tipi di flussi di lavoro sulle lettere inviate:

1. **Forms Workflow:** Si tratta dei flussi di lavoro AEM Forms on JEE per la gestione dei processi. Istruzioni per la configurazione [Forms Workflow](#formsworkflow).

1. **Flusso di lavoro AEM:** I flussi di lavoro AEM possono essere utilizzati anche come processi post per le lettere inviate. Istruzioni per la configurazione [Flusso di lavoro AEM](../../forms/using/aem-forms-workflow.md).

## Flusso di lavoro per moduli {#formsworkflow}

1. In AEM, apri Configurazione console Web Adobe Experience Manager per il server utilizzando il seguente URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Gestione configurazione](assets/2configmanager-1.png)

1. In questa pagina, individua la configurazione dell’SDK client di AEM Forms ed espandila facendo clic su di essa.
1. In URL server, immetti il nome del tuo AEM Forms sul server JEE, i dettagli di accesso e fai clic su **Salva**.

   ![Immettere il nome del server di LiveCycle](assets/1cofigmanager.png)

1. Specifica il nome utente e la password.
1. Assicurati che sun.util.calendar sia aggiunto alla configurazione del firewall di deserializzazione.

   Vai a Configurazione firewall di deserializzazione e sotto le classi Inserite nell&#39;elenco Consentiti di prefissi di pacchetti, aggiungi sun.util.calendar.

1. Ora i server sono mappati e i processi post in AEM Forms su JEE sono disponibili nell&#39;interfaccia utente AEM durante la creazione di lettere.

   ![Crea schermata delle lettere con i processi post elencati](assets/0configmanager.png)

1. Per autenticare un processo/servizio, copia il nome di un processo e torna alla pagina Configurazioni console Web Adobe Experience Manager > Configurazione SDK client AEM Forms e aggiungi il processo come nuovo servizio.

   Ad esempio, se il menu a discesa nella pagina Proprietà della lettera visualizza il nome del processo come Forms Workflow -> ValidCCPostProcess/SaveXML, aggiungere un Nome servizio come `ValidCCPostProcess/SaveXML`.

1. Per utilizzare AEM Forms sui flussi di lavoro JEE per la post-elaborazione, imposta i parametri e gli output necessari. I valori predefiniti dei parametri sono indicati di seguito.

   Vai alla pagina Configurazioni console Web di Adobe Experience Manager > **[!UICONTROL Configurazioni di gestione della corrispondenza]** e imposta i seguenti parametri:

   1. **inPDFDoc (parametro del documento PDF):** Un documento PDF come input. Questo input contiene la lettera di cui è stato effettuato il rendering come input. I nomi dei parametri indicati sono configurabili. Possono essere configurati dalle configurazioni di Gestione Corrispondenza dalla configurazione.
   1. **inXMLDoc (parametro dati XML):** Un documento XML come input. Questo input contiene i dati immessi dall&#39;utente sotto forma di XML.
   1. **inXDPDoc (parametro del documento XDP):** Un documento XML come input. Questo input contiene il layout sottostante (XDP).
   1. **inAttachmentDocs (parametro Documenti allegato):** Un parametro di input elenco. Questo input contiene tutti gli allegati come input.
   1. **redirectURL (output URL di reindirizzamento):** Un tipo di output che indica l&#39;url a cui reindirizzare.

   Il flusso di lavoro dei moduli deve avere un parametro di documento PDF o un parametro di dati XML come input con lo stesso nome specificato in **[!UICONTROL Configurazioni di gestione della corrispondenza]**. Questo è necessario per elencare il processo nel menu a discesa Post process .

## Impostazioni nell’istanza Publish {#settings-on-the-publish-instance}

1. accedere a `https://localhost:publishport/aem/forms`.
1. Passa a **[!UICONTROL Lettere]** per visualizzare la lettera pubblicata disponibile nell&#39;istanza di pubblicazione.
1. Configura le impostazioni di DS AEM. Vedi [Configurazione delle impostazioni di AEM DS](../../forms/using/configuring-the-processing-server-url-.md).

>[!NOTE]
>
>Durante l&#39;utilizzo dei flussi di lavoro Forms o AEM, prima di effettuare invii dal server di pubblicazione, è necessario configurare il servizio delle impostazioni DS. In caso contrario, la presentazione del modulo non verrà eseguita.

## Recupero istanze lettera {#letter-instances-retrieval}

Le istanze di lettere salvate possono essere ulteriormente modificate, ad esempio il recupero delle istanze di lettere e l&#39;eliminazione delle istanze di lettere, utilizzando le seguenti API definite in LetterInstanceService.

<table>
 <tbody>
  <tr>
   <td><strong>API lato server</strong></td>
   <td><strong>Nome operazione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><p>Public LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>Genera ICCException; </p> </td>
   <td>getLetterInstance</td>
   <td>Recupera l'istanza di lettera specificata </td>
  </tr>
  <tr>
   <td>Il public void deleteLetterInstance(String letterInstanceId) genera ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>Elimina l'istanza di lettera specificata </td>
  </tr>
  <tr>
   <td>L'elenco getAllLetterInstances(Query) genera ICCException; </td>
   <td>getAllLetterInstances </td>
   <td>Questa API recupera le istanze di lettere in base al parametro della query di input. Per recuperare tutte le istanze di lettere, il parametro di query può essere passato come null.<br /> </td>
  </tr>
  <tr>
   <td>LetterInstanceExists (String letterInstanceName) booleano pubblico genera ICCException; </td>
   <td>letterInstanceExists </td>
   <td>Controlla se esiste una LetterInstance con il nome specificato </td>
  </tr>
 </tbody>
</table>

## Associazione di un processo di post a una lettera {#associating-a-post-process-with-a-letter}

Nell’interfaccia utente CCR, completa i seguenti passaggi per associare un processo di post a una lettera:

1. Passa il puntatore del mouse sopra una lettera e tocca **Visualizza proprietà**.
1. Seleziona **Modifica**.
1. Nel menu a discesa Proprietà di base selezionare il processo di pubblicazione da associare alla lettera. I processi post relativi a AEM e Forms sono elencati nel menu a discesa .
1. Tocca **Salva**.
1. Dopo aver configurato la lettera con il processo post, pubblica la lettera ed eventualmente sull&#39;istanza di pubblicazione, specifica l&#39;URL di elaborazione nel servizio Impostazioni DS AEM. In questo modo il processo post viene eseguito sull&#39;istanza di elaborazione.

## Ricarica un&#39;istanza di lettera bozza  {#reloaddraft}

Un&#39;istanza di bozza di lettera può essere ricaricata nell&#39;interfaccia utente utilizzando il seguente url:

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstanceID: ID univoco dell&#39;istanza della lettera inviata.

Per ulteriori informazioni sul salvataggio di una bozza di lettera, consulta [Salvataggio di bozze e invio di istanze di lettere](../../forms/using/create-correspondence.md#savingdrafts).
