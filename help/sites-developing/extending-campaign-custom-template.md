---
title: Creazione di un modello di pagina AEM personalizzato con i componenti di Adobe Campaign Form
description: Creare un modello di pagina personalizzato che utilizza i componenti di Adobe Campaign Form
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: ad8f849384e58511de97611d1b26c4fc96022062
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 2%

---

# Creazione di un modello di pagina AEM personalizzato con i componenti di Adobe Campaign Form{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

Questa pagina spiega come creare un modello di pagina personalizzato che utilizza [Adobe Campaign Form](/help/sites-authoring/adobe-campaign-components.md) componenti esaminando il modello Geometrixx-esterni (`/apps/geometrixx-outdoors/components/page_campaign_profile`) viene implementato e indica le informazioni importanti necessarie per la creazione di un modello personalizzato.

>[!NOTE]
>
>[Le e-mail e gli esempi di moduli sono disponibili solo in Geometrixx](/help/sites-developing/we-retail.md). Scarica il contenuto di esempio di un Geometrixx da Condivisione pacchetti.

>[!CAUTION]
>
>I componenti e-mail dell’AEM sono stati dichiarati obsoleti. A causa della natura dell’e-mail, che unisce contenuti e stile, i componenti e-mail forniti come predefiniti dall’AEM vengono riutilizzati in modo limitato per i clienti, a causa della necessità di implementare stili personalizzati in tutti i componenti necessari per i progetti.
>
>I componenti e-mail possono essere implementati a livello di progetto, e i componenti e-mail AEM obsoleti illustrano come ciò possa essere ottenuto. Tuttavia, non utilizzare questi componenti obsoleti nei progetti.


Per creare un modello di pagina AEM personalizzato utilizzando i componenti di Adobe Campaign Form, è necessario disporre dei seguenti elementi:

1. **Risorsa corretta SuperType**

   Assicurati che il componente pagina erediti da `mcm/campaign/components/profile`.

   Questo è necessario affinché i servlet possano ottenere e salvare le informazioni

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **Impostazioni ClientContext**

   Quando si esaminano le impostazioni clientcontext ( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`) vengono visualizzate le seguenti impostazioni:

   * Il ClientContext punta a `/etc/clientcontext/campaign`
   * È inoltre disponibile un *config* nodo.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   In entrata **head.jsp**, vengono visualizzate le righe seguenti che utilizzano **clientcontext-config** e **cloudservice-hook**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   In entrata **body.jsp**, i servizi cloud vengono caricati nella parte inferiore della pagina:

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Proprietà pagina della campagna**

   Per poter selezionare un modello Adobe Campaign, le proprietà di pagina vengono estese con **Campagna** scheda:

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **Impostazioni modello**.

   Nel modello ( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`) vengono visualizzati i seguenti valori predefiniti:

   | **acMapping** | mapRecipient (per Adobe Campaign 6.1), profile (per Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | mail |

   ![chlimage_1-204](assets/chlimage_1-204.png)
