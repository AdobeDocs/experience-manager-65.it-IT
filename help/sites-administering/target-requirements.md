---
title: Prerequisiti per l’integrazione con Adobe Target
seo-title: Prerequisites for Integrating with Adobe Target
description: Scopri i prerequisiti per l’integrazione con Adobe Target.
seo-description: Find out about the prerequisites for integrating with Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 7%

---

# Prerequisiti per l’integrazione con Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Come parte del [Integrazione di AEM e Adobe Target](/help/sites-administering/target.md), è necessario registrarsi con Adobe Target, configurare l’agente di replica e proteggere le impostazioni delle attività sul nodo di pubblicazione.

## Registrazione con Adobe Target {#registering-with-adobe-target}

Per integrare AEM con Adobe Target, è necessario disporre di un account Adobe Target valido. Questo account deve avere **approvatore** autorizzazioni di livello minimo. Quando ti registri ad Adobe Target, ricevi un codice cliente. Per connettersi AEM ad Adobe Target è necessario il codice client e il nome di accesso e la password di Adobe Target.

Il codice client identifica l&#39;account cliente Adobe Target quando si chiama il server Adobe Target.

>[!NOTE]
>
>Per poter utilizzare l’integrazione, l’account deve essere abilitato anche dal team di Target.
>
>In caso contrario, contattare [Adobe Customer Care](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html).

## Abilitazione dell’agente di replica di Target {#enabling-the-target-replication-agent}

Test e Target [agente di replica](/help/sites-deploying/replication.md) deve essere abilitato nell’istanza di authoring. Tieni presente che questo agente di replica non è abilitato per impostazione predefinita se è stato utilizzato il [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) modalità di esecuzione per l&#39;installazione di AEM. Per ulteriori informazioni sulla protezione dell&#39;ambiente di produzione, consulta [Lista di controllo sicurezza](/help/sites-administering/security-checklist.md).

1. Nella home page di AEM, tocca o fai clic su **Strumenti** > **Distribuzione** > **Replica**.
1. Tocca o fai clic su **Agenti sull&#39;autore**.
1. Tocca o fai clic su **Test e Target (test e target)** agente di replica, quindi tocca o fai clic su **Modifica**.
1. Seleziona l’opzione Attivato, quindi tocca o fai clic su **OK**.

   >[!NOTE]
   >
   >Quando configuri l’agente di replica Test e Target, nella **Trasporti** scheda , l’URI è impostato per impostazione predefinita su **tnt:///**. Non sostituire questo URI con **https://admin.testandtarget.omniture.com**.
   >
   >Se provi a verificare la connessione con **tnt:///**, genererà un errore. Questo comportamento è previsto perché questo URI è solo per uso interno e non deve essere utilizzato con **Prova connessione**.

## Protezione del nodo Impostazioni attività {#securing-the-activity-settings-node}

È necessario proteggere il nodo delle impostazioni delle attività **cq:ActivitySettings** sull&#39;istanza di pubblicazione in modo che sia inaccessibile agli utenti normali. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.

La **cq:ActivitySettings** node è disponibile in CRXDE lite in `/content/campaigns/*nameofbrand*`* *sotto il nodo jcr:content delle attività;* *ad esempio `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Questo nodo viene creato solo dopo aver eseguito il targeting di un componente.

La **cq:ActivitySettings** il nodo sotto il jcr:content dell&#39;attività è protetto dalle seguenti ACL:

* Nega tutto per tutti
* Consenti jcr:read,rep:write per &quot;target-activity-authors&quot; (l&#39;autore è un membro di questo gruppo pronto all&#39;uso)
* Consenti jcr:read,rep:write per &quot;targetservice&quot;

Queste impostazioni assicurano che gli utenti normali non abbiano accesso alle proprietà del nodo. Utilizza gli stessi ACL sull&#39;autore e sulla pubblicazione. Vedi [Amministrazione degli utenti e sicurezza](/help/sites-administering/security.md) per ulteriori informazioni.

## Configurazione di AEM Link Externalizer {#configuring-the-aem-link-externalizer}

Quando modifichi un’attività in Adobe Target, l’URL punta a **localhost** a meno che non modifichi l’URL sul nodo di authoring AEM. Puoi configurare AEM Link Externalizer se desideri che il contenuto esportato punti a uno specifico *pubblicare* dominio.

>[!NOTE]
>
>Vedi anche [Aggiungere la configurazione cloud](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

Per configurare l&#39;esternalizzatore AEM:

>[!NOTE]
>
>Per ulteriori dettagli vedi [Esternalizzazione degli URL](/help/sites-developing/externalizer.md).

1. Passa alla console web OSGi all’indirizzo **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Trova **Day CQ Link Externalizer** e immetti il dominio per il nodo autore.

   ![chlimage_1-120](assets/aem-externalizer-01.png)
