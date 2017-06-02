---
title: "Marshaling Data with Platform Invoke | Microsoft Docs"
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
  - "platform invoke, marshaling data"
  - "data marshaling, platform invoke"
  - "marshaling, platform invoke"
ms.assetid: dc5c76cf-7b12-406f-b79c-d1a023ec245d
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Marshaling Data with Platform Invoke
Per chiamare le funzioni esportate da una libreria non gestita, un'applicazione .NET Framework richiede un prototipo di funzione nel codice gestito che rappresenta la funzione non gestita.  Per creare un prototipo che abiliti PInvoke per il marshalling dei dati in modo corretto, è necessario eseguire le operazioni seguenti:  
  
-   Applicare l'attributo [DLLImportAttribute](frlrfSystemRuntimeInteropServicesDllImportAttributeClassTopic) alla funzione o al metodo statico nel codice gestito.  
  
-   Sostituire i tipi di dati non gestiti con tipi di dati gestiti.  
  
 È possibile usare la documentazione fornita con una funzione non gestita per costruire un prototipo gestito equivalente, applicando l'attributo con i relativi campi facoltativi e sostituendo i tipi di dati non gestiti con quelli gestiti.  Per istruzioni su come applicare l'attributo **DllImportAttribute**, vedere [Utilizzo di funzioni DLL non gestite](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md).  
  
 Questa sezione fornisce esempi che dimostrano come creare prototipi di funzioni gestite per passare argomenti e ricevere valori restituiti da funzioni esportate mediante librerie non gestite.  Gli esempi illustrano anche l'uso dell'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> e della classe <xref:System.Runtime.InteropServices.Marshal> per effettuare il marshalling esplicito dei dati.  
  
## Tipi di dati PInvoke  
 La tabella seguente include un elenco di tipi di dati usati nell'API Win32 \(elencati in Wtypes.h\) e nelle funzioni di tipo C.  Molte librerie non gestite contengono funzioni che passano questi tipi di dati come parametri e valori restituiti.  La terza colonna indica il tipo di valore o la classe incorporata corrispondente di .NET Framework che si usa nel codice gestito.  In alcuni casi, è possibile sostituire il tipo elencato nella tabella con un tipo delle stesse dimensioni.  
  
|Tipo non gestito in Wtypes.h|Tipo non gestito del linguaggio C|Nome della classe gestita|Descrizione|  
|----------------------------------|---------------------------------------|-------------------------------|-----------------|  
|**HANDLE**|**void\***|<xref:System.IntPtr?displayProperty=fullName>|32 bit nei sistemi operativi Windows a 32 bit, 64 bit nei sistemi operativi Windows a 64 bit.|  
|**BYTE**|**unsigned char**|<xref:System.Byte?displayProperty=fullName>|8 bit|  
|**SHORT**|**short**|<xref:System.Int16?displayProperty=fullName>|16 bit|  
|**WORD**|**unsigned short**|<xref:System.UInt16?displayProperty=fullName>|16 bit|  
|**INT**|**int**|<xref:System.Int32?displayProperty=fullName>|32 bit|  
|**UINT**|**unsigned int**|<xref:System.UInt32?displayProperty=fullName>|32 bit|  
|**LONG**|**long**|<xref:System.Int32?displayProperty=fullName>|32 bit|  
|**BOOL**|**long**|[\<caps:sentence id\="tgt48" sentenceid\="f5f846452032b75e5fcec49a05fe125a" class\="tgtSentence"\>System.Int32\<\/caps:sentence\>](https://msdn.microsoft.com/en-us/library/system.byte.aspx)|32 bit|  
|**DWORD**|**unsigned long**|<xref:System.UInt32?displayProperty=fullName>|32 bit|  
|**ULONG**|**unsigned long**|<xref:System.UInt32?displayProperty=fullName>|32 bit|  
|**CHAR**|**char**|<xref:System.Char?displayProperty=fullName>|Decorare con ANSI.|  
|**WCHAR**|**wchar\_t**|<xref:System.Char?displayProperty=fullName>|Decorare con Unicode.|  
|**LPSTR**|**char\***|<xref:System.String?displayProperty=fullName> o <xref:System.Text.StringBuilder?displayProperty=fullName>|Decorare con ANSI.|  
|**LPCSTR**|**Const char\***|<xref:System.String?displayProperty=fullName> o <xref:System.Text.StringBuilder?displayProperty=fullName>|Decorare con ANSI.|  
|**LPWSTR**|**wchar\_t\***|<xref:System.String?displayProperty=fullName> o <xref:System.Text.StringBuilder?displayProperty=fullName>|Decorare con Unicode.|  
|**LPCWSTR**|**Const wchar\_t\***|<xref:System.String?displayProperty=fullName> o <xref:System.Text.StringBuilder?displayProperty=fullName>|Decorare con Unicode.|  
|**FLOAT**|**Float**|<xref:System.Single?displayProperty=fullName>|32 bit|  
|**DOUBLE**|**Double**|<xref:System.Double?displayProperty=fullName>|64 bit|  
  
 Per i tipi corrispondenti in [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)], C\# e C\+\+, vedere [Panoramica della libreria di classi .NET Framework](../../../docs/standard/class-library-overview.md).  
  
## PinvokeLib.dll  
 Il codice seguente definisce le funzioni della libreria fornite da Pinvoke.dll.  Molti esempi descritti in questa sezione chiamano questa libreria.  
  
### Esempio  
 [!code-cpp[PInvokeLib#1](../../../samples/snippets/cpp/VS_Snippets_CLR/pinvokelib/cpp/pinvokelib.cpp#1)]  
  
 [!code-cpp[PInvokeLib#2](../../../samples/snippets/cpp/VS_Snippets_CLR/pinvokelib/cpp/pinvokelib.h#2)]