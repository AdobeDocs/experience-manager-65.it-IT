---
title: Esportatore JSON per Content Services
seo-title: Esportatore JSON per Content Services
description: AEM Content Services è progettato per rendere più generalizzata la descrizione e la distribuzione dei contenuti in/da AEM oltre l'attenzione sulle pagine Web. Forniscono contenuti a canali che non sono pagine Web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente.
seo-description: AEM Content Services è progettato per rendere più generalizzata la descrizione e la distribuzione dei contenuti in/da AEM oltre l'attenzione sulle pagine Web. Forniscono contenuti a canali che non sono pagine Web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 4%

---


# Esportatore JSON per Content Services{#json-exporter-for-content-services}

AEM Content Services è progettato per rendere più generalizzata la descrizione e la distribuzione dei contenuti in/da AEM oltre l&#39;attenzione sulle pagine Web.

Forniscono contenuti a canali che non sono pagine Web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* [Applicazioni a pagina singola](spa-walkthrough.md)
* Applicazioni mobili native
* altri canali e punti di contatto esterni a AEM

Con frammenti di contenuto che utilizzano contenuto strutturato, puoi fornire servizi di contenuto utilizzando JSON Export per distribuire il contenuto di una pagina AEM (y) nel formato modello dati JSON. Questo può essere utilizzato dalle vostre applicazioni.

>[!NOTE]
>
>La funzionalità descritta qui è disponibile per tutti i componenti core a partire dalla [release 1.1.0 dei componenti core](https://docs.adobe.com/content/docs/en/core-components/v1.html).

## Esportatore JSON con componenti di base frammento di contenuto {#json-exporter-with-content-fragment-core-components}

Utilizzando il modulo di esportazione JSON AEM potete distribuire il contenuto di una pagina AEM (y) nel formato del modello di dati JSON. Questo può essere utilizzato dalle vostre applicazioni.

All&#39;interno AEM la consegna viene ottenuta utilizzando il selettore `model` e l&#39;estensione `.json`.

`.model.json`

1. Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Fornirà contenuti quali:

   ![chlimage_1-192](assets/chlimage_1-192.png)

In alternativa, è possibile distribuire i contenuti di un frammento di contenuto strutturato specificandone il targeting.

Tale operazione viene eseguita utilizzando l&#39;intero percorso del frammento (tramite `jcr:content`); ad esempio con un suffisso come

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

La pagina può contenere un singolo frammento di contenuto o più componenti di vari tipi. È inoltre possibile utilizzare meccanismi come i componenti elenco per cercare automaticamente i contenuti rilevanti.

* Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* Fornirà contenuti quali:

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >È possibile [adattare i propri componenti](/help/sites-developing/json-exporter-components.md) per accedere e utilizzare questi dati.

   >[!NOTE]
   >
   >Sebbene non sia un&#39;implementazione standard, [sono supportati più selettori,](json-exporter-components.md#multiple-selectors) ma `model` deve essere il primo.

### Ulteriori informazioni {#further-information}

Consulta anche:

* API HTTP di Assets

   * [API HTTP di Assets](/help/assets/mac-api-assets.md)

* Modelli Sling:

   * [Sling Models - Associazione di una classe di modelli a un tipo di risorsa dal 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM con JSON:

   * [Ottenimento di informazioni sulla pagina in formato JSON](/help/sites-developing/pageinfo.md)

## Documentazione correlata {#related-documentation}

Per maggiori dettagli, consulta:

* Argomento [Frammenti di contenuto nella guida utente di Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-authoring/content-fragments.md)
* [Abilitazione dell&#39;esportazione JSON per un componente](/help/sites-developing/json-exporter-components.md)

* [Componenti ](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) di base e componente Frammento di  [contenuto](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

