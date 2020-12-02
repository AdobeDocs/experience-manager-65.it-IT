---
title: Strumenti di verifica e tracciamento
seo-title: Strumenti di verifica e tracciamento
description: AEM fornisce un framework per il test dell’interfaccia utente dei componenti e un meccanismo per il test e il debug dei componenti
seo-description: AEM fornisce un framework per il test dell’interfaccia utente dei componenti e un meccanismo per il test e il debug dei componenti
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Strumenti di verifica e tracciamento{#testing-and-tracking-tools}

## Test {#testing}

AEM fornisce:

* [un framework per il test dell’interfaccia](/help/sites-developing/hobbes.md) utente dei componenti.
* [un meccanismo di verifica e debug dei componenti](/help/sites-developing/developer-mode.md).

Di seguito sono riportati due strumenti Open Source Testing:

**Selenio**

Il selenio viene utilizzato per il test delle funzioni in un browser con un utente per attività. Registra i passaggi di test (clic) come tabelle HTML o classi Java.

Per ulteriori informazioni, vedere [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMeter**

JMeter viene utilizzato per monitorare le richieste e può essere utilizzato per test funzionali, di prestazioni e di stress.

Per ulteriori informazioni, vedere [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

Esistono anche molti strumenti proprietari per automatizzare i test e gestire i piani di test.

### Tracciamento {#tracking}

I seguenti strumenti sono facilmente disponibili. Tuttavia, un problema fondamentale in tutti i casi è la disponibilità dei dati a tutti i membri del team - partner e cliente del progetto.

**Bugzilla**

Un sistema di monitoraggio dei bug che può essere configurato in base alle proprie esigenze.

**Fogli di calcolo**

Anche se non specificamente uno strumento di tracciamento dei bug, i fogli di calcolo sono spesso *mis* utilizzati a questo scopo, in quanto sono facili da capire e la maggior parte degli utenti ha esperienza della loro funzionalità.

Se vengono utilizzati per il tracciamento, effettuate le seguenti operazioni:

* dovrebbero essere tenuti semplici.
* il numero dei singoli fogli di calcolo dovrebbe essere limitato al minimo.
* devono essere aggiornati regolarmente.
* è necessario mantenere una sola copia master e tutti devono sapere dov&#39;è la copia master.
* devono essere accessibili a tutti i membri del progetto.
* se la sicurezza è un problema (spesso si verifica in grandi aziende) e l&#39;accesso comune non è possibile, le copie possono essere distribuite purché tutti comprendano che si tratta di copie e che non è possibile aggiornarle.

Anche in questo caso esistono molti strumenti proprietari per tenere traccia dei bug e dei requisiti delle funzioni.
