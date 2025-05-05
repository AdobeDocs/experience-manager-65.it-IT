---
title: Istruzioni di installazione delle patch AEM Forms per AEM Forms
description: Istruzioni di installazione del service pack di AEM Forms per l’ambiente OSGi e JEE
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 652878504d2225e50ea14885ec96bdd408f77ed0
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 6%

---

# Istruzioni per l’installazione di AEM 6.5 Forms Service Pack {#aem-form-patch-installation-instructions}

## Informazioni sulla versione

| Prodotto | Forms Adobe Experience Manager 6.5 |
|---|---|
| Versione | 6.5.22.0 |
| Tipo | Versione Service Pack |
| Data | 29 novembre 2024 |
| URL di download | [Ultime versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it) |

>[!NOTE]
>
>Per un elenco completo dei problemi risolti, consulta le ultime [note sulla versione di AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it).

## Cosa è incluso in Experience Manager Forms 6.5

Il service pack di Adobe Experience Manager (AEM) Forms include funzioni nuove e aggiornate, quali miglioramenti chiave richiesti dai clienti, prestazioni, stabilità e sicurezza. AEM Forms rilascia i service pack a intervalli regolari per fornire funzioni e miglioramenti più recenti. A seconda dello stack di tecnologia, scegliere uno dei percorsi seguenti per scaricare e installare il service pack nell&#39;ambiente:

* [Scarica e installa Service Pack in un ambiente AEM Form su JEE](#download-and-install-for-jee-service-pack)
* [Scarica e installa il Service Pack in un ambiente OSGi di AEM Form](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * Adobe rilascia un programma di installazione completo ogni sei Service Pack. AEM 6.5 Forms Service Pack 18 (6.5.18.0) è l&#39;ultimo programma di installazione completo di JEE. Il programma di installazione completo supporta le nuove piattaforme, mentre il programma di installazione dei Service Pack standard include nuove funzionalità, correzioni di bug e miglioramenti generali. Se stai eseguendo una nuova installazione o stai pianificando di utilizzare il software più recente per il tuo ambiente AEM 6.5 Forms su JEE, Adobe consiglia di utilizzare il programma di installazione completo di AEM 6.5.18.0 Forms su JEE rilasciato il 31 agosto 2023 invece del programma di installazione di AEM 6.5 Forms rilasciato il 8 aprile 2019 o di AEM 6.5.12.0 Forms Installer rilasciato il 3 marzo 2022. Dopo aver utilizzato il programma di installazione completo, installare il service pack più recente.
> * La funzionalità di AEM Forms, ad esempio Forms adattivo, disponibile in [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=it), è destinata esclusivamente a scopi di esplorazione e valutazione. Per l’utilizzo in produzione, è essenziale ottenere una licenza valida per AEM Forms.

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## Scaricare e installare Service Pack in un ambiente AEM Form su JEE {#download-and-install-for-jee-service-pack}

<!--
![JEE Installation](/help/forms/using/assets/jeeinstallation.png) -->

+++1 Backup dell&#39;ambiente esistente

1. Eseguire il backup dell&#39;[archivio CRX, dello schema di database e di GDS (Global Document Storage)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=it).
1. Esegui il backup della cartella &lt;*AEM_forms_root*>/deploy.

>[!NOTE]
>
> Prima di eseguire il programma di installazione di AEM Service Pack, accertarsi di disporre dei privilegi di accesso in scrittura per la directory di installazione di AEM.

+++

+++2 Scaricare il software richiesto

* [AEM Forms su JEE Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it)

* [Servlet frammento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it)
* [Pacchetto del componente aggiuntivo Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it)


+++

+++3 Installazione di pacchetti ridistribuibili di Microsoft Visual C++

* Scaricare e installare la versione a [64 bit dei pacchetti ridistribuibili di Microsoft Visual C++ per Visual Studio 2015, 2017, 2019 e 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) nel computer in cui è installato AEM 6.5 Forms.

>[!NOTE]
>
> Assicurati di installare la versione ridistribuibile, anche se è installata una versione precedente, per garantire la disponibilità della versione più recente.

+++

+++4 Installare AEM Forms su JEE Service Pack:

1. Arresta il server applicazioni.
1. Estrai l&#39;archivio del programma di installazione di **AEM Forms su JEE Service Pack** sul disco rigido:

   * **Windows**
Passare alla directory appropriata sul supporto di installazione o sulla cartella del disco rigido in cui è stata eseguita la copia     e fare doppio clic sul file `aemforms65_cfp_install.exe`.

      * (Windows a 32 bit) `Windows\Disk1\InstData\VM`
      * (Windows a 64 bit) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Passare alla directory appropriata e da una shell e digitare `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Viene avviata una procedura di installazione guidata.

1. Nel pannello introduttivo, fai clic su **[!UICONTROL Avanti]**.
1. Nella schermata **Scegli cartella di installazione**, verifica che il percorso predefinito visualizzato sia corretto per l&#39;installazione esistente oppure fai clic su **[!UICONTROL Sfoglia]** per selezionare la cartella alternativa in cui è installato AEM Forms, quindi fai clic su **[!UICONTROL Avanti]**.
1. Leggere le informazioni di riepilogo del Service Pack e fare clic su **[!UICONTROL Avanti]**.
1. Leggi le informazioni di riepilogo di pre-installazione e fai clic su **[!UICONTROL Installa]**.
1. Al termine dell’installazione, fai clic su **[!UICONTROL Avanti]** per applicare gli aggiornamenti della correzione rapida ai file installati.
1. **[Solo per Windows]:** Eseguire uno dei passaggi seguenti:

   * Deselezionare l&#39;opzione **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Eseguire **Configuration Manager** utilizzando il file **ConfigurationManager.bat** in `[aem-forms root]\configurationManager\bin`.

   * In alternativa, deselezionare l&#39;opzione **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Prima di eseguire **Configuration Manager** utilizzando **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, passare alla directory *`<AEMForms_Install_Dir>\configurationManager\bin`* e sostituire **ConfigurationManager.lax** e **ConfigurationManager_IPV6.lax** con i file [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) più recenti, cercare e sostituire **axis-1.4.1.1.jar** con **asse-1.4.1.2.jar** in questi due file.

     >[!NOTE]
     >
     >* L&#39;aggiornamento o la sostituzione del file **ConfigurationManager.bat** consente di evitare l&#39;aggiornamento manuale dei file con estensione lax.

1. **[Solo per Unix]:** La casella di controllo **Avvia Configuration Manager** è selezionata per impostazione predefinita. Fai clic su **[!UICONTROL Fine]** per eseguire Configuration Manager immediatamente o su **Configuration Manager** in un secondo momento, deseleziona l&#39;opzione **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. È possibile avviare **Configuration Manager** in un secondo momento utilizzando lo script appropriato nella directory `[AEM_forms_root]/configurationManager/bin`.

1. A seconda del server applicazioni in uso, scegliere uno dei seguenti documenti e seguire le istruzioni riportate nella sezione *Configurazione e distribuzione di AEM Forms*.

   * [Installazione e distribuzione di AEM Forms per JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_it)
   * [Installazione e distribuzione di AEM Forms per WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_it)
   * [Installazione e distribuzione di AEM Forms per WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65_it)
   * [Installazione e distribuzione di AEM Forms per JBoss® Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Installazione e distribuzione di AEM Forms per il cluster WebSphere®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Installazione e distribuzione di AEM Forms per il cluster WebLogic](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
>* Dopo aver installato AEM Forms nel service pack di JEE, è necessario rimuovere il pacchetto del componente aggiuntivo Forms dalla cartella `crx-repository\install` prima di riavviare l&#39;appserver. Scarica il pacchetto del componente aggiuntivo Forms più recente dal [portale di distribuzione software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it).
>* Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.
>* Per [Hotfix per Mitigare le vulnerabilità del framework di primavera per AEM Forms su JEE](/help/release-notes/aem-forms-hotfix.md), durante la distribuzione in un ambiente cluster è essenziale assicurarsi che i localizzatori vengano avviati utilizzando JDK 17.

+++

+++5 Installa il frammento del servlet se non è installato (**Passaggio obbligatorio**)

<!-- >[!NOTE] > > * If you are upgrading from **AEM Service Pack 6.5.15.0**, the installation of the **servlet fragment** is not required. For versions **AEM Service Pack 6.5.14.0** or earlier, it is **mandatory to install** the servlet fragment. -->

Per scaricare e installare il frammento del servlet:

1. Se non hai scaricato il frammento, scaricalo da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

2. Avvia il server applicazioni, attendi che i registri si stabilizzino e verifichi lo stato del bundle.

3. Apri i bundle della console web. URL predefinito: `http://[Server]:[Port]/system/console/bundles`.

4. Fai clic su Installa/Aggiorna. Scegliere il frammento scaricato, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Fai clic su **Installa** o **Aggiorna**. Attesa della stabilizzazione del server applicazioni

5. Arrestare il server applicazioni.

+++

+++6 Installare AEM Service Pack

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). Adobe consiglia di riavviare il sistema se il tempo di attività corrente di un’istanza è elevato.
1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup dell&#39;istanza [!DNL Experience Manager].
1. Scarica il service pack da [Distribuzione software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, vedere [Gestione pacchetti](/help/sites-administering/package-manager.md).
1. Selezionare il pacchetto, quindi selezionare **[!UICONTROL Installa]**.

**Installazione automatica**

Esistono due metodi diversi che è possibile utilizzare per installare automaticamente il service pack [!DNL ExperienceManager].<!--       UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto nella cartella `../crx-quickstart/install` quando il server è disponibile online.
Il pacchetto è      installato automaticamente.

* Utilizza l&#39;API HTTP [da Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it). Utilizzare `cmd=install&recursive=true` per installare i pacchetti nidificati.

  >[!NOTE]
  >
  >Experience Manager service pack non supporta l’installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Convalida l&#39;installazione**

  Per informazioni sulle piattaforme certificate per l&#39;utilizzo di questa versione, vedere i [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

   1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager (spversion)` in [!UICONTROL Prodotti installati].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. Tutti i bundle OSGi sono **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** nella console OSGi (usa Web)     Console: `/system/console/bundles`).
   1. La versione del bundle OSGi `org.apache.jackrabbit.oak-core` è 1.22.14 o successiva (utilizzare WebConsole: `/system/console/bundles`).

+++

+++7 Installare il pacchetto del componente aggiuntivo AEM Experience Manager Forms

1. Verificare di aver installato il service pack [!DNL Experience Manager].
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it) per il sistema operativo in uso.
1. Installare il pacchetto del componente aggiuntivo Forms come descritto in [Installazione dei pacchetti del componente aggiuntivo AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it).
1. Se si utilizzano lettere in Experience Manager 6.5 Forms, installare il [pacchetto di compatibilità AEMFD più recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it).

+++

## Scaricare e installare Service Pack in un ambiente AEM Form su OSGi {#download-and-install-for-osgi-service-pack}


<!-- ![OSGi Installation Steps](/help/forms/using/assets/osgiinstallation.png)
-->

+++1 Backup dell&#39;ambiente esistente

1. Eseguire il backup dell&#39;[archivio CRX e dello schema di database](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=it).

>[!NOTE]
>
> Se si installa AEM Forms Service Pack per il database relazionale, è necessario eseguire il backup di DB_schema.

+++

+++2 Scaricare il software richiesto

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it)
* [Pacchetto del componente aggiuntivo Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it)

+++

+++ 3. Installare i pacchetti ridistribuibili di Microsoft Visual C++

* Scaricare e installare la versione a [64 bit dei pacchetti ridistribuibili di Microsoft Visual C++ per Visual Studio 2015, 2017, 2019 e 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) nel computer in cui è installato AEM 6.5 Forms.

>[!NOTE]
>
>
> Assicurati di installare la versione ridistribuibile, anche se è installata una versione precedente, per garantire la disponibilità della versione più recente.

+++

+++4 Installare AEM Service Pack

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). Adobe consiglia di riavviare il sistema se il tempo di attività corrente di un’istanza è elevato.
1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup dell&#39;istanza [!DNL Experience Manager].
1. Scarica il service pack da [Distribuzione software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, vedere [Gestione pacchetti](/help/sites-administering/package-manager.md).
1. Selezionare il pacchetto, quindi selezionare **[!UICONTROL Installa]**.

**Installazione automatica**

Esistono due metodi diversi che è possibile utilizzare per installare automaticamente il service pack [!DNL Experience Manager].<!--  UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto nella cartella `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto è      installato automaticamente.
* Utilizza l&#39;API HTTP [da Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it). Utilizzare `cmd=install&recursive=true` per installare i pacchetti nidificati.

  >[!NOTE]
  >
  >Experience Manager service pack non supporta l’installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Convalida l&#39;installazione**

  Per informazioni sulle piattaforme certificate per l&#39;utilizzo di questa versione, vedere i [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

   1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager (spversion)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. Tutti i bundle OSGi sono **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** nella console OSGi (usa la console Web: `/system/console/bundles`).

      1. La versione del bundle OSGi `org.apache.jackrabbit.oak-core` è 1.22.14 o successiva (utilizzare la console Web: `/system/console/bundles`).

+++

+++5 Installare il pacchetto del componente aggiuntivo Adobe Experience Manager Forms (AEM)

1. Verificare di aver installato il service pack [!DNL Experience Manager].
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it) per il sistema operativo in uso.
1. Installare il pacchetto del componente aggiuntivo Forms come descritto in [Installazione dei pacchetti del componente aggiuntivo AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it).
1. Se si utilizzano lettere in Experience Manager 6.5 Forms, installare il [pacchetto di compatibilità AEMFD più recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it).

+++

## Risoluzione dei problemi

* Se durante l&#39;installazione del service pack viene chiuso il **dialogo sull&#39;interfaccia utente di Gestione pacchetti**, attendere che i registri degli errori vengano stabilizzati prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle di aggiornamento prima di essere certi che le installazioni siano riuscite. In genere, questo problema si verifica nel browser Safari ma può verificarsi in modo intermittente su qualsiasi browser.

* Una volta completata l’installazione, controlla i registri di monitoraggio (error.log) per qualsiasi attività. Attendi alcuni minuti fino a quando non ci sarà alcuna attività nei registri. Riavvia l’istanza di AEM.

* Nel caso in cui si verifichi un **errore di indisponibilità del servizio** dopo l&#39;installazione del service pack di AEM Forms 6.5.15.0 o versione successiva, [installare il frammento servlet e il bundle](/help/forms/using/aem-service-pack-installation-solution.md) per correggere l&#39;errore.
