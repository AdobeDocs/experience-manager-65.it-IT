---
title: Gestione delle campagne
seo-title: Campaign Management
description: La gestione delle campagne consente ai professionisti del marketing digitale di inviare contenuti personalizzati e creare esperienze mirate per i visitatori. Permette inoltre di orchestrare le campagne marketing per web, e-mail e dispositivi mobili, per meglio coinvolgere i visitatori.
seo-description: Campaign management provides digital marketers the opportunity to deliver personalized content and so create dedicated experiences for visitors. It allows you to orchestrate your marketing campaigns across the web, email and mobile services and so engage your visitors.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 94%

---

# Gestione delle campagne{#campaign-management}

La gestione delle campagne consente ai professionisti del marketing digitale di inviare contenuti personalizzati e creare esperienze mirate per i visitatori.

Permette inoltre di orchestrare le campagne marketing per web, e-mail e dispositivi mobili, per meglio coinvolgere i visitatori. Si possono creare i contenuti, suddividere i visitatori in diversi segmenti, inviare e promuovere contenuti destinati a specifici profili di utenti e gestire le campagne per più canali.

In questo documento vengono illustrati i vari elementi che compongono le campagne. Ulteriori informazioni sono disponibili nei seguenti documenti:

* [Teaser e strategie](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [E-mail marketing](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [Pagine di destinazione](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Offerte Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Utilizzo di Marketing Campaign Manager](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [Segmentazione](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [Impostazione della campagna](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

La gestione delle campagne consiste di vari elementi:

* **Marchi**
In AEM, i marchi sono l’unità di livello superiore e costituiscono una raccolta di 
**Campagne**.

* **Campagne**
Una campagna è una raccolta individuale 
**Esperienze**.

* **Esperienze**
Le esperienze sono composte di contenuti mirati, presentati al visitatore all’indirizzo 
**Punti di contatto**. Sono disponibili diversi tipi di esperienze:

   * **Teaser**
      [Le pagine o i paragrafi teaser](#teasers) vengono utilizzati per indirizzare alcuni **segmenti** di visitatori verso contenuti pertinenti in base ai loro interessi.

      Le pagine teaser possono:

      * presentare all’utente diverse opzioni;
      * mostrare un solo paragrafo teaser in base al segmento del visitatore in questione, ad esempio a seconda dell’età del visitatore;

      In genere, una pagina teaser è impostata come azione temporanea con una specifica durata di tempo, dopodiché viene sostituita da una successiva pagina teaser.

   * **Newsletter**

      [Le comunicazioni e-mail](#emailmarketing) sono utilizzate per coinvolgere gli utenti e incoraggiarli a visitare il sito e. In genere si tratta di newsletter che vengono inviate ai **Lead** (tipicamente raggruppati in **Elenchi**). **Nota:** Adobe non prevede ulteriori miglioramenti di questa funzionalità. Si consiglia di utilizzare [Adobe Campaign e l’integrazione con AEM](/help/sites-administering/campaign.md).

   * **Adobe Target**

       Consente l&#39;integrazione con Adobe Target (precedentemente Test&amp;Target), che offre agli addetti al marketing uno strumento di ottimizzazione del sito web di conversione, con le funzionalità necessarie per rendere continuamente i loro contenuti online e le offerte più rilevanti per i loro clienti, ottenendo una maggiore conversione. Adobe Target offre un’interfaccia intuitiva per la progettazione e l’esecuzione di test, la creazione di segmenti di pubblico e il targeting dei contenuti, il tutto in una singola applicazione.


* **Punti di contatto**

   Questi sono i punti di contatto tra il visitatore e la campagna. I punti di contatto sono associati alle esperienze create.

   Ad esempio, per i teaser si tratta della pagina di contenuto in cui si trova il paragrafo teaser, mentre per una newsletter si tratta della mailing list.

* **Lead**

   I lead si basano sulle informazioni raccolte sui visitatori e su come contattarli. **Nota:** Adobe non prevede ulteriori miglioramenti di questa funzionalità.

   Si consiglia di utilizzare [Adobe Campaign e l’integrazione con AEM](/help/sites-administering/campaign.md).

* **Elenchi**

   I lead sono in genere raggruppati in elenchi che possono essere usati per avviare azioni collettive su specifici gruppi. **Nota:** Adobe non prevede ulteriori miglioramenti di questa funzionalità.

   Si consiglia di utilizzare [Adobe Campaign e l’integrazione con AEM](/help/sites-administering/campaign.md).

* **Segmenti**

   I visitatori che arrivano a un sito hanno interessi e obiettivi diversi. La possibilità di effettuare analisi in base a fattori quali l’attività sul sito, le informazioni registrate nel profilo e l’attività su altri siti Web consente di definire diversi segmenti. Il contenuto può quindi essere mirato per le esigenze e gli interessi del visitatore, a seconda dei segmenti di corrispondenza.

* **MCM**

   La console Marketing Campaign Manager (MCM) consente di accedere a tutte le funzioni necessarie per creare e gestire le campagne, i marchi, le esperienze, i punti contatto, i lead, gli elenchi, i segmenti e i report.

   È possibile accedervi da diversi luoghi (con etichetta **Campagne**) oppure tramite l’URL:

   `http://localhost:4502/libs/mcm/content/admin.html`
