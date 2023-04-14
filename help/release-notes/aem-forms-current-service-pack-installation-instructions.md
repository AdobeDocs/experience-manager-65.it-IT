---
title: Istruzioni di installazione delle patch di AEM Forms per AEM Forms
description: Istruzioni per le installazioni dei service pack AEM Forms per l'ambiente OSGi e JEE
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 01bf12ec46966ab2c78e2e825840230ea1bd3395
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 9%

---

# Istruzioni per l&#39;installazione di AEM 6.5 Forms Service Pack {#aem-form-patch-installation-instructions}

## Informazioni sulla versione

| Prodotto | Adobe Experience Manager 6.5 Forms |
|---|---|
| Versione | 6.5.16.0 |
| Tipo | Versione Service Pack |
| Data | 2 marzo 2023 |
| URL di download | [Versioni più recenti di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>Scopri le ultime [Note sulla versione di AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it) per un elenco completo dei problemi risolti.

## Contenuto in Experience Manager Forms 6.5

Il service pack di Adobe Experience Manager (AEM) Forms include funzioni nuove e aggiornate, quali miglioramenti chiave richiesti dai clienti, prestazioni, stabilità e sicurezza. Service Pack di AEM Forms a intervalli regolari per fornire funzioni e miglioramenti più recenti. A seconda dello stack, scegli uno dei percorsi seguenti per scaricare e installare il service pack nell&#39;ambiente:

* [Download e installazione del Service Pack in un modulo AEM in un ambiente JEE](#download-and-install-for-jee-service-pack)
* [Download e installazione del Service Pack in un modulo AEM in ambiente OSGi](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> Adobe rilascia un programma di installazione completo ogni 6° service pack. AEM 6.5 Forms Service Pack 12 (6.5.12.0) su JEE è stato l&#39;ultimo programma di installazione completo. Il programma di installazione completo fornisce supporto per nuove piattaforme, mentre il programma di installazione del service pack regolare include nuove funzionalità, correzioni di bug e miglioramenti generali. Se stai eseguendo una nuova installazione o pianificando l’utilizzo del software più recente per il tuo ambiente Forms 6.5 su JEE, Adobe consiglia di utilizzare AEM 6.5.12.0 Forms su JEE full installer rilasciato il 03 marzo 2022 invece di AEM 6.5 Forms installer rilasciato il 08 aprile 2019. Dopo aver utilizzato il programma di installazione completo, installare il service pack più recente.

## Download e installazione del Service Pack in un modulo AEM in un ambiente JEE {#download-and-install-for-jee-service-pack}

![Installazione JEE](/help/forms/using/assets/jeeinstallation.png)

+++1. Esegui il backup dell’ambiente esistente:

1. Esegui il backup [Archivio CRX, schema di database e GDS (Global Document Storage)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. Eseguire il backup del &lt;*AEM_forms_root*>/distribuisci cartella.

>[!NOTE]
>
> Prima di eseguire il programma di installazione del service pack di AEM, assicurarsi di disporre dei privilegi di accesso in scrittura nella directory di installazione AEM.

+++

+++2.Scarica il software richiesto:

* [AEM Forms su JEE Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it)
* [Pacchetto di componenti aggiuntivi per Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [Servlet frammenti](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. Installa AEM Forms sul service pack JEE:

1. Arresta il server applicazioni.
1. Estrai il **Archivio del programma di installazione di AEM Forms su JEE Service Pack** sul disco rigido:

   * **Windows**
Accedere alla directory appropriata del supporto di installazione o della cartella sul disco rigido in cui è stato copiato il programma di installazione e fare doppio clic sul pulsante 
`aemforms65_cfp_install.exe` file.

      * (Windows a 32 bit) `Windows\Disk1\InstData\VM`
      * (Windows a 64 bit) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux®**
Passa alla directory appropriata e da una shell e digita 
`./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Viene avviata una procedura di installazione guidata.

1. Nel pannello introduttivo, fai clic su **[!UICONTROL Avanti]**.
1. Sulla **Scegli cartella di installazione** controlla che la posizione predefinita visualizzata sia corretta per l&#39;installazione esistente oppure fai clic su **[!UICONTROL Sfoglia]** per selezionare la cartella alternativa in cui è installato AEM moduli e fare clic su **[!UICONTROL Successivo]**.
1. Leggi le informazioni di riepilogo del Service Pack e fai clic su **[!UICONTROL Successivo]**.
1. Leggi le informazioni di riepilogo di pre-installazione e fai clic su **[!UICONTROL Installa]**.
1. Al termine dell’installazione, fai clic su **[!UICONTROL Avanti]** per applicare gli aggiornamenti della correzione rapida ai file installati.
1. **[Solo per Windows]:** Esegui uno dei seguenti passaggi:

   * Deseleziona la **Avvia Configuration Manager** prima di fare clic **[!UICONTROL Fine]**. Esegui **Gestione configurazione** utilizzando **ConfigurationManager.bat** file che si trova in `[aem-forms root]\configurationManager\bin`.

   * Oppure deseleziona la **Avvia Configuration Manager** prima di fare clic **[!UICONTROL Fine]**. Prima dell&#39;esecuzione **Gestione configurazione** utilizzo **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, passa a *`<AEMForms_Install_Dir>\configurationManager\bin`* directory e sostituzione [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) file.

      >[!NOTE]
      >
      >* Aggiornamento o sostituzione del **ConfigurationManager.bat** file ti aiuta a evitare di aggiornare manualmente i file .lax.


1. **[Solo per basati su Unix]:** La **Avvia Configuration Manager** la casella di controllo è selezionata per impostazione predefinita. Fai clic su **[!UICONTROL Fine]** per eseguire Gestione configurazione all&#39;istante o per eseguire **Gestione configurazione** in seguito, deseleziona la **Avvia Configuration Manager** prima di fare clic **[!UICONTROL Fine]**. Puoi iniziare **Gestione configurazione** in seguito utilizzando lo script appropriato nel `[AEM_forms_root]/configurationManager/bin` directory.

1. A seconda del server delle applicazioni, scegli uno dei seguenti documenti e segui le istruzioni in *Configurazione e distribuzione dei moduli AEM* sezione .

   * [Installazione e distribuzione di moduli AEM per JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installazione e distribuzione di moduli AEM per WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [Installazione e distribuzione di AEM Forms per WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [Installazione e distribuzione di moduli AEM per il cluster JBoss®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Installazione e distribuzione di moduli AEM per il cluster WebSphere®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Installazione e distribuzione del cluster AEM Forms per WebLogic](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> Dopo aver installato AEM Forms su JEE service pack, devi rimuovere il pacchetto aggiuntivo Forms da `crx-repository\install` prima di riavviare l&#39;appserver. Scarica il pacchetto aggiuntivo di Forms più recente dal [Portale di distribuzione software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

+++4. Installare il frammento del servlet

>[!NOTE]
>
> * Nel caso in cui si stia eseguendo l&#39;aggiornamento da **AEM Service Pack 6.5.15.0**, non è necessario installare **frammento servlet**. Se esegui l’aggiornamento da una versione precedente a **AEM Service Pack 6.5.15.0**, è obbligatorio installare **frammento servlet**.
> * È obbligatorio installare **frammento servlet** per tutti i server applicazioni, tranne quelli in esecuzione su **JBoss® EAP 7.4.0**.



Per scaricare e installare il frammento del servlet:

1. Se non hai scaricato il frammento, scaricalo da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. Avvia l&#39;application server, attendi che i registri si stabilizzino e controlla lo stato del bundle.

1. Apri i bundle della console Web. L’URL predefinito è `http://[Server]:[Port]/system/console/bundles`.

1. Fai clic su Installa/Aggiorna. Scegliere il frammento scaricato, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Fai clic su **Installa** o **Aggiorna**. Attesa della stabilizzazione del server applicazioni

1. Arrestare il server applicazioni.

+++

+++5. Installa AEM Service Pack

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia un riavvio se il tempo di attività corrente per un&#39;istanza è elevato.
1. Prima di installare, scegli uno snapshot o un nuovo backup del tuo [!DNL Experience Manager] istanza.
1. Scarica il service pack da [Distribuzione di software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).
1. Seleziona il pacchetto, quindi seleziona **[!UICONTROL Installa]**.

**Installazione automatica**

Esistono due metodi diversi per l&#39;installazione automatica [!DNL ExperienceManager] service pack.<!--       UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto in `../crx-quickstart/install` quando il server è disponibile online.
Il pacchetto viene installato automaticamente.

* Utilizza la [API HTTP da Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it). Utilizzo  `cmd=install&recursive=true` in modo che i pacchetti nidificati siano installati.

   >[!NOTE]
   Il service pack di Experience Manager non supporta l&#39;installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

   **Convalida l&#39;installazione**

   Per informazioni sulle piattaforme certificate per l’utilizzo con questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

   1. La pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa di versione aggiornata `Adobe Experience Manager (spversion)` sotto [!UICONTROL Prodotti installati].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (Usa console Web: `/system/console/bundles`).
   1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.2.14 o successiva (Usa WebConsole: `/system/console/     bundles`).

+++

+++6. Installare AEM pacchetto aggiuntivo di Experience Manager Forms

1. Assicurati di aver installato la [!DNL Experience Manager] service pack.
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) per il sistema operativo in uso.
1. Installa il pacchetto aggiuntivo di Forms come descritto in [Installazione dei pacchetti aggiuntivi di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Se utilizzi le lettere in Experience Manager 6.5 Forms, installa il [pacchetto di compatibilità AEM più recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Download e installazione del Service Pack in un modulo AEM in ambiente OSGi {#download-and-install-for-osgi-service-pack}

![Passaggi di installazione di OSGi](/help/forms/using/assets/osgiinstallation.png)


+++1. Esegui il backup dell’ambiente esistente:

1. Esegui il backup [Archivio CRX e schema di database](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
Se si installa il service pack AEM Forms per il database relazionale, è obbligatorio eseguire il backup di DB_schema.

+++

+++2.Scarica il software richiesto:

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it)
* [Pacchetto di componenti aggiuntivi per Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++3. Installa AEM Service Pack

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia un riavvio se il tempo di attività corrente per un&#39;istanza è elevato.
1. Prima di installare, scegli uno snapshot o un nuovo backup del tuo [!DNL Experience Manager] istanza.
1. Scarica il service pack da [Distribuzione di software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).
1. Seleziona il pacchetto, quindi seleziona **[!UICONTROL Installa]**.

**Installazione automatica**

Esistono due metodi diversi per l&#39;installazione automatica [!DNL Experience Manager] service pack.<!--  UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza la [API HTTP da Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it). Utilizzo `cmd=install&recursive=true` in modo che i pacchetti nidificati siano installati.

   >[!NOTE]
   Il service pack di Experience Manager non supporta l&#39;installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

   **Convalida l&#39;installazione**

   Per informazioni sulle piattaforme certificate per l’utilizzo con questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

   1. La pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa di versione aggiornata `Adobe Experience Manager (spversion)` sotto [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (Usa console Web: `/system/console/bundles`).

      1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.14 o successiva (Usa console Web: `/system/console/bundles`).

+++

+++4. Installare AEM pacchetto aggiuntivo di Experience Manager Forms

1. Assicurati di aver installato la [!DNL Experience Manager] service pack.
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) per il sistema operativo in uso.
1. Installa il pacchetto aggiuntivo di Forms come descritto in [Installazione dei pacchetti aggiuntivi di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Se utilizzi le lettere in Experience Manager 6.5 Forms, installa il [pacchetto di compatibilità AEM più recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Risoluzione dei problemi

* Se **Finestra di dialogo nell’interfaccia utente di Gestione pacchetti** esce durante l&#39;installazione del service pack, attendere che i registri di errore si stabilizzino prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di essere certi che le installazioni abbiano esito positivo. In genere questo problema si verifica nel browser Safari ma può verificarsi a intermittenza su qualsiasi browser.

* Controlla i log di monitoraggio (error.log) una volta che l&#39;installazione è completa per qualsiasi attività. Attendi per alcuni minuti finché non vi è alcuna attività nei registri. Riavvia l&#39;istanza AEM.

* Nel caso in cui si ottenga un **errore servizio-non disponibile** dopo aver installato il service pack AEM Forms 6.5.15.0, [installare il frammento e il bundle del servlet](/help/forms/using/aem-service-pack-installation-solution.md) per correggere l&#39;errore.
