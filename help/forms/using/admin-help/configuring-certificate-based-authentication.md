---
title: Configurazione dell’autenticazione basata su certificati
description: Importare un certificato di autorità di certificazione (CA) nell'archivio fonti attendibili e creare un mapping di certificati per l'autenticazione basata su certificati.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Configurazione dell’autenticazione basata su certificati {#configuring-certificate-based-authentication}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Gestione utenti in genere esegue l&#39;autenticazione utilizzando un nome utente e una password. Gestione utenti supporta anche l’autenticazione basata su certificati, che può essere utilizzata per autenticare gli utenti tramite Acrobat o a livello di programmazione. Per informazioni dettagliate sull&#39;autenticazione degli utenti a livello di programmazione, vedere [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

Per utilizzare l&#39;autenticazione basata su certificati, importare un certificato di Autorità di certificazione (CA) attendibile nell&#39;archivio fonti attendibili e quindi creare un mapping di certificati.

## Importa il certificato CA {#import-the-ca-certificate}

Durante l&#39;importazione del certificato, selezionare le opzioni Considera attendibili l&#39;autenticazione del certificato e Considera attendibili l&#39;identità e qualsiasi altra opzione necessaria. Per informazioni dettagliate sull&#39;importazione dei certificati, vedere [Gestione dei certificati](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configurazione della mappatura dei certificati {#configuring-certificate-mapping}

Per abilitare l’autenticazione basata su certificato per gli utenti, crea un mapping dei certificati. Un *mapping certificato* definisce un mapping tra gli attributi di un certificato e gli attributi degli utenti in un dominio. È possibile mappare più certificati allo stesso dominio.

Quando verifichi un certificato, Gestione utente carica i controlli del certificato per verificare che soddisfi i seguenti requisiti:

* Il certificato è valido.
* L&#39;autorità di certificazione specificata può verificare il certificato.
* Il certificato contiene l’attributo necessario per la mappatura.
* Il mapping specificato associa il certificato a un solo utente nel database dei moduli AEM. Gli utenti correnti e obsoleti (eliminati) vengono controllati per determinare se corrispondono ai criteri di mappatura. Pertanto, il test del certificato non riesce se più utenti, inclusi gli utenti obsoleti, hanno preso in considerazione il valore dell’attributo.

>[!NOTE]
>
>Non è possibile modificare un mapping di certificati esistente.

**Aggiungere un mapping di certificati**

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Mappatura certificato.
1. Fare clic su Nuovo mapping certificati e, nell&#39;elenco Per emittente, selezionare l&#39;alias del certificato configurato in Gestione archivio fonti attendibili.
1. Mappa uno degli attributi del certificato a un attributo dell’utente. Ad esempio, puoi mappare il nome comune del certificato all’ID di accesso dell’utente.

   Se il contenuto dell’attributo nel certificato è diverso da quello nell’attributo dell’utente nel database di User Management, puoi utilizzare un’espressione regolare Java (regex) per far corrispondere i due attributi. Ad esempio, se i nomi comuni dei certificati sono nomi come *Alex Pink (autenticazione)* e *Alex Pink (firma)* e il nome comune nel database di gestione utenti è *Alex Pink*, utilizzare un regex per estrarre la parte richiesta dell&#39;attributo del certificato (in questo esempio, *Alex Pink*). L&#39;espressione regolare specificata deve essere conforme alla specifica Java regex.

   È possibile trasformare l&#39;espressione specificando l&#39;ordine dei gruppi nella casella Ordine personalizzato. Ordine personalizzato utilizzato con il metodo `java.util.regex.Matcher.replaceAll()`. Il comportamento visualizzato corrisponderà al comportamento del metodo e la stringa di input (l’ordine personalizzato) deve essere specificata di conseguenza.

   Per verificare il regex, immettete un valore nella casella Parametro test (Test Parameter) e fate clic su Test.

   Puoi utilizzare i seguenti caratteri nel codice regex:

   * . (qualsiasi carattere)
   * &ast; (0 o più occorrenze)
   * () (specificare il gruppo tra parentesi)
   * \ (utilizzato per sostituire un carattere regex con un carattere regolare)
   * $n (utilizzato per fare riferimento all’ennesimo gruppo)

   Esempi di espressioni regolari:

   * Per estrarre &quot;Alex Pink&quot; da &quot;Alex Pink (Authentication)&quot;

     **Regex:** (.&ast;) \(autenticazione\)

   * Per estrarre &quot;Alex Pink&quot; da &quot;Alex (Authentication) Pink&quot;

     **Regex:** (.&ast;)\(autenticazione\) (.&ast;)

   * Per estrarre &quot;Pink Alex&quot; da &quot;Alex (Authentication) Pink&quot;

     **Regex:** (.&ast;)\(autenticazione\) (.&ast;)

     Ordine personalizzato: $2 $1 (secondo gruppo restituito, concatenato al primo gruppo, acquisito dal carattere spazio vuoto)

   * Per estrarre &quot;apink@sampleorg.com&quot; da &quot;smtp:apink@sampleorg.com&quot;

     **Regex:** smtp:(.&ast;)

   Per informazioni dettagliate sull&#39;utilizzo delle espressioni regolari, vedere [Esercitazione Java sulle espressioni regolari](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. Nell’elenco Per dominio, seleziona il dominio dell’utente.
1. Per verificare questa configurazione, fai clic su Sfoglia per caricare un certificato utente di esempio, fai clic su Prova certificato e, se la configurazione è corretta, fai clic su OK.

**Modifica mapping certificato esistente**

1. In Administration Console, fai clic su Impostazioni > Gestione utente > Configurazione.
1. Fai clic su Mappatura certificato.
1. Seleziona il mapping del certificato per modificarne e modificarne la configurazione. Puoi aggiornare l’espressione regolare e l’ordine personalizzato.
1. Per verificare le modifiche, fare clic su Sfoglia per caricare un certificato di esempio, fare clic su Prova certificato e quindi su OK.

**Eliminare un mapping di certificati**

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Mappatura certificato.
1. Selezionare la casella di controllo relativa al mapping dei certificati da eliminare, fare clic su Elimina e quindi su OK.
