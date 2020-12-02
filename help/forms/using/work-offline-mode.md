---
title: Utilizzo della modalità offline
seo-title: Utilizzo della modalità offline
description: 'Disconnetti il dispositivo mobile al di fuori della gamma di  rete AEM Forms o in modalità completamente offline e lavora sull''app AEM Forms '
seo-description: 'Disconnetti il dispositivo mobile al di fuori della gamma di  rete AEM Forms o in modalità completamente offline e lavora sull''app AEM Forms '
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Utilizzo della modalità offline {#working-in-the-offline-mode}

La modalità offline dell&#39;app  AEM Forms consente di lavorare senza problemi anche se l&#39;app va offline. È possibile aprire, aggiornare e inviare un modulo senza che sia necessaria alcuna connettività di rete.

Per iniziare a lavorare sull&#39;app AEM Forms , sincronizzate l&#39;app con il server AEM Forms . Tutti i moduli assegnati all&#39;utente vengono scaricati nell&#39;app. Per  AEM Forms su JEE, le attività vengono recuperate nella scheda delle attività, e i punti di avvio e altri moduli associati nella scheda Forms. Per  AEM Forms su OSGi, nella scheda Forms viene caricato solo Forms.

Per informazioni dettagliate sulla sincronizzazione dell&#39;app, consultate [Sincronizzazione dell&#39;app](/help/forms/using/sync-app.md).

## Forms disponibile offline {#making-forms-available-offline}

Quando si sincronizza l&#39;app con il server AEM Forms , i moduli vengono scaricati sul dispositivo mobile. Tuttavia, per impostazione predefinita, gli allegati associati al modulo non vengono scaricati. Ciò implica che se siete online, potete visualizzare gli allegati. Tuttavia, per essere certi di poter visualizzare l&#39;allegato in modalità offline, modificate le impostazioni predefinite nell&#39;app.

Per fare in modo che gli allegati associati siano scaricati con ciascun modulo, impostare Recupera allegati su ON. Per informazioni dettagliate, vedere [Aggiornamento delle impostazioni generali](/help/forms/using/update-general-settings.md).

Poiché il download dei dati sul dispositivo mobile può influire sulle prestazioni del dispositivo, per impostazione predefinita, l&#39;impostazione Recupera allegati è impostata su OFF. Gli allegati vengono estratti nel dispositivo per qualsiasi attività scaricata dal server dopo che l&#39;impostazione è stata aggiornata a ON. In modalità offline, un utente può quindi lavorare su tutte le attività che vengono scaricate sul dispositivo dopo aver impostato le opzioni **Recupera allegati** su ON.

## Configurazione del servizio offline per  app AEM Forms {#configuring-offline-service-for-aem-forms-app-br}

 servizio offline app AEM Forms identifica le risorse utilizzate in un modulo.  app AEM Forms si basa su questo servizio per ottenere informazioni sulle dipendenze del modulo. Per abilitare le funzionalità offline, sono necessarie informazioni sulle dipendenze del modulo. Il servizio offline  app AEM Forms memorizza nella cache i percorsi o gli URL delle risorse utilizzate in un modulo. La cache viene aggiornata in base alle modifiche apportate al modulo e al periodo di validità configurato per il servizio offline. La memorizzazione nella cache di percorsi o URL delle risorse utilizzate in un modulo migliora le prestazioni lato server.

Per configurare il componente offline lato server di  app AEM Forms:

1. Nell&#39;istanza di creazione, andate a **Adobe Experience Manager** >**Strumenti** > **Forms** > **Configura servizio offline app Forms**.

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. In Impostazioni generali potete effettuare le seguenti operazioni:

   * **Cancella cache**: Cancella la cache lato server delle dipendenze del modulo.
   * **Ripristina configurazione**: Ripristina la configurazione offline dell&#39;app AEM Forms .
   * **Validità** cache: Specifica il periodo di validità della cache offline lato server.
   * **Percorsi** di osservazione delle risorse: Specifica i percorsi in cui il servizio offline effettua il monitoraggio delle modifiche delle risorse. Se si verificano modifiche nei percorsi specificati, la cache offline di tutti i moduli dipendenti viene aggiornata. Esempio, `/etc/clientlibs/fd,/content/dam/images`.

1. Nella scheda **Cache delle risorse manuali**, specificare che il servizio offline delle dipendenze del modulo non è in grado di identificare. È possibile specificare risorse come le immagini caricate dall&#39;interno di JavaScript.  app AEM Forms scaricherà anche queste risorse per la modalità offline.
