---
title: '"Esercitazione: Creare il primo modulo adattivo"'
seo-title: '"Esercitazione: Creare il primo modulo adattivo"'
description: Scopri come creare moduli interattivi e reattivi di classe aziendale.
seo-description: Scopri come creare moduli interattivi e reattivi di classe aziendale.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
translation-type: tm+mt
source-git-commit: 43c04a8b2f1e2e7f2067cec055d8737dfc7b3e84
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---


# Esercitazione: Creare il primo modulo adattivo {#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## Introduzione {#introduction}

State cercando un&#39;esperienza **di** moduli mobile che semplifichi l&#39;iscrizione, aumenti il coinvolgimento e riduca il tempo di esecuzione, i moduli **** adattivi sono la scelta ideale per voi. I moduli adattivi offrono un&#39;esperienza mobile, automatizzata e intuitiva in termini di analisi. È possibile creare moduli di natura reattiva e interattiva, utilizzare processi automatizzati per ridurre le attività amministrative e ripetitive e utilizzare l&#39;analisi dei dati per migliorare e personalizzare l&#39;esperienza dei clienti con i moduli.

Questa esercitazione fornisce un framework end-to-end per creare un modulo adattivo. L’esercitazione è organizzata in un caso d’uso e in più guide. Ogni guida è utile per apprendere e aggiungere nuove funzioni al modulo adattivo creato con questa esercitazione. Dopo ogni guida è disponibile un modulo adattivo funzionante. È disponibile la guida per la creazione di un modulo adattivo. Le guide successive saranno disponibili a breve. Al termine di questa esercitazione, potrete:

* Creare un modulo adattivo e un modello dati modulo.
* Applicare uno stile al modulo adattivo.
* Utilizzare l&#39;editor di regole del modulo adattive per creare regole aziendali.
* Verificare e pubblicare un modulo adattivo.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

Il viaggio inizia con l&#39;apprendimento del caso d&#39;uso:

Un sito Web offre una serie di prodotti per clienti diversi. I clienti possono sfogliare il portale, selezionare e ordinare i prodotti. Ogni cliente crea un account e fornisce indirizzi di spedizione e fatturazione. Un cliente esistente, Sara Rose, sta cercando di aggiungere il suo indirizzo di spedizione al sito web. Il sito Web fornisce un modulo online per aggiungere e aggiornare gli indirizzi di spedizione.

Il sito Web viene eseguito su Adobe Experience Manager (AEM) e utilizzato AEM [!DNL Forms] per l’acquisizione e l’elaborazione dei dati. Il modulo di aggiunta e aggiornamento dell&#39;indirizzo è un modulo adattivo. Il sito Web memorizza i dettagli dei clienti in un database. Utilizzano il modulo di aggiunta e aggiornamento dell&#39;indirizzo per recuperare e visualizzare gli indirizzi disponibili. Inoltre, utilizzano il modulo adattivo per accettare indirizzi nuovi e aggiornati.

### Prerequisito {#prerequisite}

* Impostazione di un’istanza di creazione AEM.
* Installate [componente aggiuntivo](../../forms/using/installing-configuring-aem-forms-osgi.md) AEM Forms nell’istanza di creazione.
* Ottenete il driver del database JDBC (file JAR) dal provider del database. Gli esempi nell&#39;esercitazione sono basati sul [!DNL MySQL] database e utilizzano il driver [!DNL Oracle's] di database [](https://dev.mysql.com/downloads/connector/j/5.1.html)MySQL JDBC.

* Configurate un database contenente i dati del cliente con i campi riportati di seguito. Un database non è essenziale per creare un modulo adattivo. Questa esercitazione utilizza un database per visualizzare il modello dati del modulo e le funzionalità di persistenza di AEM [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## Passaggio 1: Creare un modulo adattivo {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

I moduli adattivi sono di nuova generazione, coinvolgenti, reattivi, dinamici e adattabili. L&#39;utilizzo di moduli adattivi consente di distribuire esperienze personalizzate e mirate. AEM [!DNL Forms] un editor WYSIWYG con trascinamento per creare moduli adattivi. Per ulteriori informazioni sui moduli adattivi, vedere [Introduzione alla creazione di moduli](../../forms/using/introduction-forms-authoring.md)adattivi.

Obiettivi:

* Creare un modulo adattivo che consenta al cliente di aggiungere un indirizzo di spedizione
* Campi di layout di un modulo adattivo per visualizzare e accettare le informazioni di un cliente
* Creare un&#39;azione di invio per inviare un&#39;e-mail contenente il contenuto del modulo
* Anteprima e invio di un modulo adattivo

[![Vedere la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## Step 2: Create Form Data Model {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Un modello dati del modulo consente di collegare un modulo adattivo a origini dati diverse. Ad esempio, AEM profilo utente, servizi Web RESTful, servizi Web basati su SOAP, servizi OData e database relazionali. Un modello dati Modulo è uno schema di rappresentazione dati unificato di entità e servizi aziendali disponibili nelle origini dati connesse. È possibile utilizzare il modello dati del modulo con un modulo adattivo per recuperare, aggiornare, eliminare e aggiungere dati alle origini dati connesse.

Obiettivi:

* Configurare l&#39;istanza di database del sito Web ([!DNL MySQL] database) come origini dati
* Creare il modello dati del modulo utilizzando [!DNL MySQL] il database come origine dati
* Aggiunta di oggetti del modello dati al modello dati del modulo
* Configurare i servizi di lettura e scrittura per il modello dati del modulo
* Verifica del modello di dati del modulo e dei servizi configurati con i dati di prova

[![Vedere la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## Passaggio 3: Applicazione di regole ai campi modulo adattivi {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

I moduli adattivi forniscono un editor per la scrittura di regole per gli oggetti modulo adattivi. Queste regole definiscono le azioni da eseguire sugli oggetti modulo in base a condizioni predefinite, input dell&#39;utente e azioni dell&#39;utente sul modulo. Garantisce la precisione e velocizza la compilazione dei moduli.

Obiettivi:

* Creazione e applicazione di regole ai campi modulo adattivi
* Utilizzare le regole per attivare i servizi del modello dati del modulo per aggiornare i dati al database

[![Vedere la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Passaggio 4: Stile del modulo adattivo {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

I moduli adattivi forniscono temi e un [editor](../../forms/using/themes.md) per la creazione di temi per i moduli adattivi. Un tema contiene dettagli di stile per componenti e pannelli e può essere riutilizzato in diversi moduli. Gli stili includono proprietà quali i colori di sfondo, i colori dello stato, la trasparenza, l’allineamento e le dimensioni. Quando si applica il tema al modulo, lo stile specificato si riflette sui componenti corrispondenti del modulo. I moduli adattivi supportano inoltre lo stile in linea per gli stili specifici di un modulo.

Obiettivi:

* Applicazione di un tema out-of-box a un modulo adattivo
* Creare un tema per un modulo adattivo utilizzando l&#39;editor di temi
* Utilizzo di font Web in un tema personalizzato

[![Vedere la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Passaggio 5: Verificare il modulo adattivo {#step-test-your-adaptive-form}

![11 test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

I moduli adattivi sono parte integrante delle interazioni con i clienti. È importante verificare i moduli adattivi con tutte le modifiche apportate al modulo. Verificare ogni campo di un modulo è noioso. AEM [!DNL Forms] fornire un SDK (Calvin SDK) per automatizzare il test dei moduli adattivi. Calvin consente di automatizzare il test dei moduli adattivi nel browser Web.

Obiettivi:

* Creare una suite di test per il modulo adattivo
* Creazione di test case per i moduli adattivi
* Eseguire i casi di test

[![Vedere la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](testing-your-adaptive-form.md)

## Passaggio 6: Pubblicare il modulo adattivo {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

È possibile pubblicare moduli adattivi come modulo autonomo (applicazione a pagina singola), da includere nella pagina [AEM](/help/forms/using/embed-adaptive-form-aem-sites.md)Siti o nell&#39;elenco di un AEM [!DNL Site] tramite [Forms Portal](../../forms/using/introduction-publishing-forms.md).

Obiettivi:

* Pubblicare il modulo adattivo come pagina AEM
* Incorporare il modulo adattivo in una [!DNL Sites] pagina AEM
* Incorporare il modulo adattivo in una pagina Web esterna (una pagina Web non AEM ospitata all’esterno di AEM)

[![Vedere la Guida](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)