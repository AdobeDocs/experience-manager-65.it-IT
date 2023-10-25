---
title: Manutenzione del registro di controllo dell’AEM 6
seo-title: Audit Log Maintenance in AEM 6
description: Scopri come gestire i registri di audit in Adobe Experience Manager (AEM).
seo-description: Learn about Audit Log Maintenance in Adobe Experience Manager (AEM).
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
source-git-commit: c7c32130a3257c14c98b52f9db31d80587d7993a
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Manutenzione del registro di controllo dell’AEM 6{#audit-log-maintenance-in-aem}

Gli eventi AEM idonei per la registrazione di audit generano molti dati archiviati. Questi dati possono crescere rapidamente nel tempo a causa di repliche, caricamenti di risorse e altre attività del sistema.

La manutenzione dei registri di controllo include diverse parti di funzionalità che consentono di automatizzare la manutenzione dei registri di controllo in base a criteri specifici.

Viene implementato come attività di manutenzione settimanale configurabile ed è accessibile tramite la console di monitoraggio della dashboard operazioni.

Per ulteriori informazioni, consulta [Documentazione del dashboard operazioni](/help/sites-administering/operations-dashboard.md).

Esistono tre tipi di opzioni di eliminazione del log di controllo:

1. [Eliminazione registro di controllo pagina](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Rimozione registro di controllo DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Esecuzione del log di controllo della replica](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Ciascuno può essere configurato creando regole nella console web AEM. Dopo averli configurati, puoi attivarli da **Strumenti - Operazioni - Manutenzione - Finestra di manutenzione settimanale** e l&#39;esecuzione **Attività di manutenzione del registro di controllo**.

## Configurare la rimozione del registro di controllo della pagina {#configure-page-audit-log-purging}

Per configurare la rimozione del registro di controllo, effettua le seguenti operazioni:

1. Passa all’amministratore della console Web puntando il browser su `http://localhost:4502/system/console/configMgr/`

1. Cerca un elemento denominato **Regola di rimozione del registro di controllo delle pagine** e fare clic su di esso.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Quindi, configurare il modulo di pianificazione della rimozione in base alle proprie esigenze. Opzioni disponibili:

   * **Nome regola:** il nome della regola dei criteri di audit;
   * **Percorso contenuto:** il percorso del contenuto a cui si applicherà la regola;
   * **Età minima:** il numero di giorni necessari per la conservazione dei registri di audit;
   * **Tipo di registro di controllo:** tipo di registro di controllo da eliminare.

   >[!NOTE]
   >
   >Il percorso del contenuto si applica solo agli elementi figlio del `/var/audit/com.day.cq.wcm.core.page` nell&#39;archivio.

1. Salva la regola.
1. Per poter essere eseguita, la regola appena creata deve essere esposta nel dashboard operazioni. Per farlo, vai **Strumenti - Operazioni - Manutenzione** dalla schermata iniziale dell’AEM.

1. Premere il tasto **Finestra di manutenzione settimanale** Card.

1. L’attività di manutenzione è già presente in **Attività di manutenzione del registro di controllo** Card.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. È possibile controllare la data dell&#39;esecuzione successiva, configurarla o eseguirla manualmente premendo il pulsante di riproduzione.

In AEM 6.3, se la finestra di manutenzione programmata si chiude prima che l&#39;attività di rimozione del log di controllo possa essere completata, l&#39;attività si interrompe automaticamente. L&#39;operazione riprenderà all&#39;apertura della finestra di manutenzione successiva.

**Con AEM 6.5**, è possibile interrompere manualmente un&#39;attività di rimozione del log di controllo facendo clic sul pulsante **Interrompi** icona. Alla successiva esecuzione l’attività riprenderà in modo sicuro.

>[!NOTE]
>
>Interrompere l&#39;attività di manutenzione significa sospenderne l&#39;esecuzione senza perdere la traccia del processo già in corso.

## Configurare la rimozione del registro di controllo DAM {#configure-dam-audit-log-purging}

1. Passa alla console di sistema all’indirizzo *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Cerca **Eliminazione registro di controllo DAM** e fare clic sul risultato.
1. Nella finestra successiva, configura la regola di conseguenza. Le opzioni sono:

   * **Nome regola:** il nome della regola dei criteri di audit;
   * **Percorso contenuto:** percorso del contenuto a cui verrà applicata la regola
   * **Età minima:** il numero di giorni necessari per la conservazione dei registri di audit
   * **Tipi di eventi Dam del registro di controllo:** i tipi di eventi di controllo DAM che devono essere eliminati.

1. Clic **Salva** per salvare la configurazione

## Configurare la rimozione del registro di controllo della replica  {#configure-replication-audit-log-purging}

1. Passa alla console di sistema all’indirizzo *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Cerca **Pianificazione eliminazione log di controllo della replica** e fai clic sul risultato
1. Nella finestra successiva, configura la regola di conseguenza. Le opzioni sono:

   * **Nome regola:** nome della regola dei criteri di controllo
   * **Percorso contenuto:** percorso del contenuto a cui verrà applicata la regola
   * **Età minima:** il numero di giorni necessari per la conservazione dei registri di audit
   * **Tipi di eventi di replica del registro di controllo:** i tipi di eventi di controllo di replica da eliminare

1. Clic **Salva** per salvare la configurazione.
