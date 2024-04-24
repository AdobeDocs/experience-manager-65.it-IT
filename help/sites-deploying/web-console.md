---
title: Console web in Adobe Experience Manager
description: Scopri come utilizzare la console web Adobe Experience Manager (AEM).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
exl-id: 9acbf61f-73a8-4998-9421-dd933f30ac8a
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 1%

---

# Console Web{#web-console}

La console web in Adobe Experience Manager (AEM) è basata sulla [Console di gestione web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix è uno sforzo della community per implementare la piattaforma di servizio OSGi R4, che include il framework OSGi e i servizi standard.

>[!NOTE]
>
>Nella console Web, tutte le descrizioni che menzionano le impostazioni predefinite si riferiscono alle impostazioni predefinite di Sling.
>
>I valori predefiniti dell’AEM sono propri, pertanto quelli impostati potrebbero essere diversi da quelli documentati nella console.

La console Web offre una selezione di schede per la gestione dei bundle OSGi, tra cui:

* [Configurazione](#configuration): utilizzato per configurare i bundle OSGi ed è quindi il meccanismo di base per configurare i parametri del sistema AEM
* [Bundle](#bundles): utilizzato per installare i bundle
* [Componenti](#components): utilizzato per controllare lo stato dei componenti richiesti per l’AEM

Tutte le modifiche apportate vengono immediatamente applicate al sistema in esecuzione. Non è richiesto alcun riavvio.

La console è accessibile da `../system/console`; ad esempio:

`http://localhost:4502/system/console/components`

## Configurazione {#configuration}

Il **Configurazione** La scheda viene utilizzata per configurare i bundle OSGi ed è quindi il meccanismo sottostante per configurare i parametri del sistema AEM.

>[!NOTE]
>
>Consulta [Configurazione OSGi con la console web](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli.

Il **Configurazione** È possibile accedere alla scheda tramite:

* Il menu a discesa:

  **OSGi >**

* L’URL; ad esempio:

  `http://localhost:4502/system/console/configMgr`

Viene visualizzato un elenco di configurazioni:

![screen_shot_2012-02-15alle52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Esistono due tipi di configurazioni disponibili dagli elenchi a discesa in questa schermata:

* **Configurazioni**
Consente di aggiornare le configurazioni esistenti. Hanno un’identità persistente (PID) e possono essere:

   * standard e integrale per AEM; questi sono richiesti, se eliminati i valori tornano alle impostazioni predefinite.
   * istanze create da Configurazioni di fabbrica; queste istanze vengono create dall&#39;utente; l&#39;eliminazione rimuove l&#39;istanza.

* **Configurazioni di fabbrica**
Consente di creare un&#39;istanza dell&#39;oggetto funzionalità richiesto.

  Viene allocata a un’identità persistente e quindi elencata nell’elenco a discesa Configurazioni.

Selezionando una voce dall’elenco vengono visualizzati i parametri relativi a tale configurazione:

![chlimage_1-21](assets/chlimage_1-21a.png)

Puoi quindi aggiornare i parametri come richiesto e:

* **Salva**

  Salva le modifiche apportate.

  Per una configurazione di fabbrica, viene creata un&#39;istanza con un&#39;identità persistente. La nuova istanza viene quindi elencata in Configurazioni.

* **Reimposta**

  Ripristina i parametri mostrati sullo schermo agli ultimi salvati.

* **Eliminare**

  Elimina la configurazione corrente. Se standard, i parametri vengono ripristinati alle impostazioni predefinite. Se viene creata da una configurazione di fabbrica, l&#39;istanza specifica viene eliminata.

* **Annulla associazione**

  Separa la configurazione corrente dal bundle.

* **Annulla**

  Annulla le modifiche correnti.

## Bundle {#bundles}

Il **Bundle** è il meccanismo di installazione dei bundle OSGi necessari per l’AEM. È possibile accedere alla scheda utilizzando uno dei metodi seguenti:

* Il menu a discesa:

  **OSGi >**

* L’URL; ad esempio:

  `http://localhost:4502/system/console/bundles`

Viene visualizzato un elenco di bundle:

![screen_shot_2012-02-15alle44740pm](assets/screen_shot_2012-02-15at44740pm.png)

Utilizzando questa scheda è possibile:

* **Installare o aggiornare**

  È possibile **Sfoglia** per trovare il file contenente il bundle e specificare se deve **Inizio** immediatamente e in cui **Livello iniziale**.

* **Ricarica**

  Aggiorna l&#39;elenco visualizzato.

* **Aggiorna pacchetti**

  Questa verifica i riferimenti di tutti i colli e, se necessario, li aggiorna.

  Ad esempio, dopo un aggiornamento, la vecchia e la nuova versione potrebbero essere ancora in esecuzione a causa di riferimenti precedenti. Questa opzione controlla e sposta tutti i riferimenti alla nuova versione, consentendo l’interruzione della versione precedente.

* **Avvia**

  Avvia un bundle in base al livello iniziale specificato.

* **Interrompi**

  Arresta il bundle.

* **Disinstalla**

  Disinstalla il bundle dal sistema.

* **vedi lo stato**

  L’elenco specifica lo stato del bundle; facendo clic sul nome di un bundle specifico per visualizzare ulteriori informazioni.

>[!NOTE]
>
>Dopo **Aggiorna**, l’Adobe consiglia di eseguire una **Aggiorna pacchetti**.

## Componenti {#components}

Il **Componenti** Questa scheda ti consente di abilitare e/o disabilitare i vari componenti. È accessibile da:

* Il menu a discesa:

  **Principale >**

* L’URL; ad esempio:

  `http://localhost:4502/system/console/components`

Viene visualizzato un elenco di componenti. Sono disponibili varie icone che consentono di abilitare, disabilitare o (se appropriato) aprire i dettagli di configurazione di un componente specifico.

![screen_shot_2012-02-15alle52144pm](assets/screen_shot_2012-02-15at52144pm.png)

Facendo clic sul nome di un particolare componente vengono visualizzate ulteriori informazioni sul suo stato. Qui puoi anche abilitare, disabilitare o ricaricare il componente.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>L’attivazione o la disattivazione di un componente si applica solo fino al riavvio di AEM/CRX.
>
>Lo stato iniziale è definito all’interno del descrittore del componente, che viene generato durante lo sviluppo e memorizzato nel bundle al momento della creazione del bundle.
