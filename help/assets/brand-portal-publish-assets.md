---
title: Pubblicare risorse in Brand Portal
description: Scopri come pubblicare e annullare la pubblicazione delle risorse in Brand Portal.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 41%

---

# Pubblicare risorse in Brand Portal {#publish-assets-to-brand-portal}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=it) |
| AEM 6.5 | Questo articolo |

In qualità di amministratore di Adobe Experience Manager (AEM) Assets, puoi pubblicare risorse e cartelle nell’istanza di AEM Assets Brand Portal (o pianificare il flusso di lavoro di pubblicazione in una data/ora successiva) per la tua organizzazione. Devi però prima configurare AEM Assets con Brand Portal. Per ulteriori dettagli, consulta [Configurare AEM Assets con Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Una volta completata la replica, puoi pubblicare risorse, cartelle e raccolte in Brand Portal. Per pubblicare le risorse in Brand Portal, effettua le seguenti operazioni:

>[!NOTE]
>
>Adobe consiglia di scaglionare la pubblicazione, eseguendola preferibilmente nelle ore non di picco, in modo che AEM Author non utilizzi troppe risorse.

1. Dalla console Assets, seleziona le risorse o la cartella da pubblicare e fai clic su **[!UICONTROL Pubblicazione rapida]** dalla barra degli strumenti.

   In alternativa, seleziona le risorse da pubblicare su Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Per pubblicare le risorse in Brand Portal, sono disponibili le due opzioni seguenti:
   * [Pubblicare immediatamente le risorse](#publish-to-bp-now)
   * [Pubblicare le risorse in un secondo momento](#publish-to-bp-now)

## Pubblicare subito le risorse {#publish-to-bp-now}

Per pubblicare le risorse selezionate su Brand Portal, effettua una delle seguenti operazioni:

* Dalla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**. Quindi dal menu, seleziona **[!UICONTROL Pubblica su Brand Portal]**.

* Dalla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**.

   1. Quindi dal **[!UICONTROL Azione]** seleziona **[!UICONTROL Pubblica su Brand Portal]**, e da **[!UICONTROL Pianificazione]** seleziona **[!UICONTROL Ora]**. Fai clic su **[!UICONTROL Avanti]**.

   2. Entro **[!UICONTROL Ambito]**, conferma la selezione e fai clic su **[!UICONTROL Pubblica su Brand Portal]**.

Viene visualizzato un messaggio per informare che le risorse sono state accodate per la pubblicazione su Brand Portal. Per visualizzare le risorse pubblicate, accedi all’interfaccia di Brand Portal.

## Pubblicare le risorse in un secondo momento {#publish-to-bp-later}

Per pianificare la pubblicazione delle risorse su Brand Portal in una data o un’ora successiva:

1. Dopo aver selezionato le risorse o le cartelle da pubblicare, seleziona **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti nella parte superiore.

1. On **[!UICONTROL Gestisci pubblicazione]** pagina, seleziona **[!UICONTROL Pubblica su Brand Portal]** da **[!UICONTROL Azione]** e seleziona **[!UICONTROL Più tardi]** da **[!UICONTROL Pianificazione]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Seleziona un valore per **[!UICONTROL Data di attivazione]** e specifica l’ora. Fai clic su **[!UICONTROL Avanti]**.

1. Seleziona un valore per **Data di attivazione** e specifica l’ora. Fai clic su **Avanti**.

1. Specifica un valore per **[!UICONTROL Titolo flusso di lavoro]** in **[!UICONTROL Flussi di lavoro]**. Fai clic su **[!UICONTROL Pubblica più tardi]**.

   ![publishworkflow](assets/publishworkflow.png)

Ora accedi a Brand Portal per verificare se le risorse pubblicate sono disponibili sull’interfaccia di Brand Portal.

![bp_landingpage](assets/bp_landingpage.png)
