---
title: Utilizzo della modalità offline
description: Disconnetti il tuo dispositivo mobile al di fuori dell’intervallo della rete AEM Forms o in modalità completamente offline e lavora sull’app AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: ba4ceef1-510d-41ef-94b8-4834fb7de804
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Utilizzo della modalità offline {#working-in-the-offline-mode}

La modalità offline dell’app AEM Forms consente di lavorare senza problemi anche se l’app va offline. È possibile aprire, aggiornare e inviare un modulo senza richiedere alcuna connettività di rete.

Per iniziare a lavorare sull’app AEM Forms, sincronizza l’app con il server AEM Forms. Tutti i moduli assegnati vengono scaricati nell’app. In AEM Forms su JEE, le attività vengono recuperate nella scheda attività e i moduli associati ai punti iniziali e altri moduli nella scheda Forms. Per AEM Forms su OSGi, nella scheda Forms vengono caricati solo Forms.

Per informazioni dettagliate su come sincronizzare l’app, consulta [Sincronizzazione dell’app](/help/forms/using/sync-app.md).

## Come rendere Forms disponibile offline {#making-forms-available-offline}

Quando sincronizzi l’app con il server AEM Forms, i moduli vengono scaricati sul tuo dispositivo mobile. Tuttavia, per impostazione predefinita, gli allegati associati al modulo non vengono scaricati. Ciò significa che se si è in linea, è possibile visualizzare gli allegati. Tuttavia, per garantire che tu possa visualizzare l’allegato in modalità offline, modifica le impostazioni predefinite nell’app.

Per assicurarsi che gli allegati associati vengano scaricati con ogni modulo, impostare Recupera allegati su ON. Per ulteriori informazioni, consulta [Aggiornamento delle impostazioni generali](/help/forms/using/update-general-settings.md).

Poiché il download di dati sul dispositivo mobile può influire sulle prestazioni del dispositivo, per impostazione predefinita l’impostazione Fetch attach (Recupero allegati) è disattivata. Gli allegati vengono recuperati sul dispositivo per tutte le attività scaricate dal server dopo l&#39;aggiornamento dell&#39;impostazione su ON. In modalità offline, un utente può quindi lavorare su tutte le attività scaricate sul dispositivo dopo aver impostato **Recupera allegati** su ON.

## Configurazione del servizio offline per l’app AEM Forms {#configuring-offline-service-for-aem-forms-app-br}

Il servizio offline app di AEM Forms identifica le risorse utilizzate in un modulo. L’app AEM Forms si basa su questo servizio per ottenere informazioni sulle dipendenze dei moduli. Per abilitare le funzionalità offline sono necessarie informazioni sulle dipendenze dei moduli. Il servizio offline dell’app AEM Forms memorizza nella cache i percorsi o gli URL delle risorse utilizzate in un modulo. La cache viene aggiornata in base alle modifiche nel modulo e al periodo di validità configurato per il servizio offline. La memorizzazione nella cache di percorsi o URL delle risorse utilizzate in un modulo migliora le prestazioni lato server.

Per configurare il componente offline lato server dell&#39;app AEM Forms:

1. Nell’istanza di authoring, passa a **Adobe Experience Manager** >**Strumenti** > **Forms** > **Configura servizio offline app Forms**.

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. In Impostazioni generali (General Settings) potete effettuare le seguenti operazioni:

   * **Cancella cache**: cancella la cache lato server delle dipendenze del modulo.
   * **Ripristina configurazione**: reimposta la configurazione offline dell’app AEM Forms.
   * **Validità cache**: specifica il periodo di validità per la cache offline lato server.
   * **Percorsi di osservazione delle risorse**: specifica i percorsi in cui il servizio offline monitora le modifiche alle risorse. Se si verificano modifiche nei percorsi specificati, la cache offline di tutti i moduli dipendenti viene aggiornata. Esempio: `/etc/clientlibs/fd,/content/dam/images`.

1. In **Cache risorse manuale** , specificare le dipendenze del modulo che il servizio offline non è in grado di identificare. È possibile specificare risorse quali immagini caricate da JavaScript. L’app AEM Forms scaricherà queste risorse anche per la modalità offline.
