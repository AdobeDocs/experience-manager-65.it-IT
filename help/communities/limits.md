---
title: Limiti Di Contributo
seo-title: Limiti Di Contributo
description: La funzione Limiti contributi consente di limitare i contributi per la protezione contro lo spam
seo-description: La funzione Limiti contributi consente di limitare i contributi per la protezione contro lo spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
translation-type: tm+mt
source-git-commit: d80c6609b5a0ac299b57b1d0c0e8d6210e595b97
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# Limiti contributi membri {#member-contribution-limits}

## Panoramica {#overview}

La funzione Limiti contributi permette di limitare i contributi dei membri della Comunità come mezzo di protezione contro lo spam.

Quando un membro è limitato, qualsiasi post che supera il numero consentito di contributi darà luogo a un avviso in cui viene segnalato che il limite è stato superato e il post viene rifiutato. Il membro della comunità può quindi rivolgersi al centro di messaggi della Comunità e contattare un responsabile della comunità, che può rimuovere i limiti se necessario.

I limiti dei contributi possono essere attivati individualmente dalla [console Membri](members.md) e/o configurati in modo da essere automaticamente attivati quando i visitatori del sito diventano nuovi membri.

Utilizzando la console Membri, i limiti dei contributi possono essere rimossi in modo proattivo per un membro da un manager della community in qualsiasi momento, o rimossi in modo reattivo quando un membro invia un messaggio a un manager della community che effettua tale richiesta.

##  Configurazione Limiti di contributi di contenuto generati dagli utenti AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Questa configurazione OSGi:

* Definisce le caratteristiche dei limiti di contributo (numero di posti entro un periodo di tempo).
* Identifica chi il membro sarà in grado di inviare un messaggio quando il limite sarà stato raggiunto.
* Identifica i domini che non devono mai essere vincolati.

Per raggiungere questa configurazione OSGi:

* Nell&#39;editore principale:
* Effettuate l&#39;accesso con privilegi di amministratore.
* Accedere alla [console Web](../../help/sites-deploying/configuring-osgi.md).

   * Ad esempio, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Individuare `AEM Communities User Generated Content Contribution Limits Configuration`.
* Selezionate l’icona di modifica.

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL Applica automaticamente limiti contributi UGC]**

   Se questa opzione è attivata, imposta automaticamente i limiti di contributo per gli utenti che si registrano come membri della community. Questo si riflette nel profilo del membro della community e può essere abilitato/disabilitato dalla [console dei membri](members.md). I nuovi membri con un indirizzo e-mail da un  inserire nell&#39;elenco Consentiti di domini non sono mai vincolati.

   Il valore predefinito è deselezionato.

* **[!UICONTROL Limite UGC]**

   Numero massimo di contributi.

   Il valore predefinito è 10 post.

* **[!UICONTROL Frequenza limite UGC]**

   Il periodo di tempo che limita il limite UGC.

   Il valore predefinito è 60 minuti.

* **[!UICONTROL Domini]**

   Un  elenco inserire nell&#39;elenco Consentiti di uno o più domini e-mail. Selezionate l’icona + per aggiungere altre voci.

   Gli utenti con indirizzi e-mail nel inserire nell&#39;elenco Consentiti  di domini non vengono interessati dall’applicazione automatica dei limiti di contributi UGC. Ad esempio, se il dominio `mycompany.com` viene aggiunto all&#39;elenco dei domini, a un membro con indirizzo e-mail `me@mycompany.com` non viene mai imposto il divieto di pubblicazione.

   Il valore predefinito è un inserire nell&#39;elenco Consentiti  vuoto.

* **[!UICONTROL Destinatari messaggistica]**

   Elenco di uno o più ID autorizzati di membri in grado di modificare i limiti dei contributi per i membri. Selezionate l’icona + per aggiungere altre voci.

   I membri possono raggiungere determinati membri solo quando il loro limite è stato raggiunto.

   Il valore predefinito non è alcun destinatario di messaggi.

Nota: La configurazione predefinita prevede un limite di 10 post entro un&#39;ora.
