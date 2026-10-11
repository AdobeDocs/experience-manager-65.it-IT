---
title: Authoring per headless con Adobe Experience Manager
description: Introduzione alle potenti e flessibili funzionalità headless di Adobe Experience Manager e come creare contenuti per il progetto.
exl-id: 39d2218a-4f11-459d-8514-cfd312246be5
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Developer, User, Leader
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 87%
---
# Authoring per headless con AEM - Introduzione {#author-headless-introduction}

In questa sezione del [Percorso di authoring di contenuti headless AEM](overview.md), puoi imparare i concetti e la terminologia (di base) necessari per comprendere l&#39;authoring dei contenuti per la distribuzione di contenuti headless con Adobe Experience Manager (AEM).

## Obiettivo {#objective}

* **Pubblico**: principiante
* **Obiettivo**: introdurre i concetti e la terminologia relativi all’authoring headless.

## Sistema di gestione dei contenuti (CMS) {#content-management-system}

Che cos’è un sistema di gestione dei contenuti?

Un sistema di gestione dei contenuti (CMS, Content Management System) fa esattamente ciò che dice il nome: un sistema informatico utilizzato per gestire i contenuti. Questo è un po’ generale quindi, per essere più precisi, viene (in genere) utilizzato per gestire i contenuti che desideri rendere disponibili sui siti web.

## CMS headless {#headless-cms}

Headless è un termine utilizzato per descrivere i sistemi in cui i contenuti sono separati efficacemente dal modo in cui i contenuti vengono visualizzati sul web.

Tradizionalmente, il contenuto era gestito con un CMS, e lo stesso CMS determinava il rendering di tale contenuto sulle pagine web.

Ora, headless significa che il set di contenuti può essere gestito in CMS e quindi accessibile da una o più applicazioni (indipendenti).

Per questa ragione i contenuti possono essere inviati a qualsiasi dispositivo, in una vasta gamma di formati. Questo rende l’intero processo molto più flessibile, e implica inoltre che non è necessario preoccuparsi del layout e della formattazione.

>[!NOTE]
>
>Per ulteriori informazioni sui dettagli tecnici relativi ai CMS headless, consulta Informazioni sullo sviluppo CMS headless.

## Adobe Experience Manager {#aem-cms}

Allora cos’è AEM?

Innanzitutto, AEM è un sistema di gestione dei contenuti con un’ampia gamma di funzioni personalizzabili per soddisfare le tue esigenze.

Questo significa che può essere utilizzato come un:

* CMS headless
  * I contenuti headless possono essere elaborati come **Frammenti di contenuto**.
    Si tratta di elementi autonomi di contenuto a cui è possibile accedere direttamente da una serie di applicazioni, in quanto dispongono di una struttura predefinita basata sui **Modelli per frammenti di contenuto**.
    Ciò significa che i contenuti possono essere fruiti su una vasta gamma di dispositivi, in una vasta gamma di formati e con un’ampia serie di funzionalità.
    (E se ciò non bastasse, questi frammenti possono essere utilizzati anche per la creazione di pagine web AEM, se lo si desidera.)

* CMS “tradizionale”
  * Il contenuto viene creato per le pagine web utilizzando una serie di componenti che definiscono il modo in cui verrà eseguito il rendering del contenuto sul sito web. Anche in questo caso, AEM è estremamente flessibile in quanto il team di progetto può sviluppare componenti personalizzati.

## Modellazione dei contenuti {#content-modeling}

Quindi la modellazione dei contenuti (nota anche come modellazione dei dati) è un altro termine tecnico: perché dovrebbe interessarti in qualità di autore?

Affinché le applicazioni headless possano accedere ai contenuti e utilizzarli, il contenuto deve avere una struttura predefinita. Sarebbe possibile avere i contenuti in una forma libera, ma per le applicazioni tutto diventerebbe *molto* complicato.

In sostanza, il processo di definizione della struttura del contenuto da rispettare prevede la progettazione di un modello, denominata modellazione dei dati.

Per AEM il ruolo Architetto dei contenuti (spesso una persona diversa) eseguirà la modellazione dei dati per progettare una serie di **Modelli per frammenti di contenuto**, che serviranno da base per i tuoi contenuti utilizzando **Frammenti di contenuto**.

>[!NOTE]
>
>Per ulteriori informazioni sulla modellazione dei dati, consulta il Percorso Architect di contenuti AEM headless.

## Passaggio successivo {#whats-next}

Ora che hai imparato i concetti e la terminologia, il passo successivo è [Scoprire le nozioni di base sulla creazione di frammenti di contenuto](basics.md). Questa è un’introduzione alla gestione di base di AEM e alle istruzioni su come creare i frammenti di contenuto.

## Risorse aggiuntive {#additional-resources}

* Percorso per sviluppatori headless di AEM
  * [Scopri di più sullo sviluppo di CMS headless](/help/journey-headless/developer/learn-about.md)

* [Percorso Architect di contenuti AEM headless](/help/journey-headless/architect/overview.md)

* [Percorso di traduzione dei contenuti AEM headless](/help/journey-headless/translation/overview.md)

* [Introduzione ad AEM come CMS headless](/help/sites-developing/headless/introduction.md)

* [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)

* [Tutorial per contenuti headless in AEM](https://experienceleague.adobe.com/it/docs/experience-manager-learn/getting-started-with-aem-headless/overview)
