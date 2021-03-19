---
title: Console Web
seo-title: Console Web
description: Scopri come utilizzare la console web AEM.
seo-description: Scopri come utilizzare la console web AEM.
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
feature: Configurazione
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 3%

---


# Console Web{#web-console}

La console Web in AEM si basa sulla [console di gestione Web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix è uno sforzo della comunità per implementare la piattaforma di servizi OSGi R4, che include il framework OSGi e i servizi standard.

>[!NOTE]
>
>Nella console Web tutte le descrizioni che fanno riferimento alle impostazioni predefinite si riferiscono ai valori predefiniti di Sling.
>
>AEM dispone di valori predefiniti personalizzati e pertanto i valori predefiniti impostati potrebbero essere diversi da quelli documentati nella console.

La console Web offre una selezione di schede per la manutenzione dei bundle OSGi, tra cui:

* [Configurazione](#configuration): utilizzato per configurare i bundle OSGi ed è quindi il meccanismo sottostante per configurare i parametri di sistema AEM
* [Bundle](#bundles): utilizzato per l&#39;installazione dei bundle
* [Componenti](#components): utilizzato per controllare lo stato dei componenti necessari per AEM

Tutte le modifiche apportate vengono immediatamente applicate al sistema in esecuzione. Non è necessario riavviare il sistema.

È possibile accedere alla console da `../system/console`; ad esempio:

`http://localhost:4502/system/console/components`

## Configurazione {#configuration}

La scheda **Configurazione** viene utilizzata per configurare i bundle OSGi ed è quindi il meccanismo sottostante per la configurazione AEM parametri di sistema.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Configurazione OSGi con la console Web](/help/sites-deploying/configuring-osgi.md) .

La scheda **Configurazione** è accessibile da:

* Menu a discesa:

   **OSGi >**

* URL; ad esempio:

   `http://localhost:4502/system/console/configMgr`

Verrà visualizzato un elenco di configurazioni:

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Sono disponibili due tipi di configurazioni dagli elenchi a discesa in questa schermata:

* ****
ConfigurazioniConsente di aggiornare le configurazioni esistenti. Hanno un identificatore di identità persistente (PID) e possono essere:

   * standard e integrale a AEM; se vengono eliminati, i valori vengono ripristinati alle impostazioni predefinite.
   * istanze create da configurazioni di fabbrica; queste istanze vengono create dall&#39;utente, l&#39;eliminazione rimuove l&#39;istanza.

* **Configurazioni**
di fabbricaConsente di creare un&#39;istanza dell&#39;oggetto funzionalità richiesto.

   A questo verrà assegnata un’identità persistente ed è quindi elencata nell’elenco a discesa Configurazioni .

Selezionando una voce dagli elenchi verranno visualizzati i parametri relativi a tale configurazione:

![chlimage_1-21](assets/chlimage_1-21a.png)

Puoi quindi aggiornare i parametri come richiesto e:

* **Salva**

   Salva le modifiche apportate.

   Per una configurazione di fabbrica, creerà una nuova istanza con un’identità persistente. La nuova istanza verrà quindi elencata in Configurazioni.

* **Ripristina**

   Reimposta i parametri visualizzati sullo schermo su quelli salvati per ultimi.

* **Elimina**

   Elimina la configurazione corrente. Se standard, i parametri vengono restituiti alle impostazioni predefinite. Se creato da una configurazione di fabbrica, l&#39;istanza specifica viene eliminata.

* **Separa**

   Separa la configurazione corrente dal bundle.

* **Annulla**

   Annulla le modifiche correnti.

## Bundle {#bundles}

La scheda **Bundle** è il meccanismo per installare i bundle OSGi necessari per AEM. È possibile accedere alla scheda utilizzando uno dei seguenti metodi:

* Menu a discesa:

   **OSGi >**

* URL; ad esempio:

   `http://localhost:4502/system/console/bundles`

Verrà visualizzato un elenco dei bundle:

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

Questa scheda consente di:

* **Installa o aggiorna**

   Puoi **Sfoglia** per trovare il file contenente il tuo bundle e specificare se deve **Avviare** immediatamente e in quale **Livello iniziale**.

* **Ricarica**

   Aggiorna l’elenco visualizzato.

* **Aggiorna pacchetti**

   Questo controllerà i riferimenti di tutti i pacchetti e aggiornerà se necessario.

   Ad esempio, dopo un aggiornamento potrebbe essere ancora in esecuzione sia la versione precedente che quella nuova a causa di riferimenti precedenti. Questa opzione consente di controllare e spostare tutti i riferimenti alla nuova versione, consentendo l’arresto della versione precedente.

* **Avvia**

   Avvia un bundle in base al livello iniziale specificato.

* **Arresta**

   Arresta il bundle.

* **Disinstalla**

   Disinstalla il bundle dal sistema.

* **vedere lo stato**

   L&#39;elenco specifica lo stato attuale del bundle; cliccando sul nome di un bundle specifico con mostra ulteriori informazioni.

>[!NOTE]
>
>Dopo **Aggiorna** si consiglia di eseguire un **Aggiorna pacchetti**.

## Componenti {#components}

La scheda **Componenti** consente di abilitare e/o disabilitare i vari componenti. È accessibile da:

* Menu a discesa:

   **Principale >**

* URL; ad esempio:

   `http://localhost:4502/system/console/components`

Verrà visualizzato un elenco di componenti. Sono disponibili diverse icone per abilitare, disabilitare o (se appropriato) aprire i dettagli di configurazione di un componente specifico.

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

Facendo clic sul nome di un particolare componente verranno visualizzate ulteriori informazioni sullo stato. Qui puoi anche abilitare, disabilitare o ricaricare il componente.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>L’abilitazione o la disattivazione di un componente viene applicata solo fino al riavvio di AEM/CRX.
>
>Lo stato di avvio è definito nel descrittore del componente, che viene generato durante lo sviluppo e memorizzato nel bundle al momento della creazione del bundle.

