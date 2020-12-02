---
title: ' programma di installazione patch JEE AEM Forms'
description: 'null'
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
translation-type: tm+mt
source-git-commit: c1af919d4c0fd984249e1a7009274c63b8ce9adb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---


#  AEM Forms JEE Patch Installer {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Per ulteriori informazioni o per ottenere ](https://www.adobe.com/account/sign-in.supportportal.html) la patch, contattate il supporto.

## Informazioni sul programma di installazione della patch {#about-the-patch-installer}

Il programma di installazione AEM patch Forms JEE 6.5 include tutti i problemi risolti per tutti i componenti di AEM 6.5 Forms JEE disponibili fino al rilascio di questa patch. Per un elenco completo dei problemi risolti, consultare le ultime [Note sulla versione di Service Pack](sp-release-notes.md).

## Prerequisiti per l&#39;installazione della patch {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installazione e configurazione della patch {#installing-and-configuring-the-patch}

1. Eseguire un backup della cartella &lt;*AEM_forms_root*>/deploying. È richiesto se si decide di disinstallare la correzione rapida.
1. Arrestate il server applicazione.
1. Estrarre il file di archivio del programma di installazione della patch sul disco rigido.
1. Nella directory denominata in base al sistema operativo in uso:

   * ****
WindowsIndividuate la directory appropriata nel supporto di installazione o nella cartella del disco rigido in cui avete copiato il programma di installazione, quindi fate doppio clic sul file aemforms65_cfp_install.exe.

      * (Windows a 32 bit) `Windows\Disk1\InstData\VM`
      * (Windows a 64 bit) `Windows_64Bit`\ `Disk1\InstData\VM`
   * ****
LinuxPassare alla directory appropriata e da un prompt dei comandi digitare 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Viene avviata una procedura guidata di installazione che illustra le procedure di installazione.

1. Nel pannello Introduzione, fate clic su **[!UICONTROL Next]**.
1. Nella schermata Scegli cartella di installazione, verificare che il percorso predefinito visualizzato sia corretto per l&#39;installazione esistente oppure fare clic su **[!UICONTROL Sfoglia]** per selezionare la cartella alternativa in cui sono installati AEM moduli, quindi fare clic su **[!UICONTROL Avanti]**.
1. Leggere le informazioni di riepilogo delle patch per la correzione rapida e fare clic su **[!UICONTROL Avanti]**.
1. Leggere il Riepilogo pre-installazione e fare clic su **[!UICONTROL Installa]**.
1. Al termine dell&#39;installazione, fare clic su **[!UICONTROL Next]** per applicare gli aggiornamenti della correzione rapida ai file installati.

1. Deselezionate l&#39;opzione Avvia Configuration Manager prima di fare clic su Fine. Prima di eseguire Configuration Manager con **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, passare alla directory *&lt;AEMForms_Install_Dir>\configurationManager\bin* e aggiornare **axis.jar** su **axis-1.4.1.1.jar** nei file seguenti:

   * ConfigurationManager.lax
   * ConfigurationManager_IPv6.lax

1. La casella di controllo Avvia Configuration Manager è selezionata per impostazione predefinita. Fare clic su **[!UICONTROL Fine]** per eseguire Gestione configurazione.

1. Per eseguire Configuration Manager in un secondo momento, deselezionare l&#39;opzione Avvia Configuration Manager prima di fare clic su Fine. È possibile avviare Configuration Manager in un secondo momento utilizzando lo script appropriato nella directory `[AEM_forms_root]/configurationManager/bin`.

1. A seconda del server applicazione, scegliere uno dei documenti seguenti e seguire le istruzioni riportate nella sezione *Configurazione e distribuzione AEM moduli*.

   * [Installazione e distribuzione di moduli AEM per JBoss](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installazione e distribuzione di moduli AEM per WebSphere](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Solo JBoss) Dopo aver installato la patch e configurato il server, eliminare tmp e le directory di lavoro del server applicazioni JBoss.

## Configurazioni post-distribuzione {#post-deployment-configurations}

### Configurazioni SAML {#saml-configurations}

Se l’autenticazione SAML è stata configurata e si verificano problemi con metadati IDP di grandi dimensioni, dopo l’installazione della patch effettuate le seguenti operazioni:

1. Impostate la seguente proprietà di sistema nel server applicazione:\
   `um.saml.enable.large.xml=true`
1. Riavviate il server.
1. Eliminate i provider di autenticazione SAML esistenti e aggiungeteli di nuovo per i domini esistenti come descritto nelle impostazioni SAML.

## Moduli interessati {#impacted-modules}

* Servizi basati su documenti
* Sicurezza dei documenti
* JEE per Foundation

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
