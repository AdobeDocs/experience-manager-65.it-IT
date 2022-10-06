---
title: Creare esperienze mirate in AEM Forms
seo-title: Create targeted experiences in AEM Forms
description: Utilizza Target in AEM Forms per creare esperienze personalizzate per clienti mirati.
seo-description: Use Target in AEM Forms to create customized experiences for targeted customers.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# Creare esperienze mirate in AEM Forms {#create-targeted-experiences-in-aem-forms}

## Integrare Adobe Target con AEM Forms {#integrate-adobe-target-with-aem-forms}

Adobe Target integrato con AEM consente di creare esperienze personalizzate per un pubblico specifico. Con Adobe Target puoi creare test A/B, misurare la risposta dell’utente e generare contenuti web personalizzati per gli utenti interessati. È possibile integrare Adobe Target con AEM Forms per indirizzare i componenti immagine di moduli adattivi e le comunicazioni interattive.

Configura Adobe Target in AEM per utilizzarlo con moduli adattivi e comunicazioni interattive, vedi [Creazione di una configurazione di destinazione in AEM](/help/sites-administering/target.md) e [Aggiungere un framework](/help/sites-administering/target.md).

>[!NOTE]
>
>Il targeting funziona quando viene eseguito il rendering del modulo adattivo o della comunicazione interattiva utilizzando un nome host o un indirizzo IP. Non riesce quando viene eseguito il rendering del modulo adattivo o della comunicazione interattiva utilizzando localhost.

## Creazione di un’attività Target {#creating-a-target-activity}

1. Tocca **Adobe Experience Manager > Personalizzazione > Attività**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. Nella pagina Attività , tocca **Crea > Crea marchio**.
1. Viene richiesto di scegliere un modello e di immettere le proprietà.

   Seleziona un modello, tocca **Avanti.** Immetti il titolo del brand nella sezione Proprietà e tocca **Crea.**
Il tuo marchio ora è elencato nella pagina Attività .

1. Tocca il tuo marchio nella pagina Attività .
1. Nell’area master del marchio, tocca **Crea** > **Crea attività**.

   Quando crei un’attività, specificane i dettagli, la destinazione e le impostazioni.

   La sezione Dettagli include nome, motore di destinazione e finalità. Quando selezioni Adobe Target come motore di destinazione, ottieni l’opzione di configurazione cloud di Target abilitata. Scegli la configurazione cloud di Target, scegli il tipo di attività, specifica l’obiettivo dell’attività e tocca **Successivo**. La comunicazione interattiva supporta solo il tipo di attività Targeting esperienze.

   La sezione Target ti consente di aggiungere un’esperienza di pubblico e denominarla. Fai clic su **Aggiungi esperienza** per abilitare **Selezionare il pubblico** e **Esperienza del nome** opzioni. Tocca **Selezionare il pubblico** per visualizzare un elenco dei tipi di pubblico e della relativa origine. Seleziona un pubblico dall&#39;elenco Nome pubblico . Tocca **Aggiungi esperienza** per denominare l’esperienza e tocca **Successivo**.

   La sezione Obiettivi e impostazioni ti consente di pianificare e assegnare una priorità all’attività. Imposta la data di inizio, la data di fine e la priorità dell’attività, della metrica di obiettivo, della metrica aggiuntiva e tocca **Salva**.

   L’attività è ora elencata nella pagina del tuo marchio.

   >[!NOTE]
   >
   >È possibile ignorare l’errore &quot;L’attività è stata salvata ma non è stata sincronizzata con Target. Motivo: L’esperienza seguente non ha offerte&quot;, se incontrata al momento del salvataggio dell’attività.

1. Per abilitare target, modifica il file .jsp in modo da includere le librerie client utilizzate dal modello di moduli adattivi.

   Ad esempio, nell’implementazione standard, fai clic su **Strumenti** >  **CRXDE Lite**.

   Nella barra degli indirizzi di CRXDE Lite, digita /libs/fd/af/components/page/base/head.jsp per modificare il file head.jsp.

   Questa implementazione utilizza un modello di iscrizione semplice. In questa implementazione, modifica il file head.jsp in modo da includere le seguenti librerie client:

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Per abilitare il framework di destinazione per i moduli adattivi, accedere al modulo o alla comunicazione interattiva e aprirlo in modalità di modifica.

   Per aprire un modulo o una comunicazione interattiva in modalità di modifica, tocca **Seleziona** quindi tocca **Apri**.

   In alternativa, quando si sposta il puntatore sull’icona del modulo o della comunicazione interattiva senza selezionarlo, vengono visualizzati quattro pulsanti. Puoi toccare il pulsante **Modifica** per aprire il modulo in modalità di modifica.

1. Nella barra degli strumenti della pagina, tocca **Informazioni pagina** ![theme-options](assets/theme-options.png) > **Apri proprietà**.
1. Nella scheda Generale , scegli una configurazione per **Adobe Target** campo . Tocca **Salva e chiudi**.

## Applicazione dell’attività creata a un’immagine di modulo adattivo o a un’immagine di comunicazione interattiva {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Apri il modulo adattivo e la comunicazione interattiva per la modifica. Se si apre una comunicazione interattiva, aprire il canale Web.

1. Nella modalità di creazione della comunicazione interattiva o del modulo adattivo, aggiungi un’immagine di destinazione.

   >[!NOTE]
   >
   >AEM Forms supporta il targeting solo dei componenti immagine. Assicurati che il pannello che ospita il componente immagine non contenga altri componenti e che il numero di colonne per il pannello sia impostato su 1.

1. Passa da **Modifica** a **Targeting** modalità. L&#39;opzione per cambiare modalità si trova nell&#39;angolo in alto a destra.
1. Seleziona una **MARCHIO**, seleziona **ATTIVITÀ**, e tocca **Avvia targeting**. La **Tipi di pubblico** sul lato destro dell’editor viene visualizzato il menu .

   ![menu di targeting](assets/targeting-menu.png)

1. Selezionare un pubblico dal **Tipi di pubblico** e tocca l’immagine di destinazione. Viene visualizzato un menu. Nel menu , tocca **Target**. Tocca l’immagine e tocca **Configura**. Nella finestra delle proprietà, seleziona l’immagine da visualizzare per il pubblico selezionato. Ripeti il passaggio per tutti i tipi di pubblico. Il targeting delle esperienze è abilitato per l’immagine nella comunicazione interattiva o nel modulo adattivo.

## Controlla se l&#39;attività creata si sincronizza con il server di Target {#check-if-the-created-activity-syncs-with-the-target-server}

Un’attività utilizzata per il targeting delle sincronizzazioni con il server di Target. Per verificare se l’attività è sincronizzata con il server di destinazione, controlla lo stato dell’attività nella pagina del brand.

Assicurati che lo stato dell’attività sia Sincronizzato.

## Convalidare il comportamento di Target {#validate-target-behavior}

Per convalidare il comportamento di Target:

* Utilizza il targeting con `wcmmode preview` in modalità di authoring
* Utilizza il targeting con `wcmmode preview` e `wcmmode disabled` in modalità di pubblicazione

## Monitorare il targeting per il componente immagine {#monitor-targeting-for-the-image-component}

Per monitorare il targeting dei componenti immagine sul modulo, pubblica immagini, attività e moduli adattivi.

## Problemi aperti {#open-issues}

Espressione di visibilità, impostazione dello stato attivo non riuscita per le immagini di destinazione sui moduli adattivi.
