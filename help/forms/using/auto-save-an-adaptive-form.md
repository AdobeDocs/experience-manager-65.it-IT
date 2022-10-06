---
title: Salvataggio automatico di un modulo adattivo
seo-title: Auto-save an adaptive form
description: È possibile configurare un modulo adattivo per iniziare automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo predefinito
seo-description: You can configure an adaptive form to automatically start saving the content based on an event or a pre-defined time-interval
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Adaptive Forms
exl-id: 948b2c12-895d-49e3-a943-d8fe87174fc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Salvataggio automatico di un modulo adattivo {#auto-save-an-adaptive-form}

È possibile configurare un modulo adattivo per iniziare automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo predefinito. Per impostazione predefinita, il contenuto di un modulo adattivo viene salvato in seguito a un’azione dell’utente, ad esempio premendo il pulsante salva. L’opzione di salvataggio automatico è utile in:

* Salvataggio automatico del contenuto per utenti anonimi e connessi
* Salvataggio del contenuto di un modulo senza o con intervento minimo dell’utente
* Inizio del salvataggio del contenuto di un modulo in base a un evento utente
* Salvataggio ripetuto del contenuto di un modulo dopo un intervallo di tempo specificato

## Abilitare il salvataggio automatico per un modulo adattivo {#enable-autosave-for-an-adaptive-form}

Per un modulo adattivo, l’opzione di salvataggio automatico non è abilitata. Puoi abilitare l’opzione di salvataggio automatico dal **Salvataggio automatico** nelle proprietà di un modulo adattivo. La **Salvataggio automatico** fornisce anche diverse altre opzioni di configurazione. Esegui i seguenti passaggi per abilitare e configurare l’opzione di salvataggio automatico per un modulo adattivo:

1. Per accedere alla sezione di salvataggio automatico nelle proprietà, seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **[!UICONTROL Contenitore di moduli adattivi]**, quindi tocca ![cmppr](assets/cmppr.png).
1. In **[!UICONTROL Salvataggio automatico]** sezione **[!UICONTROL Abilita]** l’opzione di salvataggio automatico.
1. In **[!UICONTROL Evento modulo adattivo]** specificare 1 o TRUE per iniziare automaticamente a salvare il modulo quando il modulo viene caricato nel browser. È inoltre possibile specificare un&#39;espressione condizionale per un evento che, quando attivato e restituito vero, inizia a salvare il contenuto del modulo.
1. Specifica il trigger. Il salvataggio automatico viene attivato in base alla configurazione. Le opzioni disponibili sono:

   * **[!UICONTROL Basato sul tempo:]** Seleziona l’opzione per iniziare a salvare il contenuto in base a un intervallo di tempo specifico.
   * **[!UICONTROL Basato su evento:]** Seleziona l’opzione per iniziare a salvare il contenuto in base all’attivazione di un evento.

   Quando selezioni un trigger, la casella Configurazione strategia è abilitata. La casella Configurazione strategia consente di:

   * Specifica un intervallo di tempo se selezioni **[!UICONTROL Basato sul tempo]** attivatore.
   * Specifica un nome evento se selezioni **[!UICONTROL Basato su eventi]** attivatore.

   Puoi anche creare e aggiungere all’elenco una strategia personalizzata. Per maggiori dettagli, vedi [Implementare una strategia personalizzata per l’salvataggio automatico dei moduli](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Solo salvataggio automatico basato su tempo) Esegui i seguenti passaggi per configurare le opzioni per l’salvataggio automatico basato su tempo.

   1. In **[!UICONTROL Salvataggio automatico in questo intervallo]** specificare l&#39;intervallo di tempo in secondi. Il modulo viene salvato ripetutamente dopo la scadenza del numero di secondi specificato nella casella Intervallo.

1. (Solo salvataggio automatico basato su eventi) Esegui i seguenti passaggi per configurare le opzioni per il salvataggio automatico basato su eventi.

   1. In **Salvataggio automatico dopo questo evento** specificare un [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) evento. Il modulo viene salvato ogni volta che l’espressione restituisce TRUE.

1. (Facoltativo) Per salvare automaticamente il contenuto per gli utenti anonimi, seleziona la **Abilita salvataggio automatico per utenti anonimi** e fai clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Affinché l’opzione di salvataggio automatico funzioni per gli utenti anonimi, è necessario configurare il servizio di configurazione comune di Forms per consentire a tutti gli utenti di visualizzare in anteprima, verificare e firmare i moduli.
   >
   >Per configurare il servizio, vai AEM configurazione della console Web in `https://server:port/system/console/configMgr` e modifica le **[!UICONTROL Servizio di configurazione comune Forms]** per scegliere **[!UICONTROL Tutti gli utenti]** in **[!UICONTROL Consenti]** e salva la configurazione.

## Implementare una strategia personalizzata per abilitare il salvataggio automatico dei moduli adattivi {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Puoi implementare un evento personalizzato per attivare la funzionalità di salvataggio automatico. Esegui i seguenti passaggi per creare e implementare l’evento personalizzato:

1. Crea cartelle libreria client e libreria client. Per i passaggi dettagliati, vedi [Utilizzo del documento Librerie lato client](/help/sites-developing/clientlibs.md).

   Ad esempio, lo script seguente utilizza l&#39;impostazione personalizzata `emailFocusChange`per attivare la funzionalità di salvataggio automatico:

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

1. Apri il modulo adattivo in modalità di creazione.

1. In modalità di modifica, seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **[!UICONTROL Contenitore di moduli adattivi]**, quindi tocca ![cmppr](assets/cmppr.png).
1. Nelle proprietà, apri la **[!UICONTROL Base]** sezione . In **[!UICONTROL Categoria libreria client]** immettere il valore della proprietà category definita durante la creazione delle cartelle della libreria client.
1. Apri la sezione Salvataggio automatico . In **[!UICONTROL Salvataggio automatico dopo questo evento]** specifica un evento personalizzato già definito nella libreria client. Fai clic su **[!UICONTROL OK]**.
