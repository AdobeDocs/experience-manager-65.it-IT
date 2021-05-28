---
title: Aggiornamento a AEM 6.5
seo-title: Aggiornamento a AEM 6.5
description: Scopri le nozioni di base per l’aggiornamento di un’installazione AEM precedente a AEM 6.5.
seo-description: Scopri le nozioni di base per l’aggiornamento di un’installazione AEM precedente a AEM 6.5.
uuid: 45368056-273c-4f1a-9da6-e7ba5c2bbc0d
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: ebd99cc4-8762-4c28-a177-d62dac276afe
docset: aem65
targetaudience: target-audience upgrader
feature: Aggiornamento
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 4%

---

# Aggiornamento a AEM 6.5 {#upgrading-to-aem}

In questa sezione viene descritto l’aggiornamento di un’installazione AEM a AEM 6.5:

* [Pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md)
* [Valutazione della complessità dell’aggiornamento con rilevatore pattern](/help/sites-deploying/pattern-detector.md)
* [Compatibilità con le versioni precedenti in AEM 6.5](/help/sites-deploying/backward-compatibility.md)

<!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [Procedura di aggiornamento](/help/sites-deploying/upgrade-procedure.md)
* [Aggiornamento di codice e personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Esecuzione di un aggiornamento sul posto](/help/sites-deploying/in-place-upgrade.md)
* [Controlli e risoluzione dei problemi post-aggiornamento](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Aggiornamenti sostenibili](/help/sites-deploying/sustainable-upgrades.md)
* [Migrazione dei contenuti Lazy](/help/sites-deploying/lazy-content-migration.md)
* [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md)

Per fare un riferimento più agevole alle istanze AEM coinvolte in queste procedure, in questi articoli sono utilizzati i termini seguenti:

* L&#39;istanza *source* è l&#39;istanza AEM da cui stai eseguendo l&#39;aggiornamento.
* L&#39;istanza *target* è quella in cui si esegue l&#39;aggiornamento.

>[!NOTE]
>
>Nell&#39;ambito degli sforzi volti a migliorare l&#39;affidabilità degli aggiornamenti, AEM ha subito una ristrutturazione completa degli archivi. Per ulteriori informazioni su come allinearsi alla nuova struttura, vedere [Ristrutturazione archivio in AEM.](/help/sites-deploying/repository-restructuring.md)

## Cosa è cambiato? {#what-has-changed}

Di seguito sono riportate le principali modifiche apportate alle note nelle ultime diverse versioni di AEM:

AEM 6.0 ha introdotto il nuovo archivio Jackrabbit Oak. I gestori di persistenza sono stati sostituiti da [Micro Kernel](/help/sites-deploying/platform.md#contentbody_title_4). A partire dalla versione 6.1, CRX2 non è più supportato. Per migrare gli archivi CRX2 dalle istanze 5.6.1, è necessario eseguire uno strumento di migrazione denominato crx2oak. Per ulteriori informazioni, consulta [Utilizzo dello strumento di migrazione CRX2OAK](/help/sites-deploying/using-crx2oak.md).

Se devi utilizzare Assets Insights e stai eseguendo l’aggiornamento da una versione precedente alla AEM 6.2, devi eseguire la migrazione delle risorse e generare gli ID tramite un tag JMX. Nei nostri test interni, le risorse 125K in un ambiente TarMK sono state migrate in un&#39;ora, ma i risultati potrebbero variare.

6.3 ha introdotto un nuovo formato per `SegmentNodeStore`, che è la base dell&#39;implementazione TarMK. Se esegui l’aggiornamento da una versione precedente alla versione 6.3 di AEM, sarà necessaria una migrazione dell’archivio come parte dell’aggiornamento, che implica tempi di inattività del sistema.

L&#39;ingegneria Adobe stima che questo sia di circa 20 minuti. La reindicizzazione non sarà necessaria. Inoltre, è stata rilasciata una nuova versione dello strumento crx2oak per lavorare con il nuovo formato dell&#39;archivio.

**Questa migrazione non è necessaria se si esegue l’aggiornamento da AEM 6.3 a AEM 6.5.**

Le attività di manutenzione pre-aggiornamento sono state ottimizzate per supportare l’automazione.

Le opzioni di utilizzo della riga di comando dello strumento crx2oak sono state modificate per essere facili da usare e supportare più percorsi di aggiornamento.

Anche i controlli post-aggiornamento sono stati resi facili dall&#39;automazione.

La raccolta periodica degli oggetti inattivi di revisioni e la raccolta degli oggetti inattivi dell&#39;archivio dati sono ora attività di manutenzione ordinaria che devono essere eseguite periodicamente. Con l&#39;introduzione di AEM 6.3, Adobe supporta e consiglia il cleanup delle revisioni online. Per informazioni su come configurare queste attività, consulta [Pulizia revisioni](/help/sites-deploying/revision-cleanup.md) .

AEM recentemente introduce il [rilevatore pattern](/help/sites-deploying/pattern-detector.md) per la valutazione della complessità dell’aggiornamento quando si inizia a pianificare l’aggiornamento. 6.5 si concentra anche sulla [compatibilità con le versioni precedenti](/help/sites-deploying/backward-compatibility.md) delle funzioni. Infine, vengono aggiunte anche le best practice per [aggiornamenti sostenibili](/help/sites-deploying/sustainable-upgrades.md) .

Per ulteriori dettagli sulle modifiche apportate alle versioni recenti di AEM, consulta le note complete sulla versione:

* [https://helpx.adobe.com/it/experience-manager/6-2/release-notes.html](https://helpx.adobe.com/it/experience-manager/6-2/release-notes.html)
* [https://helpx.adobe.com/it/experience-manager/6-3/release-notes.html](https://helpx.adobe.com/experience-manager/6-3/release-notes.html)
* [https://helpx.adobe.com/it/experience-manager/6-4/release-notes.html](https://helpx.adobe.com/it/experience-manager/6-4/release-notes.html)
* [https://helpx.adobe.com/it/experience-manager/6-5/release-notes.html](https://helpx.adobe.com/it/experience-manager/6-5/release-notes.html)

## Panoramica dell&#39;aggiornamento {#upgrade-overview}

L&#39;aggiornamento di AEM è un processo a più passaggi, a volte a più mesi. La seguente struttura è stata fornita come panoramica di ciò che è incluso in un progetto di aggiornamento e del contenuto incluso in questa documentazione:

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## Flusso di aggiornamento {#upgrade-overview-1}

Il diagramma seguente acquisisce il flusso consigliato complessivo evidenziando l’approccio di aggiornamento. Nota il riferimento alle nuove funzioni introdotte. L&#39;aggiornamento dovrebbe iniziare con il rilevatore pattern (consulta [Assessing the Upgrade Complexity with Pattern Detector](/help/sites-deploying/pattern-detector.md)), che dovrebbe consentire di decidere il percorso da seguire per la compatibilità con AEM 6.4 in base ai pattern nel rapporto generato.

La versione 6.5 di è stata messa a fuoco per mantenere tutte le nuove funzioni compatibili con le versioni precedenti, ma nei casi in cui si riscontrano ancora problemi di compatibilità con le versioni precedenti, la modalità di compatibilità consente di posticipare temporaneamente lo sviluppo per mantenere il codice personalizzato conforme alla versione 6.5. Questo approccio consente di evitare sforzi di sviluppo subito dopo l’aggiornamento (consulta [Compatibilità con le versioni precedenti in AEM 6.5](/help/sites-deploying/backward-compatibility.md)).

Infine, nel tuo ciclo di sviluppo 6.5, le funzioni introdotte in Aggiornamenti sostenibili (vedi [Aggiornamenti sostenibili](/help/sites-deploying/sustainable-upgrades.md)) ti aiutano a seguire le best practice per rendere gli aggiornamenti futuri ancora più efficienti e diretti.

![6_4_upgrade_overviewflowgraph-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
