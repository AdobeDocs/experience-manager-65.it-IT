---
title: Strumenti di test e tracciamento
description: L’AEM fornisce un framework per testare l’interfaccia utente dei componenti e un meccanismo per testare e debug i componenti
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 1%

---

# Strumenti di test e tracciamento{#testing-and-tracking-tools}

## Test {#testing}

AEM fornisce:

* [un framework per testare l’interfaccia utente dei componenti](/help/sites-developing/hobbes.md).
* [un meccanismo per testare e eseguire il debug dei componenti](/help/sites-developing/developer-mode.md).

Di seguito sono riportati due strumenti di test open source:

**Selenio**

Selenium viene utilizzato per il test di funzione in un browser con un utente per attività. Registra i passaggi di test (clic) come tabelle HTML o classi Java™.

Per ulteriori informazioni, consulta [https://www.selenium.dev/](https://www.selenium.dev/).

**JMeter**

JMeter viene utilizzato per tenere traccia delle richieste e può essere utilizzato per test funzionali, di prestazioni e di stress.

Per ulteriori informazioni, consulta [https://jmeter.apache.org/](https://jmeter.apache.org/).

Esistono anche molti strumenti proprietari per automatizzare i test e gestire i piani di test.

### Tracciamento {#tracking}

I seguenti strumenti sono facilmente disponibili. Tuttavia, un problema chiave in tutti i casi è la disponibilità dei dati per tutti i membri del team di progetto - partner e cliente.

**Bugzilla**

Un sistema di tracciamento dei bug che può essere configurato in base alle tue esigenze.

**Fogli di calcolo**

Anche se non si tratta di uno strumento specifico per il monitoraggio dei bug, i fogli di calcolo sono spesso *errore* utilizzati per questo scopo in quanto sono facili da comprendere e la maggior parte degli utenti ha esperienza delle loro funzionalità.

Se questi fogli di calcolo vengono utilizzati per il tracciamento:

* dovrebbero essere mantenuti semplici.
* il numero di singoli fogli di calcolo deve essere ridotto al minimo.
* essi devono essere aggiornati regolarmente.
* deve essere conservata una sola copia primaria e tutti devono sapere dove si trova la copia primaria.
* devono essere accessibili a tutti i membri del progetto.
* se la sicurezza è un problema (spesso si verifica nelle grandi aziende) e l’accesso comune non è possibile, è possibile distribuire le copie purché tutti comprendano che i fogli di calcolo sono copie e non possono essere aggiornati.

Anche in questo caso, esistono molti strumenti proprietari per monitorare i bug e i requisiti delle funzioni.
