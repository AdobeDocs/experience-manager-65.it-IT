---
title: Prerequisiti per l’integrazione con  Adobe Target
seo-title: Prerequisiti per l’integrazione con  Adobe Target
description: Scoprite i prerequisiti per l'integrazione con  Adobe Target.
seo-description: Scoprite i prerequisiti per l'integrazione con  Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 3%

---


# Prerequisiti per l’integrazione con  Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Come parte dell&#39; [integrazione di AEM e  Adobe Target](/help/sites-administering/target.md), è necessario registrarsi  Adobe Target, configurare l&#39;agente di replica e le impostazioni dell&#39;attività protetta sul nodo di pubblicazione.

## Registrazione con  Adobe Target {#registering-with-adobe-target}

Per integrare AEM con  Adobe Target, è necessario disporre di un account  Adobe Target valido. Questo account deve avere almeno autorizzazioni a livello di **approver** . Quando vi registrate con  Adobe Target, ricevete un codice cliente. Per collegare AEM a  Adobe Target, è necessario disporre del codice client e del nome di login e della password  Adobe Target.

Il Codice client identifica l&#39;account cliente del Adobe Target  quando si chiama il server del Adobe Target .

>[!NOTE]
>
>Per poter utilizzare l&#39;integrazione, l&#39;account deve essere abilitato anche dal team Target.
>
>In caso contrario, contatta l&#39;Assistenza clienti [](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html)Adobe.

## Abilitazione di Target Replication Agent {#enabling-the-target-replication-agent}

L&#39;agente [di](/help/sites-deploying/replication.md) replica Test e Target deve essere abilitato nell&#39;istanza di creazione. L&#39;agente di replica non è abilitato per impostazione predefinita se per l&#39;installazione di AEM è stata utilizzata la modalità di esecuzione [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) . Per ulteriori informazioni sulla protezione dell&#39;ambiente di produzione, vedere l&#39; [elenco](/help/sites-administering/security-checklist.md)di controllo della sicurezza.

1. Nella home page di AEM, tocca o fai clic su **Strumenti** > **Distribuzione** > **Replica**.
1. Tocca o fai clic su **Agenti sull&#39;autore**.
1. Tocca o fai clic sull&#39;agente di replica **Test e Target (test e target)** , quindi tocca o fai clic su **Modifica**.
1. Selezionate l&#39;opzione Attivato, quindi fate clic o toccate **OK**.

   >[!NOTE]
   >
   >Quando configurate l&#39;agente di replica Test e Target, nella scheda **Trasporto** l&#39;URI è impostato per impostazione predefinita su **tnt:///**. Non sostituite questo URI con **https://admin.testandtarget.omniture.com**.
   >
   >Se si tenta di verificare la connessione con **tnt:///**, verrà generato un errore. Questo comportamento è previsto perché l&#39;URI è solo per uso interno e non deve essere utilizzato con **Test Connection**.

## Protezione del nodo delle impostazioni dell&#39;attività {#securing-the-activity-settings-node}

You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.

Il nodo **cq:ActivitySettings** è disponibile in CRXDE lite in `/content/campaigns/*nameofbrand*`* *sotto il nodo jcr:content delle attività;* *ad esempio `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Questo nodo viene creato solo dopo aver eseguito il targeting di un componente.

Il nodo **cq:ActivitySettings** in jcr:content dell&#39;attività è protetto dai seguenti ACL:

* Nega tutti per tutti
* Consenti jcr:read,rep:write per &quot;target-activity-authors&quot; (l’autore è un membro di questo gruppo)
* Consenti jcr:read,rep:write per &quot;target service&quot;

Queste impostazioni assicurano che gli utenti normali non abbiano accesso alle proprietà del nodo. Utilizzate gli stessi ACL per l&#39;autore e la pubblicazione. Per ulteriori informazioni, consulta Amministrazione [utente e sicurezza](/help/sites-administering/security.md) .

## Configurazione di AEM Link Externalizer {#configuring-the-aem-link-externalizer}

Quando modificate un&#39;attività in  Adobe Target, l&#39;URL punta a **localhost** a meno che non cambiate l&#39;URL nel nodo di creazione di AEM. Potete configurare AEM Link Externalizer se desiderate che il contenuto esportato punti a un dominio *di pubblicazione* specifico.

>[!NOTE]
>
>Consultate anche [Aggiunta della configurazione](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)cloud.

Per configurare l’esternalizzatore AEM:

>[!NOTE]
>
>Per ulteriori dettagli, consultate [Esternalizzazione degli URL](/help/sites-developing/externalizer.md).

1. Andate alla console Web OSGi all&#39;indirizzo **https://&lt;server>:&lt;porta>/system/console/configMgr.**
1. Trova l’Externalizer di collegamento CQ **** Day e immetti il dominio per il nodo dell’autore.

   ![chlimage_1-120](assets/aem-externalizer-01.png)

