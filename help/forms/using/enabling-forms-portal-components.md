---
title: Abilitazione dei componenti del portale Forms
description: I componenti del portale Forms sono già disattivati. Abilitare i gruppi di predicati Document Services e Document Services per abilitare i componenti di Forms Portal.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 5%

---

# Abilitazione dei componenti del portale Forms {#enabling-forms-portal-components}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html?lang=it) |
| AEM 6.5 | Questo articolo |

I componenti del portale dei moduli non sono pronti all’uso. Per visualizzare i componenti nell’elenco dei componenti disponibili nella barra laterale AEM, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring del sito web e apri una pagina AEM Sites.

1. Per le pagine che utilizzano un modello statico, effettua le seguenti operazioni:

   1. Nell&#39;intestazione della pagina, selezionare ![canvas-drop-down](assets/canvas-drop-down.png) > **Design** per aprire la pagina in modalità Progettazione.
   1. Seleziona un componente (con bordo blu), quindi seleziona ![a livello di campo](assets/field-level.png) per selezionare il sistema paragrafo contenente il componente corrente.
   1. Nel sistema paragrafo, selezionare ![settings_icon](assets/settings_icon.png) per aprire la finestra di dialogo Modifica per il sistema paragrafo.
   1. Dall&#39;elenco di **[!UICONTROL Componenti consentiti]**, abilitare le caselle di controllo per i componenti **[!UICONTROL Servizi basati su documenti]** e **[!UICONTROL Predicati di servizi basati su documenti]**. Selezionare **[!UICONTROL OK]**.

1. Per le pagine che utilizzano un modello dinamico, effettua le seguenti operazioni:

   1. Nell&#39;intestazione della pagina, selezionare ![proprietà](assets/properties.png) > **Modifica modello** per aprire il modello della pagina.
   1. Selezionare **Contenitore layout** e ![Gestione feed](/help/forms/using/assets/feedmanagement.png). Nella scheda **Componenti consentiti**, abilita le opzioni **Servizi basati su documenti e Predicati di servizi basati su documenti** e seleziona ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Puoi anche abilitare componenti specifici da queste categorie selezionando i componenti. Per ulteriori informazioni sui componenti e sul loro utilizzo, vedere [Creazione di una pagina del portale dei moduli](/help/forms/using/creating-form-portal-page.md) e [Incorporamento di un componente di collegamento in una pagina](/help/forms/using/embedding-link-component-page.md).

Ora le categorie di componenti Servizi basati su documenti e Predicati di servizi basati su documenti sono disponibili nel browser Componenti. I componenti sono abilitati per tutte le pagine che utilizzano lo stesso modello.

## Articoli correlati

* [Abilitare i componenti del portale Forms](/help/forms/using/enabling-forms-portal-components.md)
* [Crea pagina portale moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare moduli su una pagina web utilizzando API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utilizzare il componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzare l’archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per integrare il componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale Forms](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
