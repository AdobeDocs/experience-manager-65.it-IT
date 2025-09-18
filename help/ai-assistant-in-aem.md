---
title: Assistente AI in AEM 6.5
description: Utilizza l’Assistente IA per trovare risposte e risolvere eventuali problemi relativi alle soluzioni disponibili in Adobe Experience Manager.
solution: Experience Manager, Experience Manager 6.5
feature: Authoring, AI Assistant, AI Tools
role: Admin, Architect, Developer, User
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
source-git-commit: 646816ab50c432c86772c228878f8114854c320f
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 4%

---

# Assistente AI in AEM 6.5 {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>I clienti AEM 6.5 e AEM 6.5 LTS che non utilizzano Cloud Manager/Experience Hub devono contattare il proprio Customer Success Engineer di Adobe per richiedere l’accesso all’Assistente all’intelligenza artificiale.

L’Assistente AI in AEM 6.5/AEM 6.5 LTS offre un’interfaccia di conversazione progettata per semplificare la ricerca delle risposte alle query relative a Adobe Experience Manager. Consente di ottenere risposte immediate alle domande relative ai prodotti AEM (*disponibili per tutti gli utenti*) e automatizza la creazione di ticket di supporto (*disponibili per gli amministratori del supporto*).

L’Assistente AI supporta AEM as a Cloud Service, incluse le seguenti soluzioni:

* Pagina panoramica di Experience Hub
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


È direttamente incorporato in AEM e accessibile dall’interfaccia utente di AEM Experience Hub, Cloud Manager e authoring.

Il seguente video di 3 minuti e 39 secondi offre una guida dettagliata dell’Assistente AI in AEM.

>[!VIDEO](https://video.tv.adobe.com/v/3470363?learn=on&captions=ita)

## Accedere all’Assistente IA in AEM{#get-access}

Per concedere agli utenti l&#39;accesso all&#39;Assistente per l&#39;intelligenza artificiale in AEM, l&#39;amministratore di Adobe deve configurare le seguenti autorizzazioni personalizzate per i profili che richiedono l&#39;accesso in **Adobe Admin Console**:

* **Accesso all&#39;Assistente AI** - Autorizzazione a utilizzare l&#39;Assistente AI in AEM per conoscere il prodotto, consentendo agli utenti di porre domande relative al prodotto nella chat dell&#39;Assistente AI. Questa autorizzazione deve essere abilitata.
* **Accesso al supporto** - Gli utenti devono inoltre disporre dell&#39;autorizzazione per aprire i ticket di supporto, che richiede il ruolo di **Amministratore supporto**.

Le richieste di Assistente IA in AEM vengono autenticate tramite Adobe Identity Management Services (IMS). Per informazioni dettagliate, vedere [Panoramica dei servizi Adobe Identity Management](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf).

**Per accedere all&#39;Assistente di intelligenza artificiale in AEM:**

1. I clienti devono disporre di un accordo aggiuntivo per accedere alla maggior parte delle funzionalità basate sull’intelligenza artificiale e di gestione degli agenti in Adobe Experience Manager. Per ulteriori informazioni, contatta il rappresentante Adobe.

<!-- OLD STEP 1 [Customers must sign the Gen AI rider with Adobe](https://fieldreadiness-adobe.highspot.com/items/665f831c9f831b011aeda057#1). 

    The GenAI Rider is a legal agreement between a customer and Adobe, required to use most AI and agentic capabilities. Contact Adobe Customer Care to learn more. -->

1. L’amministratore di AEM configura l’Assistente AI per l’utilizzo all’interno dell’organizzazione. Consulta [Configurare l&#39;Assistente AI in AEM](/help/ai-assistant-in-aem-admin.md).

<!--
>[!IMPORTANT]
>Be sure you have reviewed and submitted the user agreement so Adobe can enable AI Assistant feature for you to test out and participate in the private beta program.
>
>For any questions, send an email to [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) from your email address associated with your Adobe ID. -->

## Ambito {#scope}

L’attuale ambito di applicazione dell’Assistente all’intelligenza artificiale in AEM si concentra sulla risposta alle domande sulla conoscenza del prodotto per AEMr. as a Cloud Service. Tale ambito comprende un sostegno globale per i settori chiave. <!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **Superfici**: disponibile in AEM Experience Hub, Interfaccia utente Author, Cloud Manager.
* **Funzionalità**: conoscenza del prodotto e primo intervento per la risoluzione dei problemi e la guida, creazione automatizzata di ticket di supporto e ricerca.
* **Valore**: consente di risparmiare tempo, accelerare l&#39;apprendimento e il time-to-value, ridurre la necessità di creare ticket di supporto manualmente e migliorare l&#39;efficienza nella creazione di ticket di supporto.

## Privacy, sicurezza e governance{#privacy-security-governance}

L’Assistente per l’intelligenza artificiale in AEM è progettato con una forte enfasi sulla privacy, la sicurezza e la governance.

Questo articolo illustra le funzioni basate sulla fiducia che possono essere attese dall’Assistente IA in AEM:

* Nessun dato personale viene utilizzato dall’Assistente IA in AEM, anche a scopo di formazione.
* L’Assistente AI in AEM non ha accesso ai dati dei consumatori.
* Per interagire con l’Assistente AI in AEM è necessaria un’autorizzazione esplicita.
* I prompt forniti dall’utente (domande, query e così via) non vengono condivisi con altri clienti.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## Scopri l’Assistente all’intelligenza artificiale in AEM per conoscere i prodotti e creare ticket di supporto automatizzato {#ai-prod-insights}

La conoscenza del prodotto include concetti e argomenti derivati dalla documentazione di Adobe Experience League. Queste domande possono essere suddivise nei seguenti sottogruppi:


| Conoscenza del prodotto | Disponibile per tutti gli utenti<br>Esempi |
| :--- | :--- |
| Apprendimento puntato | <ul><li>Cos’è Universal Editor?</li><li>Come si crea un programma in Cloud Manager?</li></ul> |
| Rilevamento aperto | <ul><li>Come si utilizza Universal Editor?</li><li>Esiste un modo per copiare il contenuto da un ambiente all’altro?</li></ul> |
| Risoluzione di problemi | <ul><li>Perché non è possibile accedere a Universal Editor?</li><li>Perché la pipeline non riesce?</li></ul> |
| **Creazione ticket di supporto** | **Disponibile solo per gli amministratori del supporto &#x200B;**<br>**Esempi** |
| Creazione automatizzata di ticket di supporto per acquisire la cronologia e il contesto delle chat dell’Assistente di intelligenza artificiale | <ul><li>Crea un ticket di supporto per me.</li></ul> |
| Recupera lo stato del ticket di supporto | <ul><li>Mostrami tutti i biglietti di supporto che ho aperto.</li><li>Mostra lo stato del biglietto &quot;E-----------&quot;</li></ul> |

{style="table-layout:auto"}


## Come creare domande efficaci {#ai-craft-questions}

Per ricevere le risposte più precise dall’Assistente AI in AEM, è importante formulare le domande con chiarezza e contesto. Utilizza i seguenti suggerimenti per garantire che le query siano chiare e ben strutturate:

* Dichiara chiaramente il tuo compito o domanda in modo conciso.
* Evita formulazioni ambigue o sintassi troppo complessa per migliorare la comprensione.
* Includi un contesto pertinente all’attività o alla domanda, in quanto questo approccio aiuta l’Assistente IA in AEM a fornire risposte più precise e pertinenti.
Ad esempio, quando viene richiesto, è utile assegnare un nome alla soluzione AEM in uso: Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager o Forms.

### Esempi di domande non supportate {#ai-unsupported-questions}

| Area | Esempi |
| --- | --- |
| Informazioni operative | <ul><li>Quanti ambienti di sviluppo esistono nel mio tenant?</li><li>Chi ha avviato l’ultima pipeline di produzione?</li></ul> |
| Risoluzione di problemi | <ul><li>Perché la pipeline di produzione non riesce?</li></ul> |
| Attività e automazione | <ul><li>Configura una pipeline di qualità del codice da un ramo di sviluppo.</li></ul> |


## Utilizzare l’Assistente AI in AEM {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### Avviare un Assistente AI nella conversazione AEM

È possibile reimpostare l&#39;Assistente AI in AEM e avviare una nuova conversazione quando si desidera modificare gli argomenti. Questa funzionalità è particolarmente utile quando si risolvono problemi relativi a query che hanno esito negativo o che forniscono informazioni non corrette.

**Per avviare un Assistente IA nella conversazione AEM:**

1. Fai clic sull&#39;icona **Assistente AI** nell&#39;angolo superiore destro dell&#39;interfaccia utente di AEM (dalle pagine di Cloud Manager o dall&#39;istanza di authoring degli ambienti AEM).

   ![Icona Assistente IA sulla barra degli strumenti](/help/assets/assets-ai/ai-assistant-icon.png)

1. Nella casella di testo del pannello **Assistente AI**, nella parte inferiore, digitare la domanda o il prompt, quindi premere `Enter` o fare clic sull&#39;icona ![Invia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   >[!NOTE]
   >
   >I dati personali non devono essere inclusi nei dati inseriti, in quanto non sono necessari per l’utilizzo di questo strumento.

   ![Casella di testo nella parte inferiore del pannello dell&#39;Assistente AI](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. Per avviare una nuova conversazione (nuovo argomento o modifica dell&#39;argomento), fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **Avvia nuova conversazione**.

   ![Avvia una nuova conversazione in Assistente IA dall&#39;icona con i puntini di sospensione](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### Scopri i prompt per categoria

L’Assistente AI in AEM include una funzione di individuazione che consente di esplorare gli argomenti e le categorie supportati.

**Per individuare le richieste per categoria:**

1. Nel pannello Assistente AI, fai clic sull&#39;icona ![Scopri](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg) per attivare il pannello di individuazione dei prompt.

   ![Pannello che consente di esplorare i prompt per categoria nell&#39;Assistente AI](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   *Pannello che mostra le categorie dei prompt nell&#39;Assistente di intelligenza artificiale.*

1. Selezionare una categoria per visualizzare un elenco di prompt correlati.
1. Seleziona un prompt per visualizzare esempi dei tipi di domande a cui l’Assistente AI può rispondere.

1. Per nascondere il pannello di individuazione dei prompt, fare di nuovo clic sull&#39;icona ![Informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).

### Condividi il tuo feedback su AI Assistant in AEM

Il tuo input consente ad Adobe di migliorare l’Assistente AI per migliorare le prestazioni e la precisione.

Condividi il tuo feedback sulla tua esperienza con l’Assistente AI in AEM tramite le seguenti opzioni:

![Miniature in alto, miniature in basso e icone dei flag](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| Clic | Descrizione |
| --- | --- |
| ![Icona Anteprima](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Indica cosa è andato bene e condividere feedback positivi. |
| ![Icona della struttura delle miniature](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Fornisci suggerimenti per migliorare. Aggiungi commenti specifici sulla tua esperienza, che vengono rivisti ogni giorno. |
| ![Icona contrassegno](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Segnala i dubbi o fornisci un feedback dettagliato sulla tua interazione con l’Assistente AI in AEM. |

## Domande frequenti sull’Assistente IA in AEM {#ai-faq}

Di seguito sono riportate le risposte ad alcune domande comuni sull’Assistente IA:

* **Le informazioni sono fornite dall&#39;Assistente IA in AEM in tempo reale?**\
  No. I contenuti dell’Assistente AI provengono dalla documentazione di Adobe Experience League. Gli aggiornamenti al contenuto potrebbero richiedere un po’ di tempo per essere riflessi nelle risposte.
* **Quali applicazioni Adobe sono supportate dall&#39;Assistente all&#39;intelligenza artificiale in AEM?**\
  Attualmente, AI Assistant supporta le richieste di informazioni sulla conoscenza del prodotto in AEM as a Cloud Service, tra cui Sites, Assets, Dynamic Media, Cloud Manager e Forms.
* **Quali sono le funzionalità dell&#39;Assistente all&#39;intelligenza artificiale in AEM?**\
  L’Assistente AI in AEM è progettato per rispondere a domande relative alla conoscenza dei prodotti Adobe.
* **L&#39;Assistente IA in AEM utilizza informazioni personali per i dati di formazione?**\
  No. L’Assistente AI in AEM non utilizza informazioni personali a scopo di formazione. Evita di condividere informazioni personali su di te o di altri, inclusi nomi o dettagli di contatto, con l’Assistente AI in AEM.

<!-- IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

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
