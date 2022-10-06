---
title: Configurare AEM moduli per preacquisire informazioni sul dominio
seo-title: Configure AEM forms to prefetchdomain information
description: Configura i moduli AEM per preacquisire le informazioni sul dominio se si verifica un tempo di risposta più lento a causa di gruppi profondamente nidificati o se sei membro di molti gruppi.
seo-description: Configure AEM forms to prefetch domain information if you experience a slower response time due to deeply nested groups or if you are a member of many groups.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Configurare AEM moduli per preacquisire informazioni sul dominio {#configure-aem-forms-to-prefetchdomain-information}

Gli utenti possono riscontrare un tempo di risposta più lento se appartengono a molti gruppi (ad esempio, 500 o più) o se i gruppi sono profondamente nidificati (ad esempio, 30 livelli). Se si verifica questo problema, è possibile configurare AEM moduli per preacquisire informazioni da determinati domini.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Configurazione > Importa ed Esporta file di configurazione]**.
1. Per esportare l&#39;impostazione di configurazione corrente in un file, fai clic su **[!UICONTROL Esporta]** e salvare il file di configurazione in un altro percorso.
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

   In questo esempio, per la preacquisizione sono configurati più domini. I nomi di dominio sono separati da un &quot;/&quot;. Questo è mostrato nell’esempio precedente con *Nome_dominio1*, *Nome_dominio2* e *Domain_Name3*.

1. Per importare il file aggiornato, in Gestione utente fare clic su **[!UICONTROL Configurazione > Importa ed Esporta file di configurazione]**.
1. Fai clic su **[!UICONTROL Sfoglia]** per trovare il file, fare clic su Importa, quindi fare clic su **[!UICONTROL OK]**.
