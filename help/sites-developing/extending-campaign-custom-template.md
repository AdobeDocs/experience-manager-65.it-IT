---
title: Creazione di un modello di pagina AEM personalizzato con  componenti modulo Adobe Campaign
seo-title: Creazione di un modello di pagina AEM personalizzato con  componenti modulo Adobe Campaign
description: Creare un modello di pagina personalizzato che utilizzi  componenti Modulo Adobe Campaign
seo-description: Creare un modello di pagina personalizzato che utilizzi  componenti Modulo Adobe Campaign
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# Creazione di un modello di pagina AEM personalizzato con  componenti modulo Adobe Campaign{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

In questa pagina viene illustrato come creare un modello di pagina personalizzato che utilizza i componenti [ modulo Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md), esaminando le modalità di implementazione del modello Geometrixx-esterno ( `/apps/geometrixx-outdoors/components/page_campaign_profile`) e indicando informazioni importanti che potrebbero essere necessarie per la creazione di un modello personalizzato.

>[!NOTE]
>
>[Gli esempi di e-mail e di modulo sono disponibili solo in Geometrixx](/help/sites-developing/we-retail.md). Scaricate contenuti di Geometrixx di esempio da Package Share.

Per creare un modello di pagina AEM personalizzato utilizzando  componenti Modulo Adobe Campaign, accertarsi di disporre dei seguenti elementi:

1. **Right resourceSuperType**

   Assicurati che il componente pagina erediti da `mcm/campaign/components/profile`.

   Questo è richiesto per i servlet per ottenere e salvare informazioni

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **Impostazioni ClientContext**

   Se osservate le impostazioni contestuali del cliente ( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`), vengono visualizzate le seguenti impostazioni:

   * ClientContext punta a `/etc/clientcontext/campaign`
   * Esiste anche un nodo *config* aggiuntivo.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   In **head.jsp** sono visualizzate le seguenti righe che utilizzano il **clientcontext-config** e il **gancio-servizio-cloud**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   In **body.jsp**, i servizi cloud vengono caricati nella parte inferiore della pagina:

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Proprietà pagina campagna**

   Per poter selezionare un modello Adobe Campaign  le proprietà della pagina vengono estese con la scheda **Campaign**:

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **Impostazioni** del modello.

   Nel modello ( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`) vengono visualizzati i seguenti valori predefiniti:

   | **acMapping** | mapRecipient (per  Adobe Campaign 6.1), profilo (per  Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | mail |

   ![chlimage_1-204](assets/chlimage_1-204.png)

