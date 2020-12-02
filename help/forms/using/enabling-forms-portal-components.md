---
title: Abilitazione dei componenti del portale moduli
seo-title: Abilitazione dei componenti del portale moduli
description: I componenti di Forms Portal sono disattivati. Abilitare i gruppi Document Services e Document Services Predicates per abilitare i componenti di Forms Portal.
seo-description: I componenti di Forms Portal sono disattivati. Abilitare i gruppi Document Services e Document Services Predicates per abilitare i componenti di Forms Portal.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
translation-type: tm+mt
source-git-commit: a209b2dda04985a3f2d7c6838f11f0b5dc62d520
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Abilitazione dei componenti del portale moduli {#enabling-forms-portal-components}

I componenti del portale moduli non sono disponibili per l&#39;uso. Per visualizzare i componenti nell’elenco dei componenti disponibili AEM barra laterale, effettuate le seguenti operazioni:

1. Accedete all’istanza di creazione del sito Web e aprite una pagina AEM Sites .

1. Per le pagine che utilizzano un modello statico, effettuare le seguenti operazioni:

   1. Nell&#39;intestazione della pagina, toccate ![canvas-drop-down](assets/canvas-drop-down.png) > **Design** per aprire la pagina in modalità Progettazione.
   1. Toccate un componente (con un bordo blu), quindi toccate ![livello campo](assets/field-level.png) per selezionare il sistema di paragrafi contenente il componente corrente.
   1. Nel sistema di paragrafi, toccare ![settings_icon](assets/settings_icon.png) per aprire la finestra di dialogo Modifica per il sistema di paragrafi.
   1. Dall&#39;elenco **[!UICONTROL Componenti consentiti]**, abilitare le caselle di controllo per i componenti **[!UICONTROL Document Services]** e **[!UICONTROL Document Services Predicates]**. Toccate **[!UICONTROL OK]**.

1. Per le pagine che utilizzano un modello dinamico, effettuare le seguenti operazioni:

   1. Nell&#39;intestazione della pagina, toccare ![properties](assets/properties.png) > **Edit Template** (Modifica modello) per aprire il modello della pagina.
   1. Toccate **Contenitore di layout** e toccate ![FeedManagement](/help/forms/using/assets/feedmanagement.png). Nella scheda **Componenti consentiti**, abilitare le opzioni **Document Services and Document Services Predicates** e toccare ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Potete anche attivare componenti specifici di queste categorie selezionando i componenti. Per ulteriori informazioni sui componenti e sul loro utilizzo, vedere [Creazione di una pagina del portale dei moduli](/help/forms/using/creating-form-portal-page.md) e [Incorporazione di un componente collegamento in una pagina](/help/forms/using/embedding-link-component-page.md).

Ora, le categorie di componenti di Document Services e Document Services Predicates sono disponibili nel browser Componenti. I componenti sono abilitati per tutte le pagine che utilizzano lo stesso modello.

## Articoli correlati

* [Abilitare i componenti del portale moduli](/help/forms/using/enabling-forms-portal-components.md)
* [Pagina del portale moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare i moduli in una pagina Web utilizzando le API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzazione dell&#39;archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per l’integrazione del componente bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale moduli](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
