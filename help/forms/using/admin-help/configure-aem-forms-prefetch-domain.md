---
title: Configurare i moduli AEM per preacquisire le informazioni sul dominio
description: Configura i moduli AEM per preacquisire le informazioni sul dominio se il tempo di risposta risulta più lento a causa di gruppi profondamente nidificati o se sei membro di molti gruppi.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Configurare i moduli AEM per preacquisire le informazioni sul dominio {#configure-aem-forms-to-prefetchdomain-information}

Gli utenti possono riscontrare un tempo di risposta più lento se appartengono a più gruppi (ad esempio, 500 o più) o se i gruppi sono nidificati in profondità (ad esempio, 30 livelli). Se si verifica questo problema, è possibile configurare i moduli AEM per preacquisire le informazioni da determinati domini.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione Utente > Configurazione > Importa Ed Esporta File Di Configurazione]**.
1. Per esportare l&#39;impostazione di configurazione corrente in un file, fare clic su **[!UICONTROL Esporta]** e salvare il file di configurazione in un&#39;altra posizione.
1. Aggiungi il seguente nodo (in grassetto):

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   In questo esempio, più domini sono configurati per la preacquisizione. I nomi di dominio sono separati da &quot;/&quot;. Questo è mostrato nell’esempio precedente con *Nome_dominio1*, *Nome_dominio2*, e *Nome_dominio3*.

1. Per importare il file aggiornato, in Gestione utente fai clic su **[!UICONTROL Configurazione > Importa Ed Esporta File Di Configurazione]**.
1. Clic **[!UICONTROL Sfoglia]** per trovare il file, fare clic su Importa e quindi su **[!UICONTROL OK]**.
