---
title: Strumenti di test e tracciamento
seo-title: Testing and Tracking Tools
description: AEM fornisce un framework per la verifica dell’interfaccia utente dei componenti e un meccanismo per la verifica e il debug dei componenti
seo-description: AEM provides a framework for testing component UI and a mechanism for testing and debugging components
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 1%

---

# Strumenti di test e tracciamento{#testing-and-tracking-tools}

## Test {#testing}

AEM fornisce:

* [un framework per il test dell’interfaccia utente dei componenti](/help/sites-developing/hobbes.md).
* [un meccanismo per la verifica e il debug dei componenti](/help/sites-developing/developer-mode.md).

Di seguito sono riportati due strumenti di test Open Source:

**Selenio**

Il selenio viene utilizzato per il test delle funzioni in un browser con un utente per attività. Registra i passaggi di test (clic) come tabelle HTML o classi Java.

Per ulteriori informazioni consulta [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMeter**

JMeter viene utilizzato per monitorare le richieste e può essere utilizzato per prove funzionali, di prestazioni e di stress.

Per ulteriori informazioni consulta [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

Esistono anche molti strumenti proprietari per automatizzare i test e gestire i piani di test.

### Tracciamento {#tracking}

I seguenti strumenti sono facilmente disponibili. Tuttavia, un problema fondamentale in tutti i casi è la disponibilità dei dati a tutti i membri del team del progetto - partner e cliente.

**Bugzilla**

Un sistema di tracciamento dei bug configurabile in base alle tue esigenze.

**Fogli di calcolo**

Anche se non specificamente uno strumento di tracciamento dei bug, i fogli di calcolo sono spesso *mis* utilizzati per questo scopo, in quanto sono facili da comprendere e la maggior parte degli utenti ha esperienza della loro funzionalità.

Se vengono utilizzati per il tracciamento, allora:

* dovrebbero essere mantenuti semplici.
* il numero dei singoli fogli di calcolo dovrebbe essere ridotto al minimo.
* devono essere aggiornati regolarmente.
* è necessario mantenere una sola copia master e tutti devono sapere dove si trova la copia master.
* devono essere accessibili a tutti i membri del progetto.
* se la sicurezza è un problema (spesso si verifica in grandi aziende) e l&#39;accesso comune non è possibile, le copie possono essere distribuite purché tutti comprendano che si tratta di copie e non possono essere aggiornate.

Anche in questo caso esistono molti strumenti proprietari per il monitoraggio di bug e requisiti di funzionalità.
