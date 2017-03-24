---
title: Gli spazi dei nomi in Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.global
dev_langs:
- VB
helpviewer_keywords:
- assemblies [Visual Basic], namespaces
- name collisions
- Global keyword [Visual Basic]
- namespace pollution
- names, avoiding conflicts
- naming conflicts, namespaces
- namespaces, assemblies
- Visual Basic code, namespaces
- fully qualified names
- naming conventions, naming conflicts
- namespaces
ms.assetid: cffac744-ab8c-4f1f-ba50-732c22ab4b88
caps.latest.revision: 27
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: fe94e65ddbb4ebd2f7d26e8750a0a7ef5d3153af
ms.lasthandoff: 03/13/2017

---
# <a name="namespaces-in-visual-basic"></a>Spazi dei nomi in Visual Basic
Gli spazi dei nomi organizzano gli oggetti definiti in un assembly. Gli assembly possono contenere più spazi dei nomi, che a loro volta possono contenere altri spazi dei nomi. Gli spazi dei nomi consentono di evitare problemi di ambiguità e di semplificare i riferimenti quando si usano gruppi di oggetti di grandi dimensioni, ad esempio librerie di classi.  
  
 Ad esempio, il [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] definisce la <xref:System.Windows.Forms.ListBox>classe il <xref:System.Windows.Forms?displayProperty=fullName>dello spazio dei nomi.</xref:System.Windows.Forms?displayProperty=fullName> </xref:System.Windows.Forms.ListBox> Il frammento di codice seguente illustra come dichiarare una variabile usando il nome completo per questa classe:  
  
 [!code-vb[6 VbVbalrApplication](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_1.vb)]  
  
## <a name="avoiding-name-collisions"></a>Evitare conflitti di nomi  
 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]gli spazi dei nomi risolvere un problema talvolta noto *inquinamento dello spazio dei nomi*, in cui lo sviluppatore di una libreria di classi è ostacolato dall'uso di nomi simili in un'altra libreria. Questi conflitti con i componenti esistenti sono talvolta denominati *conflitti di nomi*.  
  
 Se, ad esempio, si crea una nuova classe denominata `ListBox`, è possibile usarla all'interno del progetto senza qualificazione. Tuttavia, se si desidera utilizzare il [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] <xref:System.Windows.Forms.ListBox>classe nello stesso progetto, è necessario utilizzare un riferimento completo per rendere univoco il riferimento.</xref:System.Windows.Forms.ListBox> Se il riferimento non è univoco, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] genera un errore per informare che il nome è ambiguo. L'esempio di codice seguente illustra come dichiarare questi oggetti:  
  
 [!code-vb[VbVbalrApplication&#7;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_2.vb)]  
  
 La figura seguente mostra due gerarchie di spazio dei nomi che contengono entrambe un oggetto denominato `ListBox`.  
  
 ![Gerarchia Namespace](../../../visual-basic/programming-guide/program-structure/media/vanamespacehierarchy.gif "vaNamespaceHierarchy")  
  
 Per impostazione predefinita, ogni file eseguibile creato con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] contiene uno spazio dei nomi con lo stesso nome del progetto. Se, ad esempio, si definisce un oggetto all'interno di un progetto denominato `ListBoxProject`, il file eseguibile ListBoxProject.exe conterrà uno spazio dei nomi chiamato `ListBoxProject`.  
  
 Più assembly possono usare lo stesso spazio dei nomi. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] considera tali assembly come un singolo set di nomi. È ad esempio possibile definire classi per uno spazio dei nomi chiamato `SomeNameSpace` in un assembly denominato `Assemb1` e altre classi per lo stesso spazio dei nomi da un assembly denominato `Assemb2`.  
  
## <a name="fully-qualified-names"></a>Nomi completi  
 I nomi completi sono riferimenti a oggetti preceduti dal nome dello spazio dei nomi in cui è definito l'oggetto. È possibile usare gli oggetti definiti in altri progetti se si crea un riferimento alla classe (scegliendo **Aggiungi riferimento** dal menu **Progetto** ) e quindi usare il nome completo per l'oggetto nel codice. Il frammento di codice seguente mostra come usare il nome completo per un oggetto dallo spazio dei nomi di un altro progetto:  
  
 [!code-vb[VbVbalrApplication n.&8;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_3.vb)]  
  
 I nomi completi impediscono i conflitti di denominazione perché consentono al compilatore di determinare quale oggetto viene usato. I nomi stessi, tuttavia, possono diventare lunghi e complessi. Per evitare questo problema, è possibile usare l'istruzione `Imports` per definire un *alias*, ossia un nome abbreviato utilizzabile al posto di un nome completo. Ad esempio, il codice seguente crea alias per due nomi completi e usa questi alias per definire due oggetti.  
  
 [!code-vb[9 VbVbalrApplication](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_4.vb)]  
  
 [!code-vb[VbVbalrApplication&#10;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_5.vb)]  
  
 Se si usa l'istruzione `Imports` senza un alias, è possibile usare tutti i nomi dello spazio dei nomi senza qualificazione, a condizione che siano univoci per il progetto. Se il progetto contiene istruzioni `Imports` per gli spazi dei nomi che contengono elementi con lo stesso nome, quando si usa il nome è necessario definirlo in modo completo. Si supponga, ad esempio, che il progetto contenga le due istruzioni `Imports` seguenti:  
  
 [!code-vb[VbVbalrApplication&#11;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_6.vb)]  
  
 Se si prova a usare `Class1` senza definirlo in modo completo, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] genererà un errore per segnalare che il nome `Class1` è ambiguo.  
  
## <a name="namespace-level-statements"></a>Istruzioni a livello di spazio dei nomi  
 All'interno di uno spazio dei nomi è possibile definire elementi quali moduli, interfacce, classi, delegati, enumerazioni, strutture e altri spazi dei nomi. Non è invece possibile definire elementi come proprietà, routine, variabili ed eventi a livello di spazio dei nomi. Questi elementi devono essere dichiarati all'interno di contenitori quali moduli, strutture o classi.  
  
## <a name="global-keyword-in-fully-qualified-names"></a>Parola chiave Global nei nomi completi  
 Se è stata definita una gerarchia nidificata di spazi dei nomi, codice all'interno della gerarchia potrebbe essere impedito l'accesso di <xref:System?displayProperty=fullName>dello spazio dei nomi di .NET Framework.</xref:System?displayProperty=fullName> Nell'esempio seguente viene illustrata una gerarchia in cui il `SpecialSpace.System` dello spazio dei nomi blocca l'accesso a <xref:System?displayProperty=fullName>.</xref:System?displayProperty=fullName>  
  
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
  
 Di conseguenza, il compilatore Visual Basic non può risolvere il riferimento a <xref:System.Int32?displayProperty=fullName>, in quanto `SpecialSpace.System` non definisce `Int32`.</xref:System.Int32?displayProperty=fullName> Per iniziare la catena di qualificazione al livello più esterno della libreria di classi di .NET Framework è possibile usare la parola chiave `Global` . Ciò consente di specificare il <xref:System?displayProperty=fullName>dello spazio dei nomi o qualsiasi altro spazio dei nomi nella libreria di classi.</xref:System?displayProperty=fullName> Questa condizione è illustrata nell'esempio seguente.  
  
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
  
 È possibile utilizzare `Global` accesso altri spazi dei nomi di primo livello, ad esempio <xref:Microsoft.VisualBasic?displayProperty=fullName>e uno spazio dei nomi associato al progetto.</xref:Microsoft.VisualBasic?displayProperty=fullName>  
  
## <a name="global-keyword-in-namespace-statements"></a>Parola chiave Global nelle istruzioni degli spazi dei nomi  
 È inoltre possibile utilizzare il `Global` (parola chiave) in un [istruzione Namespace](../../../visual-basic/language-reference/statements/namespace-statement.md). Ciò consente di definire uno spazio dei nomi all'esterno dello spazio dei nomi radice del progetto.  
  
 Tutti gli spazi dei nomi inclusi nel progetto sono basati sullo spazio dei nomi radice definito per il progetto.  Visual Studio assegna il nome del progetto come spazio dei nomi radice predefinito per tutto il codice del progetto. Se, ad esempio, il progetto è denominato `ConsoleApplication1`, i relativi elementi di programmazione appartengono allo spazio dei nomi `ConsoleApplication1`. Se si dichiara `Namespace Magnetosphere`, i riferimenti a `Magnetosphere` nel progetto accedono a `ConsoleApplication1.Magnetosphere`.  
  
 Negli esempi seguenti viene usata la parola chiave `Global` per dichiarare uno spazio dei nomi all'esterno dello spazio dei nomi radice per il progetto.  
  
 [!code-vb[VbVbalrApplication&#22;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_7.vb)]  
  
 In una dichiarazione dello spazio dei nomi la parola chiave `Global` non può essere annidata in un altro spazio dei nomi.  
  
 È possibile utilizzare il [pagina applicazione, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic) per visualizzare e modificare il **radice Namespace** del progetto.  Per i nuovi progetti, come **spazio dei nomi radice** predefinito viene usato il nome del progetto. Per impostare `Global` come spazio dei nomi di primo livello, è possibile cancellare la voce **Spazio dei nomi radice** in modo da lasciare vuota la casella. La cancellazione della voce **Spazio dei nomi radice** elimina la necessità di usare la parola chiave `Global` nelle dichiarazioni degli spazi dei nomi.  
  
 Se un'istruzione `Namespace` dichiara un nome che è anche uno spazio dei nomi in .NET Framework e la parola chiave `Global` non viene usata in un nome completo, lo spazio dei nomi di .NET Framework non sarà più disponibile. Per abilitare l'accesso allo spazio dei nomi di .NET Framework senza usare la parola chiave `Global` , è possibile includere `Global` nell'istruzione `Namespace` .  
  
 L'esempio seguente mostra la dichiarazione dello spazio dei nomi `Global` con la parola chiave `System.Text` .  
  
 Se il `Global` (parola chiave) non è presente nella dichiarazione dello spazio dei nomi <xref:System.Text.StringBuilder>potrebbero non essere accessibili senza specificare `Global.System.Text.StringBuilder`.</xref:System.Text.StringBuilder> Per un progetto denominato `ConsoleApplication1`, i riferimenti a `System.Text` accedono a `ConsoleApplication1.System.Text` se non viene usata la parola chiave `Global` .  
  
 [!code-vb[VbVbalrApplication numero&21;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_8.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Forms.ListBox></xref:System.Windows.Forms.ListBox>   
 <xref:System.Windows.Forms?displayProperty=fullName></xref:System.Windows.Forms?displayProperty=fullName>   
 [Gli assembly e Global Assembly Cache](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Procedura: creare e utilizzare assembly dalla riga di comando](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4)   
 [I riferimenti e istruzione Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Istruzione Imports (tipo e spazio dei nomi .NET)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Writing Code in Office Solutions](https://msdn.microsoft.com/library/bb608596) (Scrittura di codice nelle soluzioni Office)
