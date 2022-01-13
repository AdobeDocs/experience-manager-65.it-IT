---
title: Modulo di installazione delle patch di AEM Forms JEE
description: Modulo di installazione delle patch di AEM Forms JEE
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 29%

---

# Modulo di installazione delle patch di AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Contatta il supporto](https://www.adobe.com/account/sign-in.supportportal.html) per ulteriori informazioni o per ottenere la patch.

## Informazioni sul programma di installazione della patch {#about-the-patch-installer}

Il programma di installazione delle patch JEE per Forms 6.5 AEM include tutti i problemi risolti per tutti i componenti di JEE Forms 6.5 disponibili fino al rilascio di questa patch. Scopri le ultime  [Note sulla versione del Service Pack](release-notes.md) per un elenco completo dei problemi risolti.

## Prerequisiti per l’installazione della patch {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installazione e configurazione della patch {#installing-and-configuring-the-patch}

1. Esegui un backup del &lt;*AEM_forms_root*>/distribuisci cartella. Sarà necessaria se decidi di disinstallare la correzione rapida.
1. Arresta il server applicazioni.
1. Estrai sul disco rigido il file archivio del programma di installazione della patch.
1. Nella directory denominata in base al sistema operativo in uso:

   * **Windows**
Accedere alla directory appropriata del supporto di installazione o della cartella sul disco rigido in cui è stato copiato il programma di installazione, quindi fare doppio clic sul file aemforms65_cfp_install.exe.

      * (Windows a 32 bit) `Windows\Disk1\InstData\VM`
      * (Windows a 64 bit) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**
Passa alla directory appropriata e, dal prompt dei comandi, digita 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Viene avviata una procedura di installazione guidata.

1. Nel pannello introduttivo, fai clic su **[!UICONTROL Avanti]**.
1. Nella schermata Scegli cartella di installazione , verifica che il percorso predefinito visualizzato sia corretto per l’installazione esistente oppure fai clic su **[!UICONTROL Sfoglia]** per selezionare la cartella alternativa in cui è installato AEM moduli e fare clic su **[!UICONTROL Successivo]**.
1. Leggi le informazioni di riepilogo della patch di correzione rapida e fai clic su **[!UICONTROL Avanti]**.
1. Leggi le informazioni di riepilogo di pre-installazione e fai clic su **[!UICONTROL Installa]**.
1. Al termine dell’installazione, fai clic su **[!UICONTROL Avanti]** per applicare gli aggiornamenti della correzione rapida ai file installati.

1. Deselezionare l&#39;opzione Avvia Configuration Manager prima di fare clic su Fine. Prima di eseguire la gestione della configurazione utilizzando **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, passa a *&lt;aemforms_install_dir>\configurationManager\bin* directory e aggiornamento `ConfigurationManager.lax` e `ConfigurationManager_IPv6.lax` file con le seguenti operazioni di ridenominazione:

   * `axis.jar` a `axis-1.4.1.1.jar`
   * `serializer-2.7.1.jar` a `serializer-2.7.2.jar`
   * `xalan-2.7.1.jar` a `xalan-2.7.2.jar`
   * `xercesImpl-2.9.1.jar` a `xercesImpl-2.12.0.jar`
   * `xml-apis-2.7.1.jar` a `xml-apis-2.7.2.jar`

1. La casella di controllo Avvia Configuration Manager è selezionata per impostazione predefinita. Fai clic su **[!UICONTROL Fine]** per eseguire Configuration Manager.

1. Per eseguire Configuration Manager in un secondo momento, deseleziona l’opzione Avvia Configuration Manager prima di fare clic su Fine. Puoi avviare Configuration Manager in un secondo momento utilizzando lo script appropriato nel `[AEM_forms_root]/configurationManager/bin` directory.

1. A seconda del server delle applicazioni, scegli uno dei seguenti documenti e segui le istruzioni in *Configurazione e distribuzione dei moduli AEM* sezione .

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

* Document Services
* Document Security
* JEE per Foundation

[Contatta il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
