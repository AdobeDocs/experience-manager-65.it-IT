---
title: Abilitazione dei componenti del portale Forms
seo-title: Enabling forms portal components
description: I componenti del portale Forms sono già disattivati. Abilitare i gruppi di predicati Document Services e Document Services per abilitare i componenti di Forms Portal.
seo-description: Out of the box, Forms Portal components are disabled. Enable Document Services and Document Services Predicates groups to enable Forms Portal components.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Abilitazione dei componenti del portale Forms {#enabling-forms-portal-components}

I componenti del portale dei moduli non sono pronti all’uso. Per visualizzare i componenti nell’elenco dei componenti disponibili nella barra laterale AEM, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring del sito web e apri una pagina AEM Sites.

1. Per le pagine che utilizzano un modello statico, effettua le seguenti operazioni:

   1. Nell’intestazione della pagina, tocca ![elenco a discesa area di lavoro](assets/canvas-drop-down.png) > **Progettazione** per aprire la pagina in modalità Progettazione.
   1. Tocca un componente (con un bordo blu), quindi tocca ![a livello di campo](assets/field-level.png) per selezionare il sistema paragrafo contenente il componente corrente.
   1. Nel sistema paragrafo, tocca ![icona_impostazioni](assets/settings_icon.png) per aprire la finestra di dialogo Modifica per il sistema paragrafo.
   1. Dall’elenco di **[!UICONTROL Componenti consentiti]**, abilita le caselle di controllo per **[!UICONTROL Document Services]** e **[!UICONTROL Predicati Document Services]** componenti. Tocca **[!UICONTROL OK]**.

1. Per le pagine che utilizzano un modello dinamico, effettua le seguenti operazioni:

   1. Nell’intestazione della pagina, tocca ![proprietà](assets/properties.png) > **Modifica modello** per aprire il modello della pagina.
   1. Tocca **Contenitore di layout** e tocca ![Gestione feed](/help/forms/using/assets/feedmanagement.png). In **Componenti consentiti** , abilita **Servizi documentali e predicati servizi documentali** opzioni e tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Puoi anche abilitare componenti specifici da queste categorie selezionando i componenti. Per ulteriori informazioni sui componenti e sul loro utilizzo, consulta [Creazione di una pagina del portale dei moduli](/help/forms/using/creating-form-portal-page.md) e [Incorporazione di un componente collegamento in una pagina](/help/forms/using/embedding-link-component-page.md).

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
