---
title: Salvataggio automatico di un modulo adattivo
seo-title: Auto-save an adaptive form
description: Puoi configurare un modulo adattivo in modo che inizi automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo predefinito
seo-description: You can configure an adaptive form to automatically start saving the content based on an event or a pre-defined time-interval
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Adaptive Forms
exl-id: 948b2c12-895d-49e3-a943-d8fe87174fc4
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 1%

---

# Salvataggio automatico di un modulo adattivo {#auto-save-an-adaptive-form}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

Puoi configurare un modulo adattivo in modo che inizi automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo predefinito. Per impostazione predefinita, il contenuto di un modulo adattivo viene salvato durante un’azione dell’utente, ad esempio premendo il pulsante Salva. L’opzione di salvataggio automatico è utile in:

* Salvataggio automatico del contenuto per utenti anonimi e connessi
* Salvataggio del contenuto di un modulo senza o con un intervento minimo da parte dell&#39;utente
* Iniziare a salvare il contenuto di un modulo basato su un evento utente
* Salvataggio ripetuto del contenuto di un modulo dopo un intervallo di tempo specificato

## Abilitare il salvataggio automatico per un modulo adattivo {#enable-autosave-for-an-adaptive-form}

Per un modulo adattivo, l’opzione di salvataggio automatico non è attivata come opzione predefinita. È possibile abilitare l’opzione di salvataggio automatico da **Salvataggio automatico** nelle proprietà di un modulo adattivo. Il **Salvataggio automatico** fornisce anche diverse altre opzioni di configurazione. Per abilitare e configurare l’opzione di salvataggio automatico per un modulo adattivo, effettua le seguenti operazioni:

1. Per accedere alla sezione di salvataggio automatico nelle proprietà, seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi tocca ![cmppr](assets/cmppr.png).
1. In **[!UICONTROL Salvataggio automatico]** sezione, **[!UICONTROL Abilita]** opzione di salvataggio automatico.
1. In **[!UICONTROL Evento modulo adattivo]** , specificare 1 o TRUE per iniziare automaticamente a salvare il modulo al caricamento nel browser. È inoltre possibile specificare un&#39;espressione condizionale per un evento che, quando viene attivato e restituisce true, inizia a salvare il contenuto del modulo.
1. Specifica il trigger. Il salvataggio automatico viene attivato in base alla configurazione. Le opzioni disponibili sono:

   * **[!UICONTROL Basato su tempo:]** Seleziona l’opzione per iniziare a salvare il contenuto in base a un intervallo di tempo specifico.
   * **[!UICONTROL Basato su evento:]** Seleziona l’opzione per iniziare a salvare il contenuto in base a quando viene attivato un evento.

   Quando si seleziona un trigger, la casella Configurazione strategia (Strategy Configuration) viene attivata. La casella Configurazione strategia (Strategy Configuration) consente di:

   * Specifica un intervallo di tempo se selezioni **[!UICONTROL Basato su tempo]** trigger.
   * Specifica un nome evento se selezioni **[!UICONTROL Basato su evento]** trigger.

   Puoi anche creare e aggiungere all’elenco la tua strategia personalizzata. Per ulteriori informazioni, consulta [Implementare una strategia personalizzata per il salvataggio automatico dei moduli](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Solo salvataggio automatico basato sul tempo) Per configurare le opzioni per il salvataggio automatico basato sul tempo, effettuare le seguenti operazioni.

   1. In **[!UICONTROL Salva automaticamente in questo intervallo]** , specificare l&#39;intervallo di tempo in secondi. Il modulo viene salvato ripetutamente allo scadere del numero di secondi specificato nella casella Intervallo.

1. (Solo salvataggio automatico basato su eventi) Per configurare le opzioni per il salvataggio automatico basato su eventi, effettuare le seguenti operazioni.

   1. Nel mese **Salva automaticamente dopo questo evento** , specificare un [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) evento. Il modulo viene salvato ogni volta che l’espressione restituisce TRUE.

1. (Facoltativo) Per salvare automaticamente il contenuto per gli utenti anonimi, seleziona la **Abilita salvataggio automatico per utenti anonimi** e fai clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Affinché l&#39;opzione di salvataggio automatico funzioni per gli utenti anonimi, accertati di configurare il servizio Configurazione comune di Forms per consentire a tutti gli utenti di visualizzare in anteprima, verificare e firmare i moduli.
   >
   >Per configurare il servizio, vai alla configurazione della console web AEM all’indirizzo `https://server:port/system/console/configMgr` e modificare il **[!UICONTROL Servizio di configurazione comune di Forms]** per scegliere **[!UICONTROL Tutti gli utenti]** opzione in **[!UICONTROL Consenti]** e salva la configurazione.

## Implementare una strategia personalizzata per abilitare il salvataggio automatico per i moduli adattivi {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Puoi implementare un evento personalizzato per attivare la funzionalità di salvataggio automatico. Per creare e implementare l’evento personalizzato, effettua le seguenti operazioni:

1. Creare cartelle di librerie client e librerie client. Per i passaggi dettagliati, vedi [Utilizzo del documento Librerie lato client](/help/sites-developing/clientlibs.md).

   Ad esempio, lo script seguente utilizza il `emailFocusChange`evento per attivare la funzionalità di salvataggio automatico:

   ```javascript
   window.addEventListener("bridgeInitializeStart", function (){
       guideBridge.connect(function () { guideBridge.on("elementFocusChanged", function (event,data) {
           if(data.target.name === 'Email') {
               guideBridge.trigger("emailFocusChange");
           }
       });
      });
   });
   ```

   >[!NOTE]
   >
   >Durante la creazione delle cartelle della libreria client viene definita una proprietà di categoria. Mantieni a portata di mano il valore assegnato alla proprietà della categoria.

1. Apri il modulo adattivo in modalità di authoring.

1. In modalità di modifica, seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi tocca ![cmppr](assets/cmppr.png).
1. Nelle proprietà, apri la **[!UICONTROL Base]** sezione. In **[!UICONTROL Categoria libreria client]** immettere il valore della proprietà categoria definita durante la creazione delle cartelle della libreria client.
1. Apri la sezione Salvataggio automatico. In **[!UICONTROL Salva automaticamente dopo questo evento]** , specifica un evento personalizzato già definito nella libreria client. Fai clic su **[!UICONTROL OK]**.
