---
title: Console Web
seo-title: Console Web
description: Scoprite come utilizzare la console Web in AEM.
seo-description: Scoprite come utilizzare la console Web in AEM.
uuid: 047274ff-4d7d-4c7d-95be-06f363beae2e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: f934eb02-1f84-44f2-9f14-3f17250c9a90
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 3%

---


# Console Web{#web-console}

La console Web in AEM si basa sulla [console di gestione Web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix è uno sforzo della comunità per implementare OSGi R4 Service Platform, che include il framework OSGi e i servizi standard.

>[!NOTE]
>
>Nella console Web tutte le descrizioni che fanno riferimento alle impostazioni predefinite si riferiscono alle impostazioni predefinite di Sling.
>
>AEM ha le proprie impostazioni predefinite, pertanto le impostazioni predefinite potrebbero essere diverse da quelle documentate nella console.

La console Web offre una serie di schede per la manutenzione dei bundle OSGi, tra cui:

* [Configurazione](#configuration): utilizzato per configurare i bundle OSGi ed è quindi il meccanismo sottostante per configurare AEM parametri di sistema
* [Bundle](#bundles): utilizzati per l&#39;installazione dei bundle
* [Componenti](#components): utilizzato per controllare lo stato dei componenti richiesti per AEM

Eventuali modifiche apportate vengono applicate immediatamente al sistema in esecuzione. Non è necessario riavviare.

È possibile accedere alla console da `../system/console`; ad esempio:

`http://localhost:4502/system/console/components`

## Configurazione {#configuration}

La scheda **Configuration** viene utilizzata per configurare i bundle OSGi ed è quindi il meccanismo sottostante per configurare AEM parametri di sistema.

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Configurazione OSGi con la console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console).

È possibile accedere alla scheda **Configuration** tramite:

* Il menu a discesa:

   **OSGi >**

* L’URL; ad esempio:

   `http://localhost:4502/system/console/configMgr`

Verrà visualizzato un elenco delle configurazioni:

![screen_shot_2012-02-15at52308pm-1](assets/screen_shot_2012-02-15at52308pm-1.png)

Negli elenchi a discesa di questa schermata sono disponibili due tipi di configurazioni:

* **Configurazioni**

   Consente di aggiornare le configurazioni esistenti. Questi hanno un&#39;identità persistente (PID) e possono essere:

   * standard e integrale a AEM; se eliminati, i valori torneranno alle impostazioni predefinite.
   * istanze create da Configurazioni in fabbrica; queste istanze vengono create dall&#39;utente. L&#39;eliminazione rimuove l&#39;istanza.

* **Configurazioni di fabbrica**

   Consente di creare un&#39;istanza dell&#39;oggetto funzionalità richiesto.

   A questo verrà assegnata un&#39;identità persistente, che verrà quindi elencata nell&#39;elenco a discesa Configurazioni.

Selezionando una voce dagli elenchi, verranno visualizzati i parametri relativi a tale configurazione:

![chlimage_1-61](assets/chlimage_1-61.png)

Potete quindi aggiornare i parametri come richiesto e:

* **Salva**

   Salvare le modifiche apportate.

   Per una configurazione di fabbrica, verrà creata una nuova istanza con un&#39;identità persistente. La nuova istanza verrà quindi elencata in Configurazioni.

* **Ripristina**

   Ripristinare gli ultimi parametri visualizzati sullo schermo.

* **Elimina**

   Elimina la configurazione corrente. Se standard, i parametri vengono restituiti alle impostazioni predefinite. Se creata da una configurazione di fabbrica, l&#39;istanza specifica viene eliminata.

* **Separa**

   Separate la configurazione corrente dal bundle.

* **Annulla**

   Annulla le modifiche correnti.

## Bundle {#bundles}

La scheda **Bundles** è il meccanismo per installare i bundle OSGi necessari per AEM. È possibile accedere alla scheda tramite uno dei seguenti metodi:

* Il menu a discesa:

   **OSGi >**

* L’URL; ad esempio:

   `http://localhost:4502/system/console/bundles`

Verrà visualizzato un elenco di bundle:

![screen_shot_2012-02-15at44740pm-1](assets/screen_shot_2012-02-15at44740pm-1.png)

Questa scheda consente di:

* **Installazione o aggiornamento**

   È possibile **Browse** individuare il file che contiene il pacchetto e specificare se deve iniziare **Start** immediatamente e a quale **Livello iniziale**.

* **Ricarica**

   Aggiorna l’elenco visualizzato.

* **Aggiorna pacchetti**

   Questo controllerà i riferimenti di tutti i pacchetti e aggiornerà se necessario.

   Ad esempio, dopo un aggiornamento potrebbe essere ancora in esecuzione sia la versione precedente che quella nuova a causa di riferimenti precedenti. Questa opzione consente di controllare e spostare tutti i riferimenti alla nuova versione, consentendo l&#39;interruzione della versione precedente.

* **Avvia**

   Avvia un bundle in base al livello iniziale specificato.

* **Arresta**

   Interrompe il bundle.

* **Disinstalla**

   Disinstalla il bundle dal sistema.

* **vedere lo stato**

   L&#39;elenco specifica lo stato corrente del bundle; fate clic sul nome di un pacchetto specifico con ulteriori informazioni.

>[!NOTE]
>
>Dopo **Update** si consiglia di eseguire un **Refresh Packages**.

## Componenti {#components}

La scheda **Componenti** consente di abilitare e/o disabilitare i vari componenti. È possibile accedervi tramite:

* Il menu a discesa:

   **Principale >**

* L’URL; ad esempio:

   `http://localhost:4502/system/console/components`

Verrà visualizzato un elenco di componenti. Sono disponibili diverse icone che consentono di abilitare, disabilitare o (se del caso) aprire i dettagli di configurazione per un componente specifico.

![screen_shot_2012-02-15at52144pm-1](assets/screen_shot_2012-02-15at52144pm-1.png)

Facendo clic sul nome di un particolare componente vengono visualizzate ulteriori informazioni sullo stato. Qui è inoltre possibile attivare, disattivare o ricaricare il componente.

![chlimage_1-62](assets/chlimage_1-62.png)

>[!NOTE]
>
>L’attivazione o la disattivazione di un componente viene applicata solo fino al riavvio di AEM/CRX.
>
>Lo stato iniziale è definito nel descrittore del componente, che viene generato durante lo sviluppo e memorizzato nel bundle al momento della creazione del bundle.

