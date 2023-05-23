---
title: Integrazione di AEM e Commerce di terze parti tramite Commerce Integration Framework
description: Le aziende possono richiedere soluzioni commerce di terze parti aggiuntive per potenziare la propria vetrina. Commerce Integration Framework (CIF) può essere utilizzato in tali scenari di integrazione per collegare una soluzione commerce di terze parti ad Adobe Experience Manager utilizzando I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: e99899a4-df86-4108-991a-8b30d303a279
source-git-commit: 885d0763fca9ad4eab499081adca9b83875b27e1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 3%

---

# Integrazione AEM e Commerce di terze parti tramite Commerce Integration Framework {#aem-third-party}

L’integrazione di una soluzione non Adobe Commerce è uno scenario comune per CIF. soluzioni di terze parti con API e schemi diversi vengono connesse tramite un livello di integrazione.

## Architettura {#architecture}

L’architettura generale è la seguente:

![Panoramica dell’architettura AEM per Magenti e terze parti](../assets//AEM_nonMagento_Architecture.png)

Questo livello di integrazione ha lo scopo di mappare API e schemi di terze parti rispetto alle API e agli schemi di Adobe Commerce GraphQL supportati al di fuori dell’Experience Manager. Grazie a questa incapsulazione, la logica di integrazione e i sistemi possono essere aggiornati senza modificare il codice all’interno dell’Experience Manager.

## Requisiti della soluzione per un&#39;integrazione

Quando l’Experience Manager recupera i dati on-demand, sono necessarie API in tempo reale per il catalogo dei prodotti.

>[!TIP]
>
>Se non sono disponibili API in tempo reale, per l’integrazione deve essere utilizzata una cache di prodotto esterna con API. Esempio [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

Non è necessario implementare lo schema GraphQL completo, ma solo gli oggetti dello schema per abilitare i casi d’uso desiderati.

## Casi d’uso back-end

CIF estende l’Experience Manager con strumenti di gestione dell’esperienza di prodotto e accesso al catalogo dei prodotti in tempo reale. Questa integrazione diretta consente agli autori di accedere ai dati di e-commerce utilizzando interfacce utente incorporate quando necessario senza uscire dal contesto dei contenuti.

Per sbloccare questi casi d’uso è necessaria l’integrazione delle API del catalogo dei prodotti.

## Casi d’uso front-end

[Componenti core CIF dell’AEM](https://github.com/adobe/aem-core-cif-components) recupera e scambia dati tramite le API Adobe Commerce supportate da CIF. Per riutilizzare i componenti, è necessario implementare le rispettive API.

Per i componenti lato client critici in termini di prestazioni, si consiglia di comunicare direttamente con la soluzione di terze parti per evitare la latenza.

## Sviluppo di un’integrazione {#develop-integration}

È consigliabile utilizzare [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) per il livello di integrazione. È incluso nel componente aggiuntivo CIF per terzi. Poiché funziona con un approccio simile a quello dei microservizi, è adatto per integrare facilmente più soluzioni.

Il [implementazione di riferimento](https://github.com/adobe/commerce-cif-graphql-integration-reference) è un ottimo punto di partenza per creare l’integrazione con la soluzione commerce. Sebbene supporti GraphQL, può anche essere integrato con qualsiasi altro tipo di API, come REST.

Questo livello di integrazione non è necessario se è disponibile un livello di terze parti (ad esempio Mulesoft) o se l’integrazione viene creata sopra la soluzione di terze parti.

## Connettori predefiniti {#connectors}

I connettori rappresentano un buon punto di partenza per i progetti. Sono forniti con una connessione specifica della soluzione Commerce e una mappatura API predefinita. Questi connettori sono costruiti da terze parti e non sono gestiti da Adobe. Per ulteriori informazioni, contattare il partner.

* [Commerce SAP](https://github.com/diconium/commerce-cif-graphql-integration-hybris), realizzata da Diconium
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool), realizzata da Diconium

>[!TIP]
>
>Anche se i connettori aiutano i progetti ad accelerare l’integrazione con Commerce, non sono plug-in-play. Le soluzioni Enterprise Commerce sono in genere altamente personalizzate e richiedono un’integrazione personalizzata. È necessaria una buona conoscenza della piattaforma commerce, degli schemi GraphQL di Adobe Commerce e di Adobe I/O Runtime.
