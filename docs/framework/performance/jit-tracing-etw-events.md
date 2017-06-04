---
title: "JIT Tracing ETW Events | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "JIT tracing events [.NET Framework]"
  - "ETW, JIT tracing events (CLR)"
ms.assetid: 926adde2-c123-452e-bf4f-4b977bf06ffb
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# JIT Tracing ETW Events
<a name="top"></a> Questi eventi raccolgono informazioni relative all'esito positivo o negativo dell'incorporamento Just\-In\-Time \(JIT\) e delle chiamate tail JIT.  
  
 Gli eventi di tracciatura JIT sono costituiti dalle due categorie riportate di seguito:  
  
-   [Eventi di incorporamento JIT](#jit_inlining_events)  
  
-   [Eventi delle chiamate tail JIT](#jit_tail_call_events)  
  
<a name="jit_inlining_events"></a>   
## Eventi di incorporamento JIT  
  
### Evento MethodJitInliningFailed  
 La tabella seguente illustra la parola chiave e il livello Per altre informazioni, vedere [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`JITTracingKeyword` \(0x10\)|Dettagliato \(5\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`MethodJitInliningFailed`|186|L'incorporamento JIT non è riuscito.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|MethodBeingCompiledNameSpace|win:UnicodeString|Spazio dei nomi del metodo compilato.|  
|MethodBeingCompiledName|win:UnicodeString|Nome del metodo compilato.|  
|MethodBeingCompiledNameSignature|win:UnicodeString|Firma del metodo compilato.|  
|InlinerNamespace|win:UnicodeString|Spazio dei nomi del metodo per cui il compilatore JIT sta provando a generare il codice.|  
|InlinerName|win:UnicodeString|Nome del metodo per cui il compilatore JIT sta provando a generare codice. Potrebbe non corrispondere a `MethodBeingCompiledName` se il compilatore sta provando a incorporare codice in `MethodBeingCompiledName` anziché generare una chiamata a `InlinerName`.|  
|InlinerNameSignature|win:UnicodeString|Firma dell'entità incorporatrice.|  
|InlineeNamespace|win:UnicodeString|Spazio dei nomi dell'entità incorporata.|  
|InlineeName|win:UnicodeString|Metodo che il compilatore sta provando a incorporare \(anziché generare una chiamata a tale metodo\).|  
|InlineeNameSignature|win:UnicodeString|Firma dell'entità incorporata.|  
|FailAlways|win:Boolean|Indicazione al compilatore JIT in merito al fatto che l'incorporamento avrà sempre esito negativo per l'entità incorporata.|  
|FailReason|win:UnicodeString|INLINE\_NEVER significa che, per via di un tentativo di incorporamento precedente, l'incorporamento non avrà mai esito positivo per altri motivi; in caso contrario, testo in formato libero.|  
|ClrInstanceID|win:UnicodeString|ID univoco per l'istanza di CLR o CoreCLR.|  
  
### MethodJitInliningSucceeded Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`JITTracingKeyword` \(0x10\)|Dettagliato \(5\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`MethodJitInliningSucceeded`|185|L'incorporamento del metodo è riuscito.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|MethodBeingCompiledNameSpace|win:UnicodeString|Spazio dei nomi del metodo compilato.|  
|MethodBeingCompiledName|win:UnicodeString|Nome del metodo compilato.|  
|MethodBeingCompiledNameSignature|win:UnicodeString|Firma del metodo compilato.|  
|InlinerNamespace|win:UnicodeString|Spazio dei nomi del metodo per cui il compilatore JIT sta provando a generare il codice.|  
|InlinerName|win:UnicodeString|Nome del metodo per cui il compilatore JIT sta provando a generare codice. Potrebbe non corrispondere a `MethodBeingCompiledName` se il compilatore sta provando a incorporare codice in `MethodBeingCompiledName` anziché generare una chiamata a `InlinerName`.|  
|InlinerNameSignature|win:UnicodeString|Firma dell'entità incorporatrice.|  
|InlineeNamespace|win:UnicodeString|Spazio dei nomi dell'entità incorporata.|  
|InlineeName|win:UnicodeString|Metodo che il compilatore sta provando a incorporare \(anziché generare una chiamata a tale metodo\).|  
|InlineeNameSignature|win:UnicodeString|Firma dell'entità incorporata.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="jit_tail_call_events"></a>   
## Eventi delle chiamate tail JIT  
  
### MethodJITTailCallFailed Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`JITTracingKeyword` \(0x10\)|Dettagliato \(5\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`MethodJitTailCallFailed`|189|La chiamata tail al metodo non è riuscita.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|MethodBeingCompiledNameSpace|win:UnicodeString|Spazio dei nomi del metodo compilato.|  
|MethodBeingCompiledName|win:UnicodeString|Nome del metodo compilato.|  
|MethodBeingCompiledNameSignature|win:UnicodeString|Firma del metodo compilato.|  
|CallerNamespace|win:UnicodeString|Spazio dei nomi del metodo per cui il compilatore JIT sta provando a generare il codice.|  
|CallerName|win:UnicodeString|Nome del metodo per cui il compilatore JIT sta provando a generare codice.|  
|CallerNameSignature|win:UnicodeString|Firma del metodo chiamante.|  
|CalleeNamespace|win:UnicodeString|Spazio dei nomi del metodo chiamato.|  
|CalleeName|win:UnicodeString|Metodo verso il quale il compilatore sta provando a eseguire una chiamata tail \(anziché generare una chiamata a tale metodo\).|  
|CalleeNameSignature|win:UnicodeString|Firma del metodo chiamato.|  
|TailPrefix|win:Boolean|Prefisso della chiamata tail.|  
|FailReason|win:UnicodeString|Motivo per cui la chiamata tail non è riuscita.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
### MethodJITTailCallSucceeded Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`JITTracingKeyword` \(0x10\)|Dettagliato \(5\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`MethodJitTailCallSucceeded`|188|La chiamata tail al metodo è riuscita.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|MethodBeingCompiledNameSpace|win:UnicodeString|Spazio dei nomi del metodo compilato.|  
|MethodBeingCompiledName|win:UnicodeString|Nome del metodo compilato.|  
|MethodBeingCompiledNameSignature|win:UnicodeString|Firma del metodo compilato.|  
|CallerNamespace|win:UnicodeString|Spazio dei nomi del metodo per cui il compilatore JIT sta provando a generare il codice.|  
|CallerName|win:UnicodeString|Nome del metodo per cui il compilatore JIT sta provando a generare codice.|  
|CallerNameSignature|win:UnicodeString|Firma del metodo chiamante.|  
|CalleeNamespace|win:UnicodeString|Spazio dei nomi del metodo chiamato.|  
|CalleeName|win:UnicodeString|Metodo verso il quale il compilatore sta provando a eseguire una chiamata tail \(anziché generare una chiamata a tale metodo\).|  
|CalleeNameSignature|win:UnicodeString|Firma del metodo chiamato.|  
|TailPrefix|win:Boolean|Prefisso della chiamata tail.|  
|TailCallType|win:UnicodeString|Tipo della chiamata tail.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
## Vedere anche  
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)