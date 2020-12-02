---
title: Accesso e compilazione dei moduli pubblicati
seo-title: Accesso e compilazione dei moduli pubblicati
description: Forms Portal offre agli sviluppatori Web componenti per creare e personalizzare un portale moduli sui siti Web creati con Adobe Experience Manager (AEM).
seo-description: Forms Portal offre agli sviluppatori Web componenti per creare e personalizzare un portale moduli sui siti Web creati con Adobe Experience Manager (AEM).
uuid: 44731604-5d97-46fa-baa9-0c020c634fa7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 88dc8ef2-95ce-4906-ac28-eecc3a32a64e
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---


# Accesso e compilazione di moduli pubblicati{#accessing-and-filling-published-forms}

In una configurazione di distribuzione basata sui moduli, lo sviluppo di moduli e lo sviluppo di portale sono due attività distinte. Mentre i progettisti di moduli progettano e memorizzano i moduli in un archivio, gli sviluppatori Web creano un&#39;applicazione Web per tale elenco e gestiscono gli invii. Forms viene quindi copiato sul livello Web in quanto non è disponibile alcuna comunicazione tra l&#39;archivio dei moduli e l&#39;applicazione Web.

Spesso si verificano problemi nella gestione dei ritardi di configurazione e produzione. Ad esempio, se nella directory archivio è disponibile una versione più recente di un modulo, la finestra di progettazione del modulo sostituirà il modulo sul livello Web, modificherà l&#39;applicazione Web e ridistribuirà il modulo sul sito pubblico. La ridistribuzione dell&#39;applicazione Web può causare tempi di inattività del server. Poiché il tempo di inattività del server è un&#39;attività pianificata, le modifiche non possono essere inviate immediatamente al sito pubblico.

Forms Portal riduce i costi generali di gestione e i ritardi di produzione. Offre agli sviluppatori Web componenti per creare e personalizzare un portale moduli sui siti Web creati con Adobe Experience Manager (AEM).

Per ulteriori informazioni sul portale dei moduli e sulle relative funzionalità, vedere [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md).

## Guida introduttiva al portale dei moduli {#getting-started-with-forms-portal}

Passare alla pagina del portale dei moduli pubblicati. Per ulteriori informazioni sulla creazione di una pagina del portale dei moduli, vedere [Creazione di una pagina del portale dei moduli](../../forms/using/creating-form-portal-page.md).

Il componente Ricerca e filtro del portale Roma visualizza i moduli disponibili nell&#39;istanza Pubblica del server AEM. Questo elenco include tutti i moduli o i moduli definiti nel filtro al momento della creazione della pagina del portale dei moduli. La pagina del portale dei moduli ha un aspetto simile a quello illustrato nell&#39;immagine seguente:

![Pagina del portale moduli di esempio  ](assets/forms-portal-page.png)

Pagina del portale moduli di esempio

### Ricerca e filtro {#search-and-lister}

Il componente Cerca e registri consente di aggiungere le seguenti funzionalità al portale dei moduli:

* Elenca i moduli disponibili nella visualizzazione a pannello, a schede o a griglia. Supporta inoltre i modelli personalizzatiElenca i moduli da cartelle specifiche in Forms Manager.
* Specificare la modalità di rendering dei moduli: HTML5, PDF o entrambi.
* Specificare la modalità di rendering dei moduli PDF e XFA - HTML5, PDF o entrambi. Moduli non XFA come HTML5.
* Abilitare la ricerca di moduli in base a criteri quali proprietà del modulo, metadati e tag.
* Inviare i dati del modulo a un servlet.
* Utilizzare fogli di stile personalizzati (CSS) per personalizzare l&#39;aspetto del portale.
* Creare collegamenti ai moduli.

È possibile ricercare i moduli nella pagina Forms Portal utilizzando le seguenti opzioni:

* Ricerca full-text
* Ricerca avanzata

La ricerca full text consente di trovare ed elencare moduli basati sulle parole chiave specificate.

![Finestra di dialogo di ricerca avanzata](assets/search-panel.png)

Finestra di dialogo di ricerca avanzata

La funzione di ricerca avanzata consente di effettuare ricerche nei moduli in base alle proprietà specificate del modulo. Questo fornisce risultati più specifici della ricerca full-text. La ricerca avanzata include la ricerca basata su tag, proprietà (come Autore, Descrizione e Titolo), data di modifica e testo completo.

Lister visualizza i moduli in base ai parametri di ricerca. Ogni modulo del risultato della ricerca viene visualizzato con un&#39;icona, che è collegata in modo ipertestuale al modulo associato. È possibile fare clic sull&#39;icona per aprire e utilizzare il modulo associato.

### Compilazione di un modulo {#filling-a-form}

![Esempio di modulo adattivo](assets/filling_a_form.png)

Esempio di modulo adattivo

È possibile accedere ai moduli dal collegamento fornito insieme al modulo nel componente Ricerca e Controllo della pagina.

Ciascun modulo contiene informazioni di aiuto che consentono a un utente di compilare il modulo.

#### Bozze e invio {#drafts-and-submission}

Un utente può salvare una bozza di un modulo facendo clic sul pulsante Salva. Questo consente all&#39;utente di lavorare su un modulo per un periodo di tempo specificato prima di inviarlo.

I dati compilati nel modulo (inclusi gli allegati) vengono salvati sul server come bozza. È possibile salvare la bozza di un modulo per un numero qualsiasi di volte. Il modulo salvato viene visualizzato nella scheda Bozze del componente Bozza e invio della pagina.

Al termine della compilazione del modulo, l&#39;utente invia i moduli facendo clic sul pulsante Invia del modulo. I moduli inviati vengono visualizzati nella scheda Invii del componente Bozza e invio della pagina.

>[!NOTE]
>
>I moduli inviati vengono visualizzati nella scheda Forms inviata solo se l&#39;azione di invio per il modulo adattivo è configurata come azione di invio di Forms Portal. Per ulteriori informazioni sulle azioni di invio, vedere [Configurazione dell&#39;azione di invio](../../forms/using/configuring-submit-actions.md).

![Bozze e invii, componente](assets/draft-submission.png)

Bozze e invii, componente

## Avviare un nuovo modulo utilizzando i dati del modulo inviati {#start-a-new-form-using-submitted-form-data}

Alcuni moduli devono essere compilati e inviati molto spesso. Ad esempio, il modulo per la presentazione della dichiarazione dei redditi individuale viene inviato ogni anno. In tali casi, mentre una parte delle informazioni cambia ogni volta che si compila il modulo, la maggior parte di esso come i dati personali e familiari non cambia. Tuttavia, è comunque necessario compilare nuovamente l&#39;intero modulo da zero.

 AEM Forms consente di ottimizzare l&#39;esperienza di compilazione del modulo e di ridurre notevolmente il tempo necessario per compilare e inviare di nuovo il modulo. Gli utenti finali possono iniziare un nuovo modulo utilizzando i dati di un modulo inviato. Questa funzionalità è integrata nel componente [Bozze e invii](../../forms/using/draft-submission-component.md). Quando si aggiunge un componente Bozze e invio alla pagina del portale dei moduli e lo si pubblica, gli utenti finali potranno trovare un&#39;opzione nelle schede Forms e Bozza invio per iniziare un nuovo modulo utilizzando i dati di un modulo inviato. L&#39;immagine seguente evidenzia tale opzione.

![start-a-new-form](assets/start-a-new-form.png)

Quando si fa clic sul pulsante per avviare un nuovo modulo, viene aperto un nuovo modulo con i dati del modulo inviato corrispondente. È ora possibile esaminare e aggiornare le informazioni, a seconda delle necessità, e inviare il modulo.
