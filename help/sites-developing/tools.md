---
title: Strumenti di test e tracciamento
description: AEM fornisce un framework per testare l’interfaccia utente dei componenti e un meccanismo per testare e debug i componenti
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 5%
---
# Strumenti di test e tracciamento{#testing-and-tracking-tools}

## Test {#testing}

AEM fornisce:

* [un framework per la verifica dell&#39;interfaccia utente del componente](/help/sites-developing/hobbes.md).
* [un meccanismo per il test e il debug dei componenti](/help/sites-developing/developer-mode.md).

Di seguito sono riportati due strumenti di prova di Open Source:

**Selenio**

Selenium viene utilizzato per il test di funzione in un browser con un utente per attività. Registra i passaggi di test (clic) come tabelle HTML o classi Java™.

Per ulteriori informazioni, vedere [https://www.selenium.dev/](https://www.selenium.dev/).

**JMeter**

JMeter viene utilizzato per tenere traccia delle richieste e può essere utilizzato per test funzionali, di prestazioni e di stress.

Per ulteriori informazioni, vedere [https://jmeter.apache.org/](https://jmeter.apache.org/).

Esistono anche molti strumenti proprietari per automatizzare i test e gestire i piani di test.

### Tracciamento {#tracking}

I seguenti strumenti sono facilmente disponibili. Tuttavia, un problema chiave in tutti i casi è la disponibilità dei dati per tutti i membri del team di progetto - partner e cliente.

**Bugzilla**

Un sistema di tracciamento dei bug che può essere configurato in base alle tue esigenze.

**Fogli di calcolo**

Anche se non si tratta di uno strumento specifico per il monitoraggio dei bug, i fogli di calcolo sono spesso *mis* utilizzati a questo scopo in quanto sono facili da comprendere e la maggior parte degli utenti ha esperienza delle loro funzionalità.

Se questi fogli di calcolo vengono utilizzati per il tracciamento:

* dovrebbero essere mantenuti semplici.
* il numero di singoli fogli di calcolo deve essere ridotto al minimo.
* essi devono essere aggiornati regolarmente.
* deve essere conservata una sola copia primaria e tutti devono sapere dove si trova la copia primaria.
* devono essere accessibili a tutti i membri del progetto.
* se la sicurezza è un problema (spesso si verifica nelle grandi aziende) e l’accesso comune non è possibile, è possibile distribuire le copie purché tutti comprendano che i fogli di calcolo sono copie e non possono essere aggiornati.

Anche in questo caso, esistono molti strumenti proprietari per monitorare i bug e i requisiti delle funzioni.
