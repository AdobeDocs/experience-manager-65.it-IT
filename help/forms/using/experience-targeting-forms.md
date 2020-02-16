---
title: Creazione di esperienze mirate in AEM Forms
seo-title: Creazione di esperienze mirate in AEM Forms
description: Utilizzate Target in AEM Forms per creare esperienze personalizzate per i clienti interessati.
seo-description: Utilizzate Target in AEM Forms per creare esperienze personalizzate per i clienti interessati.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30

---


# Creazione di esperienze mirate in AEM Forms {#create-targeted-experiences-in-aem-forms}

## Integrazione di Adobe Target con AEM Forms {#integrate-adobe-target-with-aem-forms}

Adobe Target integrato con AEM consente di creare esperienze personalizzate per un pubblico target. Con Adobe Target puoi creare test A/B, misurare la risposta degli utenti e generare contenuto Web personalizzato per gli utenti interessati. Puoi integrare Adobe Target con AEM Forms per impostare come destinazione i componenti immagine di moduli adattivi e le comunicazioni interattive.

Configurate Adobe Target in AEM per utilizzarlo con moduli adattivi e comunicazioni interattive, consultate [Creazione di una configurazione Target in AEM](/help/sites-administering/target.md) e [Aggiunta di un framework](/help/sites-administering/target.md).

>[!NOTE]
>
>Il targeting funziona quando viene eseguito il rendering del modulo adattivo o della comunicazione interattiva utilizzando un nome host o un indirizzo IP. Non riesce se viene eseguito il rendering del modulo adattivo o della comunicazione interattiva utilizzando localhost.

## Creazione di un&#39;attività Target {#creating-a-target-activity}

1. Tocca **Adobe Experience Manager > Personalizzazione > Attività**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. Nella pagina Attività, toccate **Crea > Crea marchio**.
1. Viene chiesto di scegliere un modello e immettere le proprietà.

   Selezionate un modello, toccate **Avanti.** Immettete il titolo del marchio nella sezione Proprietà e toccate **Crea.**
Il tuo marchio ora è elencato nella pagina Attività.

1. Toccate il vostro marchio nella pagina Attività.
1. Nell&#39;area master del marchio, tocca **Crea** > **Crea attività**.

   Quando create un&#39;attività, specificate i relativi dettagli, target e impostazioni.

   La sezione Dettagli include nome, motore di targeting e obiettivo. Quando selezionate Adobe Target come motore di targeting, viene attivata l&#39;opzione di configurazione cloud Target. Scegliete la configurazione cloud di Target, scegliete il tipo di attività, fornite l&#39;obiettivo dell&#39;attività e toccate **Avanti**. La comunicazione interattiva supporta solo il tipo di attività Experience Targeting.

   La sezione Target consente di aggiungere un&#39;esperienza di audience e denominarla. Fate clic su **Aggiungi esperienza** per abilitare le opzioni **Seleziona audience** e **Nome esperienza** . Toccate **Seleziona audience** per visualizzare un elenco di tipi di pubblico e delle relative origini. Selezionate un&#39;audience dall&#39;elenco Nome audience. Toccate **Aggiungi esperienza** per denominare l&#39;esperienza, quindi toccate **Avanti**.

   La sezione Obiettivi e impostazioni consente di pianificare e assegnare priorità all&#39;attività. Impostate la data di inizio, la data di fine e la priorità dell&#39;attività, della metrica obiettivo, della metrica aggiuntiva e toccate **Salva**.

   L&#39;attività ora è elencata nella pagina del marchio.

   >[!NOTE]
   >
   >Potete ignorare l&#39;errore &quot;L&#39;attività è stata salvata ma non è stata sincronizzata con Target. Motivo: La seguente esperienza non include offerte&quot;, se incontrata durante il salvataggio dell&#39;attività.

1. Per abilitare la destinazione, modificare il file .jsp in modo da includere le librerie client utilizzate dal modello di moduli adattivi.

   Ad esempio, nell’implementazione standard, fate clic su **Strumenti** > **CRXDE Lite**.

   Nella barra degli indirizzi CRXDE Lite, digitate /libs/fd/af/components/page/base/head.jsp per modificare il file head.jsp.

   Questa implementazione utilizza un modello di iscrizione semplice. In questa implementazione, modificate il file head.jsp in modo da includere le seguenti librerie client:

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Per abilitare il framework di destinazione per i moduli adattivi, passare al modulo o alla comunicazione interattiva e aprirlo in modalità di modifica.

   Per aprire un modulo o una comunicazione interattiva in modalità di modifica, toccate **Seleziona** , quindi toccate **Apri**.

   In alternativa, quattro pulsanti vengono visualizzati quando si sposta il puntatore sull&#39;icona del modulo o della comunicazione interattiva senza selezionarla. È possibile toccare il pulsante **Modifica** visualizzato per aprire il modulo in modalità di modifica.

1. Nella barra degli strumenti della pagina, toccate Informazioni **** pagina - opzioni ![tema >](assets/theme-options.png) Apri proprietà ****.
1. Nella scheda Generale, scegli una configurazione per il campo **Adobe Target** . Toccate **Salva e chiudi**.

## Applicazione dell&#39;attività creata a un&#39;immagine modulo adattiva o a un&#39;immagine di comunicazione interattiva {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Aprire il modulo adattivo e la comunicazione interattiva per la modifica. Se state aprendo una comunicazione interattiva, aprite il canale Web.

1. Nella modalità di authoring della comunicazione interattiva o del modulo adattivo, aggiungere un’immagine di destinazione.

   >[!NOTE]
   >
   >AEM Forms supporta il targeting dei soli componenti immagine. Verificate che il pannello contenente il componente immagine non contenga altri componenti e che il numero di colonne del pannello sia impostato su 1.

1. Passa dalla modalità **Modifica** alla modalità **Impostazione destinazione** . L&#39;opzione per cambiare modalità è vicino all&#39;angolo in alto a destra.
1. Selezionate un **marchio**, selezionate **ATTIVITÀ** e toccate **Avvia targeting**. Il menu **Audience** viene visualizzato a destra dell&#39;editor.

   ![targeting-menu](assets/targeting-menu.png)

1. Selezionate un&#39;audience dal menu **Audiences** e toccate l&#39;immagine da usare come destinazione. Viene visualizzato un menu. Nel menu, toccate **Target**. Toccate l&#39;immagine e **selezionate Configura**. Nella finestra delle proprietà, selezionate l&#39;immagine da visualizzare per il pubblico selezionato. Ripetete il passaggio per tutte le audience. Il targeting delle esperienze è abilitato per l&#39;immagine nella comunicazione interattiva o nel modulo adattivo.

## Verificate che l&#39;attività creata sia sincronizzata con il server di Target {#check-if-the-created-activity-syncs-with-the-target-server}

Un&#39;attività utilizzata per eseguire il targeting delle sincronizzazioni con il server di Target. Per verificare se l&#39;attività è sincronizzata con il server di destinazione, controllate lo stato dell&#39;attività nella pagina del marchio.

Verificate che lo stato dell&#39;attività sia Sincronizzato.

## Convalidare il comportamento di Target {#validate-target-behavior}

Per convalidare il comportamento di Target:

* Utilizzare il targeting con `wcmmode preview` in modalità di creazione
* Utilizzare il targeting con `wcmmode preview` e `wcmmode disabled` in modalità di pubblicazione

## Monitorare la destinazione del componente immagine {#monitor-targeting-for-the-image-component}

Per monitorare il targeting dei componenti immagine sul modulo, pubblicare immagini, attività e moduli adattivi.

## Problemi aperti {#open-issues}

Espressione di visibilità, impostazione dello stato attivo non riuscita per le immagini di destinazione nei moduli adattivi.
