---
title: Configurare AEM Assets con Brand Portal
seo-title: Configurare AEM Assets con Brand Portal
description: Scopri come configurare Risorse AEM con il Portale del marchio per la pubblicazione di risorse e raccolte nel Portale del marchio.
seo-description: Scopri come configurare Risorse AEM con il Portale del marchio per la pubblicazione di risorse e raccolte nel Portale del marchio.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 28354bd9785fa83939f9e3b051aac195d7706633

---


# Configurare AEM Assets con Brand Portal {#configure-integration-65}

Risorse Adobe Experience Manager (AEM) è configurato con Brand Portal tramite Adobe I/O, che fornisce un token IMS per l’autorizzazione del tenant del Brand Portal.

>[!NOTE]
>
>La configurazione di AEM Assets con Brand Portal tramite Adobe I/O è supportata in AEM 6.5.4.0 e versioni successive.
>
>Precedentemente, Brand Portal era stato configurato nell’interfaccia classica tramite il gateway OAuth legacy, che utilizza lo scambio di token JWT per ottenere un token di accesso IMS per l’autorizzazione.
>
>La configurazione tramite OAuth legacy non è più supportata dal 6 aprile 2020 e viene modificata in configurazione tramite I/O Adobe.


>[!TIP]
>
>***Solo per i clienti esistenti***
>
>Si consiglia di continuare a utilizzare la configurazione gateway OAuth esistente. Se si verificano problemi con la configurazione del gateway OAuth precedente, eliminate la configurazione esistente e create una nuova configurazione tramite Adobe I/O.



Questa guida descrive i due casi d’uso seguenti:
* [Nuova configurazione](#configure-new-integration-65): Se sei un nuovo utente del Brand Portal e vuoi configurare l’istanza di creazione di Risorse AEM con Brand Portal, puoi creare una nuova configurazione in Adobe I/O.
* [Configurazione](#upgrade-integration-65)aggiornamento: Se sei un utente esistente di Brand Portal con l’istanza di creazione di Risorse AEM configurata con Brand Portal su gateway OAuth, è consigliabile eliminare le configurazioni esistenti e creare una nuova configurazione su Adobe I/O.

Le informazioni fornite si basano sul presupposto che chiunque legga la presente Guida abbia familiarità con le seguenti tecnologie:

* Installazione, configurazione e amministrazione di pacchetti Adobe Experience Manager e AEM

* Utilizzo di sistemi operativi Linux e Microsoft Windows

## Prerequisiti {#prerequisites}

Per configurare Risorse AEM con Brand Portal è necessario disporre di quanto segue:

* Un’istanza di creazione di AEM Assets con l’ultimo Service Pack.
* URL tenant del Brand Portal.
* Un utente con privilegi di amministratore di sistema nell’organizzazione IMS del tenant Brand Portal.


[Scaricare e installare AEM 6.5](#aemquickstart)

[Scarica e installa la versione più recente di AEM Service Pack](#servicepack)

### Scaricare e installare AEM 6.5 {#aemquickstart}

È consigliabile disporre di AEM 6.5 per configurare un’istanza di creazione AEM. Se AEM non è già operativo, scaricatelo dai seguenti percorsi:

* Se siete già clienti AEM, scaricate AEM 6.5 dal sito Web [delle licenze](http://licensing.adobe.com)Adobe.

* Se sei un partner Adobe, utilizza [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) per richiedere AEM 6.5.

Dopo aver scaricato AEM, per istruzioni su come impostare un’istanza di creazione AEM, consultate [Implementazione e manutenzione](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall).

### Download e installazione dell&#39;ultimo Service Pack di AEM {#servicepack}

Per istruzioni dettagliate, vedete

* [Note sulla versione di AEM 6.5 Service Pack](https://helpx.adobe.com/it/experience-manager/6-5/release-notes/sp-release-notes.html)

**Se non riesci a trovare il pacchetto AEM o il Service Pack più recente, contatta il supporto** .

## Create configuration {#configure-new-integration-65}

Se stai configurando Risorse AEM con Brand Portal per la prima volta, effettua i seguenti passaggi nella sequenza elencata:
1. [Ottenere il certificato pubblico](#public-certificate)
1. [Crea integrazione I/O Adobe](#createnewintegration)
1. [Crea configurazione account IMS](#create-ims-account-configuration)
1. [Configurare il servizio cloud](#configure-the-cloud-service)
1. [Verifica della configurazione](#test-integration)

### Crea configurazione IMS {#create-ims-configuration}

La configurazione IMS autentica il tenant del Brand Portal con l’istanza di creazione di AEM Assets.

La configurazione IMS prevede due passaggi:

* [Ottenere il certificato pubblico](#public-certificate)
* [Crea configurazione account IMS](#create-ims-account-configuration)

### Ottenere il certificato pubblico {#public-certificate}

Il certificato pubblico consente di autenticare il profilo sull&#39;I/O di Adobe.

1. Accedi all’istanza di creazione di Risorse AEMURL predefinito: http:// localhost:4502/aem/start.html
1. Dal pannello **Strumenti** ![Strumenti](assets/tools.png) , passa a **[!UICONTROL Protezione]** > Configurazioni **[!UICONTROL Adobe IMS]**.

   ![Interfaccia utente di configurazione account Adobe IMS](assets/ims-config1.png)

1. Viene visualizzata la pagina Configurazioni Adobe IMS.

   Fai clic su **[!UICONTROL Crea]**.

   Viene visualizzata la pagina Configurazione **[!UICONTROL account tecnico]** Adobe IMS.

1. Per impostazione predefinita, si apre la scheda **Certificato** .

   In **Cloud Solution**, selezionate **[!UICONTROL Adobe Brand Portal]**.

1. Contrassegnate la casella di controllo **[!UICONTROL Create un nuovo certificato]** e specificate un **alias** per il certificato. L’alias funge da nome della finestra di dialogo.

1. Fate clic su **[!UICONTROL Crea certificato]**. Viene visualizzata una finestra di dialogo. Fate clic su **[!UICONTROL OK]** per generare il certificato pubblico.

   ![Crea certificato](assets/ims-config2.png)

1. Fate clic su **[!UICONTROL Scarica chiave]** pubblica e salvate il file di certificato *AEM-Adobe-IMS.crt* sul computer. Il file del certificato viene utilizzato per [creare l&#39;integrazione](#createnewintegration)I/O Adobe.

   ![Scarica certificato](assets/ims-config3.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   Nella scheda **Account** , potete creare l&#39;account Adobe IMS, ma per questo dovrete disporre dei dettagli di integrazione. Tenete questa pagina aperta per ora.

   Aprite una nuova scheda e [create l&#39;integrazione](#createnewintegration) I/O Adobe per ottenere i dettagli di integrazione per le configurazioni dell&#39;account IMS.

### Crea integrazione I/O Adobe {#createnewintegration}

L&#39;integrazione I/O di Adobe genera Chiave API, Segreto cliente e Payload (JWT), necessaria per configurare le configurazioni dell&#39;account IMS.

1. Accedete alla console di I/O di Adobe con privilegi di amministratore di sistema nell’organizzazione IMS del tenant Brand Portal.

   URL predefinito: [https://console.adobe.io/](https://console.adobe.io/)

1. Fate clic su **[!UICONTROL Crea integrazione]**.

1. Selezionate **[!UICONTROL Accesso a un&#39;API]** e fate clic su **[!UICONTROL Continua]**.

   ![Crea nuova integrazione](assets/create-new-integration1.png)

1. Viene visualizzata una nuova pagina di integrazione.

   Seleziona la tua organizzazione dall’elenco a discesa.

   In **[!UICONTROL Experience Cloud]**, seleziona **[!UICONTROL AEM Brand Portal]** e fai clic su **[!UICONTROL Continua]**.

   Se l’opzione Portale marchio è disabilitata, accertatevi di aver selezionato l’organizzazione corretta dalla casella a discesa sopra l’opzione **[!UICONTROL Adobe Services]** . Se non conosci la tua organizzazione, contatta l’amministratore.

   ![Crea integrazione](assets/create-new-integration2.png)

1. Specificate un nome e una descrizione per l&#39;integrazione. Fate clic su **[!UICONTROL Seleziona un file dal computer]** e caricate il `AEM-Adobe-IMS.crt` file scaricato nella sezione [Ottieni certificati](#public-certificate) pubblici.

1. Seleziona il profilo della tua organizzazione.

   In alternativa, seleziona il profilo predefinito **[!UICONTROL Assets Brand Portal]** e fai clic su **[!UICONTROL Crea integrazione]**. L&#39;integrazione viene creata.

1. Fate clic su **[!UICONTROL Continua per visualizzare i dettagli]** dell&#39;integrazione.

   Copiare la chiave **[!UICONTROL API]**

   Fate clic su **[!UICONTROL Recupera Segreto]** cliente e copiate la chiave Segreto cliente.

   ![Informazioni su chiave API, segreto cliente e payload di un&#39;integrazione](assets/create-new-integration3.png)

1. Passate alla scheda **[!UICONTROL JWT]** e copiate il payload **** JWT.

   Le informazioni relative alla chiave API, alla chiave segreta client e al payload JWT verranno utilizzate per creare la configurazione dell&#39;account IMS.

### Crea configurazione account IMS {#create-ims-account-configuration}

Assicurarsi di aver eseguito i seguenti passaggi:

* [Ottenere il certificato pubblico](#public-certificate)
* [Crea integrazione I/O Adobe](#createnewintegration)

**Passaggi per creare la configurazione dell&#39;account IMS:**

1. Aprite la pagina Configurazione IMS, scheda **[!UICONTROL Account]** . Hai tenuto la pagina aperta alla fine della sezione [Ottieni certificato](#public-certificate)pubblico.

1. Specificate un **[!UICONTROL Titolo]** per l&#39;account IMS.

   Nel server **** di autorizzazione, immettete l’URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Incollate la chiave API, il segreto cliente e il payload JWT che avete copiato al termine dell&#39;integrazione [di](#createnewintegration)Crea I/O Adobe.

   Fai clic su **[!UICONTROL Crea]**.

   Viene creata l&#39;integrazione.

   ![Configurazione account IMS](assets/create-new-integration6.png)


1. Selezionate la configurazione IMS e fate clic su **[!UICONTROL Verifica stato]**. Viene visualizzata una finestra di dialogo.

   Fate clic su **[!UICONTROL Controlla]**. In caso di connessione riuscita, viene visualizzato il messaggio *Token recuperato* .

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Create una sola configurazione IMS valida.
>
> Verificate che la configurazione sia sana. Nel caso in cui la configurazione non sia sana, eliminarla e creare una nuova configurazione sana.


### Configurare il servizio cloud {#configure-the-cloud-service}

Per creare la configurazione del servizio cloud Brand Portal, effettuate le seguenti operazioni:

1. Accedi all’istanza di creazione di Risorse AEM

   URL predefinito: http:// localhost:4502/aem/start.html
1. Dal pannello **Strumenti** ![Strumenti](assets/tools.png) , andate a Servizi **[!UICONTROL Cloud > AEM Brand Portal]**.

   Si apre la pagina Configurazioni Brand Portal.

1. Fai clic su **[!UICONTROL Crea]**.

1. Specificate un **[!UICONTROL Titolo]** per la configurazione.

   Selezionate IMS Configuration (Configurazione IMS) creata nel passaggio, [create IMS Account configuration](#create-ims-account-configuration).

   Nell’URL **[!UICONTROL del]** servizio, immettete l’URL tenant del Portale marchio.

   ![](assets/create-cloud-service.png)

1. Click **[!UICONTROL Save and Close]**. Viene creata la configurazione cloud. L’istanza di creazione di AEM Assets ora è integrata con il tenant del Brand Portal.

### Test configuration {#test-integration}

1. Accedi all’istanza di creazione di Risorse AEM

   URL predefinito: http:// localhost:4502/aem/start.html

1. Dal pannello **Strumenti** ![Strumenti](assets/tools.png) , passare a **[!UICONTROL Distribuzione > Replica]**.

   ![](assets/test-integration1.png)

1. Viene visualizzata la pagina Replica.

   Fate clic su **[!UICONTROL Agenti sull’autore]**.

   ![](assets/test-integration2.png)

1. Per ciascun tenant vengono creati quattro agenti di replica.

   Individuate gli agenti di replica del tenant del Brand Portal.

   Fate clic sull&#39;URL dell&#39;agente di replica.

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >Gli agenti di replica lavorano in parallelo e condividono la distribuzione dei processi in modo uniforme, aumentando così la velocità di pubblicazione di quattro volte la velocità originale. Una volta configurato il servizio cloud, non è richiesta ulteriore configurazione per abilitare gli agenti di replica attivati per impostazione predefinita per abilitare la pubblicazione parallela di più risorse.

   >[!NOTE]
   >
   >Evitare di disattivare gli agenti di replica, in quanto potrebbe causare errori di replica di alcune risorse.


1. Per verificare la connessione tra l’autore di Risorse AEM e il portale dei marchi, fai clic su **[!UICONTROL Verifica connessione]**.

   ![](assets/test-integration4.png)

1. Esaminate la parte inferiore dei risultati del test per verificare che la replica sia riuscita.

   ![](assets/test-integration5.png)

   >[!NOTE]
   >
   >Gli agenti di replica lavorano in parallelo e condividono la distribuzione dei processi in modo uniforme, aumentando così la velocità di pubblicazione di quattro volte la velocità originale. Una volta configurato il servizio cloud, non è richiesta ulteriore configurazione per abilitare gli agenti di replica attivati per impostazione predefinita per abilitare la pubblicazione parallela di più risorse.

1. Verificate i risultati del test su tutti e quattro gli agenti di replica uno per uno.


   >[!NOTE]
   >
   >Evitare di disattivare gli agenti di replica, in quanto potrebbe causare errori di replica di alcune risorse.

Brand Portal è stato configurato correttamente con l’istanza di creazione di Risorse AEM. È ora possibile:

* [Pubblicare risorse da Risorse AEM a Brand Portal](../assets/brand-portal-publish-assets.md)
* [Pubblicare cartelle da Risorse AEM a Brand Portal](../assets/brand-portal-publish-folder.md)
* [Pubblicare raccolte da Risorse AEM a Brand Portal](../assets/brand-portal-publish-collection.md)
* [Configurare l’origine](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) delle risorse per consentire agli utenti del Brand Portal di contribuire e pubblicare le risorse in Risorse AEM.

## Aggiornamento della configurazione {#upgrade-integration-65}

Per aggiornare le configurazioni esistenti, eseguite i seguenti passaggi nella sequenza elencata:
1. [Verificare i processi in esecuzione](#verify-jobs)
1. [Elimina configurazioni esistenti](#delete-existing-configuration)
1. [Crea configurazione](#configure-new-integration-65)

### Verificare i processi in esecuzione {#verify-jobs}

Prima di apportare eventuali modifiche, accertati che nell’istanza di creazione di Risorse AEM non sia in esecuzione alcun processo di pubblicazione. A tal fine, è possibile verificare tutti e quattro gli agenti di replica e assicurarsi che la coda sia ideale/vuota.

1. Accedi all’istanza di creazione di Risorse AEM

   URL predefinito: http:// localhost:4502/aem/start.html

1. Dal pannello **Strumenti** ![Strumenti](assets/tools.png) , passare a **[!UICONTROL Distribuzione > Replica]**.

1. Viene visualizzata la pagina Replica.

   Fate clic su **[!UICONTROL Agenti sull’autore]**.

   ![](assets/test-integration2.png)

1. Individuate gli agenti di replica del tenant del Brand Portal.

   Verificate che la **coda sia inattiva** per tutti gli agenti di replica. Nessun processo di pubblicazione attivo.

   ![](assets/test-integration3.png)

### Elimina configurazioni esistenti {#delete-existing-configuration}

È necessario eseguire il seguente elenco di controllo durante l&#39;eliminazione delle configurazioni esistenti.
* Elimina tutti e quattro gli agenti di replica
* Elimina servizio cloud
* Elimina utente MAC

1. Accedi all’istanza di creazione di Risorse AEM e apri CRX Lite come amministratore.

   URL predefinito: http:// localhost:4502/crx/de/index.jsp

1. Individuate `/etc/replications/agents.author` ed eliminate tutti e quattro gli agenti di replica del tenant del Brand Portal in uso.

   ![](assets/delete-replication-agent.png)

1. Andate a `/etc/cloudservices/mediaportal` ed eliminate la configurazione **del servizio** Cloud.

   ![](assets/delete-cloud-service.png)

1. Individuate `/home/users/mac` ed eliminate l&#39;utente **** MAC del tenant di Brand Portal.

   ![](assets/delete-mac-user.png)


Ora puoi [creare la configurazione](#configure-new-integration-65) sull’istanza di creazione di AEM 6.5 su Adobe I/O.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

Una volta completata la replica, potete pubblicare risorse, cartelle e raccolte in Brand Portal. Per informazioni dettagliate, consultate:

* [Pubblicare risorse su Brand Portal](/help/assets/brand-portal-publish-assets.md)
* [Pubblicare le cartelle su Brand Portal](/help/assets/brand-portal-publish-folder.md)
* [Pubblicare raccolte nel portale dei marchi](/help/assets/brand-portal-publish-collection.md)
