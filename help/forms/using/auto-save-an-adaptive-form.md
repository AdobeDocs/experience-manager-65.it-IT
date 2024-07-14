---
title: Salvataggio automatico di un modulo adattivo
description: Puoi configurare un modulo adattivo in modo che inizi automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo predefinito
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components
exl-id: ff9bf466-228d-40e6-9389-15c1f2ed1d2e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Salvataggio automatico di un modulo adattivo {#auto-save-an-adaptive-form}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

Puoi configurare un modulo adattivo in modo che inizi automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo predefinito. Per impostazione predefinita, il contenuto di un modulo adattivo viene salvato durante un’azione dell’utente, ad esempio premendo il pulsante Salva. L’opzione di salvataggio automatico è utile in:

* Salvataggio automatico del contenuto per utenti anonimi e connessi
* Salvataggio del contenuto di un modulo senza o con un intervento minimo da parte dell&#39;utente
* Iniziare a salvare il contenuto di un modulo basato su un evento utente
* Salvataggio ripetuto del contenuto di un modulo dopo un intervallo di tempo specificato

## Abilitare il salvataggio automatico per un modulo adattivo {#enable-autosave-for-an-adaptive-form}

Per un modulo adattivo, l’opzione di salvataggio automatico non è attivata come opzione predefinita. Puoi abilitare l&#39;opzione di salvataggio automatico dalla sezione **Salvataggio automatico** nelle proprietà di un modulo adattivo. La sezione **Salvataggio automatico** fornisce anche diverse altre opzioni di configurazione. Per abilitare e configurare l’opzione di salvataggio automatico per un modulo adattivo, effettua le seguenti operazioni:

1. Per accedere alla sezione di salvataggio automatico nelle proprietà, seleziona un componente, quindi seleziona ![livello campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi seleziona ![cmppr](assets/cmppr.png).
1. Nella sezione **[!UICONTROL Salvataggio automatico]**, **[!UICONTROL Abilita]** l&#39;opzione di salvataggio automatico.
1. Nella casella **[!UICONTROL Evento modulo adattivo]**, specifica 1 o TRUE per iniziare automaticamente a salvare il modulo quando viene caricato nel browser. È inoltre possibile specificare un&#39;espressione condizionale per un evento che, quando viene attivato e restituisce true, inizia a salvare il contenuto del modulo.
1. Specifica il trigger. Il salvataggio automatico viene attivato in base alla configurazione. Le opzioni disponibili sono:

   * **[!UICONTROL In base al tempo:]** Selezionare l&#39;opzione per iniziare a salvare il contenuto in base a un intervallo di tempo specifico.
   * **[!UICONTROL Basato su evento:]** Selezionare l&#39;opzione per iniziare a salvare il contenuto in base all&#39;attivazione di un evento.

   Quando si seleziona un trigger, la casella Configurazione strategia (Strategy Configuration) viene attivata. La casella Configurazione strategia (Strategy Configuration) consente di:

   * Specificare un intervallo di tempo se si seleziona il trigger **[!UICONTROL Time based]**.
   * Specificare un nome evento se si seleziona il trigger **[!UICONTROL Basato su evento]**.

   Puoi anche creare e aggiungere all’elenco la tua strategia personalizzata. Per ulteriori dettagli, vedere [Implementare una strategia personalizzata per il salvataggio automatico dei moduli](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Solo salvataggio automatico basato sul tempo) Per configurare le opzioni per il salvataggio automatico basato sul tempo, effettuare le seguenti operazioni.

   1. Nella casella **[!UICONTROL Salvataggio automatico in questo intervallo]** specificare l&#39;intervallo di tempo in secondi. Il modulo viene salvato ripetutamente allo scadere del numero di secondi specificato nella casella Intervallo.

1. (Solo salvataggio automatico basato su eventi) Per configurare le opzioni per il salvataggio automatico basato su eventi, effettuare le seguenti operazioni.

   1. Nella casella **Salvataggio automatico dopo l&#39;evento** specificare un evento [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html). Il modulo viene salvato ogni volta che l’espressione restituisce TRUE.

1. (Facoltativo) Per salvare automaticamente il contenuto per utenti anonimi, selezionare l&#39;opzione **Abilita salvataggio automatico per utenti anonimi** e fare clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Affinché l&#39;opzione di salvataggio automatico funzioni per gli utenti anonimi, accertati di configurare il servizio Configurazione comune di Forms per consentire a tutti gli utenti di visualizzare in anteprima, verificare e firmare i moduli.
   >
   >Per configurare il servizio, passare alla configurazione della console Web AEM in `https://server:port/system/console/configMgr` e modificare il **[!UICONTROL Servizio di configurazione comune di Forms]** per scegliere l&#39;opzione **[!UICONTROL Tutti gli utenti]** nel campo **[!UICONTROL Consenti]** e salvare la configurazione.

## Implementare una strategia personalizzata per abilitare il salvataggio automatico per i moduli adattivi {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Puoi implementare un evento personalizzato per attivare la funzionalità di salvataggio automatico. Per creare e implementare l’evento personalizzato, effettua le seguenti operazioni:

1. Creare cartelle di librerie client e librerie client. Per i passaggi dettagliati, vedi il documento [Utilizzo di librerie lato client](/help/sites-developing/clientlibs.md).

   Ad esempio, lo script seguente utilizza l&#39;evento `emailFocusChange` personalizzato per attivare la funzionalità di salvataggio automatico:

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

1. In modalità di modifica, seleziona un componente, quindi seleziona ![livello campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi seleziona ![cmppr](assets/cmppr.png).
1. Nelle proprietà, apri la sezione **[!UICONTROL Base]**. Nella casella **[!UICONTROL Categoria libreria client]** immettere il valore della proprietà della categoria definita durante la creazione delle cartelle della libreria client.
1. Apri la sezione Salvataggio automatico. Nella casella **[!UICONTROL Salvataggio automatico dopo l&#39;evento]** specificare un evento personalizzato già definito nella libreria client. Fai clic su **[!UICONTROL OK]**.
