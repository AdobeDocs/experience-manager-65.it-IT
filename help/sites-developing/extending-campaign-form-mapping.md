---
title: Creazione di mappature di moduli personalizzate
seo-title: Creazione di mappature di moduli personalizzate
description: Quando si crea una tabella personalizzata in  Adobe Campaign, potrebbe essere necessario creare un modulo AEM mappato su tale tabella personalizzata
seo-description: Quando si crea una tabella personalizzata in  Adobe Campaign, potrebbe essere necessario creare un modulo AEM mappato su tale tabella personalizzata
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 5%

---


# Creazione di mappature di moduli personalizzate{#creating-custom-form-mappings}

Quando si crea una tabella personalizzata in  Adobe Campaign, potrebbe essere necessario creare un modulo AEM mappato su tale tabella personalizzata.

Questo documento descrive come creare mappature dei moduli personalizzate. Una volta completati i passaggi descritti in questo documento, gli utenti avranno a disposizione una pagina dell&#39;evento in cui potranno registrarsi per un evento imminente. Potete quindi seguire questi utenti tramite  Adobe Campaign.

## Prerequisiti {#prerequisites}

Dovete disporre dei seguenti elementi installati:

* Adobe Experience Manager
* Adobe Campaign Classic

Per ulteriori informazioni, vedere [Integrazione AEM con Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

## Creazione di mappature di moduli personalizzate {#creating-custom-form-mappings-2}

Per creare mappature dei moduli personalizzate, è necessario seguire questi passaggi di alto livello, descritti in dettaglio nelle sezioni seguenti:

1. Creare una tabella personalizzata.
1. Estendere la tabella **seed**.
1. Creare una mappatura personalizzata.
1. Crea una consegna basata sulla mappatura personalizzata.
1. Creare il modulo in AEM, che utilizzerà la consegna creata.
1. Inviare il modulo per verificarlo.

### Creazione di una tabella personalizzata in  Adobe Campaign {#creating-the-custom-table-in-adobe-campaign}

Iniziate creando una tabella personalizzata in  Adobe Campaign. In questo esempio, utilizziamo la seguente definizione per creare una tabella eventi:

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

Dopo aver creato la tabella eventi, eseguire la **Aggiornamento della struttura del database** per creare la tabella.

### Estensione della tabella delle sementi {#extending-the-seed-table}

In  Adobe Campaign, toccate/fate clic su **Aggiungi** per creare una nuova estensione della tabella **Indirizzi di base (nms)**.

![chlimage_1-194](assets/chlimage_1-194.png)

A questo punto, utilizzate i campi della tabella **event** per estendere la tabella **seed**:

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

A questo punto, eseguite **Aggiornamento guidato database** per applicare le modifiche.

### Creazione di un mapping personalizzato delle destinazioni {#creating-custom-target-mapping}

In **Amministrazione/gestione campagna** t, andare a **Mappature di destinazione** e aggiungere una nuova mappatura di destinazione T **.**

>[!NOTE]
>
>Accertatevi di utilizzare un nome significativo per **Nome interno**.

![chlimage_1-195](assets/chlimage_1-195.png)

### Creazione di un modello di consegna personalizzato {#creating-a-custom-delivery-template}

In questo passaggio, si sta aggiungendo un modello di consegna che utilizza la mappatura **Target** creata.

In **Risorse/Modelli**, andate al Modello di consegna e duplicate la consegna AEM esistente. Quando si fa clic su **To**, selezionare la mappatura dell&#39;evento di creazione **Target**.

![chlimage_1-196](assets/chlimage_1-196.png)

### Creazione del modulo in AEM {#building-the-form-in-aem}

In AEM, accertatevi di aver configurato un Cloud Service in **Proprietà pagina**.

Quindi, nella scheda **Adobe Campaign**, selezionare la consegna creata in [Creazione di un modello di consegna personalizzato](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

Durante la configurazione dei campi, assicurarsi di specificare nomi univoci di elementi per i campi modulo.

Una volta configurati i campi, è necessario modificare manualmente la mappatura.

In CRXDE-Lite, andate al nodo **jcr:content** (della pagina) e modificate il valore **acMapping** nel nome interno della **mappatura destinazione**.

![chlimage_1-198](assets/chlimage_1-198.png)

Nella configurazione del modulo, selezionare la casella di controllo per creare se non esistente

![chlimage_1-199](assets/chlimage_1-199.png)

### Invio del modulo {#submitting-the-form}

È ora possibile inviare il modulo e convalidare sul lato Adobe Campaign  se i valori vengono salvati.

![chlimage_1-200](assets/chlimage_1-200.png)

## Risoluzione dei problemi {#troubleshooting}

**&quot;Tipo non valido per il valore &#39;02/02/2015&#39; dall&#39;elemento &#39;@eventdate&#39; (documento di tipo &#39;Event ([adb:event])&#39;)&quot;**

Quando si invia il modulo, l&#39;errore viene registrato nel AEM **error.log**.

Formato non valido per il campo data. La soluzione alternativa consiste nel fornire il valore **yyyy-mm-dd**.

