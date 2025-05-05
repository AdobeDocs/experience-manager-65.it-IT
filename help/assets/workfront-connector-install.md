---
title: Installa [!DNL Workfront for Experience Manager enhanced connector]
description: Installa [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 3%

---

# Installa [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | Questo articolo |

Un utente con accesso amministratore in [!DNL Adobe Experience Manager] installa il connettore avanzato. Prima dell&#39;installazione, controlla il supporto della piattaforma e altri [prerequisiti per il connettore](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe richiede la distribuzione e la configurazione di [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se distribuita e configurata senza un partner certificato o [!DNL Adobe Professional Services], non è supportata da Adobe.
>
>* Adobe potrebbe rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono ridondante questo connettore; in tal caso, i clienti potrebbero dover passare dall&#39;utilizzo di questo connettore.
>
>* Adobe supporta le versioni migliorate del connettore 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per verificare la versione avanzata del connettore, passa al gruppo `digital.hoodoo` disponibile nel riquadro a sinistra in [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* Consulta [Esame di certificazione partner per il connettore avanzato Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedere [Guida all&#39;esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

Per installare il connettore, effettua le seguenti operazioni:

1. Scarica il connettore da [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [Configurare il firewall](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. In Dispatcher, consenti le intestazioni HTTP denominate `authorization`, `username` e `apikey`. Consenti `GET`, `POST` e `PUT` richieste a `/bin/workfront-tools`.
1. Verificare che i percorsi seguenti non esistano nell&#39;archivio [!DNL Experience Manager]:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Installare il pacchetto utilizzando [!UICONTROL Gestione pacchetti]. Per informazioni su come installare i pacchetti, consulta la [documentazione di Gestione pacchetti](/help/sites-administering/package-manager.md).
1. Creare `wf-workfront-users` nel gruppo utenti [!DNL Experience Manager] e assegnare l&#39;autorizzazione `jcr:all` a `/content/dam`.
1. Aggiungere una proprietà personalizzata alla definizione predefinita dell&#39;indice per **`ntFolderDamLucene(/oak:index/ntFolderDamLucene)`**. Esegui i seguenti passaggi:
   * Aggiungi una proprietà **`nt:unstructured`** denominata **`wfReferenceNumber`** a:

     `/oak:index/ntFolderDamLucene/indexRules/nt:folder/properties/wfReferenceNumber`.
   * Reindicizzare `index /oak:index/ntFolderDamLucene` capovolgendo il flag di reindicizzazione su `true`.

Un utente di sistema `workfront-tools` viene creato automaticamente e le autorizzazioni richieste vengono gestite automaticamente. Tutti gli utenti di [!DNL Workfront] che utilizzano il connettore vengono aggiunti automaticamente come parte di questo gruppo.

## Configurare la connessione tra [!DNL Experience Manager] e [!DNL Workfront] {#configure-connection}

Per creare una connessione con Workfront, effettua le seguenti operazioni:

1. In [!DNL Experience Manager], selezionare **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazione strumenti di Workfront]**.

1. Seleziona `workfront-tools` nel pannello a sinistra e seleziona l&#39;opzione **[!UICONTROL Crea]** nell&#39;area superiore destra della pagina.

1. Nella finestra di dialogo **[!UICONTROL Connessione Workfront]**, fornisci i dettagli richiesti della distribuzione di [!DNL Workfront] e seleziona l&#39;opzione **[!UICONTROL Connetti a Workfront]**. Dopo la connessione, l&#39;integrazione personalizzata del documento [!DNL Workfront] viene creata automaticamente nell&#39;ambiente [!DNL Workfront].

   ![Connetti [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Per verificare la connessione, accedervi in [!DNL Workfront] e verificare che la chiave API sia la stessa e che la connessione sia **[!UICONTROL Abilitata]**. A tale scopo, selezionare **[!UICONTROL Configurazione]** > **[!UICONTROL Documenti]** > **[!UICONTROL Integrazioni personalizzate]** in [!DNL Workfront].

## Aggiorna [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets consente di aggiornare [!DNL Workfront for Experience Manager enhanced connector] da una versione precedente alla versione più recente.

Per aggiornare [!DNL Workfront for Experience Manager enhanced connector] alla versione più recente:

1. Scarica la versione più recente del connettore avanzato da [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. Installare il pacchetto utilizzando [!UICONTROL Gestione pacchetti]. Per informazioni su come installare i pacchetti, consulta la [documentazione di Gestione pacchetti](/help/sites-administering/package-manager.md).
