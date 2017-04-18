---
title: Costanti (Visual Basic) definiti dall&quot;utente | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- constants, circular references
- Const statement [Visual Basic], user-defined constants
- user-defined constants
- scope, constants
- constants, user-defined
- circular references between constants
ms.assetid: a1206d5c-c45e-4ac2-970a-4a0be6a05fdd
caps.latest.revision: 19
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e5942d8663a8866b2f9794a86756f2bf25660ba5
ms.lasthandoff: 03/13/2017

---
# <a name="user-defined-constants-visual-basic"></a>Costanti definite dall'utente (Visual Basic)
Una costante è un nome significativo che prende il posto di un numero o una stringa che non cambia. Costanti di archiviano i valori, come suggerisce il nome, rimangono costanti durante l'esecuzione di un'applicazione. È possibile utilizzare costanti definite da controlli o ai componenti utilizzati oppure è possibile creare. Vengono descritte le costanti personalizzate come *definita dall'utente*.  
  
 Consente di dichiarare una costante con il `Const` istruzione, utilizzando le stesse linee guida per la creazione di un nome di variabile. Se `Option Strict` è `On`, è necessario dichiarare in modo esplicito il tipo di costante.  
  
## <a name="const-statement-usage"></a>Utilizzo dell'istruzione const  
 Oggetto `Const` istruzione può rappresentare un matematica o data/ora quantità:  
  
 [!code-vb[VbEnumsTask&#10;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_1.vb)]  
  
 È inoltre possibile definire `String` costanti:  
  
 [!code-vb[13 VbEnumsTask](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_2.vb)]  
  
 L'espressione a destra del segno di uguale ( `=` ) è spesso un numero o valore letterale stringa, ma può essere anche un'espressione che restituisce un numero o stringa (anche se tale espressione non può contenere chiamate alle funzioni). È anche possibile definire le costanti in termini di costanti definite in precedenza:  
  
 [!code-vb[VbEnumsTask&#15;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_3.vb)]  
  
## <a name="scope-of-user-defined-constants"></a>Ambito delle costanti definite dall'utente  
 Oggetto `Const` ambito dell'istruzione è uguale a quello di una variabile dichiarata nella stessa posizione. È possibile specificare l'ambito in uno dei modi seguenti:  
  
-   Per creare una costante che esiste solo all'interno di una routine, dichiararla all'interno di tale procedura.  
  
-   Per creare una costante che sia disponibile per tutte le routine all'interno di una classe, ma non per il codice all'esterno di tale modulo, dichiararla nella sezione dichiarazioni della classe.  
  
-   Per creare una costante che sia disponibile per tutti i membri di un assembly, ma non ai client all'esterno dell'assembly, dichiararla utilizzando il `Friend` (parola chiave) nella sezione dichiarazioni della classe.  
  
-   Per creare una costante che sia disponibile in tutta l'applicazione, dichiararla utilizzando il `Public` (parola chiave) nelle dichiarazioni di sezione della classe.  
  
 Per ulteriori informazioni, vedere [procedura: dichiarare una costante](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md).  
  
### <a name="avoiding-circular-references"></a>Riferimenti circolari  
 Poiché le costanti possono essere definite in termini di altre costanti, è possibile creare inavvertitamente un *ciclo*, o un riferimento circolare, tra due o più costanti. Si verifica un ciclo quando si dispone di due o più costanti pubbliche, ognuno dei quali viene definito come l'altro, come nell'esempio seguente:  
  
 [!code-vb[VbEnumsTask&#16;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_4.vb)]  
[!code-vb[VbEnumsTask n.&17;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_5.vb)]  
  
 Se si verifica un ciclo, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] genera un errore del compilatore.  
  
## <a name="see-also"></a>Vedere anche  
 [Const (istruzione)](../../../../visual-basic/language-reference/statements/const-statement.md)   
 [Tipi di dati costanti e letterali](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [Costanti ed enumerazioni](../../../../visual-basic/programming-guide/language-features/constants-enums/index.md)   
 [Costanti ed enumerazioni](../../../../visual-basic/language-reference/constants-and-enumerations.md)   
 [Cenni preliminari sulle enumerazioni](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [Cenni preliminari sulle costanti](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [Procedura: dichiarare un'enumerazione](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [Qualifica di nomi ed enumerazioni](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [Istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
