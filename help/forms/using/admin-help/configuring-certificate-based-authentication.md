---
title: Configurazione dell’autenticazione basata su certificato
seo-title: Configuring certificate-based authentication
description: Importa un certificato dell’Autorità di certificazione (CA) nell’archivio certificati e crea una mappatura del certificato per l’autenticazione basata su certificato.
seo-description: Import a Certificate Authority (CA) certificate into the Trust Store and create a certificate mapping for certificate-based authentication.
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Configurazione dell’autenticazione basata su certificato {#configuring-certificate-based-authentication}

In genere, la gestione utente esegue l’autenticazione utilizzando un nome utente e una password. User Management supporta anche l’autenticazione basata su certificato, che è possibile utilizzare per autenticare gli utenti tramite Acrobat o per autenticare gli utenti a livello di programmazione. Per informazioni dettagliate sull’autenticazione degli utenti a livello di programmazione, consulta [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

Per utilizzare l’autenticazione basata su certificato, importare un certificato CA (Certificate Authority, Autorità di certificazione) attendibile nell’archivio attendibilità, quindi creare una mappatura del certificato.

## Importa il certificato CA {#import-the-ca-certificate}

Durante l’importazione del certificato, selezionare le opzioni Considera attendibili per l’autenticazione del certificato e Considera attendibile l’identità e tutte le altre opzioni richieste. Per informazioni dettagliate sull&#39;importazione dei certificati, vedere [Gestione dei certificati](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configurazione della mappatura dei certificati {#configuring-certificate-mapping}

Per abilitare l’autenticazione basata su certificato per gli utenti, crea una mappatura dei certificati. A *mappatura del certificato* definisce una mappa tra gli attributi di un certificato e gli attributi degli utenti in un dominio. Puoi mappare più certificati sullo stesso dominio.

Quando si esegue il test di un certificato, Gestione utente carica il certificato e verifica che soddisfi i seguenti requisiti:

* Il certificato è valido.
* L&#39;emittente specificato può verificare il certificato.
* Il certificato contiene l’attributo necessario per la mappatura.
* La mappatura specificata mappa il certificato a un solo utente nel database dei moduli di AEM. Gli utenti attuali e obsoleti (eliminati) vengono controllati per determinare se corrispondono ai criteri di mappatura. Pertanto, il test del certificato non riesce se più di un utente, inclusi gli utenti obsoleti, considera il valore dell&#39;attributo.

>[!NOTE]
>
>Non è possibile modificare una mappatura certificato esistente.

**Aggiungere una mappatura del certificato**

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Mappatura certificato.
1. Fare clic su Nuova mappatura certificati e, nell’elenco Per l’emittente, selezionare l’alias del certificato configurato in Gestione archivio attendibilità.
1. Mappa uno degli attributi del certificato sull’attributo di un utente. Ad esempio, puoi mappare il nome comune del certificato all’ID di accesso dell’utente.

   Se il contenuto dell’attributo nel certificato è diverso da quello dell’attributo dell’utente nel database User Management, puoi utilizzare un’espressione regolare Java (regex) per associare i due attributi. Ad esempio, se i nomi comuni dei certificati sono nomi simili *Alex Pink (autenticazione)* e *Alex Pink (Firma)* e il nome comune nel database User Management è *Alex Pink*, utilizza un regex per estrarre la parte richiesta dell’attributo del certificato (in questo esempio, *Alex Pink*.) L&#39;espressione regolare specificata deve essere conforme alle specifiche di Java regex.

   È possibile trasformare l’espressione specificando l’ordine dei gruppi nella casella Ordine personalizzato. L’ordine personalizzato viene utilizzato con `java.util.regex.Matcher.replaceAll()` metodo . Il comportamento visualizzato corrisponde al comportamento di tale metodo e la stringa di input (l’ordine personalizzato) deve essere specificata di conseguenza.

   Per verificare il regex, immettere un valore nella casella Parametro test e fare clic su Test.

   È possibile utilizzare i seguenti caratteri nel regex:

   * . (qualsiasi carattere)
   * &amp;ast; (0 o più occorrenze)
   * () (specificare il gruppo tra parentesi)
   * \ (utilizzato per eseguire il escape di un carattere regex da un carattere regolare)
   * $n (utilizzato per fare riferimento al nth group)

   Esempi di espressioni regolari:

   * Per estrarre &quot;Alex Pink&quot; da &quot;Alex Pink (Authentication)&quot;

      **Regex:** (.&amp;ast;) \(Authentication\)

   * Per estrarre &quot;Alex Pink&quot; da &quot;Alex (Authentication) Pink&quot;

      **Regex:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

   * Per estrarre &quot;Pink Alex&quot; da &quot;Alex (Authentication) Pink&quot;

      **Regex:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

      Ordine personalizzato: $2 $1 (ritorno al secondo gruppo, concatenato al primo gruppo, catturato dal carattere spazio vuoto)

   * Per estrarre &quot;apink@sampleorg.com&quot; da &quot;smtp:apink@sampleorg.com&quot;

      **Regex:** smtp:(.&amp;ast;)
   Per informazioni sull’utilizzo delle espressioni regolari, consulta [Esercitazione Java sulle espressioni regolari](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. Nell’elenco Per dominio, selezionare il dominio dell’utente.
1. Per verificare questa configurazione, fare clic su Sfoglia per caricare un certificato utente di esempio, fare clic su Test certificato e, se la configurazione è corretta, fare clic su OK.

**Modificare una mappatura certificato esistente**

1. In Console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione.
1. Fai clic su Mappatura certificato.
1. Seleziona la mappatura del certificato per modificarne e modificarne la configurazione. Puoi aggiornare l’espressione regolare e l’ordine personalizzato.
1. Per verificare le modifiche, fare clic su Sfoglia per caricare un certificato di esempio, fare clic su Test certificato e quindi su OK.

**Eliminare una mappatura certificato**

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Mappatura certificato.
1. Selezionare la casella di controllo relativa alla mappatura del certificato da eliminare, fare clic su Elimina, quindi su OK.
