---
title: Configurare l’integrazione di AEM Assets con Experience Cloud
description: Scopri come configurare l’integrazione di AEM Assets con Experience Cloud.
contentOwner: AG
feature: Asset Management
role: User, Architect, Admin
exl-id: d167cf97-6829-45a7-ba46-2239d530b060
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# Configurare l’integrazione di AEM Assets con Experience Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

Se sei un cliente Adobe Experience Cloud, puoi sincronizzare le tue risorse in Adobe Experience Manager Assets con Adobe Creative Cloud e viceversa. Puoi anche sincronizzare le tue risorse con Experience Cloud e vice versa. Puoi impostare questa sincronizzazione tramite [!DNL Adobe I/O]. Nome aggiornato di [!DNL Adobe Marketing Cloud] è [!DNL Adobe Experience Cloud].

Il flusso di lavoro per impostare questa integrazione è:

1. Crea un&#39;autenticazione in [!DNL Adobe I/O] utilizzando un gateway pubblico e ottenere un ID applicazione.
1. Crea un profilo nella tua istanza AEM Assets utilizzando l’ID applicazione.
1. Utilizza questa configurazione per sincronizzare le risorse.

Nel back-end, il server AEM autentica il tuo profilo con il gateway e quindi sincronizza i dati tra Assets e Experience Cloud.

>[!NOTE]
>
>Questa funzione è obsoleta in [!DNL Assets]. Trova sostituzioni in [Best practice per l’integrazione di AEM e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md). Se hai delle domande, [contattare l&#39;assistenza clienti Adobe](https://www.adobe.com/account/sign-in.supportportal.html).

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## Creare un&#39;applicazione {#create-an-application}

1. Accedi all’interfaccia gateway di Adobe Developer accedendo a [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/).

   >[!NOTE]
   >
   >Per creare un ID applicazione è necessario disporre dei privilegi di amministratore.

1. Dal riquadro a sinistra, passa a **[!UICONTROL Strumenti per gli sviluppatori]** > **[!UICONTROL Applicazioni]** per visualizzare un elenco delle applicazioni.
1. Fai clic su **[!UICONTROL Aggiungi]** ![aem_assets_addcerchio_icon](assets/aem_assets_addcircle_icon.png) per creare un&#39;applicazione.
1. Da **[!UICONTROL Credenziali client]** elenco, selezionare **[!UICONTROL Account di servizio (asserzione JWT)]**, un servizio di comunicazione server-to-server per l’autenticazione server.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Specifica un nome per l’applicazione e una descrizione facoltativa.
1. Da **[!UICONTROL Organizzazione]** seleziona l’organizzazione per la quale desideri sincronizzare le risorse.
1. Da **[!UICONTROL Ambito]** elenco, selezionare **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]** e **[!UICONTROL cc-share]**.
1. Fai clic su **[!UICONTROL Crea]**. Un messaggio notifica la creazione dell&#39;applicazione.

   ![Notifica della corretta creazione dell&#39;applicazione per integrare AEM Assets con Creative Cloud](assets/chlimage_1-50.png)

1. Copia il **[!UICONTROL ID applicazione]** generato per la nuova applicazione.

   >[!CAUTION]
   >
   >Assicurati di non copiare inavvertitamente il **[!UICONTROL Segreto applicazione]** anziché **[!UICONTROL ID applicazione]**.

## Aggiungi una nuova configurazione ad Experience Cloud {#add-a-new-configuration}

1. Fai clic sul logo AEM sull’interfaccia utente dell’istanza AEM Assets locale e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Cloud Services legacy]**.

1. Individua il **[!UICONTROL Adobe Experience Cloud]** servizio. Se non esistono configurazioni, fai clic su **[!UICONTROL Configura ora]**. Se esistono configurazioni, fai clic su **[!UICONTROL Mostra configurazioni]** e fai clic su `+` per aggiungere una nuova configurazione.

   >[!NOTE]
   >
   >Utilizza un account Adobe ID con privilegi di amministratore per l’organizzazione.

1. In **[!UICONTROL Crea configurazione]** , specifica un titolo e un nome per la nuova configurazione e fai clic su **[!UICONTROL Crea]**.

   ![Assegnare un nome a una nuova configurazione per integrare AEM Assets e Creative Cloud](assets/aem-ec-integration-config1.png)

1. In **[!UICONTROL URL tenant]** specifica l’URL per AEM Assets. In passato, se l’URL era stato definito come `https://<tenant_id>.marketing.adobe.com`, modifica in `https://<tenant_id>.experiencecloud.adobe.com`.

   1. Vai a **Strumenti > Cloud Services > Servizi cloud precedenti**. In Adobe Experience Cloud, fai clic su **Mostra configurazioni**.
   1. Seleziona la configurazione esistente da modificare. Modifica la configurazione e sostituisci `marketing.adobe.com` a `experiencecloud.adobe.com`.
   1. Salva la configurazione. Test degli agenti di replica di sincronizzazione MAC.

1. In **[!UICONTROL ID client]** incolla l&#39;ID applicazione copiato alla fine della procedura [creare un&#39;applicazione](#create-an-application).

   ![Fornire i valori ID dell&#39;applicazione necessari per integrare AEM Assets e Creative Cloud](assets/cloudservices_tenant_info.png)

1. Sotto **[!UICONTROL Sincronizzazione]** select **[!UICONTROL Abilitato]** per abilitare la sincronizzazione e fai clic su **[!UICONTROL OK]**. Se si seleziona **disattivato**, la sincronizzazione funziona in una singola direzione.

1. Dalla pagina di configurazione, fai clic su **[!UICONTROL Visualizza chiave pubblica]** per visualizzare la chiave pubblica generata per la tua istanza. In alternativa, fai clic su **[!UICONTROL Scarica chiave pubblica per gateway OAuth]** per scaricare il file contenente la chiave pubblica. Quindi, apri il file per visualizzare la chiave pubblica.

## Abilita sincronizzazione {#enable-synchronization}

1. Visualizzare la chiave pubblica utilizzando uno dei metodi seguenti indicati nell&#39;ultimo passaggio della procedura [aggiungi una nuova configurazione all’Experience Cloud](#add-a-new-configuration). Fai clic su **[!UICONTROL Visualizza chiave pubblica]**.

1. Copia la chiave pubblica e incollala nella **[!UICONTROL Chiave pubblica]** campo dell&#39;interfaccia di configurazione dell&#39;applicazione creata in [creare un&#39;applicazione](#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. Fai clic su **[!UICONTROL Aggiorna]**. Sincronizza ora le risorse con l’istanza di AEM Assets.

## Verificare la sincronizzazione {#test-the-synchronization}

1. Fai clic sul logo AEM sull’interfaccia utente dell’istanza AEM Assets locale e passa a **[!UICONTROL Strumenti]**> **[!UICONTROL Distribuzione]**> **[!UICONTROL Replica]**per individuare i profili di replica creati per la sincronizzazione.
1. Sulla **[!UICONTROL Replica]** pagina, fai clic su **[!UICONTROL Agenti sull&#39;autore]**.
1. Dall’elenco dei profili, fai clic sul profilo di replica predefinito per la tua organizzazione per aprirlo.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Prova connessione]**.

   ![Verifica la connessione e imposta il profilo di replica predefinito per la tua organizzazione](assets/chlimage_1-54.png)

1. Al termine del resto della replica, controlla la presenza di un messaggio di successo alla fine dei risultati del test.

## Aggiungere utenti all’Experience Cloud {#add-users-to-experience-cloud}

1. Accedi ad Experience Cloud utilizzando le credenziali di amministratore.
1. Dai binari, vai a **[!UICONTROL Amministrazione]** quindi fai clic su **[!UICONTROL Avvia Enterprise Dashboard]**.
1. Dalla barra, fai clic su **[!UICONTROL Utenti]** per aprire **[!UICONTROL Gestione utente]** pagina.
1. Dalla barra degli strumenti, fai clic su **Aggiungi** ![aem_assets_add_icon](assets/aem_assets_add_icon.png).
1. Aggiungi uno o più utenti per consentire loro di condividere le risorse con Creative Cloud.

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## Exchange assets tra AEM Assets e Experience Cloud {#exchange-assets-between-aem-and-experience-cloud}

1. Accedi ad AEM Assets.
1. Nella console Risorse , crea una cartella e carica alcune risorse su di essa. Ad esempio, crea una cartella **mc-demo** e caricate una risorsa su di essa.
1. Seleziona la cartella e fai clic su **Condividi** ![assets_share](assets/do-not-localize/assets_share.png).
1. Dal menu , seleziona **[!UICONTROL Adobe Experience Cloud]** e fai clic su **[!UICONTROL Condividi]**. Un messaggio notifica che la cartella è condivisa con Experience Cloud.

   >[!NOTE]
   >
   >Condivisione di una cartella di risorse del tipo `sling:OrderedFolder`, non è supportato nel contesto della condivisione in Adobe Experience Cloud. Se desideri condividere una cartella, quando la crei in AEM Assets, non selezionare la **[!UICONTROL Ordinato]** opzione .

1. Aggiorna l’interfaccia utente di AEM Assets. La cartella creata nella console Risorse dell’istanza AEM Assets locale viene copiata nell’interfaccia utente di Experience Cloud. La risorsa caricata nella cartella in AEM Assets viene visualizzata nella copia della cartella in Experience Cloud dopo l’elaborazione da parte del server AEM.
1. Puoi anche caricare una risorsa nella copia replicata della cartella in Experience Cloud. Dopo l’elaborazione, la risorsa viene visualizzata nella cartella condivisa in AEM Assets.

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

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and vice versa for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [Best practice per l’integrazione di Assets e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md)

