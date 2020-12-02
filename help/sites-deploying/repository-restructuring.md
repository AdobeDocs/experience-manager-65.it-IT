---
title: Ristrutturazione del repository nella AEM 6.5
seo-title: Ristrutturazione del repository nella AEM 6.5
description: Scopri le basi e le motivazioni alla base della ristrutturazione del repository in AEM 6.5
seo-description: Scopri le basi e le motivazioni alla base della ristrutturazione del repository in AEM 6.5
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
translation-type: tm+mt
source-git-commit: 97b2da315fac6f84fcba6d4464bf8dd1d690cfd1
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---


# Ristrutturazione del repository nella AEM 6.5{#repository-restructuring-in-aem}

## Introduzione {#introduction}

Prima del AEM 6.4, il codice cliente era implementato in aree imprevedibili del JCR soggette a modifiche agli aggiornamenti. Per questo motivo, nelle release formali AEM era comune sovrascrivere codice, configurazione o contenuto personalizzato. Inoltre, le modifiche apportate dai clienti talvolta hanno sovrascritto AEM codice prodotto o contenuto, rompendo le funzionalità del prodotto.

delineando chiaramente le gerarchie per AEM codice prodotto e codice cliente, questi conflitti possono essere evitati.

A tal fine, a partire dalla AEM 6.4 e per essere continuati nelle release future, il contenuto verrà ristrutturato da /etc ad altre cartelle della directory archivio, insieme alle linee guida sui contenuti da seguire, nel rispetto delle seguenti regole di alto livello:

* AEM codice prodotto sarà sempre inserito in /libs, che non deve essere sovrascritto dal codice personalizzato
* Il codice personalizzato deve essere inserito in /apps, /content e /conf

## Impatto sugli aggiornamenti 6.5 {#impact-on-upgrades}

Quando eseguite l&#39;aggiornamento a AEM 6.5, un ampio sottoinsieme di contenuti in /etc verrà duplicato in altre cartelle della directory archivio. Queste nuove posizioni sono le posizioni preferite alle quali viene fatto riferimento al contenuto. Tuttavia, è stato fatto ogni tentativo per rendere l&#39;aggiornamento AEM 6.5 compatibile con le posizioni precedenti nella cartella /etc. Nella maggior parte dei casi, il codice continuerà a fare riferimento alle posizioni precedenti fino a quando le modifiche non saranno state apportate attivamente, e in molti casi manualmente, nell&#39;applicazione del cliente. Dal punto di vista della timeline, vi sono due categorie di modifiche:

* Con l&#39;aggiornamento 6.5 - una manciata delle modifiche alla ristrutturazione /etc non sono compatibili con le versioni precedenti e quindi le modifiche dovrebbero essere pianificate e implementate come parte dell&#39;aggiornamento AEM 6.5.
* Prima dell&#39;aggiornamento futuro - la maggior parte delle modifiche /etc di ristrutturazione può essere posticipata fino a qualche tempo nel futuro post-aggiornamento. Come già detto, AEM codice 6.5 continuerà a fare riferimento alle posizioni precedenti fino a quando le modifiche non saranno implementate come parte di un rilascio del cliente. Sebbene non vi sia una tempistica forzata per la quale le modifiche dovrebbero essere apportate, si consiglia che vengano effettuate prima dell&#39;aggiornamento futuro, dal momento che le funzioni future potrebbero basarsi sulle nuove posizioni a cui si fa riferimento. Inoltre, la documentazione di una data funzione farà riferimento per convenzione alle nuove posizioni e potrebbe quindi confondere l&#39;utilizzo delle vecchie posizioni.

### Guida alla ristrutturazione {#restructuring-guidance}

Durante la pianificazione dell&#39;aggiornamento a AEM 6.5, è necessario fare riferimento alle seguenti pagine per soluzione al fine di valutare lo sforzo di lavoro:

* [Ristrutturazione del repository comune a tutte le soluzioni AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [ ristrutturazione del repository AEM Sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [ ristrutturazione del repository AEM Assets](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [ Ristrutturazione dell&#39;archivio di contenuti multimediali dinamici di AEM Assets](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [ ristrutturazione del repository AEM Forms](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [ ristrutturazione del repository AEM Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM del repository di Commerce](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Ogni pagina contiene due sezioni corrispondenti all’urgenza delle modifiche necessarie. Qualsiasi cosa nella sezione &quot;Con l&#39;aggiornamento 6.5&quot; dovrebbe essere affrontata come parte del progetto di aggiornamento AEM 6.5. Qualsiasi elemento in &quot;Prima dell&#39;aggiornamento futuro&quot; può essere eventualmente posticipato fino all&#39;aggiornamento successivo.

Ogni voce della pagina include un campo &quot;Guida alla ristrutturazione&quot;, che descrive la strategia tecnica consigliata per l&#39;allineamento con il nuovo modello di repository 6.5 in modo che le nuove posizioni siano indicate per i contenuti precedentemente presenti nella cartella /etc. Un ulteriore campo &quot;Note&quot; fornisce qualsiasi contesto utile aggiuntivo.
