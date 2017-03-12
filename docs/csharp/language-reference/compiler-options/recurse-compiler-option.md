---
title: "/recurse (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/recurse"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/recurse compiler option [C#]"
  - "recurse compiler option [C#]"
  - "-recurse compiler option [C#]"
ms.assetid: 4e8212e5-04e3-45b1-8a42-41bc50e683b0
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# /recurse (C# Compiler Options)
L'opzione \/recurse consente di compilare il file di codice sorgente in tutte le directory figlio della directory specificata \(dir\) o della directory del progetto.  
  
## Sintassi  
  
```  
/recurse:[dir\]file  
```  
  
## Argomenti  
 `dir` \(facoltativo\)  
 Rappresenta la directory in cui si desidera che abbia inizio la ricerca.  Se non viene specificata alcuna directory, la ricerca avrà inizio nella directory del progetto.  
  
 `file`  
 Rappresenta uno o più file da cercare.  È consentito l'utilizzo dei caratteri jolly.  
  
## Note  
 L'opzione **\/recurse** consente di compilare file di codice sorgente in tutte le directory figlio della directory specificata \(`dir`\) o della directory del progetto.  
  
 È possibile utilizzare caratteri jolly in un nome file per compilare tutti i file corrispondenti della directory del progetto senza utilizzare **\/recurse**.  
  
 Questa opzione del compilatore non è disponibile in Visual Studio e non può essere modificata a livello di codice.  
  
## Esempio  
 Compilare tutti i file C\# della directory corrente:  
  
```  
csc *.cs  
```  
  
 Compilare tutti i file C\# della directory dir1\\dir2 e di eventuali relative sottodirectory e generare dir2.dll:  
  
```  
csc /target:library /out:dir2.dll /recurse:dir1\dir2\*.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)