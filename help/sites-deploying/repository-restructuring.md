---
title: Ristrutturazione dell’archivio in AEM 6.5
description: Scopri le nozioni di base e i motivi della ristrutturazione dell’archivio in AEM 6.5
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 835ee49e-9248-5578-a60a-15c097807178
    internal-label: Upgrading
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%
---
# Ristrutturazione dell’archivio in AEM 6.5{#repository-restructuring-in-aem}

## Introduzione {#introduction}

Prima di AEM 6.4, il codice del cliente veniva distribuito in aree imprevedibili del JCR soggette a modifiche al momento degli aggiornamenti. Per questo motivo, nelle versioni formali di AEM veniva spesso sovrascritto codice personalizzato, configurazione o contenuto. Inoltre, a volte le modifiche dei clienti sovrascrivono il codice o il contenuto del prodotto AEM, interrompendo le funzionalità del prodotto.

Delineando chiaramente le gerarchie per il codice prodotto AEM e il codice del cliente, è possibile evitare questi conflitti.

A tal fine, a partire da AEM 6.4 e per proseguire nelle versioni future, il contenuto viene ristrutturato da /etc ad altre cartelle nell’archivio, insieme a linee guida su quale contenuto viene distribuito, in conformità alle seguenti regole di alto livello:

* Il codice prodotto AEM verrà sempre inserito in /libs, che non deve essere sovrascritto dal codice personalizzato
* Il codice personalizzato deve essere inserito in /apps, /content e /conf

## Impatto sugli aggiornamenti 6.5 {#impact-on-upgrades}

Quando si esegue l’aggiornamento ad AEM 6.5, un sottoinsieme di grandi dimensioni di contenuti in /etc viene duplicato in altre cartelle nell’archivio. Queste nuove posizioni sono quelle preferite in cui viene fatto riferimento al contenuto. Tuttavia, è stato fatto ogni tentativo affinché l’aggiornamento a AEM 6.5 fosse compatibile con le versioni precedenti nelle posizioni precedenti della cartella /etc. Nella maggior parte dei casi, quindi, il codice AEM continuerà a fare riferimento alle posizioni precedenti fino a quando le modifiche non verranno apportate attivamente, e in molti casi manualmente, nell’applicazione di un cliente. Dal punto di vista della timeline, esistono due categorie di modifiche:

* Con l’aggiornamento 6.5: alcune delle modifiche di ristrutturazione /etc non sono compatibili con le versioni precedenti, pertanto le modifiche devono essere pianificate e implementate nell’ambito dell’aggiornamento ad AEM 6.5.
* Prima di un aggiornamento futuro, la maggior parte delle modifiche di ristrutturazione di /etc può essere rimandata fino a un certo momento nel futuro post-aggiornamento. Come indicato in precedenza, il codice AEM 6.5 continuerà a fare riferimento alle vecchie posizioni fino a quando le modifiche non verranno implementate come parte di una versione del cliente. Anche se non esiste una timeline forzata per cui devono essere apportate le modifiche, si consiglia di apportarle prima dell’aggiornamento futuro, poiché le funzioni future possono fare riferimento alle nuove posizioni. Inoltre, la documentazione di una determinata funzione farà riferimento per convenzione alle nuove posizioni e potrebbe quindi creare confusione se le vecchie posizioni vengono ancora utilizzate.

### Orientamenti sulla ristrutturazione {#restructuring-guidance}

Durante la pianificazione di un aggiornamento ad AEM 6.5, per valutare l’impegno di lavoro è necessario fare riferimento alle seguenti pagine per soluzione:

* [Ristrutturazione dell’archivio comune a tutte le soluzioni AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio AEM Sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio AEM Assets](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio Dynamic Media di AEM Assets](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio AEM Forms](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio AEM Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [Ristrutturazione dell’archivio AEM Commerce](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Ogni pagina contiene due sezioni corrispondenti all’urgenza delle modifiche necessarie. Tutto ciò che si trova nella sezione &quot;Aggiornamento con 6.5&quot; deve essere trattato come parte del progetto di aggiornamento ad AEM 6.5. Qualsiasi cosa in &quot;Prima di un aggiornamento futuro&quot; può essere facoltativamente differita fino a dopo l&#39;aggiornamento.

Ogni voce della pagina include un campo &quot;Linee guida per la ristrutturazione&quot;, che descrive la strategia tecnica consigliata per l’allineamento con il nuovo modello di archivio 6.5 in modo che alle nuove posizioni venga fatto riferimento per il contenuto che si trovava in precedenza nella cartella /etc. Un campo &quot;Note&quot; aggiuntivo fornisce un contesto utile aggiuntivo.
