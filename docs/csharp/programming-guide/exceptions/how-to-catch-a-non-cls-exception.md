---
title: 'Procedura: Rilevare un&quot;eccezione non CLS | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exceptions [C#], non-CLS
ms.assetid: db4630b3-5240-471a-b3a7-c7ff6ab31e8d
caps.latest.revision: 8
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3515ecab379a0e910cdd5ba82a4a39b085cc816f
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-catch-a-non-cls-exception"></a>Procedura: intercettare un'eccezione non CLS
Alcuni linguaggi .NET, incluso C++ /CLI, consentono agli oggetti di generare eccezioni che non derivano da <xref:System.Exception>. Tali eccezioni sono chiamate *eccezioni non CLS* o *non eccezioni*. In [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] non è possibile generare eccezioni non CLS, ma è possibile rilevarle in due modi:  
  
-   All'interno di un blocco `catch (Exception e)` come <xref:System.Runtime.CompilerServices.RuntimeWrappedException>.  
  
     Per impostazione predefinita, un assembly [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] rileva le eccezioni non CLS come eccezioni con wrapper. Usare questo metodo se è necessario accedere all'eccezione originale, accessibile tramite la proprietà <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A>. La procedura illustrata più avanti in questo argomento spiega come rilevare le eccezioni in questo modo.  
  
-   All'interno di un blocco catch generale, ovvero un blocco catch senza un tipo di eccezione specificato, posizionato dopo un blocco `catch (Exception)` o `catch (Exception e)`.  
  
     Usare questo metodo quando si vuole eseguire un'azione, come ad esempio la scrittura in un file di log, in risposta alle eccezioni non CLS e non è necessario accedere alle informazioni dell'eccezione. Per impostazione predefinita, Common Language Runtime esegue il wrapping di tutte le eccezioni. Per disabilitare questo comportamento, aggiungere l'attributo a livello di assembly seguente al codice, in genere nel file AssemblyInfo.cs: `[assembly: RuntimeCompatibilityAttribute(WrapNonExceptionThrows = false)]`.  
  
### <a name="to-catch-a-non-cls-exception"></a>Per rilevare un'eccezione non CLS  
  
1.  All'interno di un blocco `catch(Exception e) block` usare la parola chiave `as` per verificare se è possibile eseguire il cast di `e` in <xref:System.Runtime.CompilerServices.RuntimeWrappedException>.  
  
2.  Accedere all'eccezione originale tramite la proprietà <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A>.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come rilevare un'eccezione non CLS generata da una libreria di classi scritta in C++/CLR. Si noti che in questo esempio il codice client di [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] sa in anticipo che il tipo di eccezione generato è <xref:System.String?displayProperty=fullName>. È possibile eseguire il cast della proprietà <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A> al tipo originale, purché tale tipo sia accessibile dal codice.  
  
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
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.CompilerServices.RuntimeWrappedException>   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/index.md)
