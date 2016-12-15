---
title: "Vincoli sui parametri di tipo (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "generics [C#], vincoli di tipo"
  - "vincoli di tipo [C#]"
  - "parametri di tipo [C#], vincoli"
  - "parametro di tipo non associato [C#]"
ms.assetid: 141b003e-1ddb-4e1c-bcb2-e1c3870e6a51
caps.latest.revision: 41
caps.handback.revision: 41
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Vincoli sui parametri di tipo (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando si definisce una classe generica è possibile applicare restrizioni ai tipi che possono essere utilizzati dal codice client per gli argomenti di tipo al momento della creazione di un'istanza della classe.  Se il codice client tenta di creare un'istanza della classe con un tipo non consentito da un vincolo, verrà restituito un errore in fase di compilazione.  Queste restrizioni sono definite vincoli.  I vincoli sono specificati mediante la parola chiave contestuale `where`.  Nella tabella riportata di seguito sono elencati i sei tipi di vincoli che è possibile applicare:  
  
|Vincolo|Descrizione|  
|-------------|-----------------|  
|where T: struct|L'argomento di tipo deve essere un tipo di valore.  È possibile specificare qualsiasi tipo di valore tranne <xref:System.Nullable>.  Per ulteriori informazioni, vedere [Utilizzo dei tipi nullable](../../../csharp/programming-guide/nullable-types/using-nullable-types.md).|  
|where T : class|L'argomento di tipo deve essere un tipo di riferimento, incluso qualsiasi tipo di classe, interfaccia, delegato o matrice.|  
|where T : new\(\)|L'argomento di tipo deve disporre di un costruttore pubblico senza parametri.  Quando il vincolo `new()` viene utilizzato con altri vincoli, è necessario specificarlo per ultimo:|  
|where T : \<nome classe base\>|L'argomento di tipo deve corrispondere alla classe base specificata o derivare da tale classe.|  
|where T : \<nome interfaccia\>|L'argomento di tipo deve corrispondere all'interfaccia specificata o implementare tale interfaccia.  È possibile specificare più vincoli di interfaccia.  L'interfaccia vincolante può anche essere generica.|  
|where T : U|L'argomento di tipo fornito per T deve corrispondere all'argomento fornito per U o derivare da tale argomento.|  
  
## Vantaggi offerti dall'utilizzo dei vincoli  
 Se si desidera esaminare un elemento di un elenco generico per stabilire se è valido oppure per confrontarlo con un altro elemento, è necessario garantire al compilatore che l'operatore o il metodo da chiamare sarà supportato da un qualsiasi argomento di tipo specificato dal codice client.  A tale scopo è possibile applicare uno o più vincoli alla definizione di classe generica.  Specificando il vincolo della classe base, si garantirà ad esempio al compilatore che verranno utilizzati come argomenti di tipo solo gli oggetti del tipo specificato o derivati da esso.  In presenza di questa garanzia, il compilatore consentirà le chiamate ai metodi del tipo all'interno della classe generica.  Per l'applicazione dei vincoli viene utilizzata la parola chiave contestuale `where`.  Nell'esempio di codice riportato di seguito viene illustrata la funzionalità che è possibile aggiungere alla classe `GenericList<T>` \(in [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)\) applicando un vincolo di classe base.  
  
 [!code-cs[csProgGuideGenerics#11](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_1.cs)]  
  
 Il vincolo consente di utilizzare la proprietà `Employee.Name` nella classe generica poiché viene garantito che tutti gli elementi di tipo T sono oggetti `Employee` oppure oggetti che ereditano da `Employee`.  
  
 È possibile applicare più vincoli allo stesso parametro di tipo. I vincoli stessi possono essere tipi generici, come illustrato di seguito:  
  
 [!code-cs[csProgGuideGenerics#12](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_2.cs)]  
  
 Vincolando il parametro di tipo, il numero di operazioni e di chiamate a metodi consentite viene ampliato a quelle supportate dal tipo vincolante e da tutti i tipi nella relativa gerarchia di ereditarietà.  Di conseguenza, se durante la progettazione di classi o metodi generici si intende eseguire operazioni su membri generici diverse dalla semplice assegnazione o dalla chiamata a metodi non supportati da `System.Object`, sarà necessario applicare vincoli al parametro di tipo.  
  
 Nell'applicare il vincolo `where T : class`, evitare di utilizzare gli operatori `==` e `!=` sul parametro di tipo poiché questi operatori eseguiranno il test solo per l'identità del riferimento, non per l'uguaglianza dei valori.  Questo consiglio è valido anche se si esegue l'overload degli operatori in un tipo utilizzato come argomento,  come illustrato nel codice riportato di seguito. Il valore dell'output è false anche se la classe <xref:System.String> esegue l'overload dell'operatore `==`.  
  
 [!code-cs[csProgGuideGenerics#13](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_3.cs)]  
  
 Questo comportamento è dovuto al fatto che, in fase di compilazione, il compilatore sa solo che T è un tipo di riferimento. Di conseguenza, è necessario utilizzare gli operatori predefiniti che sono validi per tutti i tipi di riferimento.  Per verificare l'uguaglianza dei valori, è consigliabile applicare anche il vincolo `where T : IComparable<T>` e implementare tale interfaccia nelle classi che verranno utilizzate per costruire la classe generica.  
  
## Vincolo di più parametri  
 È possibile applicare vincoli a più parametri e più vincoli a un solo parametro, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideGenerics#64](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_4.cs)]  
  
## Parametri di tipo non vincolati  
 I parametri di tipo che non presentano vincoli, ad esempio T nella classe pubblica `SampleClass<T>{}`, sono noti come parametri di tipo non vincolati  e sono caratterizzati dalle seguenti regole:  
  
-   Gli operatori `!=` e `==` non possono essere utilizzati perché non si ha la garanzia che siano supportati dall'argomento di tipo concreto.  
  
-   I parametri di tipo non vincolati possono essere convertiti in e da `System.Object` oppure possono essere convertiti esplicitamente in qualsiasi tipo di interfaccia.  
  
-   È possibile eseguire il confronto con [null](../../../csharp/language-reference/keywords/null.md).  Se si confronta un parametro non vincolato con `null` e l'argomento di tipo è un tipo di valore, verrà sempre restituito il valore false.  
  
## Parametri di tipo come vincoli  
 L'utilizzo di un parametro di tipo generico come vincolo è utile quando è necessario vincolare il parametro di tipo specifico di una funzione membro al parametro del tipo che contiene tale funzione, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideGenerics#14](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_5.cs)]  
  
 Nell'esempio precedente, `T` è un vincolo di tipo nel contesto del metodo `Add` e un parametro di tipo non vincolato nel contesto della classe `List`.  
  
 I parametri di tipo possono inoltre essere utilizzati come vincoli nelle definizioni di classi generiche.  Si noti che è necessario aver dichiarato il vincolo il parametro di tipo tra parentesi angolari, insieme ad eventuali altri parametri di tipo:  
  
 [!code-cs[csProgGuideGenerics#15](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_6.cs)]  
  
 I vincoli dei parametri di tipo risultano poco utili se utilizzati in classi generiche poiché il compilatore non è in grado di utilizzare alcuna informazione sul parametro di tipo, tranne il fatto che deriva da `System.Object`.  L'utilizzo di parametri di tipo come vincoli in classi generiche negli scenari è consigliato nei casi in cui si desidera imporre una relazione di ereditarietà tra due parametri di tipo.  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [Classi generiche](../../../csharp/programming-guide/generics/generic-classes.md)   
 [Vincolo new](../../../csharp/language-reference/keywords/new-constraint.md)