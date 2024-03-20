---
title: Creare esperienze mirate in AEM Forms
description: Utilizza Target in AEM Forms per creare esperienze personalizzate per i clienti di destinazione.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Creare esperienze mirate in AEM Forms {#create-targeted-experiences-in-aem-forms}

## Integrare Adobe Target con AEM Forms {#integrate-adobe-target-with-aem-forms}

Adobe Target integrato con AEM consente di creare esperienze personalizzate per un pubblico specifico. Con Adobe Target, puoi creare test A/B, misurare la risposta degli utenti e generare contenuti web personalizzati per gli utenti di destinazione. È possibile integrare Adobe Target con AEM Forms per eseguire il targeting dei componenti immagine dei moduli adattivi e delle comunicazioni interattive.

Configura Adobe Target nell’AEM per utilizzarlo con moduli adattivi e comunicazioni interattive, consulta [Creazione di una configurazione di destinazione in AEM](/help/sites-administering/target.md) e [Aggiungere un framework](/help/sites-administering/target.md).

>[!NOTE]
>
>Il targeting funziona quando viene eseguito il rendering del modulo adattivo o della comunicazione interattiva utilizzando un nome host o un indirizzo IP. Ha esito negativo quando viene eseguito il rendering del modulo adattivo o della comunicazione interattiva tramite localhost.

## Creazione di un’attività Target {#creating-a-target-activity}

1. Seleziona **Adobe Experience Manager > Personalizzazione > Attività**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. Nella pagina Attività, seleziona **Crea > Crea marchio**.
1. Viene chiesto di scegliere un modello e di immettere le proprietà.

   Seleziona un modello, seleziona **Avanti.** Immetti il titolo del brand nella sezione Proprietà e seleziona **Crea.**
Il tuo marchio è ora elencato nella pagina Attività.

1. Seleziona il brand nella pagina Attività.
1. Nell’area master del tuo marchio, seleziona **Crea** > **Crea attività**.

   Quando crei un’attività di, ne specifichi i dettagli, la destinazione e le impostazioni.

   La sezione Dettagli include nome, motore di targeting e obiettivo. Quando selezioni Adobe Target come motore di targeting, l’opzione di configurazione cloud di Target è abilitata. Scegli la configurazione cloud di Target, scegli il tipo di attività, specifica l’obiettivo dell’attività e seleziona **Successivo**. La comunicazione interattiva supporta solo il tipo di attività Targeting esperienza.

   La sezione Target ti consente di aggiungere un’esperienza di pubblico e di denominarla. Clic **Aggiungi esperienza** per attivare **Seleziona pubblico** e **Nome esperienza** opzioni. Seleziona **Seleziona pubblico** per visualizzare un elenco dei tipi di pubblico e delle relative sorgenti. Seleziona un pubblico dall’elenco Nome pubblico. Seleziona **Aggiungi esperienza** per assegnare un nome all’esperienza e selezionarla **Successivo**.

   La sezione Obiettivi e impostazioni consente di pianificare e assegnare la priorità all’attività. Imposta la data di inizio, la data di fine e la priorità dell’attività, la metrica obiettivo, la metrica aggiuntiva e seleziona **Salva**.

   L’attività è ora elencata nella pagina del tuo marchio.

   >[!NOTE]
   >
   >È possibile ignorare l’errore &quot;L’attività è stata salvata ma non è stata sincronizzata con Target. Motivo: la seguente esperienza non ha offerte&quot;, se riscontrata durante il salvataggio dell’attività.

1. Per abilitare Target, modifica il file .jsp per includere le librerie client utilizzate dal modello di moduli adattivi.

   Ad esempio, nell’implementazione predefinita, fai clic su **Strumenti** >  **CRXDE Liti**.

   Nella barra degli indirizzi di CRXDE Liti, digita /libs/fd/af/components/page/base/head.jsp per modificare il file head.jsp.

   Questa implementazione utilizza il modello simpleEnrollment. In questa implementazione, modifica il file head.jsp per includere le seguenti librerie client:

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Per abilitare il framework di destinazione per i moduli adattivi, passa al modulo o alla comunicazione interattiva e aprilo in modalità di modifica.

   Per aprire un modulo o una comunicazione interattiva in modalità di modifica, seleziona **Seleziona** e quindi seleziona **Apri**.

   In alternativa, quando si sposta il puntatore sul modulo o sull&#39;icona di comunicazione interattiva senza selezionarlo, vengono visualizzati quattro pulsanti. È possibile selezionare **Modifica** per aprire il modulo in modalità di modifica.

1. Nella barra degli strumenti della pagina, seleziona **Informazioni pagina** ![theme-options](assets/theme-options.png) > **Apri proprietà**.
1. Nella scheda Generale, scegli una configurazione per **Adobe Target** campo. Seleziona **Salva e chiudi**.

## Applicazione dell’attività creata a un’immagine di modulo adattivo o a un’immagine di comunicazione interattiva {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Apri il modulo adattivo e la comunicazione interattiva per la modifica. Se stai aprendo una comunicazione interattiva, apri il canale web.

1. Nella modalità di authoring della comunicazione interattiva o del modulo adattivo, aggiungi un’immagine di destinazione.

   >[!NOTE]
   >
   >AEM Forms supporta il targeting solo dei componenti immagine. Assicurati che il pannello che ospita il componente immagine non contenga altri componenti e che il numero di colonne per il pannello sia impostato su 1.

1. Passa da **Modifica** a **Targeting** modalità. L’opzione per cambiare modalità è vicina all’angolo in alto a destra.
1. Seleziona un **MARCHIO**, seleziona **ATTIVITÀ**, e seleziona **Inizia impostazione destinazione**. Il **Tipi di pubblico** viene visualizzato sul lato destro dell&#39;editor.

   ![targeting-menu](assets/targeting-menu.png)

1. Selezionare un pubblico da **Tipi di pubblico** e selezionare l&#39;immagine di destinazione. Viene visualizzato un menu. Nel menu, seleziona **Target**. Seleziona l’immagine e seleziona **Configura**. Nella finestra delle proprietà, seleziona l’immagine da visualizzare per il pubblico selezionato. Ripeti il passaggio per tutti i tipi di pubblico. Il targeting dell’esperienza è abilitato per l’immagine nella comunicazione interattiva o nel modulo adattivo.

## Controlla se l’attività creata si sincronizza con il server Target {#check-if-the-created-activity-syncs-with-the-target-server}

Un’attività utilizzata per il targeting si sincronizza con il server Target. Per verificare se l’attività è sincronizzata con il server di destinazione, controlla lo stato dell’attività nella pagina del brand.

Assicurati che lo stato dell’attività sia Sincronizzato.

## Convalidare il comportamento di Target {#validate-target-behavior}

Per convalidare il comportamento di Target:

* Utilizzare il targeting con `wcmmode preview` in modalità di authoring
* Utilizzare il targeting con `wcmmode preview` e `wcmmode disabled` nella modalità di pubblicazione

## Targeting del monitor per il componente immagine {#monitor-targeting-for-the-image-component}

Per monitorare il targeting dei componenti immagine nel modulo, pubblica le immagini, le attività e il modulo adattivo.

## Problemi aperti {#open-issues}

Espressione di visibilità, attivazione del set non riuscita per le immagini di destinazione nei moduli adattivi.
