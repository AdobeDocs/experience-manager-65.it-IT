---
title: Configurazione dell'autenticazione basata su certificato
seo-title: Configurazione dell'autenticazione basata su certificato
description: Importa un certificato di autorità di certificazione (CA) nell'archivio certificati e crea una mappatura di certificati per l'autenticazione basata su certificato.
seo-description: Importa un certificato di autorità di certificazione (CA) nell'archivio certificati e crea una mappatura di certificati per l'autenticazione basata su certificato.
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---


# Configurazione dell&#39;autenticazione basata sui certificati {#configuring-certificate-based-authentication}

In genere, la gestione utente esegue l&#39;autenticazione utilizzando un nome utente e una password. Gestione utente supporta anche l&#39;autenticazione basata sui certificati, che puoi utilizzare per autenticare gli utenti tramite  Acrobat o per autenticare gli utenti a livello di programmazione. Per informazioni dettagliate sull&#39;autenticazione degli utenti a livello di programmazione, vedere [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

Per utilizzare l&#39;autenticazione basata su certificato, importare un certificato CA (Certificate Authority, autorità di certificazione) attendibile nell&#39;archivio attendibili, quindi creare una mappatura del certificato.

## Importa certificato CA {#import-the-ca-certificate}

Durante l&#39;importazione del certificato, selezionare le opzioni Considera affidabili per l&#39;autenticazione del certificato e Considera affidabili per l&#39;identità, nonché tutte le altre opzioni richieste. Per informazioni dettagliate sull&#39;importazione dei certificati, vedere [Gestione dei certificati](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configurazione del mapping dei certificati {#configuring-certificate-mapping}

Per abilitare l&#39;autenticazione basata sui certificati per gli utenti, create una mappatura dei certificati. Una *mappatura certificati* definisce una mappa tra gli attributi di un certificato e gli attributi degli utenti di un dominio. È possibile mappare più certificati allo stesso dominio.

Quando sottoponete a test un certificato, Gestione utenti carica i controlli del certificato per assicurarsi che soddisfi i seguenti requisiti:

* Il certificato è valido.
* L&#39;emittente specificato può verificare il certificato.
* Il certificato contiene l&#39;attributo richiesto per la mappatura.
* La mappatura specificata mappa il certificato a un solo utente nel database dei moduli AEM. Gli utenti attuali e obsoleti (eliminati) vengono controllati per determinare se corrispondono ai criteri di mappatura. Pertanto, il test del certificato non riesce se più di un utente, inclusi gli utenti obsoleti, ha il valore dell&#39;attributo preso in considerazione.

>[!NOTE]
>
>Non è possibile modificare una mappatura certificato esistente.

**Aggiunta di una mappatura certificato**

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Mappatura certificati.
1. Fate clic su Nuova mappatura certificati e, nell&#39;elenco Per emittente, selezionate l&#39;alias del certificato configurato in Gestione archivio certificati attendibili.
1. Mappate uno degli attributi del certificato sull&#39;attributo di un utente. Ad esempio, potete mappare il nome comune del certificato all&#39;ID di accesso dell&#39;utente.

   Se il contenuto dell&#39;attributo nel certificato è diverso dal contenuto nell&#39;attributo dell&#39;utente nel database Gestione utente, potete utilizzare un&#39;espressione regolare Java (regex) per corrispondere ai due attributi. Ad esempio, se i nomi comuni dei certificati sono nomi come *Alex Pink (Authentication)* e *Alex Pink (Signing)* e il nome comune nel database User Management è *Alex Pink*, utilizzate un regex per estrarre la parte richiesta dell&#39;attributo del certificato (in questo esempio, *Alex Pink&lt;a5) 7/>.)* L&#39;espressione regolare specificata deve essere conforme alle specifiche del regex Java.

   È possibile trasformare l&#39;espressione specificando l&#39;ordine dei gruppi nella casella Ordine personalizzato. L&#39;ordine personalizzato viene utilizzato con il metodo `java.util.regex.Matcher.replaceAll()`. Il comportamento visualizzato corrisponderà al comportamento di tale metodo e la stringa di input (l&#39;ordine personalizzato) deve essere specificata di conseguenza.

   Per verificare il regex, immettete un valore nella casella Parametro di test e fate clic su Test.

   Nel regex potete usare i seguenti caratteri:

   * . (qualsiasi carattere)
   * &amp;ast; (0 o più occorrenze)
   * () (specificare il gruppo tra parentesi)
   * \ (utilizzato per sfuggire a un carattere regex a un carattere regolare)
   * $n (utilizzato per fare riferimento all&#39;nth group)

   Esempi di espressioni regolari:

   * Per estrarre &quot;Alex Pink&quot; da &quot;Alex Pink (Autenticazione)&quot;

      **Regex:** (.&amp;ast;) \(Authentication\)

   * Per estrarre &quot;Alex Pink&quot; da &quot;Alex (Authentication) Pink&quot;

      **Regex:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

   * Per estrarre &quot;Pink Alex&quot; da &quot;Alex (Authentication) Pink&quot;

      **Regex:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

      Ordine personalizzato: $2 $1 (restituisce il secondo gruppo, concatenato al primo gruppo, catturato da uno spazio vuoto)

   * Per estrarre &quot;apink@sampleorg.com&quot; da &quot;smtp:apink@sampleorg.com&quot;

      **Regex:** smtp:(.&amp;ast;)
   Per informazioni dettagliate sull&#39;uso delle espressioni regolari, vedere [Esercitazione Java sulle espressioni regolari](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. Nell&#39;elenco Per dominio, selezionare il dominio dell&#39;utente.
1. Per verificare questa configurazione, fate clic su Sfoglia per caricare un certificato utente di esempio, fate clic su Verifica certificato e, se la configurazione è corretta, su OK.

**Modificare una mappatura certificato esistente**

1. In Admin Console, fai clic su Settings (Impostazioni) > User Management (Gestione utente) > Configuration (Configurazione).
1. Fate clic su Mapping certificato.
1. Selezionate la mappatura del certificato per modificarne e modificarne la configurazione. È possibile aggiornare l&#39;espressione regolare e l&#39;ordine personalizzato.
1. Per verificare le modifiche apportate, fate clic su Sfoglia per caricare un certificato di esempio, fate clic su Verifica certificato, quindi su OK.

**Eliminare una mappatura certificato**

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Mappatura certificati.
1. Selezionate la casella di controllo per la mappatura del certificato da eliminare, fate clic su Elimina, quindi su OK.

