---
title: Limiti dei contributi degli Stati membri
seo-title: Limiti dei contributi degli Stati membri
description: La funzione Limiti contributi consente di limitare i contributi per la protezione dallo spam
seo-description: La funzione Limiti contributi consente di limitare i contributi per la protezione dallo spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Limiti dei contributi dei membri {#member-contribution-limits}

## Panoramica {#overview}

La funzione Limiti di contribuzione consente di limitare i contributi dei membri della Comunità come mezzo di protezione contro lo spam.

Quando un membro è limitato, qualsiasi post che supera il numero consentito di contributi darà luogo a una segnalazione secondo cui il limite è stato superato e il post viene rifiutato. Il membro della comunità può quindi rivolgersi al centro messaggi della comunità e contattare un gestore della comunità che può rimuovere i limiti, se del caso.

I limiti dei contributi possono essere attivati singolarmente dalla [console Membri](members.md) e/o configurati in modo da essere attivati automaticamente quando i visitatori del sito diventano nuovi membri.

Utilizzando la console Membri, i limiti dei contributi possono essere rimossi in modo proattivo da un membro da un manager della community in qualsiasi momento oppure rimossi in modo reattivo quando un membro invia un messaggio a un manager della community che effettua tale richiesta.

## Configurazione dei limiti di contributo dei contenuti generati dagli utenti di AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Questa configurazione OSGi:

* Definisce le caratteristiche dei limiti di contribuzione (numero di posti entro un periodo di tempo).
* Identifica chi il membro sarà in grado di inviare messaggi quando il limite è stato raggiunto.
* Identifica i domini che non devono mai essere vincolati.

Per raggiungere questa configurazione OSGi:

* Nell&#39;editore principale:
* Accedi con privilegi di amministratore.
* Accedi alla [Console web](../../help/sites-deploying/configuring-osgi.md).

   * Ad esempio, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Individua `AEM Communities User Generated Content Contribution Limits Configuration`.
* Seleziona l’icona di modifica.

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL Applicare automaticamente i limiti dei contributi UGC]**

   Se questa opzione è selezionata, imposta automaticamente i limiti di contributo per gli utenti che si registrano come membri della community. Questo si riflette nel profilo del membro della community e può essere abilitato/disabilitato dalla [console dei membri](members.md). I nuovi membri con un indirizzo e-mail da un inserì nell&#39;elenco Consentiti di domini non sono mai vincolati.

   Il valore predefinito è deselezionato.

* **[!UICONTROL Limite UGC]**

   Numero massimo di contributi.

   Il valore predefinito è 10 post.

* **[!UICONTROL Frequenza limite UGC]**

   Il periodo di tempo che limita il limite UGC.

   Il valore predefinito è 60 minuti.

* **[!UICONTROL Domini]**

   Un elenco inserire nell&#39;elenco Consentiti di uno o più domini e-mail. Seleziona l’icona + per aggiungere voci.

   Gli utenti con indirizzi e-mail nel inserire nell&#39;elenco Consentiti dei domini non vengono interessati quando i limiti di contributo UGC vengono applicati automaticamente. Ad esempio, se il dominio `mycompany.com` viene aggiunto all’elenco dei domini, a un membro con indirizzo e-mail `me@mycompany.com` non verrà mai impedito di effettuare la pubblicazione.

   Il valore predefinito è un inserire nell&#39;elenco Consentiti vuoto.

* **[!UICONTROL Destinatari messaggistica]**

   Elenco di uno o più ID autorizzati dei membri in grado di modificare i limiti dei contributi per i membri. Seleziona l’icona + per aggiungere voci.

   I membri possono raggiungere i membri specificati solo quando il loro limite è stato raggiunto.

   Il valore predefinito non è alcun destinatario della messaggistica.

Nota: La configurazione predefinita comporta un limite di 10 post entro un periodo di un&#39;ora.
