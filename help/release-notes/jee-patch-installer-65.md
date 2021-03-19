---
title: Modulo di installazione delle patch di AEM Forms JEE
description: Modulo di installazione delle patch di AEM Forms JEE
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 28%

---


# Modulo di installazione delle patch JEE per AEM Forms {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Per ulteriori informazioni o per ottenere la patch, contatta ](https://www.adobe.com/account/sign-in.supportportal.html) il supporto.

## Informazioni sul programma di installazione delle patch {#about-the-patch-installer}

Il programma di installazione delle patch JEE per Forms 6.5 AEM include tutti i problemi risolti per tutti i componenti di JEE Forms 6.5 disponibili fino al rilascio di questa patch. Per un elenco completo dei problemi risolti, consulta le [Note sulla versione del Service Pack](sp-release-notes.md) più recenti.

## Prerequisiti per l’installazione della patch {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installazione e configurazione della patch {#installing-and-configuring-the-patch}

1. Esegui un backup della cartella &lt;*AEM_forms_root*>/deploy. Sarà necessaria se decidi di disinstallare la correzione rapida.
1. Arresta il server applicazioni.
1. Estrai sul disco rigido il file archivio del programma di installazione della patch.
1. Nella directory denominata in base al sistema operativo in uso:

   * **Windows**
Accedere alla directory appropriata del supporto di installazione o della cartella sul disco rigido in cui è stato copiato il programma di installazione, quindi fare doppio clic sul file aemforms65_cfp_install.exe.

      * (Windows a 32 bit) `Windows\Disk1\InstData\VM`
      * (Windows a 64 bit) `Windows_64Bit`\ `Disk1\InstData\VM`
   * ****
LinuxPassa alla directory appropriata e, dal prompt dei comandi, digita 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Viene avviata una procedura di installazione guidata.

1. Nel pannello introduttivo, fai clic su **[!UICONTROL Avanti]**.
1. Nella schermata Scegli cartella di installazione verificare che il percorso predefinito visualizzato sia corretto per l&#39;installazione esistente oppure fare clic su **[!UICONTROL Sfoglia]** per selezionare la cartella alternativa in cui è installato AEM moduli e fare clic su **[!UICONTROL Avanti]**.
1. Leggi le informazioni di riepilogo della patch di correzione rapida e fai clic su **[!UICONTROL Avanti]**.
1. Leggi le informazioni di riepilogo di pre-installazione e fai clic su **[!UICONTROL Installa]**.
1. Al termine dell’installazione, fai clic su **[!UICONTROL Avanti]** per applicare gli aggiornamenti della correzione rapida ai file installati.

1. Deselezionare l&#39;opzione Avvia Configuration Manager prima di fare clic su Fine. Prima di eseguire la gestione della configurazione utilizzando **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, accedi alla directory *&lt;AEMForms_Install_Dir>\configurationManager\bin* e aggiorna **axis.jar** axis-1.4.1.1 .jar **nei file seguenti:**

   * ConfigurationManager.lax
   * ConfigurationManager_IPv6.lax

1. La casella di controllo Avvia Configuration Manager è selezionata per impostazione predefinita. Fai clic su **[!UICONTROL Fine]** per eseguire Configuration Manager.

1. Per eseguire Configuration Manager in un secondo momento, deseleziona l’opzione Avvia Configuration Manager prima di fare clic su Fine. Puoi avviare Configuration Manager in un secondo momento utilizzando lo script appropriato nella directory `[AEM_forms_root]/configurationManager/bin`.

1. A seconda del server applicazioni, scegli uno dei seguenti documenti e segui le istruzioni contenute nella sezione *Configurazione e distribuzione di moduli AEM* .

   * [Installazione e distribuzione di moduli AEM per JBoss](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installazione e distribuzione di moduli AEM per WebSphere](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Solo JBoss) Dopo aver installato la patch e configurato il server, elimina tmp e le directory di lavoro del server applicazioni JBoss.

## Configurazioni post-distribuzione {#post-deployment-configurations}

### Configurazioni SAML {#saml-configurations}

Se hai configurato l’autenticazione SAML e hai problemi con metadati IDP di grandi dimensioni, procedi come segue dopo l’installazione della patch:

1. Imposta la seguente proprietà di sistema nel server dell&#39;applicazione:\
   `um.saml.enable.large.xml=true`
1. Riavvia il server.
1. Elimina i provider di autenticazione SAML esistenti e aggiungili di nuovo per i domini esistenti come descritto nelle impostazioni SAML.

## Moduli interessati {#impacted-modules}

* Servizi documentali
* Sicurezza dei documenti
* JEE per Foundation

[Contatta il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
