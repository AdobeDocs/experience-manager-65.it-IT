---
title: Esercitazione - Creazione della prima comunicazione interattiva
seo-title: Creazione della prima comunicazione interattiva
description: Scopri come creare la tua prima comunicazione interattiva.
seo-description: Scopri come creare la tua prima comunicazione interattiva.
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---


# Esercitazione: Creazione della prima comunicazione interattiva {#tutorial-create-your-first-interactive-communication}

Scopri come creare la tua prima comunicazione interattiva.

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

Le comunicazioni interattive centralizzano e gestiscono la creazione, l&#39;assemblaggio e la distribuzione di corrispondenze sicure, personalizzate e interattive quali corrispondenza aziendale, documenti, dichiarazioni, e-mail di marketing, fatture e kit di benvenuto. Le comunicazioni interattive possono essere distribuite su due canali: Stampa e Web. Il canale Stampa viene utilizzato per creare PDF e comunicazioni cartacee, mentre il canale Web viene utilizzato per distribuire esperienze online.

Questa esercitazione fornisce un framework end-to-end per creare una comunicazione interattiva. L’esercitazione è organizzata in un caso d’uso e in più guide. Ogni guida è utile per creare funzioni utilizzate come elementi costitutivi per creare una comunicazione interattiva.

Nell&#39;immagine seguente sono illustrati i blocchi costitutivi necessari per creare una comunicazione interattiva.

![workflow](assets/workflow.gif)

Al termine di questa esercitazione, potrete:

* Creazione di blocchi predefiniti (modello dati modulo, frammenti di documento e modelli)
* Creazione di una comunicazione interattiva
* Test e pubblicazione di una comunicazione interattiva

## Use case {#use-case}

Il viaggio inizia con l&#39;apprendimento del caso d&#39;uso:

Un operatore di telecomunicazioni invia mensilmente ai clienti via e-mail. Il progetto di legge è una comunicazione interattiva. Il messaggio e-mail include:

* Un PDF protetto da password, denominato canale di stampa in questa esercitazione. Include i dettagli del cliente, i dettagli della fattura, il riepilogo delle spese, le pratiche modalità di pagamento della fattura e i dettagli di utilizzo.
* Un collegamento alla versione Web della fattura, denominata canale Web in questa esercitazione. La versione Web della fattura, oltre ai dettagli trattati nella versione PDF, fornisce una rappresentazione grafica dei dettagli di utilizzo e delle offerte personalizzate basate su  Adobe Target. La versione Web contiene anche un modulo di pagamento online. Aiuta a effettuare pagamenti online senza lasciare l&#39;IC.
* Collegamento a servizi a valore aggiunto, ad esempio archiviazione online, abbonamenti musicali e iscrizioni video on-demand.

## Prerequisiti {#prerequisites}

* Configurate un’istanza AEM di creazione.
* Installazione [componente aggiuntivo](/help/forms/using/installing-configuring-aem-forms-osgi.md) AEM Forms nell’istanza di creazione
* Configurare il database MYSQL
* Ottenete il driver del database JDBC (file JAR) dal provider del database. Gli esempi nell&#39;esercitazione si basano sul database MySQL e utilizzano il driver [di database Oracle](https://dev.mysql.com/downloads/connector/j/5.1.html)MySQL JDBC.

## Passaggio 1: Pianificare la comunicazione interattiva {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Il primo passo nella pianificazione di una comunicazione interattiva consiste nel finalizzare il contenuto della comunicazione interattiva. Una volta completato il contenuto, è necessario analizzarlo per identificare i vari tipi di risorse necessari per creare la comunicazione interattiva.

**Obiettivi:**

Per creare un&#39;anatomia per la comunicazione interattiva con le seguenti modalità di immissione dei dati:

* Testo statico
* Modello dati modulo
* INTERFACCIA UTENTE agente
* Dati condizionali
* Immagini

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/planning-interactive-communications.md)

## Step 2: Create form data model {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Un modello dati del modulo consente di collegare una comunicazione interattiva a origini dati diverse. Ad esempio, AEM profilo utente, servizi Web RESTful, servizi Web basati su SOAP, servizi OData e database relazionali. Un modello dati modulo è uno schema di rappresentazione dati unificato di entità e servizi aziendali disponibili nelle origini dati connesse. È possibile utilizzare il modello dati del modulo con una comunicazione interattiva per recuperare dati da origini dati connesse. Per ulteriori informazioni sul modello di dati del modulo, vedere [Integrazione](/help/forms/using/data-integration.md)dei dati AEM Forms.

**Obiettivi:**

* Configurare l&#39;istanza di database (database MySQL) come origine dati
* Creare il modello dati del modulo utilizzando il database MySQL come origine dati
* Aggiunta di oggetti del modello dati al modello dati del modulo
* Configurare i servizi di lettura e scrittura per il modello dati del modulo
* Creare associazioni tra gli oggetti del modello dati
* Visualizzare i dati di esempio generati automaticamente
* Modifica dei dati di esempio
* Verifica del modello di dati del modulo e dei servizi configurati con i dati di prova

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-form-data-model0.md)

## Passaggio 3: Creazione di frammenti di documento {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

I frammenti di documento sono componenti riutilizzabili di una corrispondenza utilizzata per comporre una comunicazione interattiva. I frammenti di documento sono di tipo: Testo, Elenco e Condizione.

**Obiettivi:**

* Creazione di frammenti di documento
* Creare variabili
* Creazione e applicazione di regole

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-document-fragments.md)

## Passaggio 4: Creare i modelli {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Per creare una comunicazione interattiva, è necessario disporre di modelli nel server AEM per i canali di stampa e Web.

I modelli per il canale di stampa vengono creati  Adobe Forms Designer e caricati nel server di AEM. Questi modelli sono quindi disponibili per la creazione di una comunicazione interattiva.

I modelli per il canale Web vengono creati in AEM. Gli autori e gli amministratori dei modelli possono creare, modificare e abilitare i modelli Web. Una volta creati e abilitati, questi modelli sono disponibili per la creazione di una comunicazione interattiva.

**Obiettivi:**

* Creare modelli XDP per il canale di stampa utilizzando  Adobe Forms Designer
* Caricare i modelli XDP sul  AEM Forms Server
* Creazione e attivazione di modelli per il canale Web

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-templates-print-web.md)

## Passaggio 5: Creazione di una comunicazione interattiva {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Dopo aver creato tutti i blocchi costitutivi come il modello dati del modulo, i frammenti di documento e i modelli per la versione Web, è possibile iniziare a creare una comunicazione interattiva.

Le comunicazioni interattive possono essere distribuite attraverso due canali: Stampa e Web. Potete anche creare una comunicazione interattiva con il canale Stampa come principale. L&#39;opzione Stampa come principale per il canale Web garantisce che il contenuto, l&#39;ereditarietà e il binding dei dati del canale Web siano derivati dal canale Stampa.

**Obiettivi:**

* Creazione di comunicazioni interattive per il canale di stampa
* Creazione di comunicazioni interattive per il canale Web
* Creazione di comunicazioni interattive per la stampa e il Web con Stampa come principale
* Creazione di una tabella dinamica nella versione Web della comunicazione interattiva
* Creazione di un grafico nella versione Web della comunicazione interattiva
* Creazione di collegamenti ipertestuali nella versione Web della comunicazione interattiva

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-interactive-communication0.md)

## Passaggio 6: Test della comunicazione interattiva {#step-test-your-interactive-communication}

![11 test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

Dopo aver creato una comunicazione interattiva, è importante verificare ogni modifica apportata. Verificare ogni campo di una comunicazione interattiva è noioso.  AEM Forms fornisce un SDK (Calvin SDK) per automatizzare il test delle comunicazioni interattive nel browser Web.

**Obiettivi:**

* Crea suite di test
* Creazione di test case
* Eseguire i casi di test

## Passaggio 7: Pubblicare la comunicazione interattiva {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-small](assets/12-publish-your-adaptive-form-_small.png)

Dopo aver creato e verificato le comunicazioni interattive tramite i canali Stampa e Web, potete pubblicare queste risorse. Il caso d’uso descritto in questa esercitazione è incentrato sull’integrazione di queste risorse con un client e-mail. Il client e-mail funge da ponte per inviare le comunicazioni interattive a più indirizzi e-mail.

**Obiettivi:**

* Integrare le comunicazioni interattive con un client di posta elettronica per poter inviare una comunicazione ai clienti
* Includere un documento PDF come allegato (Comunicazione interattiva creata nel canale di stampa)
* Includi un collegamento alla versione Web della comunicazione interattiva

