---
title: "Convenzioni di lettere maiuscole/minuscole | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "nomi maiuscole-minuscole camel [.NET Framework]"
  - "classe libreria linee guida di progettazione [.NET Framework], lettere maiuscole/minuscole"
  - "Nomi di tipo Pascal [.NET Framework]"
  - "distinzione maiuscole/minuscole, convenzioni di lettere maiuscole/minuscole"
  - "nomi [.NET Framework], lettere maiuscole/minuscole"
ms.assetid: 4c4ea526-9203-486f-b72d-29d61c5b3c6d
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Convenzioni di lettere maiuscole/minuscole
Le linee guida in questo capitolo disporre un metodo semplice per l'utilizzo di case, quando applicate in modo coerente, verificare gli identificatori di tipi, membri e parametri di facile lettura.  
  
## Regole per gli identificatori  
 Per differenziare le parole in un identificatore, converte in maiuscolo la prima lettera di ogni parola nell'identificatore. Non utilizzare caratteri di sottolineatura per differenziare le parole o parimenti, in un punto qualsiasi all'interno degli identificatori. Esistono due metodi appropriati per sfruttare al meglio gli identificatori, a seconda dell'utilizzo dell'identificatore:  
  
-   Sistema Pascal  
  
-   Camel  
  
 La convenzione il sistema Pascal, utilizzata per tutti gli identificatori, ad eccezione di nomi di parametro, converte in maiuscolo il primo carattere di ogni parola \(inclusi gli acronimi su due lettere\), come illustrato negli esempi seguenti:  
  
 `PropertyDescriptor`   
 `HtmlTag`  
  
 Un caso speciale viene effettuato per acronimi di due lettere in cui sia le lettere sono scritti in maiuscolo, come illustrato nella seguente identificatore:  
  
 `IOStream`  
  
 La convenzione camel, utilizzata solo per i nomi dei parametri, converte in maiuscolo il primo carattere di ogni parola tranne la prima, come illustrato negli esempi seguenti. Come nell'esempio viene inoltre, gli acronimi di due lettere che iniziano un identificatore di maiuscole\/minuscole camel sono entrambi lettere minuscole.  
  
 `propertyDescriptor`   
 `ioStream`   
 `htmlTag`  
  
 **✓ si** utilizzare il sistema Pascal per tutti pubblici nomi membro, il tipo e spazio dei nomi costituiti da più parole.  
  
 **✓ si** utilizzare camel per i nomi di parametro.  
  
 Nella tabella seguente vengono descritte le regole di utilizzo delle maiuscole per i diversi tipi di identificatori.  
  
|Identificatore|Maiuscole e minuscole|Esempio|  
|--------------------|---------------------------|-------------|  
|Spazio dei nomi|Convenzione Pascal|`namespace System.Security { ... }`|  
|Tipo|Convenzione Pascal|`public class StreamReader { ... }`|  
|Interfaccia|Convenzione Pascal|`public interface IEnumerable { ... }`|  
|Metodo|Convenzione Pascal|`public class Object {` <br />  `public virtual string ToString();` <br /> `}`|  
|Proprietà|Convenzione Pascal|`public class String {` <br />  `public int Length { get; }` <br /> `}`|  
|Evento|Convenzione Pascal|`public class Process {` <br />  `public event EventHandler Exited;` <br /> `}`|  
|Campo|Convenzione Pascal|`public class MessageQueue {` <br />  `public static readonly TimeSpan` <br /> `InfiniteTimeout;` <br /> `}` <br /> `public struct UInt32 {` <br />  `public const Min = 0;` <br /> `}`|  
|Valore enum|Convenzione Pascal|`public enum FileMode {` <br />  `Append,` <br />  `...` <br /> `}`|  
|Parametro|Convenzione camel|`public class Convert {` <br />  `public static int ToInt32(string value);` <br /> `}`|  
  
## Sfruttando le parole composte e termini comuni  
 La maggior parte dei termini composti vengono considerate come singole parole ai fini di lettere maiuscole\/minuscole.  
  
 **X non** tutte iniziali maiuscole in cosiddette parole composte forma chiusa.  
  
 Queste sono le parole composte scritte come una singola parola, ad esempio endpoint. Ai fini di linee guida di maiuscole e minuscole, considerare una chiusura parola composta come una singola parola. Utilizzare un dizionario corrente per determinare se una parola composta è scritto in formato chiuso.  
  
|Convenzione Pascal|Convenzione camel|Non|  
|------------------------|-----------------------|---------|  
|`BitFlag`|`bitFlag`|`Bitflag`|  
|`Callback`|`callback`|`CallBack`|  
|`Canceled`|`canceled`|`Cancelled`|  
|`DoNot`|`doNot`|`Don't`|  
|`Email`|`email`|`EMail`|  
|`Endpoint`|`endpoint`|`EndPoint`|  
|`FileName`|`fileName`|`Filename`|  
|`Gridline`|`gridline`|`GridLine`|  
|`Hashtable`|`hashtable`|`HashTable`|  
|`Id`|`id`|`ID`|  
|`Indexes`|`indexes`|`Indices`|  
|`LogOff`|`logOff`|`LogOut`|  
|`LogOn`|`logOn`|`LogIn`|  
|`Metadata`|`metadata`|`MetaData, metaData`|  
|`Multipanel`|`multipanel`|`MultiPanel`|  
|`Multiview`|`multiview`|`MultiView`|  
|`Namespace`|`namespace`|`NameSpace`|  
|`Ok`|`ok`|`OK`|  
|`Pi`|`pi`|`PI`|  
|`Placeholder`|`placeholder`|`PlaceHolder`|  
|`SignIn`|`signIn`|`SignOn`|  
|`SignOut`|`signOut`|`SignOff`|  
|`UserName`|`userName`|`Username`|  
|`WhiteSpace`|`whiteSpace`|`Whitespace`|  
|`Writable`|`writable`|`Writeable`|  
  
## Distinzione fra maiuscole e minuscole  
 Linguaggi eseguiti su CLR non è richiesta per supportare la distinzione maiuscole\/minuscole, anche se alcuni. Anche se è la lingua supportata, altri linguaggi che potrebbero accedere il framework non. Le API che sono accessibili dall'esterno, pertanto, possono basarsi sui case singolarmente per distinguere i due nomi nello stesso contesto.  
  
 **X non** si presume che tutti i linguaggi di programmazione tra maiuscole e minuscole. Non sono. I nomi non può essere diversa di maiuscole\/minuscole solo.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Convenzioni di denominazione](../../../docs/standard/design-guidelines/naming-guidelines.md)