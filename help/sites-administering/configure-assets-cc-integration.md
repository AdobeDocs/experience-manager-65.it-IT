---
title: Configurare l’integrazione di AEM Assets con Experience Cloud
description: Scopri come configurare l’integrazione di AEM Assets con Experience Cloud.
contentOwner: AG
feature: Asset Management
role: User, Architect, Admin
exl-id: d167cf97-6829-45a7-ba46-2239d530b060
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# Configurare l’integrazione di AEM Assets con Experience Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

I clienti di Adobe Experience Cloud possono sincronizzare le proprie risorse in Adobe Experience Manager Assets con Adobe Creative Cloud e viceversa. Puoi anche sincronizzare le risorse con Experience Cloud e viceversa. È possibile impostare questa sincronizzazione tramite [!DNL Adobe I/O]. Il nome aggiornato di [!DNL Adobe Marketing Cloud] è [!DNL Adobe Experience Cloud].

Il flusso di lavoro per impostare questa integrazione è:

1. Creare un&#39;autenticazione in [!DNL Adobe I/O] utilizzando un gateway pubblico e ottenere un ID applicazione.
1. Crea un profilo nell’istanza di AEM Assets utilizzando l’ID applicazione.
1. Utilizza questa configurazione per sincronizzare le risorse.

Nel back-end, il server AEM autentica il profilo con il gateway e quindi sincronizza i dati tra Assets e Experience Cloud.

>[!NOTE]
>
>Questa funzionalità è obsoleta in [!DNL Assets]. Trova sostituzioni in [Best practice per l&#39;integrazione di AEM e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md). In caso di domande, [contatta l&#39;Assistenza clienti Adobe](https://www.adobe.com/account/sign-in.supportportal.html).

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## Creare un’applicazione {#create-an-application}

1. Accedi all&#39;interfaccia del gateway Adobe Developer all&#39;indirizzo [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/).

   >[!NOTE]
   >
   >Per creare un ID applicazione sono necessari privilegi di amministratore.

1. Dal riquadro di sinistra, passare a **[!UICONTROL Strumenti per sviluppatori]** > **[!UICONTROL Applicazioni]** per visualizzare un elenco di applicazioni.
1. Fai clic su **[!UICONTROL Aggiungi]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) per creare un&#39;applicazione.
1. Dall&#39;elenco **[!UICONTROL Credenziali client]**, selezionare **[!UICONTROL Account di servizio (asserzione JWT)]**, che è un servizio di comunicazione server-to-server per l&#39;autenticazione server.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Specificare un nome per l&#39;applicazione e una descrizione facoltativa.
1. Dall&#39;elenco **[!UICONTROL Organizzazione]**, selezionare l&#39;organizzazione per la quale si desidera sincronizzare le risorse.
1. Dall&#39;elenco **[!UICONTROL Ambito]**, selezionare **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]** e **[!UICONTROL cc-share]**.
1. Fai clic su **[!UICONTROL Crea]**. Un messaggio notifica che l’applicazione viene creata.

   ![Notifica di creazione dell&#39;applicazione per integrare AEM Assets con Creative Cloud](assets/chlimage_1-50.png) completata

1. Copia l&#39;**[!UICONTROL ID applicazione]** generato per la nuova applicazione.

   >[!CAUTION]
   >
   >Assicurati di non copiare inavvertitamente il **[!UICONTROL Segreto applicazione]** invece del **[!UICONTROL ID applicazione]**.

## Aggiungi una nuova configurazione all’Experience Cloud {#add-a-new-configuration}

1. Fai clic sul logo AEM nell&#39;interfaccia utente dell&#39;istanza AEM Assets locale e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service precedenti]**.

1. Individua il servizio **[!UICONTROL Adobe Experience Cloud]**. Se non esistono configurazioni, fare clic su **[!UICONTROL Configura ora]**. Se sono presenti configurazioni, fare clic su **[!UICONTROL Mostra configurazioni]** e fare clic su `+` per aggiungere una nuova configurazione.

   >[!NOTE]
   >
   >Utilizza un account Adobe ID con privilegi di amministratore dell’organizzazione.

1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un titolo e un nome per la nuova configurazione e fai clic su **[!UICONTROL Crea]**.

   ![Denomina una nuova configurazione per integrare AEM Assets e Creative Cloud](assets/aem-ec-integration-config1.png)

1. Nel campo **[!UICONTROL URL tenant]**, specifica l&#39;URL per AEM Assets. In passato, se l&#39;URL era definito come `https://<tenant_id>.marketing.adobe.com`, modificarlo in `https://<tenant_id>.experiencecloud.adobe.com`.

   1. Passa a **Strumenti > Cloud Service > Cloud Service precedenti**. In Adobe Experience Cloud, fai clic su **Mostra configurazioni**.
   1. Seleziona la configurazione esistente da modificare. Modificare la configurazione e sostituire `marketing.adobe.com` in `experiencecloud.adobe.com`.
   1. Salva la configurazione. Test degli agenti di replica sincronizzati con MAC.

1. Nel campo **[!UICONTROL ID client]**, incolla l&#39;ID applicazione copiato alla fine della procedura [crea un&#39;applicazione](#create-an-application).

   ![Fornisci i valori ID applicazione necessari per integrare AEM Assets e Creative Cloud](assets/cloudservices_tenant_info.png)

1. In **[!UICONTROL Sincronizzazione]** selezionare **[!UICONTROL Abilitato]** per abilitare la sincronizzazione e fare clic su **[!UICONTROL OK]**. Se si seleziona **disabled**, la sincronizzazione funziona in un&#39;unica direzione.

1. Dalla pagina di configurazione, fai clic su **[!UICONTROL Visualizza chiave pubblica]** per visualizzare la chiave pubblica generata per la tua istanza. In alternativa, fai clic su **[!UICONTROL Scarica chiave pubblica per OAuth Gateway]** per scaricare il file contenente la chiave pubblica. Quindi, apri il file per visualizzare la chiave pubblica.

## Abilita sincronizzazione {#enable-synchronization}

1. Visualizzare la chiave pubblica utilizzando uno dei seguenti metodi menzionati nell&#39;ultimo passaggio della procedura [aggiungere una nuova configurazione all&#39;Experience Cloud](#add-a-new-configuration). Fai clic su **[!UICONTROL Visualizza chiave pubblica]**.

1. Copia la chiave pubblica e incollala nel campo **[!UICONTROL Chiave pubblica]** dell&#39;interfaccia di configurazione dell&#39;applicazione creata in [crea un&#39;applicazione](#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. Fai clic su **[!UICONTROL Aggiorna]**. Sincronizza ora le risorse con l’istanza di AEM Assets.

## Verificare la sincronizzazione {#test-the-synchronization}

1. Fai clic sul logo AEM nell&#39;interfaccia utente dell&#39;istanza AEM Assets locale e passa a **[!UICONTROL Strumenti]**> **[!UICONTROL Distribuzione]**> **[!UICONTROL Replica]**per individuare i profili di replica creati per la sincronizzazione.
1. Nella pagina **[!UICONTROL Replica]** fare clic su **[!UICONTROL Agenti sull&#39;autore]**.
1. Nell’elenco dei profili, fai clic sul profilo di replica predefinito dell’organizzazione per aprirlo.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Verifica connessione]**.

   ![Verifica la connessione e imposta il profilo di replica predefinito per l&#39;organizzazione](assets/chlimage_1-54.png)

1. Al termine della replica, verifica la presenza di un messaggio di successo alla fine dei risultati del test.

## Aggiungi utenti all&#39;Experience Cloud {#add-users-to-experience-cloud}

1. Accedi all’Experience Cloud utilizzando le credenziali di amministratore.
1. Dalle barre, vai a **[!UICONTROL Amministrazione]** e quindi fai clic su **[!UICONTROL Avvia Enterprise Dashboard]**.
1. Dalla barra, fai clic su **[!UICONTROL Utenti]** per aprire la pagina **[!UICONTROL Gestione utenti]**.
1. Dalla barra degli strumenti, fai clic su **Aggiungi** ![aem_assets_add_icon](assets/aem_assets_add_icon.png).
1. Aggiungi uno o più utenti che possano condividere le risorse con Creative Cloud.

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## Scambio di risorse tra AEM Assets e Experience Cloud {#exchange-assets-between-aem-and-experience-cloud}

1. Accedi ad AEM Assets.
1. Nella console Assets, crea una cartella e carica alcune risorse su di essa. Ad esempio, crea una cartella **mc-demo** e carica una risorsa.
1. Seleziona la cartella e fai clic su **Condividi** ![assets_share](assets/do-not-localize/assets_share.png).
1. Dal menu, seleziona **[!UICONTROL Adobe Experience Cloud]** e fai clic su **[!UICONTROL Condividi]**. Un messaggio notifica che la cartella è condivisa con Experience Cloud.

   >[!NOTE]
   >
   >La condivisione di una cartella Assets di tipo `sling:OrderedFolder` non è supportata nel contesto della condivisione in Adobe Experience Cloud. Se desideri condividere una cartella, durante la creazione in AEM Assets non selezionare l&#39;opzione **[!UICONTROL Ordinata]**.

1. Aggiorna l’interfaccia utente di AEM Assets. La cartella creata nella console Assets dell’istanza AEM Assets locale viene copiata nell’interfaccia utente di Experience Cloud. La risorsa caricata nella cartella in AEM Assets viene visualizzata nella copia della cartella in Experience Cloud dopo l’elaborazione da parte del server AEM.
1. Puoi anche caricare una risorsa nella copia replicata della cartella in Experience Cloud. Una volta elaborata, la risorsa viene visualizzata nella cartella condivisa in AEM Assets.

<!-- Removing as per PM guidance via https://jira.corp.adobe.com/browse/CQDOC-16834?focusedCommentId=22881523&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-22881523.

## Exchange assets between AEM Assets and Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
>
>The AEM to Creative Cloud Folder Sharing feature is deprecated. Customers are strongly advised to use newer capabilities, like [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Learn more in [AEM and Creative Cloud Integration Best Practices](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets lets you share folders containing assets with Adobe Creative Cloud users.

1. In the Assets console, select the folder to share with Creative Cloud.
1. From the toolbar, click **[!UICONTROL Share]** ![assets_share](assets/do-not-localize/assets_share.png).
1. From the list, select the **[!UICONTROL Adobe Creative Cloud]** option.

   >[!NOTE]
   >
   >The options are available for users with read permissions on the root. Users must have the required permission to access the replication agent information of Marketing Cloud.

1. In the **[!UICONTROL Creative Cloud Sharing]** page, add the user to share the folder with and choose a role for the user. Click **[!UICONTROL Save]** and click **[!UICONTROL OK]**.

1. Log on to Creative Cloud with the credentials of the user you shared the folder with. The shared folder is available in Creative Cloud.

The AEM Assets-Marketing Cloud synchronization is designed in a way that the user machine instance from where the asset is uploaded retains the right to modify the asset. Only these changes are propagated to the other instance.

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and conversely for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [Best practice per l&#39;integrazione di Assets e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md)
