---
title: "Argomenti della riga di comando (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "argomenti della riga di comando [C#]"
ms.assetid: 0e597e0d-ea7a-41ba-a38a-0198122f3c26
caps.latest.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 27
---
# Argomenti della riga di comando (Guida per programmatori C#)
È possibile inviare argomenti al metodo `Main` definendo il metodo in uno dei modi seguenti:  
  
 [!code-cs[csProgGuideMain#2](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_1.cs)]  
  
 [!code-cs[csProgGuideMain#3](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_2.cs)]  
  
> [!NOTE]
>  Per attivare gli argomenti della riga di comando nel metodo `Main` in un'applicazione Windows Form, è necessario modificare manualmente la firma di `Main` in program.cs.  Il codice generato in Progettazione Windows Form crea un oggetto `Main` senza un parametro di input.  È possibile utilizzare anche <xref:System.Environment.CommandLine%2A?displayProperty=fullName> o <xref:System.Environment.GetCommandLineArgs%2A?displayProperty=fullName> per accedere agli argomenti della riga di comando da qualsiasi punto in una console o un'applicazione Windows.  
  
 Il parametro del metodo `Main` è una matrice <xref:System.String> che rappresenta gli argomenti della riga di comando.  Generalmente si determina se gli argomenti esistono eseguendo il test della proprietà `Length`, ad esempio:  
  
 [!code-cs[csProgGuideMain#4](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_3.cs)]  
  
 È anche possibile convertire gli argomenti di tipo stringa in tipi numerici utilizzando la classe <xref:System.Convert> o il metodo `Parse`.  L'istruzione seguente, ad esempio, converte `string` in un numero `long` tramite il metodo <xref:System.Int64.Parse%2A>:  
  
```  
long num = Int64.Parse(args[0]);  
```  
  
 È anche possibile utilizzare il tipo `long` di C\#, che rappresenta l'alias per `Int64`:  
  
```  
long num = long.Parse(args[0]);  
```  
  
 In alternativa, è possibile effettuare tale operazione utilizzando il metodo `ToInt64` della classe `Convert`:  
  
```  
long num = Convert.ToInt64(s);  
```  
  
 Per ulteriori informazioni, vedere <xref:System.Int64.Parse%2A> e <xref:System.Convert>.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare gli argomenti della riga di comando in un'applicazione console.  L'applicazione accetta un argomento in fase di esecuzione, lo converte in un valore integer e calcola il fattoriale del numero.  Se non viene fornito alcun argomento, l'applicazione genera un messaggio in cui viene spiegato l'utilizzo corretto del programma.  
  
 Per compilare ed eseguire l'applicazione dal prompt dei comandi, attenersi alla seguente procedura:  
  
1.  Incollare il seguente codice in qualsiasi editor di testo, quindi salvare il file come file di testo con il nome `Factorial.cs`.  
  
     [!code-cs[csProgGuideMain#16](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_4.cs)]  
  
2.  Dalla schermata **Start** o dal menu **Start**, aprire una finestra **Prompt dei comandi di sviluppo** di Visual Studio e passare alla cartella contenente il file appena creato.  
  
3.  Immettere il comando seguente per compilare l'applicazione.  
  
     `csc Factorial.cs`  
  
     Se l'applicazione non presenta errori di compilazione, viene creato un file eseguibile denominato `Factorial.exe`.  
  
4.  Immettere il comando seguente per calcolare il fattoriale di 3:  
  
     `Factorial 3`  
  
5.  Il comando produce l'output seguente: `The factorial of 3 is 6.`  
  
> [!NOTE]
>  Quando si esegue un'applicazione in Visual Studio, è possibile specificare gli argomenti della riga di comando nella [Pagina Debug, Progettazione progetti](/visual-studio/ide/reference/debug-page-project-designer).  
  
 Per ulteriori esempi sulle modalità di utilizzo degli argomenti della riga di comando, vedere [Procedura: Creare e usare assembly dalla riga di comando](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Vedere anche  
 <xref:System.Environment?displayProperty=fullName>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Main\(\) e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [Procedura: visualizzare gli argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [Procedura: accedere agli argomenti della riga di comando utilizzando foreach](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)   
 [Valori restituiti da Main\(\)](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)   
 [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md)