---
title: "/debug (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/debug"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "debug compiler option [C#]"
  - "-debug compiler option [C#]"
  - "/debug compiler option [C#]"
ms.assetid: e2b48c07-01bc-45cc-a52c-92e9085eb969
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /debug (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione **\/debug** determina, in fase di compilazione, la generazione di informazioni di debug che verranno inserite nel file o nei file di output.  
  
## Sintassi  
  
```  
/debug[+ | -]  
/debug:{full | pdbonly}  
```  
  
## Argomenti  
 `+` &#124; `-`  
 Specificando `+` o **\/debug**, il compilatore genera informazioni relative al debug e le inserisce in un database di programma \(file con estensione\).  Se si specifica l'argomento `-`, che è attivo quando **\/debug** non è specificato, non verranno create informazioni di debug.  
  
 `full` &#124; `pdbonly`  
 Determina il tipo di informazioni di debug generate dal compilatore.  L'argomento full, che è attivo se non si specifica **\/debug:pdbonly**, consente l'associazione di un debugger al programma in esecuzione.  La specifica di pdbonly consente il debug del codice sorgente quando l'avvio del programma avviene dal debugger, ma in questo caso l'assembler viene visualizzato sono quando il programma in esecuzione è collegato al debugger.  
  
## Note  
 Utilizzare questa opzione per creare build di debug.  Se non vengono specificate le opzioni **\/debug**, **\/debug\+** o **\/debug:full**, non sarà possibile eseguire il debug del file di output.  
  
 Quando si utilizza **\/debug:full**, è opportuno tenere presente che **\/debug:full** può avere un impatto considerevole sulla velocità e le dimensioni del codice JIT ottimizzato ed effetti minori sulla qualità del codice stesso.  Per la generazione del codice di rilascio, è consigliato specificare **\/debug:pdbonly** oppure evitare l'utilizzo di un file PDB.  
  
> [!NOTE]
>  L'opzione **\/debug:pdbonly** si differenzia da **\/debug:full** perché, ad esempio, se si specifica **\/debug:full**, viene creato un attributo <xref:System.Diagnostics.DebuggableAttribute> per indicare al compilatore JIT la disponibilità di informazioni di debug.  Verrà pertanto restituito un errore se il codice contiene l'attributo <xref:System.Diagnostics.DebuggableAttribute> impostato su false quando si utilizza l'opzione **\/debug:full**.  
  
 Per ulteriori informazioni su come configurare le prestazioni di debug di un'applicazione, vedere [Semplificazione del debug di un'immagine](../Topic/Making%20an%20Image%20Easier%20to%20Debug.md).  
  
 Per cambiare il percorso del file con estensione pdb, vedere [\/pdb \(Specify Debug Symbol File\)](../../../csharp/language-reference/compiler-options/pdb-compiler-option.md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Fare clic sul pulsante **Avanzate**.  
  
4.  Modificare la proprietà **Informazioni di debug**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DebugSymbols%2A>.  
  
## Esempio  
 Inserire informazioni di debug nel file di output `app.pdb`:  
  
```  
csc /debug /pdb:app.pdb test.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)