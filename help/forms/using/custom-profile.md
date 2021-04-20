---
title: Creazione di un profilo personalizzato per i moduli HTML5
seo-title: Creazione di un profilo personalizzato per i moduli HTML5
description: Un profilo di moduli HTML5 è un nodo di risorse in Apache Sling. Rappresenta una versione personalizzata del servizio di rendering dei moduli HTML5.
seo-description: Un profilo di moduli HTML5 è un nodo di risorse in Apache Sling. Rappresenta una versione personalizzata del servizio di rendering dei moduli HTML5.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---


# Creazione di un profilo personalizzato per i moduli HTML5 {#creating-a-custom-profile-for-html-forms}

Un profilo è un nodo di risorse in [Apache Sling](https://sling.apache.org/). Rappresenta la versione personalizzata del servizio di rendering dei moduli HTML5. È possibile utilizzare il servizio Rendering di moduli HTML5 per personalizzare l’aspetto, il comportamento e le interazioni dei moduli HTML5. Un nodo di profilo esiste nella cartella `/content` nell’archivio JCR. È possibile posizionare il nodo direttamente sotto la cartella `/content` o qualsiasi sottocartella della cartella `/content`.

Il nodo del profilo ha la proprietà **sling:resourceSuperType** e il valore predefinito è **xfaforms/profile**. Lo script di rendering per il nodo è in /libs/xfaforms/profile.

Gli script Sling sono script JSP. Questi script JSP fungono da contenitori per la creazione di contenuti HTML per il modulo richiesto e per gli artefatti JS / CSS richiesti. Questi script Sling sono anche indicati come **Script di rendering del profilo**. Il modulo di rendering del profilo chiama il servizio Forms OSGi per eseguire il rendering del modulo richiesto.

Lo script di profilo è in html.jsp e html.POST.jsp per le richieste di GET e POST. Puoi copiare e modificare uno o più file per sovrascrivere e aggiungere le tue personalizzazioni. Non apportare alcuna modifica diretta, l&#39;aggiornamento della patch sovrascrive tali modifiche.

Un profilo contiene vari moduli. I moduli sono formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp e footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

I moduli formRuntime.jsp contengono riferimenti delle librerie client. Vengono inoltre descritti i metodi per estrarre le informazioni sulle impostazioni internazionali dalla richiesta e includere nella richiesta i messaggi localizzati. È possibile includere librerie JavaScript personalizzate o stili in formRuntime.jsp.

## config.jsp {#config-jsp}

Il modulo config.jsp contiene varie configurazioni come registrazione, servizi proxy e versione comportamentale. Puoi aggiungere la tua configurazione e personalizzazione widget al modulo config.jsp. Puoi anche aggiungere configurazioni come la registrazione dei widget personalizzati al modulo config.jsp.

## toolbar.jsp {#toolbar-jsp}

La barra degli strumenti.jsp contiene codice per creare una barra degli strumenti colorata. Per rimuovere la barra degli strumenti, rimuovi toolbar.jsp da HTML.jsp

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

1. Copia il nodo predefinito e incolla il nodo in una cartella diversa (*/content/profiles*) con nome *hrform*.

1. Seleziona il nuovo nodo *hrform* e aggiungi una proprietà stringa: *sling:resourceType* con valore: *hrform/demo*.

1. Fai clic su Salva tutto nel menu della barra degli strumenti per salvare le modifiche.

### Creare lo script del renderer del profilo {#create-the-profile-renderer-script}

Dopo aver creato un profilo personalizzato, aggiungi le informazioni di rendering a questo profilo. Quando ricevi una richiesta per il nuovo profilo, CRX verifica l&#39;esistenza della cartella /apps per la pagina JSP da sottoporre a rendering. Crea la pagina JSP nella cartella /apps .

1. Nel riquadro a sinistra, passa alla cartella `/apps` .
1. Fai clic con il pulsante destro del mouse sulla cartella `/apps` e scegli di creare una cartella denominata **hrform**.
1. All&#39;interno della cartella **hrform** crea una cartella denominata **demo**.
1. Fare clic sul pulsante **Salva tutto**.
1. Passa a `/libs/xfaforms/profile/html.jsp` e copia il nodo **html.jsp**.
1. Incolla il nodo **html.jsp** nella cartella `/apps/hrform/demo` creata sopra con lo stesso nome **html.jsp** e fai clic su **Salva**.
1. Se hai altri componenti dello script di profilo, segui i passaggi 1-6 per copiare i componenti nella cartella /apps/hrform/demo .

1. Per verificare che il profilo sia stato creato, apri l’URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Per verificare i moduli, [Importa i moduli](/help/forms/using/get-xdp-pdf-documents-aem.md) dal file system locale in AEM Forms e [visualizza in anteprima il modulo](/help/forms/using/previewing-forms.md) nell&#39;istanza di authoring AEM server.
