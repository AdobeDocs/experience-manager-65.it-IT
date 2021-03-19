---
title: Salvataggio automatico di un modulo adattivo
seo-title: Salvataggio automatico di un modulo adattivo
description: È possibile configurare un modulo adattivo per iniziare automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo predefinito
seo-description: È possibile configurare un modulo adattivo per iniziare automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo predefinito
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Moduli adattivi
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---


# Salvataggio automatico di un modulo adattivo {#auto-save-an-adaptive-form}

È possibile configurare un modulo adattivo per iniziare automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo predefinito. Per impostazione predefinita, il contenuto di un modulo adattivo viene salvato in seguito a un’azione dell’utente, ad esempio premendo il pulsante salva. L’opzione di salvataggio automatico è utile in:

* Salvataggio automatico del contenuto per utenti anonimi e connessi
* Salvataggio del contenuto di un modulo senza o con intervento minimo dell’utente
* Inizio del salvataggio del contenuto di un modulo in base a un evento utente
* Salvataggio ripetuto del contenuto di un modulo dopo un intervallo di tempo specificato

## Abilitare il salvataggio automatico per un modulo adattivo {#enable-autosave-for-an-adaptive-form}

Per un modulo adattivo, l’opzione di salvataggio automatico non è abilitata. È possibile abilitare l’opzione di salvataggio automatico dalla sezione **Salvataggio automatico** nelle proprietà di un modulo adattivo. La sezione **Salvataggio automatico** fornisce anche diverse altre opzioni di configurazione. Esegui i seguenti passaggi per abilitare e configurare l’opzione di salvataggio automatico per un modulo adattivo:

1. Per accedere alla sezione di salvataggio automatico nelle proprietà, seleziona un componente, quindi tocca ![livello campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi tocca ![cmppr](assets/cmppr.png).
1. Nella sezione **[!UICONTROL Salvataggio automatico]**, **[!UICONTROL Abilita]** l&#39;opzione di salvataggio automatico.
1. Nella casella **[!UICONTROL Evento modulo adattivo]**, specificare 1 o TRUE per iniziare automaticamente il salvataggio del modulo quando il modulo viene caricato nel browser. È inoltre possibile specificare un&#39;espressione condizionale per un evento che, quando attivato e restituito vero, inizia a salvare il contenuto del modulo.
1. Specifica il trigger. Il salvataggio automatico viene attivato in base alla configurazione. Le opzioni disponibili sono:

   * **[!UICONTROL Basato su tempo:]** seleziona l’opzione per iniziare a salvare il contenuto in base a un intervallo di tempo specifico.
   * **[!UICONTROL Basato su evento:]** seleziona l’opzione per iniziare a salvare il contenuto in base all’attivazione di un evento.

   Quando selezioni un trigger, la casella Configurazione strategia è abilitata. La casella Configurazione strategia consente di:

   * Specificare un intervallo di tempo se si seleziona il trigger **[!UICONTROL Time based]**.
   * Specifica un nome evento se selezioni il trigger **[!UICONTROL Basato su evento]** .

   Puoi anche creare e aggiungere all’elenco una strategia personalizzata. Per informazioni dettagliate, vedere [Implementare una strategia personalizzata per l&#39;salvataggio automatico dei moduli](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Solo salvataggio automatico basato su tempo) Esegui i seguenti passaggi per configurare le opzioni per l’salvataggio automatico basato su tempo.

   1. Nella casella **[!UICONTROL Salvataggio automatico in questo intervallo]**, specificare l&#39;intervallo di tempo in secondi. Il modulo viene salvato ripetutamente dopo la scadenza del numero di secondi specificato nella casella Intervallo.

1. (Solo salvataggio automatico basato su eventi) Esegui i seguenti passaggi per configurare le opzioni per il salvataggio automatico basato su eventi.

   1. Nella casella **Salvataggio automatico dopo questo evento**, specificare un evento [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html). Il modulo viene salvato ogni volta che l’espressione restituisce TRUE.

1. (Facoltativo) Per salvare automaticamente il contenuto per gli utenti anonimi, selezionare l&#39;opzione **Abilita salvataggio automatico per utenti anonimi** e fare clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Affinché l’opzione di salvataggio automatico funzioni per gli utenti anonimi, è necessario configurare il servizio di configurazione comune di Forms per consentire a tutti gli utenti di visualizzare in anteprima, verificare e firmare i moduli.
   >
   >Per configurare il servizio, accedi AEM configurazione della console Web in `https://server:port/system/console/configMgr` e modifica il **[!UICONTROL Servizio di configurazione comune Forms]** per scegliere l&#39;opzione **[!UICONTROL Tutti gli utenti]** nel campo **[!UICONTROL Consenti]** e salvare la configurazione.

## Implementare una strategia personalizzata per abilitare il salvataggio automatico dei moduli adattivi {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Puoi implementare un evento personalizzato per attivare la funzionalità di salvataggio automatico. Esegui i seguenti passaggi per creare e implementare l’evento personalizzato:

1. Crea cartelle libreria client e libreria client. Per passaggi dettagliati, consulta il documento [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md).

   Ad esempio, lo script seguente utilizza l&#39;evento personalizzato `emailFocusChange`per attivare la funzionalità di salvataggio automatico:

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

1. In modalità di modifica, seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi tocca ![cmppr](assets/cmppr.png).
1. Nelle proprietà, apri la sezione **[!UICONTROL Base]** . Nella casella **[!UICONTROL Categoria libreria client]**, immettere il valore della proprietà categoria definita durante la creazione delle cartelle libreria client.
1. Apri la sezione Salvataggio automatico . Nella casella **[!UICONTROL Salvataggio automatico dopo questo evento]** , specifica un evento personalizzato già definito nella libreria client. Fai clic su **[!UICONTROL OK]**.

