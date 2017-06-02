---
title: "Procedura: caricare assembly in un dominio applicazione | Microsoft Docs"
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
  - "domini applicazione, caricamento di assembly"
  - "caricamento di assembly"
ms.assetid: 1432aa2d-bd83-4346-bf3b-a1b7920e2aa9
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: caricare assembly in un dominio applicazione
È possibile procedere in diversi modi per caricare un assembly in un dominio applicazione.  L'approccio consigliato è l'utilizzo del metodo <xref:System.Reflection.Assembly.Load%2A> `static` \(`Shared` in Visual Basic\) della classe [System.Reflection.Assembly](https://msdn.microsoft.com/en-us/library/system.reflection.aspx).  Per caricare gli assembly è possibile inoltre utilizzare i seguenti metodi:  
  
-   Il metodo <xref:System.Reflection.Assembly.LoadFrom%2A> della classe [Assembly](https://msdn.microsoft.com/en-us/library/system.reflection.aspx) per caricare un assembly specificando il percorso del file.  Se gli assembly vengono caricati utilizzando questo metodo viene utilizzato un contesto di caricamento diverso.  
  
-   I metodi <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A> e <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> per caricare un assembly nel contesto ReflectionOnly.  Gli assembly caricati in questo contesto possono essere esaminati ma non eseguiti. In questo modo è possibile esaminare assembly destinati ad altre piattaforme.  Vedere [How to: Load Assemblies into the Reflection\-Only Context](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md).  
  
> [!NOTE]
>  Il contesto ReflectionOnly è stata introdotto con .NET Framework versione 2.0.  
  
-   Metodi quali <xref:System.AppDomain.CreateInstance%2A> e <xref:System.AppDomain.CreateInstanceAndUnwrap%2A> della classe <xref:System.AppDomain> per caricare assembly in un dominio dell'applicazione.  
  
-   Il metodo <xref:System.Type.GetType%2A> della classe <xref:System.Type> per caricare assembly.  
  
-   Il metodo <xref:System.AppDomain.Load%2A> della classe <xref:System.AppDomain?displayProperty=fullName> per caricare assembly, anche se è utilizzato principalmente per l'interoperabilità COM.  Non utilizzarlo per caricare assembly in un dominio applicazione diverso da quello da cui è chiamato.  
  
> [!NOTE]
>  A partire da .NET Framework versione 2.0, il runtime non carica un assembly compilato con una versione di .NET Framework successiva a quella del runtime attualmente caricato.  Questa indicazione è valida per la combinazione di componenti principali e secondari del numero di versione.  
  
 È possibile specificare la modalità di condivisione del codice con compilazione JIT tra domini applicazione.  Per ulteriori informazioni, vedere [Application Domains and Assemblies](http://msdn.microsoft.com/it-it/433b04ae-4ba8-4849-9dbd-79194f240346).  
  
## Esempio  
 Nel codice riportato di seguito si carica un assembly denominato "example.exe" o "example.dll" nel dominio applicazione corrente, si ottiene un tipo denominato `Example` dall'assembly, si ottiene un metodo senza parametri denominato `MethodA` per tale tipo e si esegue il metodo.  Per un'illustrazione completa sulle modalità di recupero di informazioni da un assembly caricato, vedere [Caricamento dinamico e utilizzo dei tipi](../../../docs/framework/reflection-and-codedom/dynamically-loading-and-using-types.md).  
  
 [!code-cpp[System.AppDomain.Load#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source2.cpp#2)]
 [!code-csharp[System.AppDomain.Load#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source2.cs#2)]
 [!code-vb[System.AppDomain.Load#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source2.vb#2)]  
  
## Vedere anche  
 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A>   
 [Hosting Overview](http://msdn.microsoft.com/it-it/ea527626-99e3-4995-81c4-c8f3e60eb6d5)   
 [Programming with Application Domains](http://msdn.microsoft.com/it-it/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [Reflection](../../../docs/framework/reflection-and-codedom/reflection.md)   
 [Uso dei domini dell'applicazione](../../../docs/framework/app-domains/use.md)   
 [How to: Load Assemblies into the Reflection\-Only Context](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)   
 [Application Domains and Assemblies](http://msdn.microsoft.com/it-it/433b04ae-4ba8-4849-9dbd-79194f240346)