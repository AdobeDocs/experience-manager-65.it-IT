---
title: Configurare i moduli AEM per le informazioni di preacquisizione del dominio
seo-title: Configurare i moduli AEM per le informazioni di preacquisizione del dominio
description: Configurate i moduli AEM per la preacquisizione delle informazioni sul dominio in caso di tempi di risposta più lenti a causa di gruppi nidificati o di membri di molti gruppi.
seo-description: Configurate i moduli AEM per la preacquisizione delle informazioni sul dominio in caso di tempi di risposta più lenti a causa di gruppi nidificati o di membri di molti gruppi.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Configurare i moduli AEM per le informazioni di preacquisizione del dominio {#configure-aem-forms-to-prefetchdomain-information}

Gli utenti potrebbero riscontrare un tempo di risposta più lento se appartengono a molti gruppi (ad esempio, 500 o più) o se i gruppi sono nidificati in profondità (ad esempio, 30 livelli). In caso di problemi, puoi configurare i moduli AEM per preacquisire informazioni da alcuni domini.

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Configurazione > Importa ed esporta file]** di configurazione.
1. Per esportare l’impostazione di configurazione corrente in un file, fate clic su **[!UICONTROL Esporta]** e salvate il file di configurazione in un’altra posizione.
1. Aggiungete il seguente nodo (in grassetto):

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

   In questo esempio, più domini sono configurati per la preacquisizione. I nomi di dominio sono separati da &quot;/&quot;. Questo è illustrato nell&#39;esempio precedente con *Domain_Name1*, *Domain_Name2* e *Domain_Name3*.

1. Per importare il file aggiornato, in Gestione utente fate clic su **[!UICONTROL Configurazione > Importa ed esporta file]** di configurazione.
1. Fate clic su **[!UICONTROL Sfoglia]** per trovare il file, fate clic su Importa, quindi su **[!UICONTROL OK]**.

