---
title: Limiti contributi membri
description: La funzione Limiti contributi consente di limitare i contributi da proteggere dallo spam
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---

# Limiti contributi membri {#member-contribution-limits}

## Panoramica {#overview}

La funzione Limiti contributi consente di limitare i contributi dei membri della community come mezzo di protezione contro lo spam.

Quando un membro è limitato, qualsiasi post che supera il numero consentito di contributi genera un avviso che indica che il limite è stato superato e il post viene rifiutato. Il membro della community può quindi recarsi al centro messaggi della community e contattare un manager della community che può rimuovere i limiti, se necessario.

I limiti di contribuzione possono essere abilitati singolarmente dall&#39; [Console Membri](members.md) e/o configurato per essere abilitato automaticamente quando i visitatori del sito diventano nuovi membri.

Utilizzando la console Membri, i limiti di contribuzione possono essere rimossi in modo proattivo per un membro da un manager di community in qualsiasi momento, oppure rimossi in modo reattivo quando un membro invia un messaggio a un manager di community effettuando una richiesta di questo tipo.

## Configurazione dei limiti di contributo per i contenuti generati dagli utenti di AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Questa configurazione OSGi:

* Definisce le caratteristiche dei limiti di contribuzione (numero di posti in un periodo di tempo).
* Identifica l&#39;utente che può inviare un messaggio quando viene raggiunto il limite.
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

  Il valore predefinito è dieci post.

* **[!UICONTROL Frequenza limite UGC]**

  Il periodo di tempo che vincola il limite UGC.

  Il valore predefinito è 60 minuti.

* **[!UICONTROL Domini]**

  Inserire nell&#39;elenco Consentiti Un elenco di e-mail di uno o più domini di e-mail di. Seleziona l’icona + per inserire ulteriori voci.

  Gli utenti con indirizzi e-mail nel inserito nell&#39;elenco Consentiti di domini di non vengono interessati quando i limiti di contributi UGC vengono applicati automaticamente. Ad esempio, se dominio `mycompany.com` viene aggiunto all’elenco dei domini, quindi un membro con indirizzo e-mail `me@mycompany.com` non è mai soggetto a restrizioni per la registrazione.

  Il valore predefinito è un elenco Consentiti di vuoto.

* **[!UICONTROL Destinatari di messaggistica]**

  Elenco di uno o più ID autorizzabili dei membri in grado di modificare i limiti di contribuzione per i membri. Seleziona l’icona + per inserire ulteriori voci.

  I membri possono raggiungere determinati membri solo una volta raggiunto il loro limite.

  L&#39;impostazione predefinita non è nessun destinatario di messaggistica.

Nota: la configurazione predefinita comporta un limite di dieci post in un periodo di un’ora.
