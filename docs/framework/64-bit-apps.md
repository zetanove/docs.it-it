---
title: Applicazioni a 64 bit | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- applications [C++], 64-bit
- 64-bit applications [C++]
- 64-bit programming [C++]
ms.assetid: fd4026bc-2c3d-4b27-86dc-ec5e96018181
caps.latest.revision: 53
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 987c7063c5e6dce10233761b6e37ed102d5878a9
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="64-bit-applications"></a>Applicazioni a 64 bit
Quando si compila un'applicazione, è possibile specificare che deve essere eseguita in un sistema operativo Windows a 64 bit come applicazione nativa o in WOW64 (Windows a 32 bit in Windows a 64 bit). WOW64 è un ambiente di compatibilità che consente di eseguire in un sistema a 64 bit un'applicazione a 32 bit. WOW64 è incluso in tutte le versioni a 64 bit del sistema operativo Windows.  
  
## <a name="running-32-bit-vs-64-bit-applications-on-windows"></a>Confronto tra l'esecuzione di applicazioni a 32 bit e a 64 bit in Windows  
 Tutte le applicazioni basate su .NET Framework 1.0 o 1.1 sono considerate applicazioni a 32 bit in un sistema operativo a 64 bit e vengono sempre eseguite in WOW64 e in Common Language Runtime (CLR) a 32 bit. Le applicazioni a 32 bit basate su [!INCLUDE[net_v40_long](../../includes/net-v40-long-md.md)] o versioni successive vengono eseguite anche in WOW64 in sistemi a 64 bit.  
  
 Visual Studio installa la versione a 32 bit di CLR in un computer x86 e sia la versione a 32 bit che la versione a 64 bit appropriata di CLR in un computer Windows a 64 bit. Poiché Visual Studio è un'applicazione a 32 bit, quando viene installato in un sistema a 64 bit, viene eseguito in WOW64.  
  
> [!NOTE]
>  Data la progettazione dell'emulazione x86 e del sottosistema WOW64 per la famiglia di processori Itanium, l'esecuzione delle applicazioni è limitata a un solo processore. Questi fattori riducono le prestazioni e la scalabilità delle applicazioni .NET Framework a 32 bit eseguite in sistemi basati su Itanium. Si consiglia di usare [!INCLUDE[net_v40_long](../../includes/net-v40-long-md.md)], che include il supporto a 64 bit nativo per sistemi basati su Itanium, per migliorare le prestazioni e la scalabilità.  
  
 Per impostazione predefinita, quando si esegue un'applicazione gestita a 64 bit in un sistema operativo Windows a 64 bit, non è possibile creare oggetti di più di 2 gigabyte (GB). Tuttavia, in [!INCLUDE[net_v45](../../includes/net-v45-md.md)], è possibile aumentare questo limite.  Per altre informazioni, vedere l'[elemento \<gcAllowVeryLargeObjects>](../../docs/framework/configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md).  
  
 Molti assembly vengono eseguiti allo stesso modo sia su CLR a 32 bit che su CLR a 64 bit. Tuttavia, alcuni programmi possono comportarsi in modo diverso, a seconda della versione di CLR, se contengono uno o più dei seguenti elementi:  
  
-   Strutture contenenti membri che cambiano dimensione in base alla piattaforma (ad esempio, tutti i tipi puntatore).  
  
-   Operazioni aritmetiche che includono dimensioni costanti.  
  
-   Dichiarazioni pInvoke o COM non corrette che usano `Int32` anziché `IntPtr` per gli handle.  
  
-   Codice che esegue il cast di `IntPtr` a `Int32`.  
  
 Per altre informazioni su come eseguire il trasferimento di un'applicazione a 32 bit in modo che funzioni in CLR a 64 bit, vedere la pagina relativa alla [migrazione del codice gestito da 32 bit a 64 bit](http://go.microsoft.com/fwlink/?LinkId=150542) in MSDN Library.  
  
## <a name="general-64-bit-programming-information"></a>Informazioni generali sulla programmazione a 64 bit  
 Per informazioni generali sulla programmazione a 64 bit, vedere i seguenti documenti:  
  
-   Per altre informazioni sulla versione a 64 bit di CLR in un computer Windows a 64 bit, vedere la pagina relativa al [Centro per sviluppatori .NET Framework](http://go.microsoft.com/fwlink/?LinkId=37079) sul sito Web di MSDN.  
  
-   Nella documentazione di [!INCLUDE[winsdkshort](../../includes/winsdkshort-md.md)] vedere la pagina relativa alla [guida alla programmazione per Windows a 64 bit](http://go.microsoft.com/fwlink/p/?LinkId=253512).  
  
-   Per informazioni su come scaricare una versione a 64 bit di CLR, vedere la [pagina di download del Centro per sviluppatori .NET Framework](http://go.microsoft.com/fwlink/?LinkId=50953) sul sito Web di MSDN.  
  
-   Per informazioni sul supporto di Visual Studio per la creazione di applicazioni a 64 bit, vedere [Supporto a 64 bit per IDE di Visual Studio](http://msdn.microsoft.com/library/b08ff3ad-c6fd-468f-94d5-01a61aab6833).  
  
## <a name="compiler-support-for-creating-64-bit-applications"></a>Supporto dei compilatori per la creazione di applicazioni a 64 Bit  
 Per impostazione predefinita, quando si usa .NET Framework per compilare un'applicazione in un computer a 32 bit o a 64 bit, l'applicazione verrà eseguita in un computer a 64 bit come applicazione nativa (ovvero, non in WOW64). La tabella seguente elenca i documenti che illustrano come usare i compilatori di Visual Studio per creare applicazioni a 64 bit che verranno eseguite come native, in WOW64 o in entrambi i modi.  
  
|Compilatore|Opzione del compilatore|  
|--------------|---------------------|  
|Visual Basic|[/platform (Visual Basic)](~/docs/visual-basic/reference/command-line-compiler/platform.md)|  
|Visual C#|[/platform (opzioni del compilatore C#)](~/docs/csharp/language-reference/compiler-options/platform-compiler-option.md)|  
|Visual C++|È possibile creare applicazioni Microsoft Intermediate Language (MSIL) indipendenti dalla piattaforma usando **/clr:safe**. Per altre informazioni, vedere [/clr (Compilazione Common Language Runtime)](/cpp/build/reference/clr-common-language-runtime-compilation).<br /><br /> Visual C++ include un compilatore separato per ogni sistema operativo a 64 bit. Per altre informazioni sull'uso di Visual C++ per creare applicazioni native eseguibili in un sistema operativo Windows a 64 bit, vedere [Programmazione a 64 bit con Visual C++](http://msdn.microsoft.com/library/h2k70f3s\(v=vs.80\)).|  
  
## <a name="determining-the-status-of-an-exe-file-or-dll-file"></a>Determinazione dello stato di un file EXE o di un file DLL  
 Per determinare se un file EXE o un file DLL deve essere eseguito solo su una piattaforma specifica o in WOW64, usare [CorFlags.exe (strumento di conversione CorFlags)](../../docs/framework/tools/corflags-exe-corflags-conversion-tool.md) senza opzioni. È anche possibile usare CorFlags.exe per modificare lo stato della piattaforma di un file EXE o di un file DLL. Il numero di versione del runtime principale dell'intestazione CLR di un assembly di Visual Studio è impostato su 2, mentre quello secondario è impostato su 5. Le applicazioni con la versione di runtime secondaria impostata su 0 sono considerate applicazioni legacy e vengono sempre eseguite in WOW64.  
  
 Per eseguire query a livello di codice di un file EXE o DLL per determinare se deve essere eseguito solo su una piattaforma specifica o in WOW64, usare il metodo <xref:System.Reflection.Module.GetPEKind%2A?displayProperty=fullName>.
