---
title: Limiti contributi membri
seo-title: Member Contribution Limits
description: La funzione Limiti contributi consente di limitare i contributi da proteggere dallo spam
seo-description: Contribution limits feature lets you limit the contributions to protect against spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 1%

---

# Limiti contributi membri {#member-contribution-limits}

## Panoramica {#overview}

La funzione Limiti contributi consente di limitare i contributi dei membri della community come mezzo per proteggere dallo spam.

Quando un membro è limitato, qualsiasi post che superi il numero consentito di contributi genera un avviso che informa che il limite è stato superato e il post viene rifiutato. Il membro della community può quindi recarsi al centro messaggi della community e contattare un manager della community che può rimuovere i limiti, se necessario.

I limiti di contribuzione possono essere abilitati singolarmente dall&#39; [Console Membri](members.md) e/o configurato per essere abilitato automaticamente quando i visitatori del sito diventano nuovi membri.

Utilizzando la console Membri, i limiti di contribuzione possono essere rimossi in modo proattivo per un membro da un manager di community in qualsiasi momento, oppure rimossi in modo reattivo quando un membro invia un messaggio a un manager di community effettuando una richiesta di questo tipo.

## Configurazione dei limiti di contributo per i contenuti generati dagli utenti di AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Questa configurazione OSGi:

* Definisce le caratteristiche dei limiti di contribuzione (numero di posti in un periodo di tempo).
* Identifica l&#39;utente che potrà inviare il messaggio quando il limite è stato raggiunto.
* Identifica i domini che non devono mai essere vincolati.

Per raggiungere questa configurazione OSGi:

* Nel server di pubblicazione principale:
* Accedi con privilegi di amministratore.
* Accedere a [Console web](../../help/sites-deploying/configuring-osgi.md).

   * Ad esempio: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Individua `AEM Communities User Generated Content Contribution Limits Configuration`.
* Seleziona l’icona Modifica.

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL Applica automaticamente limiti contributi UGC]**

   Se questa opzione è selezionata, imposta automaticamente i limiti di contribuzione per gli utenti che si registrano come membri della community. Questo si riflette nel profilo del membro della community e può essere abilitato/disabilitato dal [console dei membri](members.md). I nuovi membri con un indirizzo e-mail da una inserisce nell&#39;elenco Consentiti di domini di un’organizzazione non sono mai vincolati.

   L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Limite UGC]**

   Numero massimo di contributi.

   Il valore predefinito è 10 post.

* **[!UICONTROL Frequenza limite UGC]**

   Il periodo di tempo che vincola il limite UGC.

   Il valore predefinito è 60 minuti.

* **[!UICONTROL Domini]**

   Inserire nell&#39;elenco Consentiti Un elenco di e-mail di uno o più domini di e-mail di. Seleziona l’icona + per aggiungere altre voci.

   Gli utenti con indirizzi e-mail nel inserito nell&#39;elenco Consentiti di domini di non vengono interessati quando i limiti di contributi UGC vengono applicati automaticamente. Ad esempio, se dominio `mycompany.com` viene aggiunto all’elenco dei domini, quindi un membro con indirizzo e-mail `me@mycompany.com` non è mai soggetto a restrizioni per la registrazione.

   Il valore predefinito è un elenco Consentiti di vuoto.

* **[!UICONTROL Destinatari di messaggistica]**

   Elenco di uno o più ID autorizzabili dei membri in grado di modificare i limiti di contribuzione per i membri. Seleziona l’icona + per aggiungere altre voci.

   I membri possono raggiungere determinati membri solo una volta raggiunto il loro limite.

   L&#39;impostazione predefinita non è nessun destinatario di messaggistica.

Nota: la configurazione predefinita comporta un limite di 10 post in un periodo di un&#39;ora.
