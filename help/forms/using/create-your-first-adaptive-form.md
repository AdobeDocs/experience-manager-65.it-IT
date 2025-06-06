---
title: 'Tutorial: creare il primo modulo adattivo'
description: Scopri come creare moduli di classe aziendale, interattivi e reattivi.
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f941782f9a4201e7bff898853d3fc18954418500
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 3%

---

# Tutorial: creare il primo modulo adattivo {#tutorial-create-your-first-adaptive-form}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=it) |
| AEM 6.5 | Questo articolo |


![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## Introduzione {#introduction}

Sei alla ricerca di un&#39;esperienza di **moduli** per dispositivi mobili che semplifichi l&#39;iscrizione, aumenti il coinvolgimento e riduca i tempi di risposta, **moduli adattivi** è la soluzione ideale per te. I moduli adattivi offrono un’esperienza di moduli per dispositivi mobili, automazione e analisi. Puoi creare facilmente moduli reattivi e interattivi, utilizzare processi automatizzati per ridurre le attività amministrative e ripetitive e utilizzare l’analisi dei dati per migliorare e personalizzare l’esperienza dei clienti con i tuoi moduli.

Questa esercitazione fornisce un framework end-to-end per creare un modulo adattivo. Il tutorial è organizzato in un caso d’uso e più guide. Ogni guida ti aiuta ad apprendere e aggiungere nuove funzioni al modulo adattivo creato in questa esercitazione. Puoi utilizzare un modulo adattivo dopo ogni guida. È disponibile la guida per creare un modulo adattivo. Le guide successive saranno presto disponibili. Al termine di questa esercitazione, dovresti essere in grado di effettuare le seguenti operazioni:

* Crea un modulo adattivo e un modello dati per modulo.
* Personalizza lo stile del modulo adattivo.
* Utilizza l’editor di regole per moduli adattivi per creare regole business.
* Testare e pubblicare un modulo adattivo.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

Il percorso inizia con l’apprendimento del caso d’uso:

Un sito web offre una gamma di prodotti per diversi clienti. I clienti navigano nel portale, selezionano e ordinano i prodotti. Ogni cliente crea un account e fornisce gli indirizzi di spedizione e fatturazione. Un cliente esistente, Sara Rose, sta cercando di aggiungere il suo indirizzo di spedizione al sito web. Il sito Web fornisce un modulo online per aggiungere e aggiornare gli indirizzi di spedizione.

Il sito Web viene eseguito su Adobe Experience Manager (AEM) e utilizza AEM [!DNL Forms] per l&#39;acquisizione e l&#39;elaborazione dei dati. Il modulo di aggiunta e aggiornamento degli indirizzi è un modulo adattivo. Il sito web memorizza i dettagli dei clienti in un database. Utilizzano il modulo di aggiunta e aggiornamento degli indirizzi per recuperare e visualizzare gli indirizzi disponibili. Inoltre, utilizzano il modulo adattivo per accettare indirizzi nuovi e aggiornati.

### Prerequisito {#prerequisite}

* Configura un&#39;istanza [dell&#39;autore AEM](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html?lang=it#author-and-publish-installs)
* Installa il componente aggiuntivo [AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) nell&#39;istanza di authoring.
* Ottenere il driver del database JDBC (file JAR) dal provider del database. Esempi nell&#39;esercitazione sono basati sul database [!DNL MySQL] e utilizzano [!DNL Oracle's] [Driver di database MySQL JDBC](https://dev.mysql.com/downloads/connector/j/5.1.html).

* Configura un database contenente i dati dei clienti con i campi visualizzati di seguito. Un database non è essenziale per creare un modulo adattivo. Questa esercitazione utilizza un database per visualizzare il modello di dati modulo e le funzionalità di persistenza dell&#39;AEM [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## Passaggio 1: creare un modulo adattivo {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

I moduli adattivi sono di nuova generazione, coinvolgenti, reattivi, dinamici e di natura adattiva. Utilizzando i moduli adattivi, puoi offrire esperienze personalizzate e mirate. L&#39;AEM [!DNL Forms] fornisce un editor di WYSIWYG per la creazione di moduli adattivi tramite trascinamento della selezione. Per ulteriori informazioni sui moduli adattivi, consulta [Introduzione alla creazione di moduli adattivi](../../forms/using/introduction-forms-authoring.md).

Obiettivi:

* Crea un modulo adattivo che consenta a un cliente di aggiungere un indirizzo di spedizione.
* Layout dei campi di un modulo adattivo per visualizzare e accettare informazioni da un cliente.
* Crea un’azione di invio per inviare un’e-mail contenente il contenuto del modulo.
* Visualizzare in anteprima e inviare un modulo adattivo.

[![Consulta la Guida](assets/see-the-guide-sm.png)](create-adaptive-form.md)

## Passaggio 2: creare il modello dati del modulo {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Un modello dati modulo consente di collegare un modulo adattivo a origini dati diverse. Ad esempio, profilo utente AEM, servizi web RESTful, servizi web basati su SOAP, servizi OData e database relazionali. Un modello dati modulo è uno schema di rappresentazione dati unificato di entità business e servizi disponibili nelle origini dati connesse. È possibile utilizzare il modello dati del modulo con un modulo adattivo per recuperare, aggiornare, eliminare e aggiungere dati alle origini dati connesse.

Obiettivi:

* Configurare l&#39;istanza di database del sito Web ([!DNL MySQL] database) come origine dati.
* Creare il modello dati del modulo utilizzando il database [!DNL MySQL] come origine dati.
* Aggiungi oggetti modello dati in modo da poter formare il modello dati.
* Configurare i servizi di lettura e scrittura per il modello dati del modulo.
* Verificare il modello dati del modulo e i servizi configurati con i dati di test.

[![Consulta la Guida](assets/see-the-guide-sm.png)](create-form-data-model.md)

## Passaggio 3: applicare le regole ai campi del modulo adattivo {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

I moduli adattivi forniscono un editor per scrivere regole sugli oggetti modulo adattivi. Queste regole definiscono le azioni da attivare sugli oggetti modulo in base a condizioni preimpostate, input dell&#39;utente e azioni dell&#39;utente sul modulo. Consente di garantire la precisione e velocizza l’esperienza di compilazione dei moduli.

Obiettivi:

* Crea e applica regole ai campi del modulo adattivo.
* Utilizzare le regole per attivare i servizi modello dati modulo per aggiornare i dati nel database.

[![Consulta la Guida](assets/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Passaggio 4: Personalizzare lo stile del modulo adattivo {#step-style-your-adaptive-form}

![adapative-form-styling](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

I moduli adattivi forniscono temi e un [editor](../../forms/using/themes.md) per creare temi per i moduli adattivi. Un tema contiene dettagli sullo stile di componenti e pannelli ed è possibile riutilizzarlo in diversi formati. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l’allineamento e le dimensioni. Quando si applica il tema al modulo, lo stile specificato viene applicato ai componenti corrispondenti del modulo. I moduli adattivi supportano anche lo stile in linea per gli stili specifici di un modulo.

Obiettivi:

* Applicare un tema preconfigurato a un modulo adattivo.
* Crea un tema per il modulo adattivo utilizzando l’editor del tema.
* Utilizzare i Web Fonts in un tema personalizzato.

[![Consulta la Guida](assets/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Passaggio 5: creare un Publish per il modulo adattivo {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

È possibile pubblicare moduli adattivi come modulo autonomo (applicazione a pagina singola), includere nella pagina [Sites](/help/forms/using/embed-adaptive-form-aem-sites.md) dell&#39;AEM o inserire un elenco in una pagina AEM [!DNL Site] utilizzando [Forms Portal](../../forms/using/introduction-publishing-forms.md).

Obiettivi:

* Publish il modulo adattivo come pagina AEM.
* Incorpora il modulo adattivo in una pagina AEM [!DNL Sites].
* Incorpora il modulo adattivo in una pagina web esterna (una pagina web non AEM ospitata al di fuori dell’AEM).

[![Consulta la Guida](assets/see-the-guide-sm.png)](publish-your-adaptive-form.md)
