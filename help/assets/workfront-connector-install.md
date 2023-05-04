---
title: Installa [!DNL Workfront for Experience Manager enhanced connector]
description: Installa [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 4%

---

# Installa [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | Questo articolo |

Un utente con accesso amministratore in [!DNL Adobe Experience Manager] installa il connettore avanzato. Prima di eseguire l’installazione, controlla il supporto della piattaforma e altri [prerequisiti per il connettore](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* L&#39;Adobe richiede la distribuzione e la configurazione del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se implementato e configurato senza un partner certificato o [!DNL Adobe Professional Services], non è supportato da Adobe.
>
>* Adobe può rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono tale connettore ridondante; in questo caso, potrebbe essere richiesto ai clienti di effettuare la transizione dall’utilizzo di questo connettore.
>
>* Adobe supporta le versioni di connettore avanzate 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per controllare la versione del connettore avanzato, passa alla `digital.hoodoo` gruppo disponibile nel riquadro a sinistra in [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it).
>
>* Vedi [Esame di certificazione dei partner per Workfront per il connettore avanzato Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedi [Guida all’esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


Per installare il connettore, effettua le seguenti operazioni:

1. Scarica il connettore da [[!DNL Software Distribution] collegamento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [Configurare il firewall](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. Sul dispatcher, consenti intestazioni HTTP denominate `authorization`, `username`e `apikey`. Consenti `GET`, `POST`e `PUT` richieste a `/bin/workfront-tools`.
1. Assicurati che i percorsi seguenti non esistano in [!DNL Experience Manager] archivio:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Installa il pacchetto utilizzando [!UICONTROL Gestione pacchetti]. Per informazioni su come installare i pacchetti, consulta [Documentazione su Gestione pacchetti](/help/sites-administering/package-manager.md).
1. Crea `wf-workfront-users` in [!DNL Experience Manager] Gruppo di utenti e assegna l’autorizzazione `jcr:all` a `/content/dam`.

Utente di sistema `workfront-tools` viene creato automaticamente e le autorizzazioni richieste vengono gestite automaticamente. Tutti gli utenti da [!DNL Workfront] che utilizzano il connettore viene aggiunto automaticamente come parte di questo gruppo.

## Configura la connessione tra [!DNL Experience Manager] e [!DNL Workfront] {#configure-connection}

Per creare una connessione con Workfront, effettua le seguenti operazioni:

1. In [!DNL Experience Manager], seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione strumenti Workfront]**.

1. Seleziona `workfront-tools` nel pannello a sinistra e seleziona **[!UICONTROL Crea]** nell’area in alto a destra della pagina.

1. In **[!UICONTROL Connessione Workfront]** , fornire i dettagli richiesti [!DNL Workfront] distribuzione e seleziona **[!UICONTROL Connessione a Workfront]** opzione . Una volta connessa correttamente, la [!DNL Workfront] l’integrazione personalizzata dei documenti viene creata automaticamente in [!DNL Workfront] ambiente.

   ![Connetti [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Per verificare la connessione, accedervi in [!DNL Workfront] e verifica che la chiave API sia la stessa e che la connessione sia **[!UICONTROL Abilitato]**. A questo scopo, seleziona **[!UICONTROL Configurazione]** > **[!UICONTROL Documenti]** > **[!UICONTROL Integrazioni personalizzate]** in [!DNL Workfront].

## Aggiorna [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets consente di aggiornare [!DNL Workfront for Experience Manager enhanced connector] da una versione precedente alla versione più recente.

Per aggiornare [!DNL Workfront for Experience Manager enhanced connector] all’ultima versione:

1. Scarica la versione più recente del connettore avanzato da [[!DNL Software Distribution] collegamento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. Installa il pacchetto utilizzando [!UICONTROL Gestione pacchetti]. Per informazioni su come installare i pacchetti, consulta [Documentazione su Gestione pacchetti](/help/sites-administering/package-manager.md).
