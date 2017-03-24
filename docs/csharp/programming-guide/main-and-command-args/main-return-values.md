---
title: "Valori restituiti da Main() (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "metodo Main [C#], valori restituiti"
ms.assetid: c2f5a1d8-1676-4bea-bc7e-44a97e72d5bc
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# Valori restituiti da Main() (Guida per programmatori C#)
Il metodo `Main` può restituire `void`:  
  
 [!code-cs[csProgGuideMain#12](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/main-return-values_1.cs)]  
  
 Può anche restituire un `int`:  
  
 [!code-cs[csProgGuideMain#13](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/main-return-values_2.cs)]  
  
 Se il valore restituito da `Main` non viene utilizzato, la restituzione di `void` consente di semplificare leggermente il codice.  La restituzione di un valore intero consente tuttavia al programma di comunicare le informazioni sullo stato ad altri programmi o script che richiamano il file eseguibile.  Nell'esempio seguente viene illustrato come è possibile accedere al valore restituito da `Main`.  
  
## Esempio  
 In questo esempio viene utilizzato un file batch per eseguire un programma e testare il valore restituito dalla funzione `Main`.  Quando si esegue un programma in ambiente Windows, qualsiasi valore restituito dalla funzione `Main` viene archiviato in una variabile di ambiente denominata `ERRORLEVEL`.  Un file batch può determinare il risultato dell'esecuzione tramite l'esame della variabile `ERRORLEVEL`.  Un valore restituito pari a zero indica in genere che l'esecuzione è avvenuta in modo corretto.  L'esempio seguente rappresenta un semplice programma che restituisce il valore zero dalla funzione `Main`.  Lo zero indica che il programma è stato eseguito correttamente.  Salvare il programma come MainReturnValTest.cs.  
  
 [!code-cs[csProgGuideMain#14](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/main-return-values_3.cs)]  
  
## Esempio  
 Poiché in questo esempio viene utilizzato un file batch, è consigliabile compilare il codice da un prompt dei comandi.  Seguire le istruzioni in [How to: Set Environment Variables for the Visual Studio Command Line](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md) per abilitare le compilazioni da riga di comando o utilizzare il prompt dei comandi di Visual Studio, disponibile nel menu **Start** in **Visual Studio Tools**.  Al prompt dei comandi passare alla cartella in cui è stato salvato il programma.  Il comando seguente consente di compilare MainReturnValTest.cs e produrre il file eseguibile MainReturnValTest.exe.  
  
 `csc MainReturnValTest.cs`  
  
 Creare quindi un file batch per eseguire MainReturnValTest.exe e visualizzare il risultato.  Incollare il codice seguente in un file di testo e salvarlo come `test.bat` nella cartella che contiene MainReturnValTest.cs e MainReturnValTest.exe.  Eseguire il file batch digitando `test` al prompt dei comandi.  
  
 Poiché il codice restituisce zero, il file batch indicherà un esito positivo.  Se tuttavia si modifica MainReturnValTest.cs in modo che restituisca un valore diverso da zero e quindi si ricompila il programma, l'esecuzione successiva del file batch indicherà un esito negativo.  
  
```  
rem test.bat  
@echo off  
MainReturnValTest  
@if "%ERRORLEVEL%" == "0" goto good  
  
:fail  
    echo Execution Failed  
    echo return value = %ERRORLEVEL%  
    goto end  
  
:good  
    echo Execution succeeded  
    echo Return value = %ERRORLEVEL%  
    goto end  
  
:end  
```  
  
## Esempio di output  
 `Execution succeeded`  
  
 `Return value = 0`  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Main\(\) e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [Procedura: visualizzare gli argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [Procedura: accedere agli argomenti della riga di comando utilizzando foreach](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)