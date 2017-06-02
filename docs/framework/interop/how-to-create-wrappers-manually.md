---
title: "How to: Create Wrappers Manually | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "wrappers, creating manually"
ms.assetid: cc2a70d8-6a58-4071-a8cf-ce28c018c09b
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Create Wrappers Manually
Se si decide di dichiarare manualmente i tipi COM nel codice sorgente gestito, è consigliabile iniziare con una libreria dei tipi o un file IDL esistente.  Se non si ha il file IDL o non è possibile generare un file di libreria dei tipi, simulare i tipi COM mediante la creazione di dichiarazioni gestite e l'esportazione dell'assembly risultante in una libreria dei tipi.  
  
### Per simulare i tipi COM dall'origine gestita  
  
1.  Dichiarare i tipi in un linguaggio conformi a Common Language Specification \(CLS\) e compilare il file.  
  
2.  Esportare l'assembly contenente i tipi con l'[utilità di esportazione della libreria dei tipi \(Tlbexp.exe\)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md).  
  
3.  Usare la libreria dei tipi COM esportata come base per la dichiarazione dei tipi gestiti orientati a COM.  
  
### Per creare un Runtime Callable Wrapper \(RCW\)  
  
1.  Se si dispone di un file IDL o di un file di libreria dei tipi, decidere quali classi e interfacce includere nell'RCW personalizzato.  È possibile escludere i tipi che non si intende usare direttamente o indirettamente nell'applicazione.  
  
2.  Creare un file di origine in un linguaggio conforme a Common Language Specification e dichiarare i tipi.  Per una descrizione completa del processo di conversione dell'importazione, vedere [Riepilogo della conversione della libreria dei tipi in assembly](http://msdn.microsoft.com/it-it/bf3f90c5-4770-4ab8-895c-3ba1055cc958).  In pratica, quando si crea un RCW personalizzato si esegue manualmente la conversione dei tipi fornita dall'[utilità di importazione della libreria dei tipi \(Tlbimp.exe\)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md).  Nell'esempio riportato nella sezione seguente vengono illustrati i tipi di un file della libreria dei tipi o IDL e i tipi corrispondenti nel codice C\#.  
  
3.  Dopo aver completato le dichiarazioni, compilare il file come si compila qualunque altro codice sorgente gestito.  
  
4.  Come per i tipi importati con Tlbimp.exe, alcuni tipi richiedono altre informazioni che è possibile aggiungere direttamente al codice.  Per dettagli, vedere [Procedura: Modificare assembly di interoperabilità](http://msdn.microsoft.com/it-it/16aacb20-2269-42bf-a812-b6a7df17e277).  
  
## Esempio  
 Il codice seguente mostra un esempio di interfaccia `ISATest` e di classe `SATest` in IDL e i tipi corrispondenti nel codice sorgente C\#.  
  
 **IDL o file di libreria dei tipi**  
  
```  
 [  
object,  
uuid(40A8C65D-2448-447A-B786-64682CBEF133),  
dual,  
helpstring("ISATest Interface"),  
pointer_default(unique)  
 ]  
interface ISATest : IDispatch  
 {  
[id(1), helpstring("method InSArray")]   
HRESULT InSArray([in] SAFEARRAY(int) *ppsa, [out,retval] int *pSum);  
 };  
 [  
uuid(116CCA1E-7E39-4515-9849-90790DA6431E),  
helpstring("SATest Class")  
 ]  
coclass SATest  
 {  
  [default] interface ISATest;  
 };  
```  
  
 **Wrapper nel codice sorgente gestito**  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
using System.Runtime.CompilerServices;  
  
[assembly:Guid("E4A992B8-6F5C-442C-96E7-C4778924C753")]  
[assembly:ImportedFromTypeLib("SAServerLib")]  
namespace SAServer  
{  
 [ComImport]  
 [Guid("40A8C65D-2448-447A-B786-64682CBEF133")]  
 [TypeLibType(TypeLibTypeFlags.FLicensed)]  
 public interface ISATest  
 {  
  [DispId(1)]  
  //[MethodImpl(MethodImplOptions.InternalCall,  
  // MethodCodeType=MethodCodeType.Runtime)]  
  int InSArray( [MarshalAs(UnmanagedType.SafeArray,  
      SafeArraySubType=VarEnum.VT_I4)] ref int[] param );  
 }   
 [ComImport]  
 [Guid("116CCA1E-7E39-4515-9849-90790DA6431E")]  
 [ClassInterface(ClassInterfaceType.None)]   
 [TypeLibType(TypeLibTypeFlags.FCanCreate)]  
 public class SATest : ISATest   
 {  
  [DispId(1)]  
  [MethodImpl(MethodImplOptions.InternalCall,   
  MethodCodeType=MethodCodeType.Runtime)]  
  extern int ISATest.InSArray( [MarshalAs(UnmanagedType.SafeArray,   
  SafeArraySubType=VarEnum.VT_I4)] ref int[] param );  
 }  
}  
```  
  
## Vedere anche  
 [Customizing Runtime Callable Wrappers](http://msdn.microsoft.com/it-it/4652beaf-77d0-4f37-9687-ca193288c0be)   
 [COM Data Types](http://msdn.microsoft.com/it-it/f93ae35d-a416-4218-8700-c8218cc90061)   
 [How to: Edit Interop Assemblies](http://msdn.microsoft.com/it-it/16aacb20-2269-42bf-a812-b6a7df17e277)   
 [Type Library to Assembly Conversion Summary](http://msdn.microsoft.com/it-it/bf3f90c5-4770-4ab8-895c-3ba1055cc958)   
 [Tlbimp.exe \(Type Library Importer\)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)   
 [Tlbexp.exe \(Type Library Exporter\)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)