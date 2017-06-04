---
title: "Inoltro dei tipi in Common Language Runtime | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assembly [.NET Framework], inoltro del tipo"
  - "inoltro del tipo"
ms.assetid: 51f8ffa3-c253-4201-a3d3-c4fad85ae097
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Inoltro dei tipi in Common Language Runtime
L'inoltro dei tipi consente di spostare un tipo in un altro assembly senza dover ricompilare le applicazioni in cui viene utilizzato l'assembly originale.  
  
 Si supponga ad esempio che in un'applicazione venga utilizzata la classe `Example` in un assembly denominato `Utility.dll`.  Gli sviluppatori dell'assembly `Utility.dll` possono decidere di eseguire il refactoring dell'assembly e di spostare nel corso del processo la classe `Example` in un altro assembly.  Se la versione precedente dell'assembly `Utility.dll` viene sostituita con la nuova versione dell'assembly `Utility.dll` e l'assembly complementare, l'applicazione in cui viene utilizzata la classe `Example` avrà esito negativo perché non è possibile trovare la classe `Example` nella nuova versione dell'assembly `Utility.dll`.  
  
 Gli sviluppatori dell'assembly `Utility.dll` possono ovviare a questo problema inoltrando richieste della classe `Example` utilizzando l'attributo <xref:System.Runtime.CompilerServices.TypeForwardedToAttribute>.  Se l'attributo è stato applicato alla nuova versione dell'assembly `Utility.dll`, le richieste della classe `Example` verranno inoltrate all'assembly in cui è ora contenuta la classe  e l'applicazione esistente continuerà a funzionare normalmente, senza ricompilazione.  
  
> [!NOTE]
>  In .NET Framework versione 2.0 non è possibile inoltrare i tipi da assembly scritti in Visual Basic.  È tuttavia possibile utilizzare in un'applicazione scritta in Visual Basic tipi inoltrati,  ovvero se nell'applicazione viene utilizzato un assembly codificato in C\# o C\+\+ e un tipo di questo assembly viene inoltrato a un altro assembly, nell'applicazione Visual Basic sarà possibile utilizzare il tipo inoltrato.  
  
## Inoltro di tipi  
 La procedura di inoltro dei tipi prevede quattro passaggi:  
  
1.  Spostare il codice sorgente del tipo dall'assembly originale nell'assembly di destinazione.  
  
2.  Nell'assembly originale del tipo aggiungere una classe <xref:System.Runtime.CompilerServices.TypeForwardedToAttribute> per il tipo spostato.  Nel codice riportato di seguito viene illustrato l'attributo per un tipo denominato `Example` che è stato spostato.  
  
    ```csharp  
    [assembly:TypeForwardedToAttribute(typeof(Example))]  
    ```  
  
    ```cpp#  
    [assembly:TypeForwardedToAttribute(Example::typeid)]  
    ```  
  
3.  Compilare l'assembly in cui è ora contenuto il tipo.  
  
4.  Ricompilare l'assembly originale del tipo, con un riferimento all'assembly in cui è ora contenuto il tipo.  Se ad esempio si compila un file C\# dalla riga di comando, utilizzare l'opzione [\/reference \(Import Metadata\)](../Topic/-reference%20\(C%23%20Compiler%20Options\).md) per specificare l'assembly contenente il tipo.  In C\+\+ utilizzare la direttiva [\#using](../Topic/%23using%20Directive%20\(C++\).md) nel file di origine per specificare l'assembly contenente il tipo.  
  
## Vedere anche  
 <xref:System.Runtime.CompilerServices.TypeForwardedToAttribute>   
 [Type Forwarding \(C\+\+\/CLI\)](../Topic/Type%20Forwarding%20\(C++-CLI\).md)   
 [Direttiva \#using](../Topic/%23using%20Directive%20\(C++\).md)