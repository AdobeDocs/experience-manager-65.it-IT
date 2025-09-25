---
title: Configurare AEM Forms per precaricare le informazioni sul dominio
description: Configura AEM Forms per precaricare le informazioni sul dominio se il tempo di risposta risulta più lento a causa di gruppi profondamente nidificati o se sei membro di molti gruppi.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '192'
ht-degree: 100%

---

# Configurare AEM Forms per precaricare le informazioni sul dominio {#configure-aem-forms-to-prefetchdomain-information}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Gli utenti possono riscontrare un tempo di risposta più lento se appartengono a più gruppi (ad esempio, 500 o più) o se i gruppi sono profondamente nidificati (ad esempio, 30 livelli). Se si verifica questo problema, puoi configurare AEM Forms per la preacquisizione delle informazioni da determinati domini.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utenti > Configurazione > Importa ed esporta file di configurazione]**.
1. Per esportare l’impostazione di configurazione corrente in un file, fai clic su **[!UICONTROL Esporta]** e salva il file di configurazione in un altro percorso.
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

   In questo esempio, più domini sono configurati per la preacquisizione. I nomi dominio sono separati da “/”. Ciò è illustrato nell’esempio precedente con *Domain_Name1*, *Domain_Name2* e *Domain_Name3*.

1. Per importare il file aggiornato, in gestione utenti fai clic su **[!UICONTROL Configurazione > Importa ed esporta file di configurazione]**.
1. Fai clic su **[!UICONTROL Sfoglia]** per trovare il file, fai clic su Importa, quindi su **[!UICONTROL OK]**.
