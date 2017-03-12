---
title: "Cenni preliminari sull&#39;interoperabilit&#224; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, interoperabilità"
  - "interoperabilità C++"
  - "interoperabilità COM"
  - "interoperabilità, informazioni sull'interoperabilità"
  - "platform invoke"
ms.assetid: c025b2e0-2357-4c27-8461-118f0090aeff
caps.latest.revision: 43
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 43
---
# Cenni preliminari sull&#39;interoperabilit&#224; (Guida per programmatori C#)
In questo argomento vengono descritti i metodi per attivare l'interoperabilità tra codice gestito e non gestito in C\#.  
  
## Platform Invoke  
 *Platform invoke* costituisce un servizio che consente la chiamata di funzioni non gestite implementate in librerie a collegamento dinamico \(DLL, Dynamic\-Link Library\), quali quelle della API Microsoft Win32, da parte del codice gestito.  Tale servizio trova e chiama una funzione esportata ed esegue il marshalling dei relativi argomenti \(interi, stringhe, matrici, strutture e così via\) nell'attraversamento dei limiti di interoperabilità, secondo necessità.  
  
 Per ulteriori informazioni, vedere [Consuming Unmanaged DLL Functions](../Topic/Consuming%20Unmanaged%20DLL%20Functions.md) e [Procedura: utilizzare platform invoke per riprodurre un file audio](../../../csharp/programming-guide/interop/how-to-use-platform-invoke-to-play-a-wave-file.md).  
  
> [!NOTE]
>  [Common Language Runtime](../Topic/Common%20Language%20Runtime%20\(CLR\).md) \(CLR\) gestisce l'accesso alle risorse di sistema.  La chiamata del codice gestito all'esterno di CLR consente di ignorare il meccanismo di sicurezza e pertanto costituisce un rischio per la sicurezza.  Il codice non gestito può ad esempio chiamare direttamente le risorse nel codice non gestito, ignorando i meccanismi di sicurezza di CLR.  Per ulteriori informazioni, [.NET Framework Security](http://go.microsoft.com/fwlink/?LinkId=37122) \(informazioni in lingua inglese\).  
  
## Interoperabilità C\+\+  
 È possibile utilizzare l'interoperabilità C\+\+, nota anche come It Just Works \(IJW\), per eseguire il wrapping di una classe C\+\+ nativa in modo che possa essere utilizzata da codice creato in C\# o in un altro linguaggio .NET Framework.  A tale scopo, scrivere il codice C\+\+ per eseguire il wrapping di un componente DLL o COM nativo.  A differenza degli altri linguaggi .NET Framework, in [!INCLUDE[vcprvc](../../../csharp/programming-guide/interop/includes/vcprvc-md.md)] viene fornito il supporto per l'interoperabilità che consente la presenza di codice gestito e codice non gestito nella stessa applicazione e persino nello stesso file.  Quindi compilare il codice C\+\+ mediante l'opzione **\/clr** del compilatore per produrre un assembly gestito.  Infine, aggiungere un riferimento all'assembly nel progetto C\# e utilizzare gli oggetti di cui è stato eseguito il wrapping nello stesso modo in cui verrebbero utilizzate altre classi gestite.  
  
## Esposizione di componenti COM a C\#  
 È possibile utilizzare un componente COM da un progetto C\#.  La procedura generale è la seguente:  
  
1.  Individuare un componente COM da utilizzare e registrarlo.  Per registrare o annullare la registrazione di una DLL COM, utilizzare regsvr32.exe.  
  
2.  Aggiungere al progetto un riferimento al componente COM o alla libreria dei tipi.  
  
     Quando si aggiunge il riferimento, [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] utilizza [Tlbimp.exe \(Type Library Importer\)](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md), che accetta una libreria dei tipi come input, per generare come output un assembly di interoperabilità .NET Framework.  L'assembly, denominato anche Runtime Callable Wrapper \(RCW\), contiene classi e interfacce gestite che eseguono il wrapping delle classi e delle interfacce COM presenti nella libreria dei tipi.   [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] aggiunge al progetto un riferimento per l'assembly generato.  
  
3.  Creare un'istanza di una classe definita in RCW.  Questa operazione crea, a sua volta, un'istanza dell'oggetto COM.  
  
4.  Utilizzare l'oggetto nello stesso modo in cui si utilizzano altri oggetti gestiti.  Quando l'oggetto viene recuperato tramite Garbage Collection, anche l'istanza dell'oggetto COM viene rilasciata dalla memoria.  
  
 Per ulteriori informazioni, vedere [Exposing COM Components to the .NET Framework](../Topic/Exposing%20COM%20Components%20to%20the%20.NET%20Framework.md).  
  
## Esposizione di C\# a COM  
 I client COM possono utilizzare i tipi C\# esposti correttamente.  Le operazioni da eseguire per esporre i tipi C\# sono elencate di seguito.  
  
1.  Aggiungere attributi di interoperabilità al progetto C\#.  
  
     È possibile rendere visibile un assembly COM modificando le proprietà del progetto [!INCLUDE[csprcs](../../../csharp/includes/csprcs-md.md)].  Per ulteriori informazioni, vedere [Finestra di dialogo Informazioni assembly](/visual-studio/ide/reference/assembly-information-dialog-box).  
  
2.  Generare una libreria dei tipi COM e registrarla per l'utilizzo di COM  
  
     È possibile modificare le proprietà del progetto [!INCLUDE[csprcs](../../../csharp/includes/csprcs-md.md)] per registrare automaticamente l'assembly C\# per l'interoperabilità COM.  [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] utilizza [Regasm.exe \(Assembly Registration Tool\)](../Topic/Regasm.exe%20\(Assembly%20Registration%20Tool\).md), mediante l'opzione della riga di comando `/tlb` che accetta un assembly gestito come input per generare una libreria dei tipi.  In questa libreria dei tipi vengono descritti i tipi `public` nell'assembly e aggiunte voci del Registro per consentire ai client COM di creare classi gestite.  
  
 Per ulteriori informazioni, vedere [Exposing .NET Framework Components to COM](../Topic/Exposing%20.NET%20Framework%20Components%20to%20COM.md) e [Esempio di classe COM](../../../csharp/programming-guide/interop/example-com-class.md).  
  
## Vedere anche  
 [Miglioramento delle prestazioni di interoperabilità](http://go.microsoft.com/fwlink/?LinkId=99564)   
 [Introduzione di interoperabilità COM](http://go.microsoft.com/fwlink/?LinkId=112406)   
 [Marshalling tra codice gestito e non gestito](http://go.microsoft.com/fwlink/?LinkId=112398)   
 [Interoperating with Unmanaged Code](../Topic/Interoperating%20with%20Unmanaged%20Code.md)   
 [Advanced COM Interoperability](http://msdn.microsoft.com/it-it/3ada36e5-2390-4d70-b490-6ad8de92f2fb)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)