---
title: "Procedura: intercettare un&#39;eccezione non CLS | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "eccezioni [C#], non CLS"
ms.assetid: db4630b3-5240-471a-b3a7-c7ff6ab31e8d
caps.latest.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 8
---
# Procedura: intercettare un&#39;eccezione non CLS
Alcuni linguaggi .NET, incluso C\+\+\/CLI, consentono agli oggetti di generare eccezioni che non derivano dalla classe <xref:System.Exception>.  Tali eccezioni sono chiamate *eccezioni non CLS* o *non eccezioni*.  In [!INCLUDE[csprcs](../../../csharp/includes/csprcs-md.md)] non è possibile generare eccezioni non CLS, ma è possibile intercettarle in due modi:  
  
-   All'interno di un blocco `catch (Exception e)` come classe <xref:System.Runtime.CompilerServices.RuntimeWrappedException>.  
  
     Per impostazione predefinita, in [!INCLUDE[csprcs](../../../csharp/includes/csprcs-md.md)] un assembly intercetta eccezioni non CLS come eccezioni wrapped.  Utilizzare questo metodo se è necessario accedere all'eccezione originale, a cui è possibile accedere tramite la proprietà <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A>.  Nella procedura descritta più avanti in questo argomento viene illustrato come intercettare le eccezioni in questo modo.  
  
-   All'interno di un blocco catch generale \(un blocco catch senza tipo di eccezione specificato\) posizionato dopo un blocco `catch (Exception)` o `catch (Exception e)`.  
  
     Utilizzare questo metodo se si desidera eseguire un'azione \(ad esempio la scrittura in un file di log\) in risposta alle eccezioni non CLS e non è necessario accedere alle informazioni sull'eccezione.  Per impostazione predefinita, Common Language Runtime esegue il wrapping di tutte le eccezioni.  Per disabilitare questo comportamento, aggiungere questo attributo a livello di assembly al codice, in genere nel file AssemblyInfo.cs: `[assembly: RuntimeCompatibilityAttribute(WrapNonExceptionThrows = false)]`.  
  
### Per intercettare un'eccezione non CLS  
  
1.  All'interno di un `catch(Exception e) block` utilizzare la parola chiave `as` per verificare se è possibile eseguire il cast di `e` nella classe <xref:System.Runtime.CompilerServices.RuntimeWrappedException>.  
  
2.  Accedere all'eccezione originale tramite la proprietà <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A>.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come intercettare un'eccezione non CLS generata da una libreria di classi scritta in C\+\+\/CLR.  Si noti che in questo esempio il codice client di [!INCLUDE[csprcs](../../../csharp/includes/csprcs-md.md)] sa in anticipo che il tipo di eccezione generato è <xref:System.String?displayProperty=fullName>.  È possibile eseguire il cast della proprietà <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A> al tipo originale a condizione che tale tipo sia accessibile dal codice.  
  
```  
// Class library written in C++/CLR.  
   ThrowNonCLS.Class1 myClass = new ThrowNonCLS.Class1();  
  
   try  
   {  
    // throws gcnew System::String(  
    // "I do not derive from System.Exception!");  
    myClass.TestThrow();   
   }  
  
   catch (Exception e)  
   {  
    RuntimeWrappedException rwe = e as RuntimeWrappedException;  
    if (rwe != null)      
    {  
      String s = rwe.WrappedException as String;  
      if (s != null)  
      {  
        Console.WriteLine(s);  
      }  
    }  
    else  
    {  
       // Handle other System.Exception types.  
    }  
   }             
```  
  
## Vedere anche  
 <xref:System.Runtime.CompilerServices.RuntimeWrappedException>   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)