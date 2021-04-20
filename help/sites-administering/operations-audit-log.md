---
title: Manutenzione del registro di controllo in AEM 6
seo-title: Manutenzione del registro di controllo in AEM 6
description: Scopri la Manutenzione del log di controllo in AEM.
seo-description: Scopri la Manutenzione del log di controllo in AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# Manutenzione del registro di controllo in AEM 6{#audit-log-maintenance-in-aem}

AEM eventi idonei per la registrazione di controllo generano molti dati archiviati. Questi dati possono crescere rapidamente nel tempo a causa di repliche, caricamenti di risorse e altre attività del sistema.

La manutenzione del registro di controllo include diverse parti di funzionalità che consentono di automatizzare la manutenzione del registro di controllo in base a criteri specifici.

Viene implementato come attività di manutenzione settimanale configurabile ed è accessibile tramite la console di monitoraggio di Operations Dashboard.

Per ulteriori informazioni, consulta la [Documentazione dashboard delle operazioni](/help/sites-administering/operations-dashboard.md).

Sono disponibili tre tipi di opzioni di eliminazione del log di controllo:

1. [Pulizia del registro di controllo delle pagine](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Rimozione del log di controllo DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Eliminazione del registro di controllo della replica](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

È possibile configurarle creando regole nella Console Web AEM. Una volta configurati, è possibile attivarli andando su **Strumenti - Operazioni - Manutenzione - Manutenzione settimanale** ed eseguendo l&#39; **Attività di manutenzione AuditLog**.

## Configurare l’eliminazione del log di controllo della pagina {#configure-page-audit-log-purging}

Segui questi passaggi per configurare l’eliminazione del registro di controllo:

1. Vai all&#39;amministratore della console Web puntando il browser su `http://localhost:4502/system/console/configMgr/`

1. Cerca un elemento denominato **Regola di eliminazione del registro di controllo delle pagine** e fai clic su di esso.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Quindi, configura la pianificazione della rimozione in base alle tue esigenze. Le opzioni disponibili sono:

   * **nome della regola:** il nome della regola di politica di audit;
   * **Percorso del contenuto:** il percorso del contenuto a cui si applicherà la regola;
   * **età minima:** il tempo in giorni necessario per mantenere i registri di audit;
   * **Tipo di registro di controllo:** il tipo di registro di controllo che deve essere eliminato.

   >[!NOTE]
   >
   >Il percorso del contenuto si applica solo agli elementi secondari del nodo `/var/audit/com.day.cq.wcm.core.page` nell’archivio.

1. Salva la regola.
1. La regola appena creata deve essere esposta nel dashboard delle operazioni per eseguirla. Per farlo, vai **Strumenti - Operazioni - Manutenzione** dalla schermata di benvenuto AEM.

1. Premere la scheda **Finestra di manutenzione settimanale**.

1. L’attività di manutenzione è già presente nella scheda **Attività di manutenzione AuditLog**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. È possibile controllare la data dell&#39;esecuzione successiva, configurarla o eseguirla manualmente premendo il pulsante di riproduzione.

In AEM 6.3, se la finestra di manutenzione programmata viene chiusa prima del completamento dell&#39;attività di eliminazione del log di controllo, l&#39;attività viene arrestata automaticamente. Viene ripreso quando si apre la prossima finestra di manutenzione.

**Con AEM 6.5**, puoi interrompere manualmente un&#39;attività di eliminazione del log di controllo facendo clic sull&#39;icona  **** Stopicon. All&#39;esecuzione successiva l&#39;attività riprenderà in modo sicuro.

>[!NOTE]
>
>Per interrompere l’attività di manutenzione, sospenderne l’esecuzione senza perdere traccia del processo già in corso.

## Configurare l’eliminazione del log di controllo DAM {#configure-dam-audit-log-purging}

1. Passa alla console di sistema all&#39;indirizzo *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Cerca la regola **DAM audit Log Purge** e fai clic sul risultato.
1. Nella finestra successiva, configura di conseguenza la regola. Le opzioni sono:

   * **nome della regola:** il nome della regola di politica di audit;
   * **Percorso del contenuto:** il percorso del contenuto a cui si applicherà la regola
   * **Età minima:** tempo in giorni per mantenere i registri di controllo
   * **Tipi di eventi Dam del registro di controllo:**  i tipi di eventi di controllo DAM che devono essere eliminati.

1. Fai clic su **Salva** per salvare la configurazione

## Configurare l&#39;eliminazione del log di controllo della replica {#configure-replication-audit-log-purging}

1. Passa alla console di sistema all&#39;indirizzo *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Cerca **Utilità di pianificazione eliminazione registro di replica** e fai clic sul risultato
1. Nella finestra successiva, configura di conseguenza la regola. Le opzioni sono:

   * **Nome regola:** il nome della regola dei criteri di audit
   * **Percorso del contenuto:** il percorso del contenuto a cui si applicherà la regola
   * **Età minima:** tempo in giorni per mantenere i registri di controllo
   * **Tipi di eventi di replica del registro di controllo:**  i tipi di eventi di controllo di replica che devono essere eliminati

1. Fai clic su **Salva** per salvare la configurazione.
