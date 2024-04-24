---
title: Istruzioni di installazione delle patch AEM Forms per AEM Forms
description: Istruzioni di installazione del service pack di AEM Forms per l’ambiente OSGi e JEE
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 6%

---

# Istruzioni per l’installazione di AEM 6.5 Forms Service Pack {#aem-form-patch-installation-instructions}

## Informazioni sulla versione

| Prodotto | Forms Adobe Experience Manager 6.5 |
|---|---|
| Versione | 6.5.20.0 |
| Tipo | Versione Service Pack |
| Data | 29 febbraio 2024 |
| URL di download | [Ultime versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>Scopri le ultime novità [Note sulla versione di AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it) per un elenco completo dei problemi risolti.

## Cosa è incluso in Experience Manager Forms 6.5

Il service pack di Adobe Experience Manager (AEM) Forms include funzioni nuove e aggiornate, quali miglioramenti chiave richiesti dai clienti, prestazioni, stabilità e sicurezza. AEM Forms rilascia i service pack a intervalli regolari per fornire funzioni e miglioramenti più recenti. A seconda dello stack di tecnologia, scegliere uno dei percorsi seguenti per scaricare e installare il service pack nell&#39;ambiente:

* [Scaricare e installare Service Pack in un modulo AEM in un ambiente JEE](#download-and-install-for-jee-service-pack)
* [Scaricare e installare Service Pack in un modulo AEM in ambiente OSGi](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * In Adobe viene rilasciato un programma di installazione completo ogni sei Service Pack. AEM 6.5 Forms Service Pack 18 (6.5.18.0) è l’ultimo programma di installazione completo di JEE. Il programma di installazione completo supporta le nuove piattaforme, mentre il programma di installazione dei Service Pack standard include nuove funzionalità, correzioni di bug e miglioramenti generali. Se stai eseguendo una nuova installazione o pianificando di utilizzare il software più recente per il tuo Forms AEM 6.5 in ambiente JEE, Adobe consiglia di utilizzare il programma di installazione completo di AEM 6.5.18.0 Forms su JEE rilasciato il 31 agosto 2023 invece del programma di installazione di AEM 6.5 Forms rilasciato il 08 aprile 2019 o 6.5.12.0 AEM Forms Installer rilasciato il 03 marzo 2022. Dopo aver utilizzato il programma di installazione completo, installare il service pack più recente.
> * La funzione di AEM Forms, ad esempio Forms adattivo, disponibile in [QuickStart per AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=it), sono destinati esclusivamente a scopi di esplorazione e valutazione. Per l’utilizzo in produzione, è essenziale ottenere una licenza valida per AEM Forms.

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## Scaricare e installare Service Pack in un modulo AEM in un ambiente JEE {#download-and-install-for-jee-service-pack}

<!--
![JEE Installation](/help/forms/using/assets/jeeinstallation.png) -->

+++1 Backup dell&#39;ambiente esistente

1. Eseguire il backup del [Archivio CRX, schema di database e GDS (Global Document Storage)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. Eseguire il backup di &lt;*AEM_forms_root* cartella >/deploy.

>[!NOTE]
>
> Prima di eseguire il programma di installazione del Service Pack per l&#39;AEM, verificare di disporre dei privilegi di accesso in scrittura per la directory di installazione dell&#39;AEM.

+++

+++2 Scaricare il software richiesto

* [AEM Forms su JEE Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [Service Pack AEM](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it)
* [Pacchetto del componente aggiuntivo Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [Servlet frammento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3 Installazione di pacchetti ridistribuibili di Microsoft Visual C++

* Scarica e installa [Versione a 64 bit di Microsoft Visual C++ Redistributable per Visual Studio 2015, 2017, 2019 e 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) sul computer in cui è installato AEM 6.5 Forms.

>[!NOTE]
>
> Assicurati di installare la versione ridistribuibile, anche se è installata una versione precedente, per garantire la disponibilità della versione più recente.

+++

+++4 Installare AEM Forms su JEE Service Pack:

1. Arresta il server applicazioni.
1. Estrai **Archivio del programma di installazione di AEM Forms su JEE Service Pack** sul disco rigido:

   * **Windows**
Passare alla directory appropriata sul supporto di installazione o sulla cartella del disco rigido in cui è stato copiato il programma di installazione, quindi fare doppio clic sul pulsante `aemforms65_cfp_install.exe` file.

      * (Windows a 32 bit) `Windows\Disk1\InstData\VM`
      * (Windows a 64 bit) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Passare alla directory appropriata e da una shell e digitare `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Viene avviata una procedura di installazione guidata.

1. Nel pannello introduttivo, fai clic su **[!UICONTROL Avanti]**.
1. Il giorno **Scegli cartella di installazione** , verificare che il percorso predefinito visualizzato sia corretto per l&#39;installazione esistente oppure fare clic su **[!UICONTROL Sfoglia]** per selezionare la cartella alternativa in cui è installato AEM forms, quindi fare clic su **[!UICONTROL Successivo]**.
1. Leggere le informazioni di riepilogo del Service Pack e fare clic su **[!UICONTROL Successivo]**.
1. Leggi le informazioni di riepilogo di pre-installazione e fai clic su **[!UICONTROL Installa]**.
1. Al termine dell’installazione, fai clic su **[!UICONTROL Avanti]** per applicare gli aggiornamenti della correzione rapida ai file installati.
1. **[Solo per Windows]:** Effettuare una delle seguenti operazioni:

   * Deseleziona la **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Esegui **Gestione configurazione** utilizzando **ConfigurationManager.bat** file in `[aem-forms root]\configurationManager\bin`.

   * Oppure deseleziona il **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Prima dell’esecuzione **Gestione configurazione** utilizzo **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, passa a *`<AEMForms_Install_Dir>\configurationManager\bin`* e sostituire il **ConfigurationManager.lax** e **ConfigurationManager_IPV6.lax** con il più recente [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) file, Cerca e sostituisci **axis-1.4.1.1.jar** con **axis-1.4.1.2.jar** in questi due file.

     >[!NOTE]
     >
     >* Aggiornamento o sostituzione del **ConfigurationManager.bat** file consente di evitare l&#39;aggiornamento manuale dei file con estensione lax.

1. **[Solo per Unix]:** Il **Avvia Configuration Manager** per impostazione predefinita. Clic **[!UICONTROL Fine]** per eseguire Configuration Manager immediatamente o per eseguire **Gestione configurazione** in seguito, deseleziona la **Avvia Configuration Manager** prima di fare clic su **[!UICONTROL Fine]**. Puoi iniziare **Gestione configurazione** in un secondo momento utilizzando lo script appropriato nel `[AEM_forms_root]/configurationManager/bin` directory.

1. In base al server applicazioni in uso, scegliere uno dei seguenti documenti e seguire le istruzioni riportate nella *Configurazione e distribuzione dei moduli AEM* sezione.

   * [Installazione e distribuzione di moduli AEM per JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installazione e distribuzione di moduli AEM per WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [Installazione e distribuzione di AEM Forms per WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [Installazione e distribuzione di moduli AEM per cluster JBoss®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Installazione e distribuzione di moduli AEM per cluster WebSphere®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Installazione e distribuzione di AEM Forms per il cluster WebLogic](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
>* Dopo aver installato AEM Forms su JEE Service Pack, è necessario rimuovere il pacchetto del componente aggiuntivo Forms da `crx-repository\install` prima di riavviare appserver. Scarica il pacchetto più recente del componente aggiuntivo Forms da [Portale di distribuzione software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
>* Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

+++

+++5 Installare il frammento del servlet (AEM Service Pack 6.5.14.0 o precedente)

>[!NOTE]
>
> * Se si esegue l&#39;aggiornamento da **AEM Service Pack 6.5.15.0**, l&#39;installazione del **frammento servlet** non è obbligatorio. Per le versioni **AEM Service Pack 6.5.14.0** In precedenza, era obbligatorio installare il frammento servlet.
> * È necessario installare **frammento servlet** per tutti i server applicazioni, tranne quelli in esecuzione su **JBoss® EAP 7.4.0**.


Per scaricare e installare il frammento del servlet:

1. Se non hai scaricato il frammento, scaricalo da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

2. Avvia il server applicazioni, attendi che i registri si stabilizzino e verifichi lo stato del bundle.

3. Apri i bundle della console web. L’URL predefinito è `http://[Server]:[Port]/system/console/bundles`.

4. Fai clic su Installa/Aggiorna. Scegli il frammento scaricato, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Clic **Installa** o **Aggiorna**. Attesa della stabilizzazione del server applicazioni

5. Arrestare il server applicazioni.

+++

+++6 Installare il Service Pack di AEM

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia di riavviare se il tempo di attività corrente per un&#39;istanza è elevato.
1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup del file [!DNL Experience Manager] dell&#39;istanza.
1. Scarica il service pack da [Distribuzione di software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).
1. Seleziona il pacchetto, quindi seleziona **[!UICONTROL Installa]**.

**Installazione automatica**

Esistono due metodi diversi che è possibile utilizzare per installare automaticamente [!DNL ExperienceManager] service pack.<!--       UPDATE FOR EACH NEW RELEASE -->

* Inserisci la confezione in `../crx-quickstart/install` quando il server è disponibile online.
Il pacchetto viene installato automaticamente.

* Utilizza il [API HTTP da Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). Utilizzare  `cmd=install&recursive=true` affinché i pacchetti nidificati vengano installati.

  >[!NOTE]
  >
  >Experience Manager Service Pack non supporta l&#39;installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Convalidare l’installazione**

  Per informazioni sulle piattaforme certificate per l’utilizzo di questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

   1. Pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa della versione aggiornata `Adobe Experience Manager (spversion)` in [!UICONTROL Prodotti installati].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (usa la console web: `/system/console/bundles`).
   1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.14 o successiva (utilizzare WebConsole: `/system/console/bundles`).

+++

+++7 Installare il pacchetto del componente aggiuntivo Experience Manager Forms per AEM

1. Verificare di aver installato [!DNL Experience Manager] service pack.
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) per il sistema operativo in uso.
1. Installare il pacchetto del componente aggiuntivo Forms come descritto in [Installazione dei pacchetti del componente aggiuntivo AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Se si utilizzano lettere in Experience Manager 6.5 Forms, installare [pacchetto di compatibilità AEMFD più recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Scaricare e installare Service Pack in un modulo AEM in ambiente OSGi {#download-and-install-for-osgi-service-pack}


<!-- ![OSGi Installation Steps](/help/forms/using/assets/osgiinstallation.png)
-->

+++1 Backup dell&#39;ambiente esistente

1. Eseguire il backup del [Archivio CRX e schema database](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
> Se si installa AEM Forms Service Pack per il database relazionale, è necessario eseguire il backup di DB_schema.

+++

+++2 Scaricare il software richiesto

* [Service Pack AEM](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it)
* [Pacchetto del componente aggiuntivo Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++ 3. Installare i pacchetti ridistribuibili di Microsoft Visual C++

* Scarica e installa [Versione a 64 bit di Microsoft Visual C++ Redistributable per Visual Studio 2015, 2017, 2019 e 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) sul computer in cui è installato AEM 6.5 Forms.

>[!NOTE]
>
>
> Assicurati di installare la versione ridistribuibile, anche se è installata una versione precedente, per garantire la disponibilità della versione più recente.

+++

+++4 Installare il Service Pack di AEM

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia di riavviare se il tempo di attività corrente per un&#39;istanza è elevato.
1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup del file [!DNL Experience Manager] dell&#39;istanza.
1. Scarica il service pack da [Distribuzione di software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).
1. Seleziona il pacchetto, quindi seleziona **[!UICONTROL Installa]**.

**Installazione automatica**

Esistono due metodi diversi che è possibile utilizzare per installare automaticamente [!DNL Experience Manager] service pack.<!--  UPDATE FOR EACH NEW RELEASE -->

* Inserisci la confezione in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza il [API HTTP da Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). Utilizzare `cmd=install&recursive=true` affinché i pacchetti nidificati vengano installati.

  >[!NOTE]
  >
  >Experience Manager Service Pack non supporta l&#39;installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Convalidare l’installazione**

  Per informazioni sulle piattaforme certificate per l’utilizzo di questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

   1. Pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa della versione aggiornata `Adobe Experience Manager (spversion)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (usa la console web: `/system/console/bundles`).

      1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.14 o successiva (utilizzare la console Web: `/system/console/bundles`).

+++

+++5 Installare il pacchetto del componente aggiuntivo Adobe Experience Manager Forms (AEM)

1. Verificare di aver installato [!DNL Experience Manager] service pack.
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) per il sistema operativo in uso.
1. Installare il pacchetto del componente aggiuntivo Forms come descritto in [Installazione dei pacchetti del componente aggiuntivo AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Se si utilizzano lettere in Experience Manager 6.5 Forms, installare [pacchetto di compatibilità AEMFD più recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Risoluzione dei problemi

* Se **Finestra di dialogo sull’interfaccia utente di Gestione pacchetti** esce durante l’installazione del service pack; attendi che i registri di errore si stabilizzino prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle di aggiornamento prima di essere certi che le installazioni siano riuscite. In genere, questo problema si verifica nel browser Safari ma può verificarsi in modo intermittente su qualsiasi browser.

* Una volta completata l’installazione, controlla i registri di monitoraggio (error.log) per qualsiasi attività. Attendi alcuni minuti fino a quando non ci sarà alcuna attività nei registri. Riavvia l’istanza AEM.

* Nel caso in cui si ottenga un **errore di servizio non disponibile** dopo l’installazione di AEM Forms 6.5.15.0 o successivo service pack, [installare il frammento e il bundle del servlet](/help/forms/using/aem-service-pack-installation-solution.md) per correggere l’errore.
