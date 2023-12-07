---
title: Programma di installazione patch per AEM Forms JEE
description: Scopri come utilizzare AEM Forms JEE Patch Installer per risolvere i problemi dei componenti di Forms AEM 6.5.
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 19%

---

# Programma di installazione patch per AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Contatta il supporto](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=homehome?lang=it#support) per ulteriori informazioni o per ottenere la patch.

## Informazioni sul programma di installazione delle patch {#about-the-patch-installer}

Il programma di installazione delle patch per Forms JEE per AEM 6.5 include tutti i problemi risolti relativi a tutti i componenti di Forms JEE per AEM 6.5 disponibili fino al rilascio di questa patch. Scopri le ultime novità  [Note sulla versione del Service Pack](release-notes.md) per un elenco completo dei problemi risolti.

## Prerequisiti per l’installazione della patch {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installazione e configurazione della patch {#installing-and-configuring-the-patch}

1. Effettua una copia di backup di &lt;*AEM_forms_root* cartella >/deploy. Sarà necessaria se decidi di disinstallare la correzione rapida.
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
1. Il giorno **Scegli cartella di installazione** , verificare che il percorso predefinito visualizzato sia corretto per l&#39;installazione esistente oppure fare clic su **[!UICONTROL Sfoglia]** per selezionare la cartella alternativa in cui è installato AEM forms, quindi fare clic su **[!UICONTROL Successivo]**.
1. Leggi le informazioni di riepilogo della patch di correzione rapida e fai clic su **[!UICONTROL Avanti]**.
1. Leggi le informazioni di riepilogo di pre-installazione e fai clic su **[!UICONTROL Installa]**.
1. Al termine dell’installazione, fai clic su **[!UICONTROL Avanti]** per applicare gli aggiornamenti della correzione rapida ai file installati.

1. **[Solo per Windows]:** Effettua le seguenti operazioni:
   * Deseleziona la **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Esegui **Gestione configurazione** utilizzando **ConfigurationManager.bat** file in `[aem-forms root]\configurationManager\bin`.

   * Oppure deseleziona il **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Prima dell’esecuzione **Gestione configurazione** utilizzo **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, passa a *`<AEMForms_Install_Dir>\configurationManager\bin`* directory e sostituzione [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) file.

   >[!NOTE]
   >
   >Utilizzo di **ConfigurationManager.bat** file consente di evitare di aggiornare manualmente il nome dei file con estensione lax.
   >

1. **[Solo per Unix]:**

   * Il **Avvia Configuration Manager** per impostazione predefinita. Clic **[!UICONTROL Fine]** per eseguire Configuration Manager immediatamente o per eseguire **Gestione configurazione** in seguito, deseleziona la **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Puoi iniziare **Gestione configurazione** in un secondo momento utilizzando lo script appropriato nel `[AEM_forms_root]/configurationManager/bin` directory.

1. In base al server applicazioni in uso, scegliere uno dei seguenti documenti e seguire le istruzioni riportate nella *Configurazione e distribuzione dei moduli AEM* sezione.

   * [Installazione e distribuzione di moduli AEM per JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installazione e distribuzione di moduli AEM per WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Solo JBoss®) Dopo aver installato la patch e configurato il server, eliminare tmp e le directory di lavoro del server applicazioni JBoss®.

## Configurazioni post-distribuzione {#post-deployment-configurations}

### Configurazioni SAML {#saml-configurations}

Se l’autenticazione SAML è configurata e si verificano problemi con metadati IDP di grandi dimensioni, dopo l’installazione della patch effettua le seguenti operazioni:

1. Impostare la seguente proprietà di sistema nel server applicazioni:\
   `um.saml.enable.large.xml=true`
1. Riavviare il server.
1. Elimina i provider di autenticazione SAML esistenti e aggiungili nuovamente per i domini esistenti come descritto in Impostazioni SAML.

## Moduli interessati {#impacted-modules}

* Document Services
* Document Security
* JEE per Foundation

[Contatta il supporto](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=homehome?lang=it#support)
