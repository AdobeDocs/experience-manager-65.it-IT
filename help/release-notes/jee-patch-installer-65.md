---
title: Programma di installazione patch per AEM Forms JEE
description: Scopri come utilizzare AEM Forms JEE Patch Installer per risolvere i problemi dei componenti di Forms AEM 6.5.
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
hide: true
hidefromtoc: true
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 17%

---

# Programma di installazione patch per AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Contattare il supporto tecnico](https://experienceleague.adobe.com/it?support-solution=General&support-tab=homehome?lang=it#support) per ulteriori informazioni o per ottenere la patch.

## Informazioni sul programma di installazione delle patch {#about-the-patch-installer}

Il programma di installazione delle patch per Forms JEE per AEM 6.5 include tutti i problemi risolti relativi a tutti i componenti di Forms JEE per AEM 6.5 disponibili fino al rilascio di questa patch. Per un elenco completo dei problemi risolti, consulta le ultime [note sulla versione del Service Pack](release-notes.md).

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
1. Nella schermata **Scegli cartella di installazione**, verifica che il percorso predefinito visualizzato sia corretto per l&#39;installazione esistente oppure fai clic su **[!UICONTROL Sfoglia]** per selezionare la cartella alternativa in cui sono installati i moduli AEM, quindi fai clic su **[!UICONTROL Avanti]**.
1. Leggi le informazioni di riepilogo della patch di correzione rapida e fai clic su **[!UICONTROL Avanti]**.
1. Leggi le informazioni di riepilogo di pre-installazione e fai clic su **[!UICONTROL Installa]**.
1. Al termine dell’installazione, fai clic su **[!UICONTROL Avanti]** per applicare gli aggiornamenti della correzione rapida ai file installati.

1. **[Solo per Windows]:** Effettuare le seguenti operazioni:
   * Deselezionare l&#39;opzione **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Eseguire **Configuration Manager** utilizzando il file **ConfigurationManager.bat** in `[aem-forms root]\configurationManager\bin`.

   * In alternativa, deselezionare l&#39;opzione **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Prima di eseguire **Configuration Manager** utilizzando **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, passare alla directory *`<AEMForms_Install_Dir>\configurationManager\bin`* e sostituire **ConfigurationManager.lax** e **ConfigurationManager_IPV6.lax** con i file [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) più recenti, cercare e sostituire **axis-1.4.1.1.jar** **axis-1.4.1.2.jar** in questi due file.

   >[!NOTE]
   >
   >L&#39;utilizzo del file **ConfigurationManager.bat** consente di evitare l&#39;aggiornamento manuale del nome dei file con estensione lax.
   >

1. **[Solo per Unix]:**

   * La casella di controllo **Avvia Configuration Manager** è selezionata per impostazione predefinita. Fai clic su **[!UICONTROL Fine]** per eseguire Configuration Manager immediatamente o su **Configuration Manager** in un secondo momento, deseleziona l&#39;opzione **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. È possibile avviare **Configuration Manager** in un secondo momento utilizzando lo script appropriato nella directory `[AEM_forms_root]/configurationManager/bin`.

1. A seconda del server applicazioni in uso, scegliere uno dei seguenti documenti e seguire le istruzioni riportate nella sezione *Configurazione e distribuzione dei moduli AEM*.

   * [Installazione e distribuzione di moduli AEM per JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_it)
   * [Installazione e distribuzione di moduli AEM per WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_it)

1. (Solo JBoss®) Dopo aver installato la patch e configurato il server, eliminare tmp e le directory di lavoro del server applicazioni JBoss®.

## Configurazioni di distribuzione Post {#post-deployment-configurations}

### Configurazioni SAML {#saml-configurations}

Se l’autenticazione SAML è configurata e si verificano problemi con metadati IDP di grandi dimensioni, dopo l’installazione della patch effettua le seguenti operazioni:

1. Impostare la seguente proprietà di sistema nel server applicazioni:\
   `um.saml.enable.large.xml=true`
1. Riavviare il server.
1. Elimina i provider di autenticazione SAML esistenti e aggiungili nuovamente per i domini esistenti come descritto in Impostazioni SAML.

>[!NOTE]
>
> Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

## Moduli interessati {#impacted-modules}

* Document Services
* Document Security
* JEE per Foundation

[Contatta il supporto](https://experienceleague.adobe.com/it?support-solution=General&support-tab=homehome?lang=it#support)
