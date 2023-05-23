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

# Tutorial: crea la tua prima comunicazione interattiva {#tutorial-create-your-first-interactive-communication}

Scopri come creare la tua prima comunicazione interattiva.

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

Le comunicazioni interattive centralizzano e gestiscono la creazione, l’assemblaggio e la distribuzione di corrispondenze sicure, personalizzate e interattive quali corrispondenza aziendale, documenti, dichiarazioni, e-mail di marketing, fatture e kit di benvenuto. Le comunicazioni interattive possono essere distribuite tramite due canali: stampa e web. Il canale Stampa viene utilizzato per creare PDF e comunicazioni cartacee, mentre il canale Web viene utilizzato per fornire esperienze online.

Questo tutorial fornisce un framework end-to-end per creare una comunicazione interattiva. Il tutorial è organizzato in un caso d’uso e più guide. Ogni guida ti aiuta a creare funzioni utilizzate come blocchi predefiniti per creare una comunicazione interattiva.

L’immagine seguente illustra i blocchi predefiniti necessari per creare una comunicazione interattiva.

![flusso di lavoro](assets/workflow.gif)

Al termine di questa esercitazione, sarai in grado di:

* Creare blocchi predefiniti (modello dati modulo, frammenti di documenti e modelli)
* Creare una comunicazione interattiva
* Testare e pubblicare una comunicazione interattiva

## Caso d’uso {#use-case}

Il percorso inizia con l’apprendimento del caso d’uso:

Un operatore di telecomunicazioni invia fatture mensili ai clienti tramite e-mail. Il conto è una comunicazione interattiva. L’e-mail include:

* Un PDF protetto da password, denominato Canale di stampa in questa esercitazione. Include i dettagli del cliente, i dettagli della fattura, il riepilogo delle spese, le modalità pratiche di pagamento della fattura e i dettagli di utilizzo.
* Collegamento alla versione web di Bill, definito canale web in questa esercitazione. La versione web del disegno di legge, oltre ai dettagli trattati nella versione PDF, fornisce una rappresentazione grafica dei dettagli di utilizzo e delle offerte personalizzate basate su Adobe Target. La versione web contiene anche un modulo di pagamento online. Consente di effettuare pagamenti online senza uscire dall&#39;IC.
* Un collegamento a servizi a valore aggiunto, come archiviazione online, abbonamenti musicali e video on-demand.

## Prerequisiti {#prerequisites}

* Configura un’istanza di authoring AEM.
* Installa [Componente aggiuntivo AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) sull’istanza di authoring
* Configurare il database MYSQL
* Ottenere il driver del database JDBC (file JAR) dal provider del database. Gli esempi del tutorial si basano sul database MySQL e utilizzano Oracle [Driver di database MySQL JDBC](https://dev.mysql.com/downloads/connector/j/5.1.html).

## Passaggio 1: pianificare la comunicazione interattiva {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Il primo passo nella pianificazione di una comunicazione interattiva è finalizzare il contenuto della comunicazione interattiva. Dopo aver finalizzato il contenuto, devi analizzarlo per identificare i vari tipi di risorse necessari per creare la comunicazione interattiva.

**Obiettivi:**

Per creare un&#39;anatomia per la comunicazione interattiva con le seguenti modalità di immissione dei dati:

* Testo statico
* Modello dati modulo
* Interfaccia utente agente
* Dati condizionali
* Immagini

[ ](/help/forms/using/planning-interactive-communications.md)

## Passaggio 2: creare il modello dati del modulo {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Un modello per dati modulo consente di collegare una comunicazione interattiva per utilizzare origini dati diverse. Ad esempio, profilo utente AEM, servizi web RESTful, servizi web basati su SOAP, servizi OData e database relazionali. Un modello dati modulo è uno schema di rappresentazione dati unificato di entità business e servizi disponibili nelle origini dati connesse. È possibile utilizzare il modello dati del modulo con una comunicazione interattiva per recuperare i dati dalle origini dati connesse. Per ulteriori informazioni sul modello dati del modulo, consulta [Integrazione dei dati di AEM Forms](/help/forms/using/data-integration.md).

**Obiettivi:**

* Configurare l&#39;istanza di database (database MySQL) come origine dati
* Creare il modello dati del modulo utilizzando il database MySQL come origine dati
* Aggiungi oggetti modello dati al modello dati modulo
* Configurare i servizi di lettura e scrittura per il modello dati del modulo
* Creare associazioni tra gli oggetti modello dati
* Visualizza dati di esempio generati automaticamente
* Modifica dati di esempio
* Test del modello di dati del modulo e servizi configurati con i dati di test

[ ](/help/forms/using/create-form-data-model0.md)

## Passaggio 3: creare frammenti di documento {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

I frammenti di documento sono componenti riutilizzabili di una corrispondenza utilizzati per comporre una comunicazione interattiva. I frammenti di documento sono di tipo Testo, Elenco e Condizione.

**Obiettivi:**

* Creare frammenti di documenti
* Creare le variabili
* Creare e applicare regole

[ ](/help/forms/using/create-document-fragments.md)

## Passaggio 4: creare modelli {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Per creare una comunicazione interattiva, è necessario che sul server AEM siano disponibili modelli per la stampa e i canali Web.

I modelli per il canale di stampa vengono creati in Adobe Forms Designer e caricati sul server AEM. Questi modelli sono quindi disponibili per l’utilizzo durante la creazione di una comunicazione interattiva.

I modelli per il canale web vengono creati in AEM. Gli autori e gli amministratori dei modelli possono creare, modificare e abilitare i modelli web. Una volta creati e abilitati, questi modelli sono disponibili per l’uso durante la creazione di una comunicazione interattiva.

**Obiettivi:**

* Creazione di modelli XDP per il canale di stampa con Adobe Forms Designer
* Carica i modelli XDP sul server AEM Forms
* Creare e abilitare modelli per il canale web

[ ](/help/forms/using/create-templates-print-web.md)

## Passaggio 5: creare una comunicazione interattiva {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Dopo aver creato tutti i blocchi predefiniti, ad esempio il modello di dati del modulo, i frammenti di documento e i modelli per la versione web, puoi iniziare a creare una comunicazione interattiva.

Le comunicazioni interattive possono essere distribuite attraverso due canali: stampa e web. Puoi anche creare una comunicazione interattiva con il canale di stampa come principale. L’opzione Stampa come principale per il canale web assicura che il contenuto, l’ereditarietà e l’associazione dati del canale web siano derivati dal canale Stampa.

**Obiettivi:**

* Creare una comunicazione interattiva per il canale di stampa
* Creare comunicazioni interattive per il canale web
* Creare comunicazioni interattive a mezzo Stampa e Web con Stampa come principale
* Creare una tabella dinamica nella versione web della comunicazione interattiva
* Creare un grafico nella versione web della comunicazione interattiva
* Creare collegamenti ipertestuali nella versione web della comunicazione interattiva

[ ](/help/forms/using/create-interactive-communication0.md)

## Passaggio 6: pubblicare la comunicazione interattiva {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Dopo aver creato e testato le comunicazioni interattive utilizzando i canali di stampa e web, puoi pubblicare queste risorse. Il caso d’uso descritto in questa esercitazione si concentra sull’integrazione di queste risorse con un client e-mail. Il client e-mail funge da ponte per inviare le comunicazioni interattive a più indirizzi e-mail.

**Obiettivi:**

* Integrare le comunicazioni interattive con un client e-mail per poter inviare una comunicazione ai clienti
* Includere un documento PDF come allegato (comunicazione interattiva creata nel canale di stampa)
* Includi un collegamento alla versione web della comunicazione interattiva
