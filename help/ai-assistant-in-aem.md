---
title: Assistente AI in AEM 6.5
description: Utilizza l’Assistente IA per trovare risposte e risolvere eventuali problemi relativi alle soluzioni disponibili in Adobe Experience Manager.
solution: Experience Manager, Experience Manager 6.5
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
autotag-review: '2026-05-18T18:36:07.915Z'
TQID: 'https://experienceleague.adobe.com/dlFmrtn05S20z96wtAfkpGliITeVJhVkofqPix6QMxk'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2:
  - id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1379
ht-degree: 93%

---

# Assistente AI in AEM 6.5 {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>I clienti che non utilizzano AEM 6.5 e AEM 6.5 LTS, Cloud Manager/Experience Hub devono contattare il proprio Adobe Customer Success Engineer per richiedere l’accesso all’Assistente IA.

L’Assistente AI in AEM 6.5/AEM 6.5 LTS offre un’interfaccia di conversazione progettata per semplificare la ricerca delle risposte alle query relative a Adobe Experience Manager. Aiuta a ottenere risposte immediate alle domande relative al prodotto AEM (*disponibile per tutti gli utenti*) e ad automatizzare la creazione di ticket di supporto (*disponibile per gli amministratori del supporto*).

L’Assistente IA supporta AEM as a Cloud Service, incluse le seguenti soluzioni:

* Pagina della panoramica di Experience Hub
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


È direttamente incorporato in AEM e accessibile dall’interfaccia utente di AEM Experience Hub, Cloud Manager e authoring.

Il seguente video, della durata di 3 minuti e 25 secondi, offre una guida dettagliata all’Assistente IA in AEM.

>[!VIDEO](https://video.tv.adobe.com/v/3475357/?learn=on&enablevpops)

## Accedere all’Assistente IA in AEM{#get-access}

Per accedere all’Assistente IA in AEM, i clienti devono disporre dei seguenti requisiti:

* Autorizzazione all’uso dell’Assistente IA in AEM per le informazioni sui prodotti. Questa autorizzazione consente di porre domande relative ai prodotti nella chat dell’Assistente IA e deve essere abilitata.
* Autorizzazione all’apertura di ticket di supporto che richiede il ruolo di **amministratore di supporto**.

>[!NOTE]
>
>Le richieste all’Assistente IA in AEM vengono autenticate tramite Adobe Identity Management Services (IMS). Per ulteriori dettagli, consulta la [panoramica di Adobe Identity Management Services](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf).

**Per accedere all’Assistente IA in AEM:**

1. I clienti devono disporre di un accordo aggiuntivo per poter accedere alla maggior parte delle funzionalità basate su intelligenza artificiale e agentiche in Adobe Experience Manager. Per ulteriori informazioni, contatta il rappresentante Adobe.

1. Per utilizzare l’Assistente IA in AEM, è obbligatorio disporre dell’autorizzazione per accedere alla knowledge del prodotto tramite l’Assistente IA. Questa autorizzazione è attivata per impostazione predefinita.

   Se desideri controllare chi può accedere alla knowledge del prodotto, invia un’e-mail ad [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID. Adobe può abilitare il controllo degli accessi a livello di utente. Una volta abilitato, il tuo amministratore può concedere l’accesso a livello di utente seguendo i passaggi descritti in [Configurare l’Assistante IA in AEM](/help/ai-assistant-in-aem-admin.md).


## Ambito {#scope}

L’ambito corrente dell’Assistente per l’intelligenza artificiale in AEM si concentra sulla risoluzione delle domande relative alla conoscenza del prodotto per AEMr. as a Cloud Service. Questo ambito include un supporto completo per le aree principali. <!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **Superfici**: disponibili in AEM Experience Hub, Author UI, Cloud Manager.
* **Funzionalità**: conoscenza del prodotto e primo punto di riferimento per la risoluzione dei problemi e assistenza, creazione automatizzata di ticket di supporto e ricerca.
* **Valore**: consente di risparmiare tempo, di accelerare l’apprendimento e il time-to-value, di ridurre la necessità di creare manualmente ticket di supporto e di migliorare l’efficienza nella creazione dei ticket di supporto.

## Privacy, sicurezza e governance{#privacy-security-governance}

L’Assistente IA in AEM è progettato ponendo una particolare attenzione su privacy, sicurezza e governance.

Questo articolo illustra le funzionalità incentrate sull’attendibilità che ci si può aspettare dall’Assistente IA in AEM:

* L’Assistente IA in AEM non utilizza dati personali, nemmeno a fini della formazione.
* L’Assistente IA in AEM non ha accesso ai dati dei consumer.
* È richiesta un’autorizzazione esplicita per interagire con l’Assistente IA in AEM.
* I prompt forniti dall’utente (domande, query e così via) non vengono condivisi con altri consumer.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## Scoprire l’Assistente IA in AEM per la conoscenza del prodotto e la creazione automatizzata di ticket di supporto {#ai-prod-insights}

La conoscenza del prodotto comprende concetti e argomenti presenti nella documentazione di Adobe Experience League. Queste domande possono essere classificate nei seguenti sottogruppi:


| Conoscenza del prodotto | Disponibilità per tutti gli utenti<br>Esempi |
| :--- | :--- |
| Apprendimento mirato | <ul><li>Che cos’è l’editor universale?</li><li>Come posso creare un programma in Cloud Manager?</li></ul> |
| Individuazione aperta | <ul><li>Come posso utilizzare l’editor universale?</li><li>Esiste un modo per copiare il contenuto da un ambiente all’altro?</li></ul> |
| Risoluzione di problemi | <ul><li>Perché non riesco ad accedere all’editor universale?</li><li>Perché la mia pipeline non funziona?</li></ul> |
| **Creazione ticket di supporto** | **Disponibile solo per gli amministratori del supporto &#x200B;**<br>**Esempi** |
| Creazione automatizzata di ticket di supporto per acquisire la cronologia e il contesto delle chat dell’Assistente IA | <ul><li>Crea un ticket di supporto per me.</li></ul> |
| Recupero dello stato del ticket di supporto | <ul><li>Mostra tutti i ticket di supporto che ho aperto.</li><li>Mostra lo stato del ticket “E-----------”</li></ul> |

{style="table-layout:auto"}


## Come formulare domande efficaci {#ai-craft-questions}

Per ottenere risposte più precise dall’Assistente IA in AEM, è importante formulare le domande in modo chiaro e contestualizzato. Segui questi suggerimenti per assicurarti che le tue richieste siano chiare e ben strutturate:

* Spiega chiaramente la tua attività o domanda in modo conciso.
* Evita formulazioni ambigue o sintassi eccessivamente complesse per migliorare la comprensione.
* Includi il contesto pertinente relativo alla tua attività o domanda, poiché questo approccio aiuta l’Assistente IA in AEM a fornire risposte più precise e pertinenti.
Ad esempio, nel tuo prompt, è utile indicare la soluzione AEM su cui stai lavorando: Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager o Forms.

### Esempi di domande non supportate {#ai-unsupported-questions}

| Area | Esempi |
| --- | --- |
| Insight operativi | <ul><li>Quanti ambienti di sviluppo sono presenti nel mio tenant?</li><li>Chi ha avviato l’ultima pipeline di produzione?</li></ul> |
| Risoluzione di problemi | <ul><li>Perché la pipeline di produzione non funziona?</li></ul> |
| Attività e automazione | <ul><li>Configura una pipeline di qualità del codice da un ramo di sviluppo.</li></ul> |


## Utilizzare l’Assistente IA in AEM {#ai-use}

<!--
UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md).
-->


### Iniziare una conversazione con l’Assistente IA in AEM

Puoi ripristinare l’Assistente IA in AEM e iniziare una nuova conversazione quando desideri cambiare argomento. Questa funzionalità è particolarmente utile per risolvere i problemi relativi a query che non riescono o che forniscono informazioni errate.

**Per iniziare una conversazione con l’Assistente IA in AEM:**

1. Fai clic sull’icona **Assistente IA** nell’angolo in alto a destra dell’interfaccia utente di AEM (dalle pagine di Cloud Manager o dall’istanza di authoring degli ambienti AEM).

   ![Icona dell’Assistente IA sulla barra degli strumenti](/help/assets/assets-ai/ai-assistant-icon.png)

1. Nella casella di testo del pannello **Assistente IA**, accanto alla parte inferiore, digita la domanda o il prompt, quindi premi `Enter` o fai clic su ![icona di invio](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   >[!NOTE]
   >
   >I dati personali non devono essere inclusi negli input, in quanto non sono necessari per l’utilizzo di questo strumento.

   ![Casella di testo nella parte inferiore del pannello dell’Assistente IA](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. Per iniziare una nuova conversazione (nuovo argomento o modifica dell’argomento), fai clic su ![icona altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **Inizia nuova conversazione**.

   ![Inizia una nuova conversazione con l’Assistente IA dall’icona con i puntini di sospensione](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### Individuare i prompt per categoria

L’Assistente IA in AEM include una funzione di individuazione che ti aiuta a esplorare gli argomenti e le categorie supportati.

**Per individuare i prompt per categoria:**

1. Nel pannello dell’Assistente IA, fai clic su ![icona con lampadina](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg) per attivare il pannello di individuazione dei prompt.

   ![Pannello che consente di esplorare i prompt per categoria nell’Assistente IA](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   *Pannello che mostra le categorie dei prompt nell’Assistente IA.*

1. Seleziona una categoria per visualizzare un elenco di prompt correlati.
1. Seleziona un prompt per visualizzare esempi dei tipi di domande a cui l’Assistente IA può rispondere.

1. Per nascondere il pannello di individuazione dei prompt, fai di nuovo clic su ![icona con lampadina](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).

### Condividere il feedback sull’Assistante IA in AEM

Il tuo feedback consente ad Adobe di migliorare l’Assistente IA per assicurare prestazioni più elevate e maggiore precisione.

Condividi il tuo feedback sulla tua esperienza con l’Assistente IA in AEM tramite le seguenti opzioni:

![Icone con pollice su, pollice giù e bandierina](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| Clic | Descrizione |
| --- | --- |
| ![Icona pollice su](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Spiega cosa è andato bene e condividi feedback positivi. |
| ![Icona pollice giù](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Fornisci suggerimenti di miglioramento. Aggiungi commenti specifici sulla tua esperienza: vengono esaminati ogni giorno. |
| ![Icona bandierina](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Segnala eventuali problemi o fornisci un feedback dettagliato sulla tua esperienza con l’Assistente IA in AEM. |

## Domande frequenti sull’Assistente IA in AEM {#ai-faq}

Ecco le risposte ad alcune domande frequenti sull’Assistente IA:

* **Le informazioni fornite dall’Assistente IA in AEM sono in tempo reale?**\
  No. L’Assistente IA attinge i propri contenuti dalla documentazione di Adobe Experience League. Gli aggiornamenti ai contenuti potrebbero richiedere un po’ di tempo prima di comparire nelle sue risposte.
* **Quali applicazioni Adobe supporta l’Assistente IA in AEM?**\
  Attualmente, AI Assistant supporta le richieste di informazioni sulla conoscenza del prodotto in AEM as a Cloud Service, tra cui Sites, Assets, Dynamic Media, Cloud Manager e Forms.
* **Quali sono le funzionalità dell’Assistente IA in AEM?**\
  L’Assistente AI in AEM è progettato per rispondere a domande relative alla conoscenza del prodotto di Adobe.
* **L’Assistente IA in AEM utilizza informazioni personali per addestrare i dati?**\
  No. L’Assistente IA in AEM non utilizza informazioni personali a fini dell’addestramento. Evita di condividere informazioni personali su di te o su altre persone, inclusi nomi o dettagli di contatto.

<!--
IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

## AEM Forms AI Assistant (Forms Experience Builder) {#ai-forms-builder}

In addition to the general AI Assistant in AEM for product knowledge, AEM offers a specialized **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. This enhanced assistant can actively help you create and configure forms through natural language prompts and answer questions specific to forms.

### Key capabilities

The AEM Forms AI Assistant provides:

* **Form Creation**: Create new forms from scratch using natural language descriptions.
* **Design Import**: Convert existing designs (PDF, Figma, images) into functional AEM Forms. 
* **Form Configuration**: Add fields, panels, validation rules, and conditional logic.
* **Layout Management**: Organize form structure and optimize for different devices.
* **Integration Setup**: Configure form submissions and data handling.
* **Product Knowledge**: Answer questions about AEM Forms features and best practices.

### Where to access

The AEM Forms AI Assistant is available in the following:

* **Universal Editor**: For Edge Delivery Services forms with visual editing capabilities.
* **Adaptive Forms Editor**: For detailed form configuration and advanced features.
* **Forms Management UI**: For high-level form creation and management tasks.

### Getting started

>[!NOTE]
>
> The AEM Forms AI Assistant (Forms Experience Builder) is available under the private beta program. Send an email from your work address to [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) to request access.

To learn more about using the AEM Forms AI Assistant , see the [AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md) documentation.

### Example Use Cases

* **"Create a customer feedback form with name, email, rating, and comments fields"**
* **"Convert this uploaded PDF application form into a digital adaptive form"**  
* **"Add conditional logic to show spouse information only when marital status is 'Married'"**
* **"Configure this form to submit data to the Customer Relationship Management system"**

This specialized AEM Forms AI Assistant represents the next evolution in form building, combining the power of AI with AEM's robust forms capabilities to streamline your form creation workflow.
-->
