---
title: Pubblicare raccolte su Brand Portal
seo-title: Pubblicare raccolte su Brand Portal
description: Scoprite come pubblicare e annullare la pubblicazione delle raccolte in Brand Portal.
seo-description: Scoprite come pubblicare e annullare la pubblicazione delle raccolte in Brand Portal.
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
translation-type: tm+mt
source-git-commit: 9f923782d3d0a7bdf45b18e8025bd2d083acf77c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 36%

---


# Pubblicare raccolte su Brand Portal {#publish-collections-to-brand-portal}

Come amministratore di Adobe Experience Manager (AEM) Assets, potete pubblicare le raccolte nell&#39;istanza  AEM Assets Brand Portal per la vostra organizzazione. Tuttavia, è prima necessario integrare  AEM Assets con il Portale marchio. Per ulteriori dettagli, consulta [Configurare AEM Assets con Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Se apportate modifiche successive alla raccolta originale in  AEM Assets, le modifiche non vengono applicate al portale marchio finché non pubblicate nuovamente la raccolta. Questa caratteristica garantisce che le modifiche in corso di lavoro non siano disponibili in Brand Portal. Solo le modifiche approvate pubblicate da un amministratore sono infatti disponibili in Brand Portal.

>[!NOTE]
>
>I frammenti di contenuto non possono essere pubblicati su Brand Portal. Pertanto, se selezionate frammenti di contenuto in AEM Author, l&#39;azione **Pubblica su Brand Portal** non è disponibile.
>
>Se le raccolte contenenti frammenti di contenuto vengono pubblicate da AEM Author a Brand Portal, tutto il contenuto della cartella tranne i frammenti di contenuto viene replicato nell&#39;interfaccia Brand Portal.

## Pubblicare una raccolta in Brand Portal {#publish-a-collection-to-brand-portal}

1. Nell’interfaccia utente di AEM Assets, fai clic sul logo AEM.
1. Dalla pagina **Navigazione**, passa a **Risorse > Raccolte**.
1. Dalla console Raccolte, selezionate la raccolta che desiderate pubblicare nel portale dei marchi.

   ![select_collection](assets/select_collection.png)

1. Dalla barra degli strumenti, fai clic su **Pubblica su Brand Portal**.
1. Nella finestra di dialogo di conferma, fai clic su **Pubblica**.
1. Chiudi il messaggio di conferma.
1. Accedete a Brand Portal come amministratore. La raccolta pubblicata è disponibile nella console Raccolte.

   ![raccolta pubblicata](assets/published_collection.png)

## Annullare la pubblicazione delle raccolte {#unpublish-collections}

Potete annullare la pubblicazione delle raccolte pubblicate da  AEM Assets al Brand Portal. Dopo aver annullato la pubblicazione della raccolta originale, la relativa copia non è più disponibile per gli utenti di Brand Portal.

1. Dalla console Raccolte dell&#39;istanza di AEM Assets  e selezionate la raccolta da annullare la pubblicazione.

   ![select_collection-1](assets/select_collection-1.png)

1. Dalla barra degli strumenti, fai clic sull’icona **Rimuovi da Brand Portal**.
1. Nella finestra di dialogo, fai clic su **Annulla pubblicazione**.
1. Chiudi il messaggio di conferma. La raccolta viene rimossa dall’interfaccia di Brand Portal.

