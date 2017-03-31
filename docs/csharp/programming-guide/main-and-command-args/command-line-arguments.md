---
title: Argomenti della riga di comando (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- command-line arguments [C#]
ms.assetid: 0e597e0d-ea7a-41ba-a38a-0198122f3c26
caps.latest.revision: 27
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4034f1575321c94f003a12a83df617d4a0d50702
ms.lasthandoff: 03/13/2017

---
# <a name="command-line-arguments-c-programming-guide"></a>Argomenti della riga di comando (Guida per programmatori C#)
È possibile inviare argomenti al metodo `Main` definendo il metodo in uno dei modi seguenti:  
  
 [!code-cs[csProgGuideMain#2](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_1.cs)]  
  
 [!code-cs[csProgGuideMain#3](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_2.cs)]  
  
> [!NOTE]
>  Per attivare gli argomenti della riga di comando nel metodo `Main` in un'applicazione Windows Form, è necessario modificare manualmente la firma di `Main` in program.cs. Il codice generato da Progettazione Windows Form crea un `Main` senza un parametro di input. È anche possibile usare <xref:System.Environment.CommandLine%2A?displayProperty=fullName> o <xref:System.Environment.GetCommandLineArgs%2A?displayProperty=fullName> per accedere agli argomenti della riga di comando da qualsiasi posizione in una console o un'applicazione Windows.  
  
 Il parametro del metodo `Main` è una matrice <xref:System.String> che rappresenta gli argomenti della riga di comando. In genere si determina se gli argomenti esistono eseguendo il test della proprietà `Length`, ad esempio:  
  
 [!code-cs[csProgGuideMain#4](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_3.cs)]  
  
 È anche possibile convertire gli argomenti stringa in tipi numerici con la classe <xref:System.Convert> o il metodo `Parse`. Ad esempio, l'istruzione seguente converte `string` in un numero `long` con il metodo <xref:System.Int64.Parse%2A>:  
  
```  
long num = Int64.Parse(args[0]);  
```  
  
 È anche possibile usare il tipo C# `long`, che fa da alias per `Int64`:  
  
```  
long num = long.Parse(args[0]);  
```  
  
 Nella classe `Convert` il metodo `ToInt64` consente di eseguire la stessa operazione:  
  
```  
long num = Convert.ToInt64(s);  
```  
  
 Per altre informazioni, vedere <xref:System.Int64.Parse%2A> e <xref:System.Convert>.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare gli argomenti della riga di comando in un'applicazione console. L'applicazione accetta un argomento in fase di esecuzione, lo converte in un numero intero e calcola il fattoriale del numero. Se non viene specificato nessun argomento, l'applicazione produce un messaggio che descrive l'uso corretto del programma.  
  
 Per compilare ed eseguire l'applicazione al prompt dei comandi, seguire questa procedura:  
  
1.  Incollare il codice seguente in un editor di testo, quindi salvare il file come file di testo con il nome `Factorial.cs`.  
  
     [!code-cs[csProgGuideMain#16](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_4.cs)]  
  
2.  Dalla schermata **Start** o dal menu **Start**, aprire una finestra **Prompt dei comandi per gli sviluppatori** di Visual Studio e selezionare la cartella contenente il file appena creato.  
  
3.  Immettere il seguente comando per compilare l'applicazione.  
  
     `csc Factorial.cs`  
  
     Se l'applicazione non presenta errori di compilazione, viene creato un file eseguibile denominato `Factorial.exe`.  
  
4.  Immettere il comando seguente per calcolare il fattoriale di 3:  
  
     `Factorial 3`  
  
5.  Il comando produce il seguente output: `The factorial of 3 is 6.`  
  
> [!NOTE]
>  Quando si esegue un'applicazione in Visual Studio, è possibile specificare argomenti della riga di comando nella [Pagina Debug, Progettazione progetti](https://docs.microsoft.com/visualstudio/ide/reference/debug-page-project-designer).  
  
 Per altri esempi d'uso degli argomenti della riga di comando, vedere [Procedura: Creare e usare assembly dalla riga di comando](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Environment?displayProperty=fullName>   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Main() e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/index.md)   
 [Procedura: Visualizzare gli argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [Procedura: Accedere agli argomenti della riga di comando usando foreach](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)   
 [Valori restituiti da Main()](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)   
 [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md)
