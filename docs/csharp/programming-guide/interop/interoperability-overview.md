---
title: "Cenni preliminari sull&quot;interoperabilità (Guida per programmatori C#) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- COM interop
- C# language, interoperability
- C++ Interop
- interoperability, about interoperability
- platform invoke
ms.assetid: c025b2e0-2357-4c27-8461-118f0090aeff
caps.latest.revision: 43
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
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 5084c4af3334c39f844fec67a1ab05dd9443bf27
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="interoperability-overview-c-programming-guide"></a>Cenni preliminari sull'interoperabilità (Guida per programmatori C#)
In questo argomento vengono descritti i metodi per consentire l'interoperabilità tra il codice gestito C# e il codice non gestito.  
  
## <a name="platform-invoke"></a>Platform invoke  
 *Platform invoke* è un servizio che consente al codice gestito di chiamare funzioni non gestite implementate in librerie a collegamento dinamico (DLL), come quelle nell'API Microsoft Win32. Individua e richiama una funzione esportata ed esegue il marshalling degli argomenti (Integer, stringhe, matrici, strutture e così via) nel limite dell'interazione, in base alle necessità.  
  
 Per altre informazioni, vedere [Consuming Unmanaged DLL Functions](../../../framework/interop/consuming-unmanaged-dll-functions.md) (Uso di funzioni DLL non gestite) e [Procedura: Usare platform invoke per riprodurre un file audio](../../../csharp/programming-guide/interop/how-to-use-platform-invoke-to-play-a-wave-file.md).  
  
> [!NOTE]
>  Il [Common Language Runtime](../../../standard/clr.md) (CLR) gestisce l'accesso alle risorse di sistema. La chiamata di codice non gestito esterno al CLR ignora questo meccanismo di sicurezza e presenta pertanto un rischio per la sicurezza. Ad esempio, il codice non gestito può chiamare direttamente le risorse nel codice non gestito, ignorando i meccanismi di sicurezza CLR. Per altre informazioni, vedere [Protezione di .NET Framework](http://go.microsoft.com/fwlink/?LinkId=37122).  
  
## <a name="c-interop"></a>interoperabilità C++  
 È possibile usare l'interoperabilità C++, nota anche come It Just Works (IJW), per eseguire il wrapping di una classe C++ nativa in modo che possa essere usata dal codice creato in C# o in un altro linguaggio .NET Framework. A tale scopo, scrivere codice C++ per eseguire il wrapping di un componente COM o DLL nativo. A differenza degli altri linguaggi .NET Framework, [!INCLUDE[vcprvc](../../../csharp/programming-guide/interop/includes/vcprvc_md.md)] offre un supporto all'interoperabilità che consente la presenza di codice gestito e non gestito nella stessa applicazione e perfino nello stesso file. Compilare quindi il codice C++ mediante l'opzione del compilatore **/clr** per produrre un assembly gestito. Infine, aggiungere un riferimento all'assembly nel progetto C# e usare gli oggetti con wrapping esattamente come si userebbero altre classi gestite.  
  
## <a name="exposing-com-components-to-c"></a>Esposizione di componenti COM a C#  
 È possibile usare un componente COM da un progetto C#. La procedura generale è la seguente:  
  
1.  Individuare un componente COM da usare e registrarlo. Usare regsvr32.exe per registrare o annullare la registrazione di una DLL COM.  
  
2.  Aggiungere al progetto un riferimento alla libreria dei componenti o dei tipi COM.  
  
     Quando si aggiunge il riferimento [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] usa [Tlbimp.exe (utilità di importazione della libreria dei tipi)](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382), che accetta una libreria dei tipi come input, per generare un assembly di interoperabilità di .NET Framework. L'assembly, denominato anche Runtime Callable Wrapper (RCW), contiene le classi gestite e le interfacce che eseguono il wrapping delle classi e interfacce COM presenti nella libreria dei tipi. [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] aggiunge al progetto un riferimento all'assembly generato.  
  
3.  Creare un'istanza di una classe definita nell'RCW. Essa, a sua volta, crea un'istanza dell'oggetto COM.  
  
4.  Usare l'oggetto allo stesso modo di altri oggetti gestiti. Quando l'oggetto viene recuperato da Garbage Collection, anche l'istanza dell'oggetto COM viene rilasciata dalla memoria.  
  
 Per altre informazioni, vedere [Esposizione di componenti COM a .NET Framework](http://msdn.microsoft.com/library/e78b14f1-e487-43cd-9c6d-1a07483f1730).  
  
## <a name="exposing-c-to-com"></a>Esposizione di C# a COM  
 I client COM possono usare i tipi di C# che sono stati esposti in modo corretto. I passaggi di base per esporre tipi di C# sono i seguenti:  
  
1.  Aggiungere gli attributi di interoperabilità nel progetto C#.  
  
     È possibile rendere un assembly visibile a COM modificando le proprietà di progetto [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)]. Per altre informazioni, vedere [Finestra di dialogo Informazioni assembly](https://docs.microsoft.com/visualstudio/ide/reference/assembly-information-dialog-box).  
  
2.  Generare una libreria dei tipi COM e registrarla per l'uso di COM.  
  
     È possibile modificare le proprietà di progetto [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] per registrare automaticamente l'assembly C# per l'interoperabilità COM. [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] usa [Regasm.exe (strumento di registrazione di assembly)](http://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb), tramite l'opzione della riga di comando `/tlb`, che accetta un assembly gestito come input, per generare una libreria dei tipi. Questa libreria dei tipi descrive i tipi `public` nell'assembly e aggiunge le voci del Registro di sistema in modo che i client COM possano creare classi gestite.  
  
 Per altre informazioni, vedere [Esposizione di componenti .NET Framework a COM](http://msdn.microsoft.com/library/e42a65f7-1e61-411f-b09a-aca1bbce24c6) e [Esempio di classe COM](../../../csharp/programming-guide/interop/example-com-class.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Improving Interop Performance](http://go.microsoft.com/fwlink/?LinkId=99564)  (Miglioramento delle prestazioni di interoperabilità)  
 [Introduzione all'interoperabilità COM](http://go.microsoft.com/fwlink/?LinkId=112406)   
 [Marshaling between Managed and Unmanaged Code](http://go.microsoft.com/fwlink/?LinkId=112398)  (Marshalling tra codice gestito e non gestito)  
 [Interoperabilità con codice non gestito](https://msdn.microsoft.com/library/sd10k43k)   
 [Interoperabilità COM avanzata](http://msdn.microsoft.com/en-us/3ada36e5-2390-4d70-b490-6ad8de92f2fb)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)
