---
title: Accesso e compilazione dei moduli pubblicati
seo-title: Accessing and filling published forms
description: Forms Portal fornisce agli sviluppatori web componenti per creare e personalizzare un portale moduli sui siti web creati con Adobe Experience Manager (AEM).
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: 44731604-5d97-46fa-baa9-0c020c634fa7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 88dc8ef2-95ce-4906-ac28-eecc3a32a64e
docset: aem65
exl-id: aedf890c-a2f1-412f-8897-2492ffab335a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# Accesso e compilazione dei moduli pubblicati{#accessing-and-filling-published-forms}

In una configurazione di distribuzione del portale incentrata sui moduli, lo sviluppo dei moduli e lo sviluppo del portale sono due attività distinte. Mentre i progettisti di moduli progettano e archiviano i moduli in un archivio, gli sviluppatori web creano un&#39;applicazione Web per tale elenco e gestiscono gli invii. Forms viene quindi copiato sul livello web in quanto non vi è comunicazione tra l’archivio dei moduli e l’applicazione web.

Questo si traduce spesso in problemi di gestione della configurazione e dei ritardi di produzione. Ad esempio, se nell’archivio è disponibile una versione più recente di un modulo, la finestra di progettazione del modulo sostituisce il modulo sul livello web, modifica l’applicazione web e ridistribuisce il modulo sul sito pubblico. La ridistribuzione dell&#39;applicazione Web può causare tempi di inattività del server. Poiché il downtime del server è un’attività pianificata, le modifiche non possono essere inviate immediatamente al sito pubblico.

Forms Portal riduce i costi generali di gestione e i ritardi di produzione. Fornisce agli sviluppatori web componenti per creare e personalizzare un portale moduli sui siti web creati con Adobe Experience Manager (AEM).

Per ulteriori informazioni sul portale dei moduli e sulle sue funzioni, vedere [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md).

## Guida introduttiva a Forms portal {#getting-started-with-forms-portal}

Passare alla pagina del portale moduli pubblicati. Per ulteriori informazioni sulla creazione di una pagina del portale dei moduli, vedere [Creazione di una pagina del portale moduli](../../forms/using/creating-form-portal-page.md).

Il componente Ricerca e filtro di roms portal visualizza i moduli disponibili nell’istanza Pubblica del server AEM. Questo elenco include tutti i moduli o i moduli definiti nel filtro al momento della creazione della pagina del portale dei moduli. La pagina del portale dei moduli si presenta simile a quella mostrata nell’immagine seguente:

![Pagina del portale moduli di esempio ](assets/forms-portal-page.png)

Pagina del portale moduli di esempio

### Ricerca e filtro {#search-and-lister}

Il componente Ricerca e filtro consente di aggiungere le funzionalità seguenti al portale dei moduli:

* Elenca i moduli disponibili come predefiniti in pannelli, schede o viste a griglia. Supporta inoltre modelli personalizzatiElenca moduli da cartelle specifiche in Forms Manager.
* Specificare la modalità di rendering dei moduli: HTML5, PDF o entrambi.
* Specifica la modalità di rendering dei moduli PDF e XFA - HTML5, PDF o entrambi. Moduli non XFA come HTML5.
* Abilita la ricerca di moduli in base a criteri quali proprietà del modulo, metadati e tag.
* Invia i dati del modulo a un servlet.
* Utilizza i fogli di stile personalizzati (CSS) per personalizzare l’aspetto del portale.
* Creare collegamenti ai moduli.

È possibile cercare i moduli nella pagina Forms Portal utilizzando le seguenti opzioni:

* Ricerca full-text
* Ricerca avanzata

La ricerca full-text consente di trovare ed elencare i moduli in base alle parole chiave specificate.

![Finestra di dialogo di ricerca avanzata](assets/search-panel.png)

Finestra di dialogo di ricerca avanzata

La funzione Ricerca avanzata consente di eseguire ricerche nei moduli in base alle proprietà specificate del modulo. Questo fornisce risultati più specifici della ricerca full-text. La ricerca avanzata include la ricerca basata su tag, proprietà (come Autore, Descrizione e Titolo), data di modifica e testo completo.

Lister visualizza i moduli in base ai parametri di ricerca. Ogni modulo del risultato della ricerca viene visualizzato con un’icona, collegata in modo ipertestuale al modulo associato. È possibile fare clic sull’icona per aprire e utilizzare il modulo associato.

### Compilazione di un modulo {#filling-a-form}

![Un esempio di modulo adattivo](assets/filling_a_form.png)

Un esempio di modulo adattivo

È possibile accedere ai moduli dal collegamento fornito insieme al modulo nel componente Ricerca e Registrazione della pagina.

Ogni modulo contiene informazioni di aiuto che consentono all’utente di compilare il modulo.

#### Bozze e invio {#drafts-and-submission}

Per salvare una bozza di modulo, un utente può fare clic sul pulsante Salva. Questo consente all’utente di lavorare su un modulo per un periodo di tempo precedente all’invio.

I dati compilati nel modulo (inclusi gli allegati) vengono salvati come bozza sul server. La bozza di un modulo può essere salvata per un numero qualsiasi di volte. Il modulo salvato viene visualizzato nella scheda Bozze del componente Bozza e invio della pagina.

Al termine della compilazione del modulo, l’utente invia i moduli facendo clic sul pulsante Invia del modulo. I moduli inviati vengono visualizzati nella scheda Invii del componente Bozza e invio della pagina.

>[!NOTE]
>
>I moduli inviati vengono visualizzati nella scheda Inviato Forms solo se l’azione di invio per il modulo adattivo è configurata come Azione di invio di Forms Portal. Per ulteriori informazioni sull’invio di azioni, consulta [Configurazione dell’azione Invia](../../forms/using/configuring-submit-actions.md).

![Componente Bozze e invii](assets/draft-submission.png)

Componente Bozze e invii

## Avviare un nuovo modulo utilizzando i dati del modulo inviati {#start-a-new-form-using-submitted-form-data}

Ci sono alcuni moduli che è necessario compilare e inviare abbastanza spesso. Ad esempio, il modulo per la presentazione della dichiarazione dei redditi individuale viene inviato ogni anno. In questi casi, mentre alcune informazioni cambiano ogni volta che si compila il modulo, la maggior parte come i dati personali e familiari non cambiano. Tuttavia, è comunque necessario compilare nuovamente l’intero modulo da zero.

AEM Forms consente di ottimizzare l’esperienza di compilazione del modulo e di ridurre notevolmente il tempo necessario per compilare e inviare nuovamente il modulo. Gli utenti finali possono iniziare un nuovo modulo utilizzando i dati di un modulo inviato. Questa funzionalità è incorporata nella [Componente Bozze e invii](../../forms/using/draft-submission-component.md). Quando si aggiunge il componente Bozze e invio alla pagina del portale dei moduli e lo si pubblica, gli utenti finali troveranno un’opzione nelle schede Inviato Forms e Bozza Forms per avviare un nuovo modulo utilizzando i dati di un modulo inviato. L’immagine seguente evidenzia tale opzione.

![start-a-new-form](assets/start-a-new-form.png)

Quando si fa clic sul pulsante per avviare un nuovo modulo, viene aperto un nuovo modulo con i dati del modulo inviato corrispondente. È ora possibile esaminare e aggiornare le informazioni, a seconda delle necessità, e inviare il modulo.
