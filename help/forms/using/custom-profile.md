---
title: Creazione di un profilo personalizzato per i moduli HTML5
seo-title: Creazione di un profilo personalizzato per i moduli HTML5
description: Un profilo di moduli HTML5 è un nodo di risorse in Apache Sling. Rappresenta una versione personalizzata del servizio di rendering moduli HTML5.
seo-description: Un profilo di moduli HTML5 è un nodo di risorse in Apache Sling. Rappresenta una versione personalizzata del servizio di rendering moduli HTML5.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Creazione di un profilo personalizzato per i moduli HTML5 {#creating-a-custom-profile-for-html-forms}

Un profilo è un nodo di risorse in [Apache Sling](https://sling.apache.org/). Rappresenta la versione personalizzata del servizio di rappresentazione moduli HTML5. È possibile utilizzare il servizio di rappresentazione moduli HTML5 per personalizzare l’aspetto, il comportamento e le interazioni dei moduli HTML5. Un nodo di profilo esiste nella `/content` cartella nell&#39;archivio JCR. Potete posizionare il nodo direttamente sotto la `/content` cartella o in qualsiasi sottocartella della `/content` cartella.

Il nodo del profilo ha la proprietà **sling:resourceSuperType** e il valore predefinito è **xfaforms/profile**. Lo script di rendering per il nodo si trova in /libs/xfaforms/profile.

Gli script Sling sono script JSP. Questi script JSP fungono da contenitori per l&#39;assemblaggio dell&#39;HTML per il modulo richiesto e degli artefatti JS / CSS richiesti. Questi script Sling sono denominati anche script **di rendering** profilo. Il renderer di profili richiama il servizio Forms OSGi per eseguire il rendering del modulo richiesto.

Lo script di profilo è in html.jsp e html.POST.jsp per le richieste GET e POST. Potete copiare e modificare uno o più file per sovrascrivere e aggiungere le personalizzazioni. Non apportate alcuna modifica, l’aggiornamento della patch sovrascrive tali modifiche.

Un profilo contiene vari moduli. I moduli sono formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_piè.jsp e piè di pagina.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

I moduli formRuntime.jsp contengono riferimenti delle librerie client. Inoltre, mostra i metodi per estrarre le informazioni sulle impostazioni internazionali dalla richiesta e includere i messaggi localizzati nella richiesta. È possibile includere libs o stili JavaScript personalizzati in formRuntime.jsp.

## config.jsp {#config-jsp}

Il modulo config.jsp contiene diverse configurazioni come registrazione, servizi proxy e versione di comportamento. Puoi aggiungere la tua configurazione e personalizzazione widget al modulo config.jsp. Potete inoltre aggiungere al modulo config.jsp configurazioni come la registrazione dei widget personalizzati.

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp contiene codice per creare una barra degli strumenti colorata. Per rimuovere la barra degli strumenti, rimuovere toolbar.jsp da HTML.jsp

## formBody.jsp {#formbody-jsp}

Il modulo formBody.jsp è destinato alla rappresentazione HTML del modulo XFA.

## nav_footer.jsp {#nav-footer-jsp}

Inizialmente, il modulo HTML5 esegue il rendering solo della prima pagina del modulo. Quando un utente scorre il modulo, viene caricato il resto dei moduli. Rende l&#39;esperienza di caricamento più veloce. Il componente nav_piè.jsp contiene tutti gli stili e gli elementi necessari per facilitare il caricamento delle pagine sullo scorrimento.

## footer.jsp {#footer-jsp}

Il modulo piè di pagina.jsp è vuoto. Consente di aggiungere script utilizzati solo per l&#39;interazione con l&#39;utente.

## Creazione di profili personalizzati {#creating-custom-profiles}

Per creare un profilo personalizzato, effettuate le seguenti operazioni:

### Crea nodo profilo {#create-profile-node}

1. Passate all&#39;interfaccia CRX DE all&#39;URL: `https://'[server]:[port]'/crx/de` ed effettuate l&#39;accesso all&#39;interfaccia con le credenziali di amministratore.

1. Nel riquadro a sinistra, passare alla posizione */content/xfaforms/profile*.

1. Copiate il nodo predefinito e incollate il nodo in un&#39;altra cartella (*/content/profile*) con *il nome hrform*.

1. Selezionare il nuovo nodo, *hrform* e aggiungere una proprietà stringa: *sling:resourceType* con valore: *hrform/demo*.

1. Fate clic sul menu Salva tutto nella barra degli strumenti per salvare le modifiche.

### Creare lo script del renderer del profilo {#create-the-profile-renderer-script}

Dopo aver creato un profilo personalizzato, aggiungete le informazioni di rendering a questo profilo. Quando viene ricevuta una richiesta per il nuovo profilo, CRX verifica l&#39;esistenza della cartella /apps per la pagina JSP da sottoporre a rendering. Create la pagina JSP nella cartella /apps.

1. Nel riquadro a sinistra, individuate la `/apps` cartella.
1. Fate clic con il pulsante destro del mouse sulla `/apps` cartella e scegliete di creare una cartella con il nome **hrform**.
1. All’interno della cartella **hrform** , create una cartella denominata **demo**.
1. Fate clic sul pulsante **Salva tutto** .
1. Andate a `/libs/xfaforms/profile/html.jsp` e copiate il nodo **html.jsp**.
1. Incollate il nodo **html.jsp** nella `/apps/hrform/demo` cartella precedentemente creata con lo stesso nome **html.jsp** e fate clic su **Salva**.
1. Se disponete di altri componenti dello script di profilo, seguite i passaggi da 1 a 6 per copiare i componenti nella cartella /apps/hrform/demo.

1. Per verificare che il profilo sia stato creato, apri URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Per verificare i moduli, [importare i moduli](/help/forms/using/get-xdp-pdf-documents-aem.md) dal file system locale ai AEM Forms e [visualizzare l&#39;anteprima del modulo](/help/forms/using/previewing-forms.md) nell&#39;istanza di creazione del server AEM.
