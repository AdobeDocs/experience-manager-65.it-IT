---
title: Esportatore JSON per Content Services
seo-title: Esportatore JSON per Content Services
description: AEM Content Services è progettato per rendere più generalizzata la descrizione e la distribuzione dei contenuti in/da AEM, oltre a concentrarsi sulle pagine Web. Forniscono contenuti ai canali che non sono pagine Web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente.
seo-description: AEM Content Services è progettato per rendere più generalizzata la descrizione e la distribuzione dei contenuti in/da AEM, oltre a concentrarsi sulle pagine Web. Forniscono contenuti ai canali che non sono pagine Web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Esportatore JSON per Content Services{#json-exporter-for-content-services}

AEM Content Services è progettato per rendere più generalizzata la descrizione e la distribuzione dei contenuti in/da AEM, oltre a concentrarsi sulle pagine Web.

Forniscono contenuti ai canali che non sono pagine Web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* Applicazioni a pagina singola
* Applicazioni mobili native
* altri canali e punti di contatto esterni ad AEM

Con frammenti di contenuto che utilizzano contenuto strutturato, potete fornire servizi di contenuto utilizzando JSON Export per distribuire il contenuto di una pagina AEM(y) nel formato modello dati JSON. Questo può essere utilizzato dalle vostre applicazioni.

>[!NOTE]
>
>La funzionalità descritta qui è disponibile per tutti i componenti core a partire dalla [release 1.1.0 dei componenti](https://docs.adobe.com/content/docs/en/core-components/v1.html)core.

## Esportatore JSON con componenti di base frammento di contenuto {#json-exporter-with-content-fragment-core-components}

Utilizzando AEM JSON Export è possibile distribuire il contenuto di una pagina AEM (y) nel formato del modello di dati JSON. Questo può essere utilizzato dalle vostre applicazioni.

In AEM la consegna viene ottenuta utilizzando il suffisso

`.model.json`

1. Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Fornirà contenuti quali:

   ![chlimage_1-192](assets/chlimage_1-192.png)

In alternativa, è possibile distribuire i contenuti di un frammento di contenuto strutturato specificandone il targeting.

Questo avviene utilizzando l&#39;intero percorso del frammento (tramite il `jcr:content`); ad esempio con un suffisso come

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

La pagina può contenere un singolo frammento di contenuto o più componenti di vari tipi. È inoltre possibile utilizzare meccanismi come i componenti elenco per cercare automaticamente contenuti rilevanti.

* Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* Fornirà contenuti quali:

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >È possibile [adattare i propri componenti](/help/sites-developing/json-exporter-components.md) per accedere e utilizzare questi dati.

### Ulteriori informazioni {#further-information}

Consulta anche:

* API HTTP Assets

   * [API HTTP Assets](/help/assets/mac-api-assets.md)

* Modelli Sling:

   * [Sling Models - Associazione di una classe di modelli a un tipo di risorsa dal 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM con JSON:

   * [Come ottenere informazioni sulla pagina in formato JSON](/help/sites-developing/pageinfo.md)

## Related Documentation {#related-documentation}

Per maggiori dettagli, consulta:

* Argomento Frammenti di [contenuto nella guida utente delle risorse](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelli per frammenti di contenuto](/help/assets/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-authoring/content-fragments.md)
* [Abilitazione dell&#39;esportazione JSON per un componente](/help/sites-developing/json-exporter-components.md)

* [Componenti](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) di base e componente Frammento di [contenuto](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

