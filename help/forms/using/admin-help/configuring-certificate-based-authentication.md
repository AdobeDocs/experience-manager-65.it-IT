---
title: Configurazione dell’autenticazione basata su certificati
description: Importa un certificato di Autorità di certificazione (CA) nell’archivio di certificati attendibili e crea una mappatura di certificati per l’autenticazione basata su certificati.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '730'
ht-degree: 100%

---

# Configurazione dell’autenticazione basata su certificati {#configuring-certificate-based-authentication}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

La Gestione utenti in genere esegue l’autenticazione utilizzando un nome utente e una password. La Gestione utenti supporta anche l’autenticazione basata su certificati, che può essere utilizzata per autenticare gli utenti tramite Acrobat o a livello di programmazione. Per informazioni dettagliate sull’autenticazione degli utenti a livello di programmazione, consulta [Programmazione con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_it).

Per utilizzare l’autenticazione basata su certificati, importa un certificato di Autorità di certificazione (CA) attendibile nell’archivio di certificati attendibili e quindi crea una mappatura di certificati.

## Importare il certificato CA {#import-the-ca-certificate}

Durante l’importazione del certificato, seleziona le opzioni Considera attendibile l’autenticazione del certificato e Considera attendibile l’identità e qualsiasi altra opzione necessaria. Per informazioni dettagliate sull’importazione dei certificati, consulta [Gestione dei certificati](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configurazione della mappatura dei certificati {#configuring-certificate-mapping}

Per abilitare l’autenticazione basata su certificati per gli utenti, crea una mappatura dei certificati. Una *mappatura dei certificati* definisce una mappatura tra gli attributi di un certificato e gli attributi degli utenti in un dominio. Puoi mappare più certificati allo stesso dominio.

Quando verifichi un certificato, la Gestione utenti carica i controlli del certificato per assicurare che soddisfi i seguenti requisiti:

* Questo certificato è valido.
* L’emittente specificato può verificare il certificato.
* Il certificato contiene l’attributo necessario per la mappatura.
* La mappatura specificata associa il certificato a un solo utente nel database di AEM Forms. Gli utenti correnti e obsoleti (eliminati) vengono controllati per determinare se corrispondono ai criteri di mappatura. Pertanto, il test del certificato non riesce se più utenti, inclusi quelli obsoleti, hanno preso in considerazione il valore dell’attributo.

>[!NOTE]
>
>Non è possibile modificare una mappatura di certificati esistente.

**Aggiungere la mappatura di un certificato**

1. Nella console di amministrazione fai clic su Impostazioni > Gestione utenti > Configurazione > Mappatura certificato.
1. Fai clic su Mappatura di nuovi certificati e, nell’elenco Per emittente, seleziona l’alias del certificato configurato in Gestione archivio di certificati attendibili.
1. Mappa uno degli attributi del certificato a un attributo dell’utente. Ad esempio, puoi mappare il nome comune del certificato all’ID di accesso dell’utente.

   Se il contenuto dell’attributo nel certificato è diverso da quello nell’attributo dell’utente nel database della Gestione utenti, puoi utilizzare un’espressione regolare Java (regex) per far corrispondere i due attributi. Ad esempio, se i nomi comuni dei certificati sono nomi come *Alex Pink (autenticazione)* e *Alex Pink (firma)* e il nome comune nel database della gestione utenti è *Alex Pink*, utilizza un regex per estrarre la parte dell’attributo del certificato richiesta (in questo esempio, *Alex Pink*). L’espressione regolare specificata deve essere conforme alla specifica Java regex.

   Puoi trasformare l’espressione specificando l’ordine dei gruppi nella casella Ordine personalizzato. L’ordine personalizzato è utilizzato con il metodo `java.util.regex.Matcher.replaceAll()`. Il comportamento visualizzato corrisponderà al comportamento del metodo e la stringa di input (l’ordine personalizzato) deve essere specificata di conseguenza.

   Per testare il regex, immetti un valore nella casella Parametro di test e fai clic su Test.

   Nel regex puoi utilizzare i seguenti caratteri:

   * . (qualsiasi carattere)
   * &amp;ast; (0 o più occorrenze)
   * () (specifica il gruppo tra parentesi)
   * \ (utilizzato per sostituire un carattere regex con un carattere regolare)
   * $n (utilizzato per fare riferimento all’n-esimo gruppo)

   Esempi di espressioni regolari:

   * Per estrarre “Alex Pink” da “Alex Pink (Authentication)”

     **Regex:** (.&amp;ast;) \(Authentication\)

   * Per estrarre “Alex Pink” da “Alex (Authentication) Pink”

     **Regex:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

   * Per estrarre “Pink Alex” da “Alex (Authentication) Pink”

     **Regex:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

     Ordine personalizzato: $2 $1 (secondo gruppo restituito, concatenato al primo gruppo, acquisito dal carattere di spazio vuoto)

   * Per estrarre “apink@sampleorg.com” da “smtp:apink@sampleorg.com”

     **Regex:** smtp:(.&amp;ast;)

   Per informazioni dettagliate sull’utilizzo delle espressioni regolari, consulta [Tutorial di Java sulle espressioni regolari](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. Nell’elenco Per dominio seleziona il dominio dell’utente.
1. Per testare questa configurazione, fai clic su Sfoglia per caricare un certificato utente di esempio, fai clic su Testa certificato e, se la configurazione è corretta, fai clic su OK.

**Modifica della mappatura di un certificato esistente**

1. Nella console di amministrazione fai clic su Impostazioni > Gestione utenti > Configurazione.
1. Fai clic su Mappatura certificato.
1. Seleziona la mappatura del certificato da modificare e cambiane la configurazione. Puoi aggiornare l’espressione regolare e l’ordine personalizzato.
1. Per verificare le modifiche, fai clic su Sfoglia per caricare un certificato di esempio, su Testa certificato, quindi su OK.

**Eliminazione della mappatura di un certificato**

1. Nella console di amministrazione fai clic su Impostazioni > Gestione utenti > Configurazione > Mappatura certificato.
1. Seleziona la casella di controllo relativa alla mappatura del certificato da eliminare, fai clic su Elimina, quindi su OK.
