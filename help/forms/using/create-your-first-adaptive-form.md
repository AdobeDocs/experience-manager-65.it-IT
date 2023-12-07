---
title: "Tutorial: creare il primo modulo adattivo"
description: Scopri come creare moduli di classe aziendale, interattivi e reattivi.
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 6%

---

# Tutorial: creare il primo modulo adattivo {#tutorial-create-your-first-adaptive-form}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=it) |
| AEM 6.5 | Questo articolo |


![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## Introduzione {#introduction}

Stai cercando un mobile-friendly **esperienza Forms** che semplifica l&#39;iscrizione, aumenta il coinvolgimento e riduce i tempi di risposta, **moduli adattivi** è una misura perfetta per te. I moduli adattivi offrono un’esperienza di moduli per dispositivi mobili, automazione e analisi. Puoi creare facilmente moduli reattivi e interattivi, utilizzare processi automatizzati per ridurre le attività amministrative e ripetitive e utilizzare l’analisi dei dati per migliorare e personalizzare l’esperienza dei clienti con i tuoi moduli.

Questa esercitazione fornisce un framework end-to-end per creare un modulo adattivo. Il tutorial è organizzato in un caso d’uso e più guide. Ogni guida ti aiuta ad apprendere e aggiungere nuove funzioni al modulo adattivo creato in questa esercitazione. Puoi utilizzare un modulo adattivo dopo ogni guida. È disponibile la guida per creare un modulo adattivo. Le guide successive saranno presto disponibili. Al termine di questa esercitazione, sarai in grado di:

* Crea un modulo adattivo e un modello dati per modulo.
* Personalizza lo stile del modulo adattivo.
* Utilizza l’editor di regole per moduli adattivi per creare regole business.
* Testare e pubblicare un modulo adattivo.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

Il percorso inizia con l’apprendimento del caso d’uso:

Un sito web offre una gamma di prodotti per diversi clienti. I clienti navigano nel portale, selezionano e ordinano i prodotti. Ogni cliente crea un account e fornisce gli indirizzi di spedizione e fatturazione. Un cliente esistente, Sara Rose, sta cercando di aggiungere il suo indirizzo di spedizione al sito web. Il sito Web fornisce un modulo online per aggiungere e aggiornare gli indirizzi di spedizione.

Il sito web viene eseguito su Adobe Experience Manager (AEM) e utilizza l&#39;AEM [!DNL Forms] per l’acquisizione e l’elaborazione dei dati. Il modulo di aggiunta e aggiornamento degli indirizzi è un modulo adattivo. Il sito web memorizza i dettagli dei clienti in un database. Utilizzano il modulo di aggiunta e aggiornamento degli indirizzi per recuperare e visualizzare gli indirizzi disponibili. Inoltre, utilizzano il modulo adattivo per accettare indirizzi nuovi e aggiornati.

### Prerequisito {#prerequisite}

* Imposta un [Istanza di authoring AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#author-and-publish-installs)
* Installa [Componente aggiuntivo AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) nell’istanza di authoring.
* Ottenere il driver del database JDBC (file JAR) dal provider del database. Esempi nell’esercitazione sono basati su [!DNL MySQL] database e utilizzo [!DNL Oracle's] [Driver di database MySQL JDBC](https://dev.mysql.com/downloads/connector/j/5.1.html).

* Imposta un database contenente i dati dei clienti con i campi visualizzati di seguito. Un database non è essenziale per creare un modulo adattivo. Questo tutorial utilizza un database per visualizzare il modello di dati dei moduli e le funzionalità di persistenza dell’AEM [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## Passaggio 1: creare un modulo adattivo {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

I moduli adattivi sono di nuova generazione, coinvolgenti, reattivi, dinamici e di natura adattiva. Utilizzando i moduli adattivi, puoi offrire esperienze personalizzate e mirate. AEM [!DNL Forms] fornisce un editor WYSIWYG con trascinamento per creare moduli adattivi. Per ulteriori informazioni sui moduli adattivi, consulta [Introduzione all’authoring di moduli adattivi](../../forms/using/introduction-forms-authoring.md).

Obiettivi:

* Creare un modulo adattivo che consenta a un cliente di aggiungere un indirizzo di spedizione
* Layout dei campi di un modulo adattivo per visualizzare e accettare le informazioni di un cliente
* Crea un’azione di invio per inviare un’e-mail contenente il contenuto del modulo
* Anteprima e invio di un modulo adattivo

[![Consulta la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## Passaggio 2: creare il modello dati del modulo {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Un modello per dati modulo consente di collegare un modulo adattivo a origini dati diverse. Ad esempio, profilo utente AEM, servizi web RESTful, servizi web basati su SOAP, servizi OData e database relazionali. Un modello dati modulo è uno schema di rappresentazione dati unificato di entità business e servizi disponibili nelle origini dati connesse. È possibile utilizzare il modello dati del modulo con un modulo adattivo per recuperare, aggiornare, eliminare e aggiungere dati alle origini dati connesse.

Obiettivi:

* Configurare l&#39;istanza di database del sito Web ([!DNL MySQL] database) come origini dati
* Crea il modello dati del modulo utilizzando [!DNL MySQL] database come origine dati
* Aggiungi oggetti modello dati al modello dati modulo
* Configurare i servizi di lettura e scrittura per il modello dati del modulo
* Test del modello di dati del modulo e servizi configurati con i dati di test

[![Consulta la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## Passaggio 3: applicare le regole ai campi del modulo adattivo {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

I moduli adattivi forniscono un editor per scrivere regole sugli oggetti modulo adattivi. Queste regole definiscono le azioni da attivare sugli oggetti modulo in base a condizioni preimpostate, input dell&#39;utente e azioni dell&#39;utente sul modulo. Consente di garantire precisione e velocizza l’esperienza di compilazione dei moduli.

Obiettivi:

* Creare e applicare regole ai campi del modulo adattivo
* Utilizzare le regole per attivare i servizi modello dati modulo per aggiornare i dati nel database

[![Consulta la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Passaggio 4: Personalizzare lo stile del modulo adattivo {#step-style-your-adaptive-form}

![adapative-form-styling](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

I moduli adattivi forniscono temi e un [editor](../../forms/using/themes.md) creare temi per i moduli adattivi. Un tema contiene dettagli sullo stile di componenti e pannelli ed è possibile riutilizzarlo in diversi formati. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l’allineamento e le dimensioni. Quando si applica il tema al modulo, lo stile specificato viene applicato ai componenti corrispondenti del modulo. I moduli adattivi supportano anche lo stile in linea per gli stili specifici di un modulo.

Obiettivi:

* Applicare un tema preconfigurato a un modulo adattivo
* Creare un tema per il modulo adattivo tramite l’editor tema
* Utilizzare i font per web in un tema personalizzato

[![Consulta la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Passaggio 5: pubblicare il modulo adattivo {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

È possibile pubblicare moduli adattivi come modulo autonomo (applicazione a pagina singola) da includere nell’AEM [Pagina Sites](/help/forms/using/embed-adaptive-form-aem-sites.md)o su un elenco di AEM [!DNL Site] utilizzo [Forms Portal](../../forms/using/introduction-publishing-forms.md).

Obiettivi:

* Pubblicare il modulo adattivo come pagina AEM
* Incorporare il modulo adattivo in un AEM [!DNL Sites] Pagina
* Incorporare il modulo adattivo in una pagina web esterna (una pagina web non AEM ospitata al di fuori dell’AEM)

[![Consulta la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
