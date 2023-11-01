---
title: Ristrutturazione dell’archivio in AEM 6.5
seo-title: Repository Restructuring in AEM 6.5
description: Scopri le nozioni di base e i motivi della ristrutturazione dell’archivio in AEM 6.5
seo-description: Learn about the basics and reasoning behind the repository restructuring in AEM 6.5
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Ristrutturazione dell’archivio in AEM 6.5{#repository-restructuring-in-aem}

## Introduzione {#introduction}

Prima di AEM 6.4, il codice del cliente veniva distribuito in aree imprevedibili del JCR soggette a modifiche durante gli aggiornamenti. Per questo motivo, nelle versioni formali dell’AEM veniva spesso sovrascritto codice, configurazione o contenuto personalizzati. Inoltre, i cambiamenti dei clienti a volte sovrascrivono il codice o il contenuto del prodotto AEM, interrompendo le funzionalità del prodotto.

Delineando chiaramente le gerarchie per codice prodotto AEM e codice cliente, questi conflitti possono essere evitati.

A tal fine, a partire dalla versione 6.4 dell’AEM e per proseguire nelle versioni future, i contenuti vengono ristrutturati da /etc ad altre cartelle nell’archivio, insieme a linee guida su quali contenuti vengono spostati, in conformità alle seguenti regole di alto livello:

* Il codice prodotto AEM verrà sempre inserito in /libs, che non deve essere sovrascritto dal codice personalizzato
* Il codice personalizzato deve essere inserito in /apps, /content e /conf

## Impatto sugli aggiornamenti 6.5 {#impact-on-upgrades}

Quando si esegue l’aggiornamento a AEM 6.5, un sottoinsieme di grandi dimensioni di contenuti in /etc viene duplicato in altre cartelle dell’archivio. Queste nuove posizioni sono quelle preferite in cui viene fatto riferimento al contenuto. Tuttavia, è stato fatto ogni tentativo affinché l’aggiornamento AEM 6.5 fosse compatibile con le versioni precedenti delle posizioni nella cartella /etc e così nella maggior parte dei casi le vecchie posizioni continueranno ad essere referenziate dal codice AEM fino a quando le modifiche non saranno attivamente, e in molti casi manualmente, effettuate nell’applicazione di un cliente. Dal punto di vista della timeline, esistono due categorie di modifiche:

* Con l’aggiornamento 6.5 - alcune delle modifiche di ristrutturazione /etc non sono compatibili con le versioni precedenti e pertanto le modifiche dovrebbero essere pianificate e implementate nell’ambito dell’aggiornamento AEM 6.5.
* Prima di un aggiornamento futuro, la maggior parte delle modifiche di ristrutturazione di /etc può essere rimandata fino a un certo momento nel futuro post-aggiornamento. Come accennato in precedenza, il codice AEM 6.5 continuerà a fare riferimento alle vecchie posizioni fino a quando le modifiche non saranno implementate come parte di una versione del cliente. Anche se non esiste una timeline forzata per cui devono essere apportate le modifiche, si consiglia di apportarle prima dell’aggiornamento futuro, poiché le funzioni future possono fare riferimento alle nuove posizioni. Inoltre, la documentazione di una determinata funzione farà riferimento per convenzione alle nuove posizioni e potrebbe quindi creare confusione se le vecchie posizioni vengono ancora utilizzate.

### Orientamenti sulla ristrutturazione {#restructuring-guidance}

Durante la pianificazione di un aggiornamento a AEM 6.5, per valutare l’impegno di lavoro è necessario fare riferimento alle seguenti pagine per soluzione:

* [Ristrutturazione dell’archivio comune a tutte le soluzioni AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio AEM Sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio AEM Assets](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio AEM Assets Dynamic Medie](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio AEM Forms](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio AEM Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio Commerce dell’AEM](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Ogni pagina contiene due sezioni corrispondenti all’urgenza delle modifiche necessarie. Tutto ciò che si trova nella sezione &quot;Aggiornamento 6.5&quot; deve essere trattato come parte del progetto di aggiornamento AEM 6.5. Qualsiasi cosa in &quot;Prima di un aggiornamento futuro&quot; può essere facoltativamente differita fino a dopo l&#39;aggiornamento.

Ogni voce della pagina include un campo &quot;Linee guida per la ristrutturazione&quot;, che descrive la strategia tecnica consigliata per l’allineamento con il nuovo modello di archivio 6.5 in modo che alle nuove posizioni venga fatto riferimento per il contenuto che si trovava in precedenza nella cartella /etc. Un campo &quot;Note&quot; aggiuntivo fornisce un contesto utile aggiuntivo.
