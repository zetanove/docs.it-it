---
title: "/bugreport (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/bugreport"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/bugreport compiler option [C#]"
  - "-bugreport compiler option [C#]"
  - "bugreport compiler option [C#]"
ms.assetid: f39665e3-4f6f-4357-88a2-3274c7bec0c1
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /bugreport (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che le informazioni di debug devono essere inserite in un file per essere analizzate in seguito.  
  
## Sintassi  
  
```  
/bugreport:file  
```  
  
## Argomenti  
 `file`  
 Rappresenta il nome del file in cui si desidera inserire il report sui bug.  
  
## Note  
 L'opzione **\/bugreport** specifica che le informazioni riportate di seguito devono essere inserite in `file`:  
  
-   Una copia di tutti i file di codice sorgente della compilazione.  
  
-   Un elenco delle opzioni del compilatore utilizzate nella compilazione.  
  
-   Informazioni sulla versione del compilatore in uso, del runtime e del sistema operativo.  
  
-   Moduli e assembly, salvati come cifre esadecimali, a cui viene fatto riferimento, ad eccezione degli assembly forniti con .NET Framework e SDK.  
  
-   Eventuale output del compilatore.  
  
-   Una descrizione del problema, richiesta mediante un messaggio.  
  
-   Una descrizione, richiesta mediante un messaggio, delle possibili modalità di correzione del problema.  
  
 Se questa opzione viene utilizzata con **\/errorreport:prompt** o **\/errorreport:send**, le informazioni contenute nel file saranno inviate a Microsoft Corporation.  
  
 Poiché in `file` verrà inserita una copia di tutti i file di codice sorgente, può essere preferibile riprodurre il presunto problema di codice nel programma più breve possibile.  
  
 Questa opzione del compilatore non è disponibile in Visual Studio e non può essere modificata a livello di codice.  
  
 Si noti che la visualizzazione del contenuto del file generato implica l'esposizione del codice sorgente e quindi la possibile divulgazione accidentale delle informazioni.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [\/errorreport \(Set Error Reporting Behavior\)](../../../csharp/language-reference/compiler-options/errorreport-compiler-option.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)