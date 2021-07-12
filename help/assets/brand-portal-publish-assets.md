---
title: Pubblicare risorse su Brand Portal
seo-title: Pubblicare risorse su Brand Portal
description: Scopri come pubblicare e annullare la pubblicazione delle risorse in Brand Portal.
seo-description: Scopri come pubblicare e annullare la pubblicazione delle risorse in Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: User
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 44%

---

# Pubblicare risorse su Brand Portal {#publish-assets-to-brand-portal}

In qualità di amministratore di Adobe Experience Manager (AEM) Assets, puoi pubblicare risorse e cartelle nell’istanza AEM Assets Brand Portal (o pianificare il flusso di lavoro di pubblicazione in una data/ora successiva) per la tua organizzazione. Devi però prima configurare AEM Assets con Brand Portal. Per ulteriori dettagli, consulta [Configurare AEM Assets con Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Una volta completata la replica, puoi pubblicare risorse, cartelle e raccolte in Brand Portal. Per pubblicare le risorse in Brand Portal, effettua le seguenti operazioni:

>[!NOTE]
>
>Adobe consiglia di scaglionare la pubblicazione, eseguendola preferibilmente nelle ore non di picco, in modo che AEM Author non utilizzi troppe risorse.

1. Dalla console di Assets, seleziona le risorse o la cartella da pubblicare e fai clic su **[!UICONTROL Pubblicazione rapida]** nella barra degli strumenti.

   In alternativa, seleziona le risorse da pubblicare in Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Per pubblicare le risorse in Brand Portal, sono disponibili le due opzioni seguenti:
   * [Pubblicare immediatamente le risorse](#publish-to-bp-now)
   * [Pubblicare le risorse in un secondo momento](#publish-to-bp-now)

## Pubblicare subito le risorse {#publish-to-bp-now}

Per pubblicare le risorse selezionate su Brand Portal, effettua una delle seguenti operazioni:

* Dalla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**. Dal menu, seleziona **[!UICONTROL Pubblica in Brand Portal]**.

* Dalla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**.

   1. Quindi, da **[!UICONTROL Azione]** seleziona **[!UICONTROL Pubblica in Brand Portal]**, e da **[!UICONTROL Pianificazione]** seleziona **[!UICONTROL Ora]**. Fai clic su **[!UICONTROL Avanti]**.

   2. In **[!UICONTROL Ambito]**, conferma la selezione e fai clic su **[!UICONTROL Pubblica in Brand Portal]**.

Viene visualizzato un messaggio per informare che le risorse sono state accodate per la pubblicazione su Brand Portal. Per visualizzare le risorse pubblicate, accedi all’interfaccia di Brand Portal.

## Pubblicare le risorse in un secondo momento {#publish-to-bp-later}

Per pianificare la pubblicazione delle risorse su Brand Portal in una data o un’ora successiva:

1. Dopo aver selezionato le risorse o le cartelle da pubblicare, seleziona **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti in alto.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione]**, seleziona **[!UICONTROL Pubblica in Brand Portal]** da **[!UICONTROL Azione]** e seleziona **[!UICONTROL Più tardi]** da **[!UICONTROL Pianificazione]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Seleziona un valore per **[!UICONTROL Data di attivazione]** e specifica l’ora. Fai clic su **[!UICONTROL Avanti]**.

1. Seleziona un valore per **Data di attivazione** e specifica l’ora. Fai clic su **Avanti**.

1. Specifica un valore per **[!UICONTROL Titolo flusso di lavoro]** in **[!UICONTROL Flussi di lavoro]**. Fai clic su **[!UICONTROL Pubblica più tardi]**.

   ![publishworkflow](assets/publishworkflow.png)

Ora accedi a Brand Portal per verificare se le risorse pubblicate sono disponibili nell’interfaccia Brand Portal.

![bp_landing_page](assets/bp_landing_page.png)
