---
title: Creazione di mappature di moduli personalizzati
description: Quando crei una tabella personalizzata in Adobe Campaign, potrebbe essere utile creare in AEM un modulo mappato su tale tabella personalizzata
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: bce6c586-9962-4217-82cb-c837e479abc0
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 5%
---
# Creazione di mappature di moduli personalizzati{#creating-custom-form-mappings}

Quando crei una tabella personalizzata in Adobe Campaign, potrebbe essere utile creare in AEM un modulo mappato su tale tabella personalizzata.

Questo documento descrive come creare mapping di moduli personalizzati. Dopo aver completato i passaggi descritti in questo documento, fornirai agli utenti una pagina evento in cui possono iscriversi per un evento in programma. Puoi quindi seguire questi utenti tramite Adobe Campaign.

## Prerequisiti {#prerequisites}

Devi avere installato quanto segue:

* Adobe Experience Manager
* Adobe Campaign Classic

Per ulteriori informazioni, vedere [Integrazione di AEM con Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

## Creazione di mappature di moduli personalizzati {#creating-custom-form-mappings-2}

Per creare mappature di moduli personalizzate, è necessario seguire questi passaggi di alto livello, descritti in dettaglio nelle sezioni seguenti:

1. Crea una tabella personalizzata.
1. Estendere la tabella **seed**.
1. Creare una mappatura personalizzata.
1. Crea una consegna in base alla mappatura personalizzata.
1. Crea il modulo in AEM, che utilizzerà la consegna creata.
1. Inviare il modulo per verificarlo.

### Creazione della tabella personalizzata in Adobe Campaign {#creating-the-custom-table-in-adobe-campaign}

Inizia creando una tabella personalizzata in Adobe Campaign. In questo esempio, usiamo la seguente definizione per creare una tabella eventi:

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

Dopo aver creato la tabella eventi, eseguire la **Procedura guidata Aggiorna struttura database** per creare la tabella.

### Estensione della tabella dei valori iniziali {#extending-the-seed-table}

In Adobe Campaign, selezionare **Aggiungi** per creare un&#39;estensione della tabella **Indirizzi seed (nms)**.

![chlimage_1-194](assets/chlimage_1-194.png)

Utilizzare ora i campi della tabella **event** per estendere la tabella **seed**:

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

In seguito, eseguire **Aggiornamento guidato database** per applicare le modifiche.

### Creazione di una mappatura di destinazione personalizzata {#creating-custom-target-mapping}

In **Amministrazione/Gestione campagne** t, vai a **Mappature target** e aggiungi un nuovo T **Mappatura target.**

>[!NOTE]
>
>Assicurarsi di utilizzare un nome significativo per **Nome interno**.

![chlimage_1-195](assets/chlimage_1-195.png)

### Creazione di un modello di consegna personalizzato {#creating-a-custom-delivery-template}

In questo passaggio, stai aggiungendo un modello di consegna che utilizza la mappatura **Target** creata.

In **Risorse/Modelli**, passa al Modello di consegna e duplica la consegna AEM esistente. Quando fai clic su **A**, seleziona l&#39;evento di creazione **Mappatura target**.

![chlimage_1-196](assets/chlimage_1-196.png)

### Creazione di un modulo in AEM {#building-the-form-in-aem}

In AEM, assicurati di aver configurato un Cloud Service in **Proprietà pagina**.

Quindi, nella scheda **Adobe Campaign**, seleziona la consegna creata in [Creazione di un modello di consegna personalizzato](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

Durante la configurazione dei campi, accertati di specificare nomi di elementi univoci per i campi modulo.

Dopo aver configurato i campi, devi modificare manualmente la mappatura.

In CRXDE-lite, vai al nodo **jcr:content** (della pagina) e modifica il valore **acMapping** nel nome interno del mapping **Target**.

![chlimage_1-198](assets/chlimage_1-198.png)

Nella configurazione del modulo, accertati di selezionare la casella di controllo per creare se non esistente

![chlimage_1-199](assets/chlimage_1-199.png)

### Invio del modulo {#submitting-the-form}

Ora puoi inviare il modulo e verificare sul lato Adobe Campaign se i valori vengono salvati.

![chlimage_1-200](assets/chlimage_1-200.png)

## Risoluzione di problemi {#troubleshooting}

**&quot;Tipo non valido per il valore &#39;02/02/2015&#39; dall&#39;elemento &#39;@eventdate&#39; (documento di tipo &#39;Event ([adb:event])&#39;)&quot;**

Durante l&#39;invio del modulo, questo errore viene registrato nel **error.log** in AEM.

Il formato del campo data non è valido. La soluzione alternativa consiste nel fornire **aaaa-mm-gg** come valore.
