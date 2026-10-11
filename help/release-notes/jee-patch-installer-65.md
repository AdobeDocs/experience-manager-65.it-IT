---
title: Programma di installazione patch per AEM Forms JEE
description: Scopri come utilizzare AEM Forms JEE Patch Installer per risolvere i problemi dei componenti di AEM 6.5 Forms.
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
hide: true
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 26%
---
# Programma di installazione patch per AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Contattare il supporto tecnico](https://experienceleague.adobe.com/it?support-solution=General&support-tab=homehome?lang=it#support) per ulteriori informazioni o per ottenere la patch.

## Informazioni sul programma di installazione delle patch {#about-the-patch-installer}

Il programma di installazione delle patch di AEM 6.5 Forms JEE include tutti i problemi risolti relativi a tutti i componenti di AEM 6.5 Forms JEE disponibili fino al rilascio di questa patch. Per un elenco completo dei problemi risolti, consulta le ultime [note sulla versione del Service Pack](release-notes.md).

## Prerequisiti per l’installazione della patch {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installazione e configurazione della patch {#installing-and-configuring-the-patch}

1. Esegui un backup della cartella &lt;*AEM_forms_root*>/deploy. Sarà necessaria se decidi di disinstallare la correzione rapida.
1. Arresta il server applicazioni.
1. Estrai sul disco rigido il file archivio del programma di installazione della patch.
1. Nella directory denominata in base al sistema operativo in uso:

   * **Windows**
     Passare alla directory appropriata sul supporto di installazione o sulla cartella del disco rigido in cui è stato copiato il programma di installazione, quindi fare doppio clic sul file aemforms65_cfp_install.exe.

     * (Windows a 32 bit) `Windows\Disk1\InstData\VM`
     * (Windows a 64 bit) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
     Passare alla directory appropriata e dal prompt dei comandi digitare `./aem65_cfp_install.bin`.

     * (Linux®) `Linux/Disk1/InstData/NoVM`

   Viene avviata una procedura di installazione guidata.

1. Nel pannello introduttivo, fai clic su **[!UICONTROL Avanti]**.
1. Nella schermata **Scegli cartella di installazione**, verifica che il percorso predefinito visualizzato sia corretto per l&#39;installazione esistente oppure fai clic su **[!UICONTROL Sfoglia]** per selezionare la cartella alternativa in cui è installato AEM Forms, quindi fai clic su **[!UICONTROL Avanti]**.
1. Leggi le informazioni di riepilogo della patch di correzione rapida e fai clic su **[!UICONTROL Avanti]**.
1. Leggi le informazioni di riepilogo di pre-installazione e fai clic su **[!UICONTROL Installa]**.
1. Al termine dell’installazione, fai clic su **[!UICONTROL Avanti]** per applicare gli aggiornamenti della correzione rapida ai file installati.

1. **[Solo per Windows]:** Effettuare le seguenti operazioni:
   * Deselezionare l&#39;opzione **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Eseguire **Configuration Manager** utilizzando il file **ConfigurationManager.bat** in `[aem-forms root]\configurationManager\bin`.

   * In alternativa, deselezionare l&#39;opzione **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Prima di eseguire **Configuration Manager** utilizzando **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, passare alla directory *`<AEMForms_Install_Dir>\configurationManager\bin`* e sostituire **ConfigurationManager.lax** e **ConfigurationManager_IPV6.lax** con i file [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) più recenti, cercare e sostituire **axis-1.4.1.1.jar** con **asse-1.4.1.2.jar** in questi due file.

   >[!NOTE]
   >
   >L&#39;utilizzo del file **ConfigurationManager.bat** consente di evitare l&#39;aggiornamento manuale del nome dei file con estensione lax.
   >

1. **[Solo per Unix]:**

   * La casella di controllo **Avvia Configuration Manager** è selezionata per impostazione predefinita. Fai clic su **[!UICONTROL Fine]** per eseguire Configuration Manager immediatamente o su **Configuration Manager** in un secondo momento, deseleziona l&#39;opzione **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. È possibile avviare **Configuration Manager** in un secondo momento utilizzando lo script appropriato nella directory `[AEM_forms_root]/configurationManager/bin`.

1. A seconda del server applicazioni in uso, scegliere uno dei seguenti documenti e seguire le istruzioni riportate nella sezione *Configurazione e distribuzione di AEM Forms*.

   * [Installazione e distribuzione di AEM Forms per JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_it)
   * [Installazione e distribuzione di AEM Forms per WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_it)

1. (Solo JBoss®) Dopo aver installato la patch e configurato il server, eliminare tmp e le directory di lavoro del server applicazioni JBoss®.

## Configurazioni post-distribuzione {#post-deployment-configurations}

### Configurazioni SAML {#saml-configurations}

Se l’autenticazione SAML è configurata e si verificano problemi con metadati IDP di grandi dimensioni, dopo l’installazione della patch effettua le seguenti operazioni:

1. Impostare la seguente proprietà di sistema nel server applicazioni:\
   `um.saml.enable.large.xml=true`
1. Riavvia il server.
1. Elimina i provider di autenticazione SAML esistenti e aggiungili nuovamente per i domini esistenti come descritto in Impostazioni SAML.

>[!NOTE]
>
> Si consiglia di utilizzare il comando “Ctrl + C” per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

## Moduli interessati {#impacted-modules}

* Servizi per documenti
* Protezione dei documenti
* JEE per Foundation

[Contatta il supporto](https://experienceleague.adobe.com/it?support-solution=General&support-tab=homehome?lang=it#support)
