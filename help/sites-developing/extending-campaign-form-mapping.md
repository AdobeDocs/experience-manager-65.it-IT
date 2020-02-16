---
title: Creazione di mappature di moduli personalizzate
seo-title: Creazione di mappature di moduli personalizzate
description: Quando crei una tabella personalizzata in Adobe Campaign, potresti voler creare in AEM un modulo mappato su tale tabella personalizzata
seo-description: Quando crei una tabella personalizzata in Adobe Campaign, potresti voler creare in AEM un modulo mappato su tale tabella personalizzata
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creazione di mappature di moduli personalizzate{#creating-custom-form-mappings}

Quando crei una tabella personalizzata in Adobe Campaign, potresti voler creare in AEM un modulo mappato su tale tabella personalizzata.

Questo documento descrive come creare mappature dei moduli personalizzate. Una volta completati i passaggi descritti in questo documento, gli utenti avranno a disposizione una pagina dell&#39;evento in cui potranno registrarsi per un evento imminente. Puoi quindi seguire questi utenti tramite Adobe Campaign.

## Prerequisiti {#prerequisites}

Dovete disporre dei seguenti elementi installati:

* Adobe Experience Manager
* Adobe Campaign Classic

See [Integrating AEM with Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) for more information.

## Creazione di mappature di moduli personalizzate {#creating-custom-form-mappings-2}

Per creare mappature dei moduli personalizzate, è necessario seguire questi passaggi di alto livello, descritti in dettaglio nelle sezioni seguenti:

1. Creare una tabella personalizzata.
1. Estende la tabella **sementi** .
1. Creare una mappatura personalizzata.
1. Crea una consegna basata sulla mappatura personalizzata.
1. Create il modulo in AEM, che utilizzerà la consegna creata.
1. Inviare il modulo per verificarlo.

### Creazione di una tabella personalizzata in Adobe Campaign {#creating-the-custom-table-in-adobe-campaign}

Per iniziare, crea una tabella personalizzata in Adobe Campaign. In questo esempio, utilizziamo la seguente definizione per creare una tabella eventi:

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

Dopo aver creato la tabella degli eventi, eseguite la procedura guidata **** Aggiorna struttura del database per creare la tabella.

### Estensione della tabella delle sementi {#extending-the-seed-table}

In Adobe Campaign, tocca o fai clic su **Aggiungi** per creare una nuova estensione della tabella degli indirizzi **seed (nms)** .

![chlimage_1-194](assets/chlimage_1-194.png)

A questo punto, utilizzate i campi della tabella **evento** per estendere la tabella **seed** :

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

A questo punto, eseguite la procedura guidata **** Aggiorna database per applicare le modifiche.

### Creazione di una mappatura di destinazione personalizzata {#creating-custom-target-mapping}

In **Amministrazione/** Gestione campagne, andate a Mappature **** Target e aggiungete una nuova mappatura **Target.**

>[!NOTE]
>
>Accertatevi di usare un nome significativo per il nome **** interno.

![chlimage_1-195](assets/chlimage_1-195.png)

### Creazione di un modello di consegna personalizzato {#creating-a-custom-delivery-template}

In questo passaggio, state aggiungendo un modello di consegna che utilizza la mappatura **** Target creata.

In **Risorse/Modelli**, passa al Modello di consegna e duplica la consegna AEM esistente. Quando fate clic su **A**, selezionate la creazione della mappatura **di** destinazione dell&#39;evento.

![chlimage_1-196](assets/chlimage_1-196.png)

### Creazione del modulo in AEM {#building-the-form-in-aem}

In AEM, accertati di aver configurato un servizio Cloud in Proprietà **** pagina.

Quindi, nella scheda **Adobe Campaign** , seleziona la consegna creata in [Creazione di un modello](#creating-a-custom-delivery-template)di consegna personalizzato.

![chlimage_1-197](assets/chlimage_1-197.png)

Durante la configurazione dei campi, assicurarsi di specificare nomi univoci di elementi per i campi modulo.

Una volta configurati i campi, è necessario modificare manualmente la mappatura.

In CRXDE-Lite, andate al nodo **jcr:content** (della pagina) e modificate il valore **acMapping** sul nome interno della mappatura **di** Target.

![chlimage_1-198](assets/chlimage_1-198.png)

Nella configurazione del modulo, selezionare la casella di controllo per creare se non esistente

![chlimage_1-199](assets/chlimage_1-199.png)

### Invio del modulo {#submitting-the-form}

Ora è possibile inviare il modulo e convalidare sul lato Adobe Campaign se i valori vengono salvati.

![chlimage_1-200](assets/chlimage_1-200.png)

## Risoluzione dei problemi {#troubleshooting}

**&quot;Tipo non valido per il valore &#39;02/02/2015&#39; dall&#39;elemento &#39;@eventdate&#39; (documento di tipo &#39;Event ([adb:event])&#39;)&quot;**

Quando si invia il modulo, questo errore viene registrato nel registro **** error.log in AEM.

Formato non valido per il campo data. La soluzione alternativa consiste nel fornire il valore **yyyy-mm-dd** .

