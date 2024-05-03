---
title: Creazione di un profilo personalizzato per i moduli HTML5
description: Un profilo HTML5 forms è un nodo di risorse in Apache Sling. Rappresenta una versione personalizzata del servizio HTML5 forms Render.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: HTML5 Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Creazione di un profilo personalizzato per i moduli HTML5 {#creating-a-custom-profile-for-html-forms}

Un profilo è un nodo di risorsa in [Apache Sling](https://sling.apache.org/). Rappresenta la versione personalizzata del servizio di rendering di HTML5 forms. È possibile utilizzare il servizio di rendering dei moduli HTML5 per personalizzare l&#39;aspetto, il comportamento e le interazioni dei moduli HTML5. In è presente un nodo di profilo `/content` nell’archivio JCR. Puoi posizionare il nodo direttamente sotto il `/content` cartella o una sottocartella di `/content` cartella.

Il nodo del profilo presenta **sling:resourceSuperType** e il valore predefinito è **xfaforms/profile**. Lo script di rendering per il nodo si trova in /libs/xfaforms/profile.

Gli script Sling sono script JSP. Questi script JSP fungono da contenitori per la creazione del HTML per il modulo richiesto e gli artefatti JS/CSS richiesti. Questi script Sling sono anche denominati **Script di rendering del profilo**. Il modulo di rendering dei profili chiama il servizio Forms OSGi per eseguire il rendering del modulo richiesto.

Lo script di profilo si trova in html.jsp e html.POST.jsp per le richieste GET e POST. Puoi copiare e modificare uno o più file per ignorare e aggiungere le personalizzazioni. Non apportare modifiche sul posto; tali modifiche vengono sovrascritte dall’aggiornamento della patch.

Un profilo contiene vari moduli. I moduli sono formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp e footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

I moduli formRuntime.jsp contengono riferimenti alle librerie client. Vengono inoltre illustrati i metodi per estrarre le informazioni sulle impostazioni internazionali dalla richiesta e includere i messaggi localizzati nella richiesta. Puoi includere libs o stili JavaScript personalizzati in formRuntime.jsp.

## config.jsp {#config-jsp}

Il modulo config.jsp contiene varie configurazioni come la registrazione, i servizi proxy e la versione del comportamento. Puoi aggiungere la tua configurazione e personalizzazione del widget al modulo config.jsp. Puoi anche aggiungere al modulo config.jsp configurazioni quali la registrazione di widget personalizzati.

## toolbar.jsp {#toolbar-jsp}

Il file toolbar.jsp contiene codice per creare una barra degli strumenti colorata. Per rimuovere la barra degli strumenti, rimuovere toolbar.jsp da HTML.jsp

## formBody.jsp {#formbody-jsp}

Il modulo formBody.jsp serve per la rappresentazione HTML del modulo XFA.

## nav_footer.jsp {#nav-footer-jsp}

Inizialmente, il modulo HTML5 esegue il rendering solo della prima pagina del modulo. Quando un utente fa scorrere il modulo, viene caricato il resto dei moduli. Rende l’esperienza di caricamento più veloce. Il componente nav_footer.jsp contiene tutti gli stili e gli elementi necessari per facilitare il caricamento delle pagine durante lo scorrimento.

## footer.jsp {#footer-jsp}

Il modulo footer.jsp è vuoto. Ti consente di aggiungere script utilizzati solo per l’interazione dell’utente.

## Creazione di profili personalizzati {#creating-custom-profiles}

Per creare un profilo personalizzato, effettua le seguenti operazioni:

### Crea nodo profilo {#create-profile-node}

1. Passa all’interfaccia CRX DE all’URL: `https://'[server]:[port]'/crx/de` e accedi all’interfaccia di con le credenziali di amministratore.

1. Nel riquadro a sinistra, passa alla posizione */content/xfaforms/profiles*.

1. Copia il nodo predefinito e incolla il nodo in una cartella diversa (*/content/profiles*) con nome *hardware*.

1. Seleziona il nuovo nodo, *hardware* e aggiungi una proprietà stringa: *sling:resourceType* con valore: *hrform/demo*.

1. Fare clic su Salva tutto nel menu della barra degli strumenti per salvare le modifiche.

### Creare lo script del renderer del profilo {#create-the-profile-renderer-script}

Dopo aver creato un profilo personalizzato, aggiungi le informazioni di rendering a questo profilo. Quando riceve una richiesta per il nuovo profilo, CRX verifica l’esistenza della cartella /apps per la pagina JSP di cui eseguire il rendering. Crea la pagina JSP nella cartella /apps.

1. Nel riquadro a sinistra, passare alla `/apps` cartella.
1. Fare clic con il pulsante destro del mouse `/apps` e scegliere di creare una cartella denominata **hardware**.
1. Insider **hardware** cartella creare una cartella denominata **demo**.
1. Fai clic su **Salva tutto** pulsante.
1. Accedi a `/libs/xfaforms/profile/html.jsp` e copia il nodo **html.jsp**.
1. Incolla **html.jsp** nodo in `/apps/hrform/demo` cartella creata sopra con lo stesso nome **html.jsp** e fai clic su **Salva**.
1. Se hai altri componenti dello script di profilo, segui i passaggi 1-6 per copiare i componenti nella cartella /apps/hrform/demo.

1. Per verificare che il profilo sia stato creato, apri l’URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Per verificare i moduli: [Importare i moduli](/help/forms/using/get-xdp-pdf-documents-aem.md) dal file system locale ad AEM Forms e [visualizzare l’anteprima del modulo](/help/forms/using/previewing-forms.md) nell’istanza di authoring del server AEM.
