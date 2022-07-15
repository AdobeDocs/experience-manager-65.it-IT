---
title: 'Tutorial: crea la tua prima comunicazione interattiva'
seo-title: Create your first Interactive Communication
description: Scopri come creare la tua prima comunicazione interattiva.
seo-description: Learn to create your first Interactive Communication.
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
feature: Interactive Communication
exl-id: b20bb719-5686-466e-8dde-279b8471bfe3
source-git-commit: 471d7f48dc4653000b4852dbbeb886b05e28e644
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---

# Esercitazione: Creare la prima comunicazione interattiva {#tutorial-create-your-first-interactive-communication}

Scopri come creare la tua prima comunicazione interattiva.

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

Le comunicazioni interattive centralizzano e gestiscono la creazione, l&#39;assemblaggio e la distribuzione di corrispondenze sicure, personalizzate e interattive quali corrispondenza aziendale, documenti, dichiarazioni, e-mail di marketing, fatture e kit di benvenuto. Le comunicazioni interattive possono essere distribuite tramite due canali: Stampa e Web. Il canale Stampa viene utilizzato per creare PDF e comunicazioni su carta, mentre il canale Web viene utilizzato per fornire esperienze online.

Questa esercitazione fornisce un framework end-to-end per creare una comunicazione interattiva. L’esercitazione è organizzata in un caso d’uso e in più guide. Ogni guida consente di creare funzionalità utilizzate come blocchi predefiniti per la creazione di una comunicazione interattiva.

L’immagine seguente illustra i blocchi predefiniti necessari per creare una comunicazione interattiva.

![workflow](assets/workflow.gif)

Al termine di questa esercitazione, potrai:

* Creazione di blocchi predefiniti (modello dati modulo, frammenti di documento e modelli)
* Creare una comunicazione interattiva
* Test e pubblicazione di una comunicazione interattiva

## Caso d’uso {#use-case}

Il percorso inizia con l’apprendimento del caso d’uso:

Un operatore di telefonia invia ai clienti fatture mensili tramite e-mail. Il disegno di legge è una comunicazione interattiva. L’e-mail include:

* Un PDF protetto da password, denominato canale di stampa in questa esercitazione. Include i dettagli del cliente, dettagli della fattura, riepilogo delle spese, modalità pratiche di pagamento della fattura e dettagli di utilizzo.
* Un collegamento alla versione Web della fattura, definita canale Web in questa esercitazione. La versione web del disegno di legge, oltre ai dettagli trattati nella versione PDF, fornisce una rappresentazione grafica dei dettagli di utilizzo e delle offerte personalizzate basate su Adobe Target. La versione web contiene anche un modulo di pagamento online. Aiuta a effettuare pagamenti online senza lasciare l&#39;IC.
* Un collegamento a servizi a valore aggiunto quali archiviazione online, abbonamenti musicali e abbonamenti video on-demand.

## Prerequisiti {#prerequisites}

* Imposta un&#39;istanza di authoring AEM.
* Installa [Componente aggiuntivo AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) sull’istanza dell’autore
* Configurare il database MYSQL
* Ottenere il driver del database JDBC (file JAR) dal provider del database. Gli esempi nell&#39;esercitazione sono basati sul database MySQL e utilizzano Oracle [Driver del database JDBC MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html).

## Passaggio 1: Pianificare la comunicazione interattiva {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Il primo passo nella pianificazione di una comunicazione interattiva è quello di finalizzare il contenuto della comunicazione interattiva. Al termine della finalizzazione del contenuto, devi analizzarlo per identificare i vari tipi di risorse necessari per creare la comunicazione interattiva.

**Obiettivi:**

Per creare un’anatomia per la comunicazione interattiva con le seguenti modalità di immissione dei dati:

* Testo statico
* Modello dati modulo
* Interfaccia utente agente
* Dati condizionali
* Immagini

[ ](/help/forms/using/planning-interactive-communications.md)

## Passaggio 2: Crea modello dati modulo {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Un modello di dati modulo consente di collegare una comunicazione interattiva a diverse origini dati. Ad esempio, AEM profilo utente, servizi web RESTful, servizi web basati su SOAP, servizi OData e database relazionali. Un modello di dati modulo è uno schema unificato di rappresentazione dei dati delle entità e dei servizi aziendali disponibili nelle origini dati connesse. È possibile utilizzare il modello dati del modulo con una comunicazione interattiva per recuperare i dati dalle origini dati connesse. Per ulteriori informazioni sul modello dati modulo, vedere [Integrazione dei dati di AEM Forms](/help/forms/using/data-integration.md).

**Obiettivi:**

* Configura l&#39;istanza di database (database MySQL) come origine dati
* Creare il modello dati del modulo utilizzando il database MySQL come origine dati
* Aggiunta di oggetti del modello dati al modello dati del modulo
* Configurare i servizi di lettura e scrittura per il modello dati del modulo
* Creare associazioni tra gli oggetti del modello dati
* Visualizzare dati di esempio generati automaticamente
* Modifica dei dati di esempio
* Verificare il modello dati del modulo e i servizi configurati con i dati di prova

[ ](/help/forms/using/create-form-data-model0.md)

## Passaggio 3: Creazione di frammenti di documento {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

I frammenti di documento sono componenti riutilizzabili di una corrispondenza utilizzati per comporre una comunicazione interattiva. I frammenti di documento sono di tipo: Testo, Elenco e Condizione.

**Obiettivi:**

* Creazione di frammenti di documento
* Creare variabili
* Creare e applicare regole

[ ](/help/forms/using/create-document-fragments.md)

## Passaggio 4: Creare modelli {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Per creare una comunicazione interattiva, è necessario disporre di modelli disponibili sul server AEM per i canali Stampa e Web.

I modelli per il canale Stampa vengono creati in Adobe Forms Designer e caricati sul server AEM. Questi modelli sono quindi disponibili per l’utilizzo durante la creazione di una comunicazione interattiva.

I modelli per il canale Web vengono creati in AEM. Gli autori e gli amministratori dei modelli possono creare, modificare e abilitare i modelli web. Una volta creati e abilitati, questi modelli sono disponibili per l’utilizzo durante la creazione di una comunicazione interattiva.

**Obiettivi:**

* Creare modelli XDP per il canale di stampa utilizzando Adobe Forms Designer
* Caricare i modelli XDP sul server AEM Forms
* Creare e abilitare modelli per il canale Web

[ ](/help/forms/using/create-templates-print-web.md)

## Passaggio 5: Creare una comunicazione interattiva {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Dopo aver creato tutti i blocchi predefiniti, ad esempio il modello dati del modulo, i frammenti di documento e i modelli per la versione web, puoi iniziare a creare una comunicazione interattiva.

Le comunicazioni interattive possono essere trasmesse attraverso due canali: Stampa e Web. È inoltre possibile creare una comunicazione interattiva con il canale Stampa come principale. L&#39;opzione Stampa come master per il canale Web assicura che il contenuto, l&#39;ereditarietà e il binding dei dati del canale Web siano derivati dal canale Stampa.

**Obiettivi:**

* Creazione di comunicazioni interattive per il canale di stampa
* Creare comunicazioni interattive per il canale web
* Creazione di comunicazioni interattive per la stampa e il web con Stampa come principale
* Creazione di una tabella dinamica nella versione Web della comunicazione interattiva
* Crea un grafico nella versione Web della comunicazione interattiva
* Creare collegamenti ipertestuali nella versione Web di Interactive Communication

[ ](/help/forms/using/create-interactive-communication0.md)

## Passaggio 6: Pubblicare la comunicazione interattiva {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Una volta create e testate le comunicazioni interattive utilizzando i canali Stampa e Web, è possibile pubblicare tali risorse. Il caso d’uso descritto in questa esercitazione si concentra sull’integrazione di queste risorse con un client e-mail. Il client e-mail funge da ponte per inviare le comunicazioni interattive a più indirizzi e-mail.

**Obiettivi:**

* Integra le comunicazioni interattive con un client e-mail per poter inviare una comunicazione ai clienti
* Includere un documento PDF come allegato (Comunicazione interattiva creata nel canale Stampa)
* Includere un collegamento alla versione Web della comunicazione interattiva
