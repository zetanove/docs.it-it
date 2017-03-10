---
title: "/codepage (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/codepage"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/codepage compiler option [C#]"
  - "codepage compiler option [C#]"
  - "-codepage compiler option [C#]"
ms.assetid: 75942989-b69a-4308-90a0-840c73d2c478
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# /codepage (C# Compiler Options)
Con questa opzione viene specificata la tabella codici da utilizzare in fase di compilazione, se la tabella codici richiesta è diversa da quella corrente predefinita per il sistema.  
  
## Sintassi  
  
```  
/codepage:id  
```  
  
## Argomenti  
 `id`  
 Identificativo della tabella codici da utilizzare nella compilazione per tutti i file di codice sorgente.  
  
## Note  
 Se si esegue la compilazione di uno o più file di codice sorgente che non supportano l'utilizzo della tabella codici predefinita del computer in uso, è possibile utilizzare l'opzione **\/codepage** per specificare quale tabella codici utilizzare.  L'opzione **\/codepage** viene applicata a tutti i file di codice sorgente inclusi nella compilazione.  
  
 Se i file di codice sorgente sono stati creati con la stessa tabella codici attiva sul computer oppure con UNICODE o UTF\-8, non sarà necessario utilizzare **\/codepage**.  
  
 Vedere [GetCPInfo](http://go.microsoft.com/fwlink/?LinkId=148371) per informazioni su come individuare le tabelle codici supportate nel sistema.  
  
 Questa opzione del compilatore non è disponibile in Visual Studio e non può essere modificata a livello di codice.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)