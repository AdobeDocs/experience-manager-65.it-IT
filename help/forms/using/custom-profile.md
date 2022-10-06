---
title: Creazione di un profilo personalizzato per i moduli HTML5
seo-title: Creating a custom profile for HTML5 forms
description: Un profilo HTML5 forms è un nodo di risorse in Apache Sling. Rappresenta una versione personalizzata del servizio di rendering dei moduli di HTML5.
seo-description: A HTML5 forms profile is a resource node in Apache Sling. It represents a customized version of HTML5 forms Render service.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: Mobile Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Creazione di un profilo personalizzato per i moduli HTML5 {#creating-a-custom-profile-for-html-forms}

Un profilo è un nodo di risorsa in [Sling Apache](https://sling.apache.org/). Rappresenta la versione personalizzata del servizio di rendering dei moduli di HTML5. È possibile utilizzare il servizio Rendering dei moduli di HTML5 per personalizzare l’aspetto, il comportamento e le interazioni dei moduli di HTML5. Esiste un nodo di profilo nel `/content` nell’archivio JCR. Puoi posizionare il nodo direttamente sotto la `/content` o qualsiasi sottocartella del `/content` cartella.

Il nodo del profilo ha **sling:resourceSuperType** e il valore predefinito è **xfaforms/profile**. Lo script di rendering per il nodo è in /libs/xfaforms/profile.

Gli script Sling sono script JSP. Questi script JSP fungono da contenitori per la configurazione di HTML per il modulo richiesto e degli artefatti JS / CSS richiesti. Questi script Sling sono anche indicati come **Script del modulo di rendering del profilo**. Il modulo di rendering del profilo chiama il servizio Forms OSGi per eseguire il rendering del modulo richiesto.

Lo script di profilo è in html.jsp e html.POST.jsp per le richieste di GET e POST. Puoi copiare e modificare uno o più file per sovrascrivere e aggiungere le tue personalizzazioni. Non apportare alcuna modifica diretta, l&#39;aggiornamento della patch sovrascrive tali modifiche.

Un profilo contiene vari moduli. I moduli sono formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp e footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

I moduli formRuntime.jsp contengono riferimenti delle librerie client. Vengono inoltre descritti i metodi per estrarre le informazioni sulle impostazioni internazionali dalla richiesta e includere nella richiesta i messaggi localizzati. È possibile includere librerie JavaScript personalizzate o stili in formRuntime.jsp.

## config.jsp {#config-jsp}

Il modulo config.jsp contiene varie configurazioni come registrazione, servizi proxy e versione comportamentale. Puoi aggiungere la tua configurazione e personalizzazione widget al modulo config.jsp. Puoi anche aggiungere configurazioni come la registrazione dei widget personalizzati al modulo config.jsp.

## toolbar.jsp {#toolbar-jsp}

La barra degli strumenti.jsp contiene codice per creare una barra degli strumenti colorata. Per rimuovere la barra degli strumenti, rimuovere toolbar.jsp da HTML.jsp

## formBody.jsp {#formbody-jsp}

Il modulo formBody.jsp è per la rappresentazione HTML del modulo XFA.

## nav_footer.jsp {#nav-footer-jsp}

All’inizio, il modulo HTML5 esegue il rendering solo della prima pagina del modulo. Quando un utente scorre il modulo, viene caricato il resto dei moduli. Rende l&#39;esperienza di caricamento più veloce. Il componente nav_footer.jsp contiene tutti gli stili e gli elementi necessari per facilitare il caricamento delle pagine sullo scorrimento.

## footer.jsp {#footer-jsp}

Il modulo footer.jsp è vuoto. Consente di aggiungere script utilizzati solo per l’interazione con l’utente.

## Creazione di profili personalizzati {#creating-custom-profiles}

Per creare un profilo personalizzato, effettua le seguenti operazioni:

### Crea nodo profilo {#create-profile-node}

1. Passa all’interfaccia CRX DE all’URL: `https://'[server]:[port]'/crx/de` e accedi all&#39;interfaccia con le credenziali di amministratore.

1. Nel riquadro a sinistra, passa alla posizione */content/xfaforms/profiles*.

1. Copia il nodo predefinito e incolla il nodo in una cartella diversa (*/content/profiles*) con nome *forma*.

1. Seleziona il nuovo nodo, *forma* e aggiungi una proprietà stringa: *sling:resourceType* con valore: *hrform/demo*.

1. Fai clic su Salva tutto nel menu della barra degli strumenti per salvare le modifiche.

### Creare lo script del renderer del profilo {#create-the-profile-renderer-script}

Dopo aver creato un profilo personalizzato, aggiungi le informazioni di rendering a questo profilo. Quando ricevi una richiesta per il nuovo profilo, CRX verifica l&#39;esistenza della cartella /apps per la pagina JSP da sottoporre a rendering. Crea la pagina JSP nella cartella /apps .

1. Nel riquadro a sinistra, passa alla `/apps` cartella.
1. Fai clic con il pulsante destro del mouse sul pulsante `/apps` e scegliere di creare una cartella con il nome **forma**.
1. Insider **forma** creare una cartella denominata **demo**.
1. Fai clic sul pulsante **Salva tutto** pulsante .
1. Passa a `/libs/xfaforms/profile/html.jsp` e copia il nodo **html.jsp**.
1. Incolla **html.jsp** nel nodo `/apps/hrform/demo` cartella creata con lo stesso nome **html.jsp** e fai clic su **Salva**.
1. Se hai altri componenti dello script di profilo, segui i passaggi 1-6 per copiare i componenti nella cartella /apps/hrform/demo .

1. Per verificare che il profilo sia stato creato, apri URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Per verificare i moduli, [Importare i moduli](/help/forms/using/get-xdp-pdf-documents-aem.md) dal file system locale ad AEM Forms e [anteprima del modulo](/help/forms/using/previewing-forms.md) su AEM&#39;istanza di authoring del server.
