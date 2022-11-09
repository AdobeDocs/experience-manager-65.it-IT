---
title: Esportatore JSON per Content Services
seo-title: JSON Exporter for Content Services
description: AEM Content Services è progettato per generalizzare la descrizione e la consegna dei contenuti in/da AEM, non limitandosi alle pagine web. Fornisce contenuti a canali diversi dalle tradizionali pagine web di AEM, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente.
seo-description: AEM Content Services are designed to generalize the description and delivery of content in/from AEM beyond a focus on web pages. They provide the delivery of content to channels that are not traditional AEM web pages, using standardized methods that can be consumed by any client.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 34%

---

# Esportatore JSON per Content Services{#json-exporter-for-content-services}

AEM Content Services è progettato per generalizzare la descrizione e la consegna dei contenuti in/da AEM, non limitandosi alle pagine web.

Fornisce contenuti a canali diversi dalle tradizionali pagine web di AEM, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* [Applicazioni a pagina singola](spa-walkthrough.md)
* Applicazioni mobile native
* Altri canali e punti di contatto esterni ad AEM

Con i frammenti di contenuto che utilizzano contenuti strutturati, puoi fornire servizi di contenuto utilizzando l’esportatore JSON per distribuire il contenuto di una pagina (y) AEM in formato modello dati JSON. Questo può quindi essere utilizzato dalle tue applicazioni.

>[!NOTE]
>
>La funzionalità descritta di seguito è disponibile per tutti i componenti core dal momento che [versione 1.1.0 dei componenti core](https://docs.adobe.com/content/docs/en/core-components/v1.html).

## Esportazione JSON con componenti core per frammenti di contenuto {#json-exporter-with-content-fragment-core-components}

Utilizzando la funzione di esportazione JSON AEM puoi fornire il contenuto di una pagina (y) AEM nel formato del modello di dati JSON. Questo può quindi essere utilizzato dalle tue applicazioni.

All’interno AEM la consegna viene ottenuta utilizzando il selettore `model` e `.json` estensione.

`.model.json`

1. Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Fornirà contenuti quali:

   ![chlimage_1-192](assets/chlimage_1-192.png)

In alternativa, puoi distribuire il contenuto di un frammento di contenuto strutturato specificandone il targeting.

Questa operazione viene eseguita utilizzando l’intero percorso del frammento (tramite il `jcr:content`); ad esempio con un suffisso come .

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

La pagina può contenere un singolo frammento di contenuto o più componenti di vari tipi. È inoltre possibile utilizzare meccanismi quali i componenti elenco per cercare automaticamente i contenuti rilevanti.

* Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* Fornirà contenuti quali:

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >È possibile [adattare i propri componenti](/help/sites-developing/json-exporter-components.md) per accedere e utilizzare tali dati.

   >[!NOTE]
   >
   >Sebbene non sia un’implementazione standard, [sono supportati più selettori,](json-exporter-components.md#multiple-selectors) ma `model` deve essere il primo.

### Ulteriori informazioni {#further-information}

Consulta anche:

* API HTTP di Assets

   * [API HTTP di Assets](/help/assets/mac-api-assets.md)

* Modelli Sling:

   * [Sling Models - Associazione di una classe di modello a un tipo di risorsa a partire dal 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM con JSON:

   * [Ottenimento di informazioni di pagina in formato JSON](/help/sites-developing/pageinfo.md)

## Documentazione correlata {#related-documentation}

Per maggiori dettagli vedi:

* La [Argomento Frammenti di contenuto nella guida utente di Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-authoring/content-fragments.md)
* [Abilitazione dell’esportazione JSON per un componente](/help/sites-developing/json-exporter-components.md)

* [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [Componente Frammento di contenuto](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
