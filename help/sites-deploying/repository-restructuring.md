---
title: Ristrutturazione repository in AEM 6.5
seo-title: Ristrutturazione repository in AEM 6.5
description: Informazioni sulle nozioni di base e sulle motivazioni alla base della ristrutturazione dell'archivio in AEM 6.5
seo-description: Informazioni sulle nozioni di base e sulle motivazioni alla base della ristrutturazione dell'archivio in AEM 6.5
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
translation-type: tm+mt
source-git-commit: 97b2da315fac6f84fcba6d4464bf8dd1d690cfd1

---


# Ristrutturazione repository in AEM 6.5{#repository-restructuring-in-aem}

## Introduzione {#introduction}

Prima di AEM 6.4, il codice cliente era implementato in aree del JCR imprevedibili soggette a modifiche agli aggiornamenti. Per questo motivo, nelle release formali di AEM era comune sovrascrivere codice, configurazione o contenuto personalizzati. Inoltre, a volte le modifiche apportate dai clienti hanno sovrascritto il codice o il contenuto del prodotto AEM, rompendo le funzionalità del prodotto.

delineando chiaramente le gerarchie per il codice prodotto AEM e il codice cliente, questi conflitti possono essere evitati.

A tal fine, a partire da AEM 6.4 e per essere continuati nelle release future, il contenuto verrà ristrutturato da /etc ad altre cartelle della directory archivio, insieme a linee guida sui contenuti da inserire, in conformità alle seguenti regole di alto livello:

* Il codice prodotto AEM verrà sempre inserito in /libs, che non deve essere sovrascritto dal codice personalizzato
* Il codice personalizzato deve essere inserito in /apps, /content e /conf

## Impatto sugli aggiornamenti 6.5 {#impact-on-upgrades}

Quando eseguite l’aggiornamento ad AEM 6.5, un ampio sottoinsieme di contenuti in /etc verrà duplicato in altre cartelle della directory archivio. Queste nuove posizioni sono le posizioni preferite alle quali viene fatto riferimento al contenuto. Tuttavia, è stato fatto ogni tentativo per far sì che l&#39;aggiornamento di AEM 6.5 sia compatibile con le versioni precedenti nella cartella /etc. Nella maggior parte dei casi, il codice AEM continuerà a fare riferimento alle posizioni precedenti fino a quando le modifiche non saranno state apportate attivamente, e in molti casi manualmente, nell&#39;applicazione del cliente. Dal punto di vista della timeline, vi sono due categorie di modifiche:

* Con l&#39;aggiornamento 6.5 - una manciata delle modifiche /etc non sono compatibili con le versioni precedenti, pertanto le modifiche dovrebbero essere pianificate e implementate nell&#39;ambito dell&#39;aggiornamento di AEM 6.5.
* Prima dell&#39;aggiornamento futuro - la maggior parte delle modifiche /etc di ristrutturazione può essere posticipata fino a qualche tempo nel futuro post-aggiornamento. Come già detto, il codice AEM 6.5 continuerà a fare riferimento alle posizioni precedenti fino a quando le modifiche non saranno implementate come parte di un rilascio del cliente. Sebbene non vi sia una tempistica forzata per la quale le modifiche dovrebbero essere apportate, si consiglia che vengano effettuate prima dell&#39;aggiornamento futuro, dal momento che le funzioni future potrebbero basarsi sulle nuove posizioni a cui si fa riferimento. Inoltre, la documentazione di una data funzione farà riferimento per convenzione alle nuove posizioni e potrebbe quindi confondere l&#39;utilizzo delle vecchie posizioni.

### Orientamenti sulla ristrutturazione {#restructuring-guidance}

Durante la pianificazione per l’aggiornamento ad AEM 6.5, per valutare il lavoro occorre fare riferimento alle seguenti pagine per soluzione:

* [Ristrutturazione del repository comune a tutte le soluzioni AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell&#39;archivio AEM Sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione archivio di AEM Assets](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione archivio Dynamic Media di AEM Assets](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell&#39;archivio di AEM Forms](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell&#39;archivio di AEM Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione archivio AEM Commerce](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Ogni pagina contiene due sezioni corrispondenti all’urgenza delle modifiche necessarie. Qualsiasi cosa presente nella sezione &quot;Con l&#39;aggiornamento 6.5&quot; dovrebbe essere trattata come parte del progetto di aggiornamento di AEM 6.5. Qualsiasi elemento in &quot;Prima dell&#39;aggiornamento futuro&quot; può essere eventualmente posticipato fino all&#39;aggiornamento successivo.

Ogni voce della pagina include un campo &quot;Guida alla ristrutturazione&quot;, che descrive la strategia tecnica consigliata per l&#39;allineamento con il nuovo modello di repository 6.5 in modo che le nuove posizioni siano indicate per i contenuti precedentemente presenti nella cartella /etc. Un ulteriore campo &quot;Note&quot; fornisce qualsiasi contesto utile aggiuntivo.
