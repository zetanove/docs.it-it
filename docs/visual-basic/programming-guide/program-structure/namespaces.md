---
title: "Spazi dei nomi in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.global"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "assembly [Visual Basic], spazi dei nomi"
  - "conflitti dei nomi"
  - "Global (parola chiave) [Visual Basic]"
  - "inquinamento dello spazio dei nomi"
  - "nomi, evitare conflitti"
  - "conflitti di denominazione, spazi dei nomi"
  - "spazi dei nomi, assembly"
  - "Visual Basic (codice), spazi dei nomi"
  - "nomi completi"
  - "convenzioni di denominazione, conflitti di denominazione"
  - "spazi dei nomi"
ms.assetid: cffac744-ab8c-4f1f-ba50-732c22ab4b88
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# Spazi dei nomi in Visual Basic
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Gli spazi dei nomi organizzano gli oggetti definiti in un assembly. Gli assembly possono contenere più spazi dei nomi, che a loro volta possono contenere altri spazi dei nomi. Gli spazi dei nomi consentono di evitare problemi di ambiguità e di semplificare i riferimenti quando si usano gruppi di oggetti di grandi dimensioni, ad esempio librerie di classi.  
  
 Ad esempio, [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] definisce la classe <xref:System.Windows.Forms.ListBox> nello spazio dei nomi <xref:System.Windows.Forms?displayProperty=fullName>. Il frammento di codice seguente illustra come dichiarare una variabile usando il nome completo per questa classe:  
  
 [!code-vb[VbVbalrApplication#6](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_1.vb)]  
  
## Evitare conflitti di nomi  
 Gli spazi dei nomi di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] consentono di risolvere un problema, talvolta chiamato *inquinamento dello spazio dei nomi*, per cui lo sviluppatore di una libreria di classi incontra difficoltà a causa dell'uso di nomi simili in un'altra libreria. Questi conflitti con i componenti esistenti sono talvolta denominati *conflitti di nomi*.  
  
 Se, ad esempio, si crea una nuova classe denominata `ListBox`, è possibile usarla all'interno del progetto senza qualificazione. Tuttavia, se si vuole usare la classe <xref:System.Windows.Forms.ListBox> di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] nello stesso progetto, è necessario usare un riferimento completo per rendere univoco il riferimento. Se il riferimento non è univoco, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] genera un errore per informare che il nome è ambiguo. L'esempio di codice seguente illustra come dichiarare questi oggetti:  
  
 [!code-vb[VbVbalrApplication#7](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_2.vb)]  
  
 La figura seguente mostra due gerarchie di spazio dei nomi che contengono entrambe un oggetto denominato `ListBox`.  
  
 ![Gerarchia dello spazio dei nomi](../../../visual-basic/programming-guide/program-structure/media/vanamespacehierarchy.png "vaNamespaceHierarchy")  
  
 Per impostazione predefinita, ogni file eseguibile creato con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] contiene uno spazio dei nomi con lo stesso nome del progetto. Se, ad esempio, si definisce un oggetto all'interno di un progetto denominato `ListBoxProject`, il file eseguibile ListBoxProject.exe conterrà uno spazio dei nomi chiamato `ListBoxProject`.  
  
 Più assembly possono usare lo stesso spazio dei nomi.[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] considera tali assembly come un singolo set di nomi. È ad esempio possibile definire classi per uno spazio dei nomi chiamato `SomeNameSpace` in un assembly denominato `Assemb1` e altre classi per lo stesso spazio dei nomi da un assembly denominato `Assemb2`.  
  
## Nomi completi  
 I nomi completi sono riferimenti a oggetti preceduti dal nome dello spazio dei nomi in cui è definito l'oggetto. È possibile usare gli oggetti definiti in altri progetti se si crea un riferimento alla classe \(scegliendo **Aggiungi riferimento** dal menu **Progetto**\) e quindi usare il nome completo per l'oggetto nel codice. Il frammento di codice seguente mostra come usare il nome completo per un oggetto dallo spazio dei nomi di un altro progetto:  
  
 [!code-vb[VbVbalrApplication#8](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_3.vb)]  
  
 I nomi completi impediscono i conflitti di denominazione perché consentono al compilatore di determinare quale oggetto viene usato. I nomi stessi, tuttavia, possono diventare lunghi e complessi. Per evitare questo problema, è possibile usare l'istruzione `Imports` per definire un *alias*, ossia un nome abbreviato utilizzabile al posto di un nome completo. Ad esempio, il codice seguente crea alias per due nomi completi e usa questi alias per definire due oggetti.  
  
 [!code-vb[VbVbalrApplication#9](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_4.vb)]  
  
 [!code-vb[VbVbalrApplication#10](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_5.vb)]  
  
 Se si usa l'istruzione `Imports` senza un alias, è possibile usare tutti i nomi dello spazio dei nomi senza qualificazione, a condizione che siano univoci per il progetto. Se il progetto contiene istruzioni `Imports` per gli spazi dei nomi che contengono elementi con lo stesso nome, quando si usa il nome è necessario definirlo in modo completo. Si supponga, ad esempio, che il progetto contenga le due istruzioni `Imports` seguenti:  
  
 [!code-vb[VbVbalrApplication#11](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_6.vb)]  
  
 Se si prova a usare `Class1` senza definirlo in modo completo, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] genererà un errore per segnalare che il nome `Class1` è ambiguo.  
  
## Istruzioni a livello di spazio dei nomi  
 All'interno di uno spazio dei nomi è possibile definire elementi quali moduli, interfacce, classi, delegati, enumerazioni, strutture e altri spazi dei nomi. Non è invece possibile definire elementi come proprietà, routine, variabili ed eventi a livello di spazio dei nomi. Questi elementi devono essere dichiarati all'interno di contenitori quali moduli, strutture o classi.  
  
## Parola chiave Global nei nomi completi  
 Se è stata definita una gerarchia annidata di spazi dei nomi, è possibile che per il codice interno alla gerarchia venga bloccato l'accesso allo spazio dei nomi <xref:System?displayProperty=fullName> di .NET Framework. L'esempio seguente illustra una gerarchia in cui lo spazio dei nomi `SpecialSpace.System` blocca l'accesso a <xref:System?displayProperty=fullName>.  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As System.Int32  
                Dim n As System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 Di conseguenza, il compilatore di Visual Basic non è in grado di risolvere il riferimento a <xref:System.Int32?displayProperty=fullName> perché `SpecialSpace.System` non definisce `Int32`. Per iniziare la catena di qualificazione al livello più esterno della libreria di classi di .NET Framework è possibile usare la parola chiave `Global`. In questo modo si può specificare lo spazio dei nomi <xref:System?displayProperty=fullName> o qualsiasi altro spazio dei nomi nella libreria di classi. Questa condizione è illustrata nell'esempio seguente.  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As Global.System.Int32  
                Dim n As Global.System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 Usando `Global` è possibile accedere ad altri spazi dei nomi a livello di radice, ad esempio <xref:Microsoft.VisualBasic?displayProperty=fullName>, e a qualsiasi spazio dei nomi associato al progetto.  
  
## Parola chiave Global nelle istruzioni degli spazi dei nomi  
 La parola chiave `Global` può essere usata anche in un oggetto [Namespace Statement](../../../visual-basic/language-reference/statements/namespace-statement.md). Ciò consente di definire uno spazio dei nomi all'esterno dello spazio dei nomi radice del progetto.  
  
 Tutti gli spazi dei nomi inclusi nel progetto sono basati sullo spazio dei nomi radice definito per il progetto.  Visual Studio assegna il nome del progetto come spazio dei nomi radice predefinito per tutto il codice del progetto. Se, ad esempio, il progetto è denominato `ConsoleApplication1`, i relativi elementi di programmazione appartengono allo spazio dei nomi `ConsoleApplication1`. Se si dichiara `Namespace Magnetosphere`, i riferimenti a `Magnetosphere` nel progetto accedono a `ConsoleApplication1.Magnetosphere`.  
  
 Negli esempi seguenti viene usata la parola chiave `Global` per dichiarare uno spazio dei nomi all'esterno dello spazio dei nomi radice per il progetto.  
  
 [!code-vb[VbVbalrApplication#22](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_7.vb)]  
  
 In una dichiarazione dello spazio dei nomi la parola chiave `Global` non può essere annidata in un altro spazio dei nomi.  
  
 È possibile usare [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic) per visualizzare e modificare lo **spazio dei nomi radice** del progetto.  Per i nuovi progetti, come **spazio dei nomi radice** predefinito viene usato il nome del progetto. Per impostare `Global` come spazio dei nomi di primo livello, è possibile cancellare la voce **Spazio dei nomi radice** in modo da lasciare vuota la casella. La cancellazione della voce **Spazio dei nomi radice** elimina la necessità di usare la parola chiave `Global` nelle dichiarazioni degli spazi dei nomi.  
  
 Se un'istruzione `Namespace` dichiara un nome che è anche uno spazio dei nomi in .NET Framework e la parola chiave `Global` non viene usata in un nome completo, lo spazio dei nomi di .NET Framework non sarà più disponibile. Per abilitare l'accesso allo spazio dei nomi di .NET Framework senza usare la parola chiave `Global`, è possibile includere `Global` nell'istruzione `Namespace`.  
  
 L'esempio seguente mostra la dichiarazione dello spazio dei nomi `System.Text` con la parola chiave `Global`.  
  
 Se `Global` non è presente nella dichiarazione dello spazio dei nomi, <xref:System.Text.StringBuilder> non è accessibile, a meno che non si specifichi `Global.System.Text.StringBuilder`. Per un progetto denominato `ConsoleApplication1`, i riferimenti a `System.Text` accedono a `ConsoleApplication1.System.Text` se non viene usata la parola chiave `Global`.  
  
 [!code-vb[VbVbalrApplication#21](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_8.vb)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.ListBox>   
 <xref:System.Windows.Forms?displayProperty=fullName>   
 [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura: Creare e usare assembly dalla riga di comando](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md)   
 [References and the Imports Statement](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Imports Statement \(.NET Namespace and Type\)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Scrittura di codice nelle soluzioni Office](/office-dev/office-dev/writing-code-in-office-solutions)