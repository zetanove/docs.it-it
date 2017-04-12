---
title: Risoluzione dei problemi di variabili in Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- troubleshooting [Visual Basic], variables
- variables [Visual Basic], troubleshooting
ms.assetid: 928a2dc8-e565-4ae4-8ba3-80cc0cb50090
caps.latest.revision: 20
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 9cddf7ced50c42514ebc9a613f49adee31edde0b
ms.lasthandoff: 03/13/2017

---
# <a name="troubleshooting-variables-in-visual-basic"></a>Risoluzione dei problemi relativi alle variabili in Visual Basic
Questa pagina vengono elencati alcuni problemi comuni che possono verificarsi quando si utilizzano variabili in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## <a name="unable-to-access-members-of-an-object"></a>Impossibile accedere ai membri di un oggetto  
 Se il codice tenta di accedere a una proprietà o metodo su un oggetto, possono verificarsi due diversi errori:  
  
-   Il compilatore può generare un messaggio di errore se si dichiara la variabile oggetto con un tipo specifico e poi si fa riferimento a un membro che non è definito con quel tipo.  
  
-   Fase di esecuzione <xref:System.MemberAccessException>si verifica quando l'oggetto assegnato a una variabile oggetto non viene esposto il membro il codice sta tentando di accedere.</xref:System.MemberAccessException> Nel caso di una variabile di [tipo di dati Object](../../../../visual-basic/language-reference/data-types/object-data-type.md), questa eccezione può anche verificarsi se il membro non è `Public`. Questo perché l'associazione tardiva consente l'accesso solo ai membri `Public` .  
  
 Quando il [istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) Imposta tipo di controllo `On`, una variabile oggetto può accedere solo ai metodi e proprietà della classe che dichiara la classe. Questa condizione è illustrata nell'esempio seguente.  

 [!code-vb[VbVbalrVariables n.&2;](../../../../visual-basic/programming-guide/language-features/variables/codesnippet/VisualBasic/troubleshooting-variables_1.vb)]  
  
 In questo esempio, `p` può utilizzare solo i membri della <xref:System.Object>classe stessa, che non prevedono la `Left` proprietà.</xref:System.Object> D'altra parte, `q` è stato dichiarato come tipo di <xref:System.Windows.Forms.Label>, pertanto è possibile utilizzare tutti i metodi e proprietà della <xref:System.Windows.Forms.Label>classe il <xref:System.Windows.Forms>dello spazio dei nomi.</xref:System.Windows.Forms> </xref:System.Windows.Forms.Label> </xref:System.Windows.Forms.Label>  
  
### <a name="correct-approach"></a>Approccio corretto  
 Per poter accedere a tutti i membri di un oggetto di una determinata classe, dichiarare la variabile oggetto con il tipo di tale classe dove possibile. Se è non possibile, ad esempio se si conosce il tipo di oggetto in fase di compilazione, è necessario impostare `Option Strict` a `Off` e dichiarare la variabile di [tipo di dati Object](../../../../visual-basic/language-reference/data-types/object-data-type.md). In questo modo oggetti di qualsiasi tipo possono essere assegnati alla variabile, perciò occorre eseguire i passaggi necessari per assicurarsi che l'oggetto attualmente assegnato sia di un tipo accettabile. È possibile utilizzare il [operatore TypeOf](../../../../visual-basic/language-reference/operators/typeof-operator.md) a tal fine.  
  
## <a name="other-components-cannot-access-your-variable"></a>Altri componenti non possono accedere alla variabile  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]i nomi sono *tra maiuscole e minuscole*. Se due nomi differiscono solo nelle maiuscole, il compilatore li interpreta come un unico nome. Ad esempio, se si ha `ABC` e `abc` , il compilatore li interpreta come se facessero riferimento allo stesso elemento dichiarato.  
  
 Il Common Language Runtime (CLR) usa invece l'associazione *che distingue fra maiuscole e minuscole* . Perciò, quando si genera un assembly o una DLL e la si rende disponibile ad altri assembly, i nomi distinguono fra maiuscole e minuscole. Se ad esempio si definisce una classe con un elemento denominato `ABC`e altri assembly usano la classe mediante il Common Language Runtime, devono fare riferimento all'elemento come `ABC`. Se in seguito si ricompila la classe e si cambia il nome dell'elemento in `abc`, gli altri assembly che usano la classe non possono più accedere a quell'elemento. Pertanto, quando si rilascia una versione aggiornata di un assembly, non si devono modificare le maiuscole e le minuscole degli elementi pubblici.  
  
 Per ulteriori informazioni, vedere [Common Language Runtime](http://msdn.microsoft.com/library/059a624e-f7db-4134-ba9f-08b676050482).  
  
### <a name="correct-approach"></a>Approccio corretto  
 Per consentire agli altri componenti di accedere alle variabili, trattare i loro nomi come se distinguessero fra maiuscole e minuscole. Quando si testa la classe o il modulo, assicurarsi che gli altri assembly si associno alle variabili giuste. Dopo aver pubblicato un componente, non apportare modifiche ai nomi delle variabili esistenti e neppure alla loro combinazione di maiuscole e minuscole.  
  
## <a name="wrong-variable-being-used"></a>Variabile usata non corretta  
 Quando si dispone di più di una variabile con lo stesso nome, il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore tenta di risolvere ogni riferimento a tale nome. Se le variabili hanno un ambito diverso, il compilatore risolve il riferimento secondo la dichiarazione con l'ambito più ristretto. Se hanno lo stesso ambito, la risoluzione non riuscirà e il compilatore segnalerà un errore. Per ulteriori informazioni, vedere [riferimenti a elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
### <a name="correct-approach"></a>Approccio corretto  
 Evitare l'uso di variabili con lo stesso nome ma un ambito diverso. Se si usano altri assembly o progetti, evitare il più possibile l'uso di nomi definiti in questi componenti esterni. Se si hanno più variabili con lo stesso nome, assicurarsi di qualificare ogni riferimento a esso. Per ulteriori informazioni, vedere [riferimenti a elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Variabili](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [Dichiarazione di variabile](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Variabili oggetto](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Dichiarazione di variabili oggetto](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [Procedura: accedere ai membri di un oggetto](../../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)   
 [Valori di variabili oggetto](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [Procedura: determinare a quale tipo fa riferimento una variabile oggetto](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-what-type-an-object-variable-refers-to.md)   
 [Riferimenti a elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Nomi di elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
