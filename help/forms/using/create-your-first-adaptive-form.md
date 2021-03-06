---
title: '"Esercitazione: Crea il tuo primo modulo adattivo"'
seo-title: 'Tutorial: Create your first adaptive form'
description: Scopri come creare moduli interattivi, di classe aziendale e reattivi.
seo-description: Learn to create business class, interactive, and responsive forms.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
source-git-commit: 471d7f48dc4653000b4852dbbeb886b05e28e644
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 9%

---

# Esercitazione: Creare il primo modulo adattivo {#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## Introduzione {#introduction}

Stai cercando un mobile-friendly **esperienza dei moduli** che semplifica l&#39;iscrizione, aumenta l&#39;impegno e riduce i tempi di consegna, **moduli adattivi** È una vestibilità perfetta per te. I moduli adattivi offrono un’esperienza mobile, automatizzata e con moduli compatibili con le analisi. È possibile creare facilmente moduli reattivi e interattivi, utilizzare processi automatizzati per ridurre le attività amministrative e ripetitive e utilizzare l’analisi dei dati per migliorare e personalizzare l’esperienza dei clienti con i moduli.

Questa esercitazione fornisce un framework end-to-end per creare un modulo adattivo. L’esercitazione è organizzata in un caso d’uso e in più guide. Ogni guida è utile per apprendere e aggiungere nuove funzioni al modulo adattivo creato in questa esercitazione. Hai un modulo adattivo funzionante dopo ogni guida. È disponibile la guida per la creazione di un modulo adattivo . Le guide successive saranno presto disponibili. Al termine di questa esercitazione, potrai:

* Creare un modello di dati modulo adattivo e modulo.
* Assegna uno stile al modulo adattivo.
* Utilizza l’editor di regole del modulo adattivo per creare regole aziendali.
* Test e pubblicazione di un modulo adattivo.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

Il percorso inizia con l’apprendimento del caso d’uso:

Un sito web offre una gamma di prodotti per diversi clienti. I clienti navigano nel portale, selezionano e ordinano i prodotti. Ogni cliente crea un account e fornisce indirizzi di spedizione e fatturazione. Una cliente esistente, Sara Rose, sta cercando di aggiungere il suo indirizzo di spedizione al sito web. Il sito web fornisce un modulo online per aggiungere e aggiornare gli indirizzi di spedizione.

Il sito web viene eseguito su Adobe Experience Manager (AEM) e utilizza AEM [!DNL Forms] per l’acquisizione e l’elaborazione dei dati. Il modulo di aggiunta e aggiornamento dell’indirizzo è un modulo adattivo. Il sito web memorizza i dettagli dei clienti in un database. Utilizzano il modulo di aggiunta e aggiornamento dell’indirizzo per recuperare e visualizzare gli indirizzi disponibili. Utilizzano anche il modulo adattivo per accettare indirizzi nuovi e aggiornati.

### Prerequisito {#prerequisite}

* Imposta un&#39;istanza di authoring AEM.
* Installa [Componente aggiuntivo AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) sull’istanza di authoring.
* Ottenere il driver del database JDBC (file JAR) dal provider del database. Gli esempi nell’esercitazione si basano su [!DNL MySQL] database e utilizzo [!DNL Oracle's] [Driver del database JDBC MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html).

* Imposta un database contenente i dati del cliente con i campi visualizzati di seguito. Un database non è essenziale per creare un modulo adattivo. Questa esercitazione utilizza un database per visualizzare il modello dati del modulo e le funzionalità di persistenza di AEM [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## Passaggio 1: Creare un modulo adattivo {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

I moduli adattivi sono di nuova generazione, coinvolgenti, reattivi, dinamici e adattivi in natura. Utilizzando i moduli adattivi, puoi fornire esperienze personalizzate e mirate. AEM [!DNL Forms] fornisci un editor WYSIWYG con trascinamento per creare moduli adattivi. Per ulteriori informazioni sui moduli adattivi, consulta [Introduzione alla creazione di moduli adattivi](../../forms/using/introduction-forms-authoring.md).

Obiettivi:

* Creare un modulo adattivo che consenta a un cliente di aggiungere un indirizzo di spedizione
* Layout dei campi di un modulo adattivo per visualizzare e accettare le informazioni di un cliente
* Creare un’azione di invio per inviare un’e-mail contenente il contenuto del modulo
* Anteprima e invio di un modulo adattivo

[![Vedi la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## Passaggio 2: Crea modello dati modulo {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Un modello di dati modulo consente di collegare un modulo adattivo a diverse origini dati. Ad esempio, AEM profilo utente, servizi web RESTful, servizi web basati su SOAP, servizi OData e database relazionali. Un modello dati Modulo è uno schema di rappresentazione dei dati unificato delle entità e dei servizi aziendali disponibili nelle origini dati connesse. È possibile utilizzare il modello dati del modulo con un modulo adattivo per recuperare, aggiornare, eliminare e aggiungere dati alle origini dati connesse.

Obiettivi:

* Configura l’istanza di database del sito web ([!DNL MySQL] database) come origini dati
* Creare il modello dati del modulo utilizzando [!DNL MySQL] database come origine dati
* Aggiunta di oggetti del modello dati al modello dati del modulo
* Configurare i servizi di lettura e scrittura per il modello dati del modulo
* Verificare il modello dati del modulo e i servizi configurati con i dati di prova

[![Vedi la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## Passaggio 3: Applicazione di regole ai campi del modulo adattivo {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

I moduli adattivi forniscono un editor per la scrittura di regole sugli oggetti modulo adattivi. Queste regole definiscono le azioni da eseguire sugli oggetti modulo in base a condizioni preimpostate, input dell’utente e azioni dell’utente sul modulo. Consente di garantire l’accuratezza e di accelerare l’esperienza di compilazione dei moduli.

Obiettivi:

* Creazione e applicazione di regole ai campi del modulo adattivo
* Utilizzare le regole per attivare i servizi del modello dati modulo per aggiornare i dati al database

[![Vedi la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Passaggio 4: Personalizzare lo stile del modulo adattivo {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

I moduli adattivi forniscono temi e [editor](../../forms/using/themes.md) per creare temi per i moduli adattivi. Un tema contiene dettagli di stile per componenti e pannelli e può essere riutilizzato in diversi moduli. Gli stili includono proprietà quali colori di sfondo, colori dello stato, trasparenza, allineamento e dimensioni. Quando si applica il tema al modulo, lo stile specificato si riflette sui componenti corrispondenti del modulo. I moduli adattivi supportano anche lo stile in linea per gli stili specifici di un modulo.

Obiettivi:

* Applicare un tema preconfigurato a un modulo adattivo
* Creare un tema per un modulo adattivo utilizzando l’editor di temi
* Utilizzare i font web in un tema personalizzato

[![Vedi la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Passaggio 5: Pubblicare il modulo adattivo {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

È possibile pubblicare moduli adattivi come modulo autonomo (applicazione a pagina singola), incluso in AEM [Pagina Sites](/help/forms/using/embed-adaptive-form-aem-sites.md)o un elenco su un AEM [!DNL Site] utilizzo [Portale Forms](../../forms/using/introduction-publishing-forms.md).

Obiettivi:

* Pubblicare il modulo adattivo come pagina AEM
* Incorporare il modulo adattivo in un AEM [!DNL Sites] Pagina
* Incorporare il modulo adattivo in una pagina web esterna (una pagina web non AEM ospitata all’esterno di AEM)

[![Vedi la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
