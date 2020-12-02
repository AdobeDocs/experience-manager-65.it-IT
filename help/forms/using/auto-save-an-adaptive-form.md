---
title: Salvataggio automatico di un modulo adattivo
seo-title: Salvataggio automatico di un modulo adattivo
description: È possibile configurare un modulo adattivo per avviare automaticamente il salvataggio del contenuto in base a un evento o a un intervallo di tempo predefinito
seo-description: È possibile configurare un modulo adattivo per avviare automaticamente il salvataggio del contenuto in base a un evento o a un intervallo di tempo predefinito
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# Salvataggio automatico di un modulo adattivo {#auto-save-an-adaptive-form}

È possibile configurare un modulo adattivo per avviare automaticamente il salvataggio del contenuto in base a un evento o a un intervallo di tempo predefinito. Per impostazione predefinita, il contenuto di un modulo adattivo viene salvato in seguito a un&#39;azione dell&#39;utente, ad esempio premendo il pulsante Salva. L’opzione di salvataggio automatico è utile in:

* Salvataggio automatico dei contenuti per utenti anonimi e connessi
* Salvataggio del contenuto di un modulo senza intervento da parte dell&#39;utente
* Avvio del salvataggio del contenuto di un modulo in base a un evento utente
* Salvataggio ripetuto del contenuto di un modulo dopo un intervallo di tempo specificato

## Abilita salvataggio automatico per un modulo adattivo {#enable-autosave-for-an-adaptive-form}

Per un modulo adattivo, l&#39;opzione di salvataggio automatico non è abilitata. È possibile abilitare l&#39;opzione di salvataggio automatico dalla sezione **Salvataggio automatico** nelle proprietà di un modulo adattivo. La sezione **Salvataggio automatico** offre anche diverse altre opzioni di configurazione. Per attivare e configurare l’opzione di salvataggio automatico per un modulo adattivo, effettuate le seguenti operazioni:

1. Per accedere alla sezione di salvataggio automatico nelle proprietà, selezionare un componente, quindi toccare ![livello campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi toccare ![cmppr](assets/cmppr.png).
1. Nella sezione **[!UICONTROL Salvataggio automatico]**, **[!UICONTROL Abilitare]** l&#39;opzione di salvataggio automatico.
1. Nella casella **[!UICONTROL Evento modulo adattivo]**, specificare 1 o TRUE per avviare automaticamente il salvataggio del modulo quando il modulo viene caricato nel browser. È inoltre possibile specificare un&#39;espressione condizionale per un evento che, quando viene attivato e restituisce true, inizia a salvare il contenuto del modulo.
1. Specifica l&#39;attivatore. Il salvataggio automatico viene attivato in base alla configurazione in uso. Le opzioni disponibili sono:

   * **[!UICONTROL Base temporale:]** selezionare l&#39;opzione per iniziare a salvare il contenuto in base a un intervallo di tempo specifico.
   * **[!UICONTROL Basato su evento:]** selezionare l&#39;opzione per avviare il salvataggio del contenuto in base all&#39;attivazione di un evento.

   Quando selezionate un attivatore, la casella Configurazione strategia è abilitata. La finestra Configurazione strategia consente di:

   * Specificare un intervallo di tempo se si seleziona il trigger **[!UICONTROL Time based]**.
   * Specificate un nome evento se selezionate l&#39;attivatore **[!UICONTROL basato sull&#39;evento]**.

   Potete anche creare e aggiungere all&#39;elenco una strategia personalizzata. Per informazioni dettagliate, vedere [Implementazione di una strategia personalizzata per l&#39;salvataggio automatico dei moduli](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Solo salvataggio automatico basato su tempo) Effettuate le seguenti operazioni per configurare le opzioni per l&#39;salvataggio automatico basato su tempo.

   1. Nella casella **[!UICONTROL Salvataggio automatico su questo intervallo]**, specificare l&#39;intervallo di tempo in secondi. Il modulo viene salvato ripetutamente dopo la scadenza del numero di secondi specificato nella casella di intervallo.

1. (Solo salvataggio automatico basato su eventi) Effettuate le seguenti operazioni per configurare le opzioni per il salvataggio automatico basato su eventi.

   1. Nella casella **Salvataggio automatico dopo questo evento**, specificare un evento [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html). Il modulo viene salvato ogni volta che l&#39;espressione restituisce TRUE.

1. (Facoltativo) Per salvare automaticamente il contenuto per gli utenti anonimi, selezionare l&#39;opzione **Abilita salvataggio automatico per utenti anonimi**, quindi fare clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Affinché l&#39;opzione di salvataggio automatico funzioni correttamente per gli utenti anonimi, è necessario configurare il servizio di configurazione comune di Forms in modo da consentire a tutti gli utenti di visualizzare in anteprima, verificare e firmare i moduli.
   >
   >Per configurare il servizio, andate AEM configurazione della console Web in `https://server:port/system/console/configMgr` e modificate il **[!UICONTROL servizio di configurazione comune Forms]** per scegliere l&#39;opzione **[!UICONTROL Tutti gli utenti]** nel campo **[!UICONTROL Consenti]** e salvate la configurazione.

## Implementare una strategia personalizzata per abilitare il salvataggio automatico per i moduli adattivi {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Potete implementare un evento personalizzato per attivare la funzionalità di salvataggio automatico. Per creare e implementare l&#39;evento personalizzato, effettuate le seguenti operazioni:

1. Creare cartelle libreria client e libreria client. Per i passaggi dettagliati, vedere il documento [Using Client-Side Libraries](/help/sites-developing/clientlibs.md).

   Ad esempio, lo script seguente utilizza l&#39;evento `emailFocusChange`personalizzato per attivare la funzionalità di salvataggio automatico:

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
   >Durante la creazione delle cartelle della libreria client viene definita una proprietà category. Mantenere a portata di mano il valore assegnato alla proprietà category.

1. Aprite il modulo adattivo in modalità di creazione.

1. In modalità di modifica, selezionate un componente, quindi toccate ![livello campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi toccate ![cmppr](assets/cmppr.png).
1. Nelle proprietà, aprire la sezione **[!UICONTROL Base]**. Nella casella **[!UICONTROL Categoria libreria client]**, immettere il valore della proprietà category definita durante la creazione delle cartelle libreria client.
1. Aprite la sezione Salvataggio automatico. Nella casella **[!UICONTROL Salvataggio automatico dopo questo evento]**, specificate un evento personalizzato già definito nella libreria client. Fai clic su **[!UICONTROL OK]**.

