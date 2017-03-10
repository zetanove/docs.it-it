---
title: "Anonymous Type Definition (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "anonymous types [Visual Basic], type definition"
ms.assetid: 7a8a0ddc-55ba-4d67-869e-87a84d938bac
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Anonymous Type Definition (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In risposta alla dichiarazione di un'istanza di un tipo anonimo, il compilatore crea una nuova definizione di classe che contiene le proprietà specificate per il tipo.  
  
## Codice generato dal compilatore  
 Per la seguente definizione di `product`, il compilatore crea una nuova definizione di classe che contiene le proprietà `Name`, `Price`e `OnHand`.  
  
 [!code-vb[VbVbalrAnonymousTypes#25](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-type-definition_1.vb)]  
  
 La definizione di classe contiene definizioni di proprietà simili alle seguenti.  Si noti che non è disponibile un metodo `Set` per le proprietà chiave.  I valori delle proprietà chiave sono di sola lettura.  
  
```vb#  
Public Class $Anonymous1  
    Private _name As String  
    Private _price As Double  
    Private _onHand As Integer  
     Public ReadOnly Property Name() As String  
        Get  
            Return _name  
        End Get  
    End Property  
  
    Public ReadOnly Property Price() As Double  
        Get  
            Return _price  
        End Get  
    End Property  
  
    Public Property OnHand() As Integer  
        Get  
            Return _onHand  
        End Get  
        Set(ByVal Value As Integer)  
            _onHand = Value  
        End Set  
    End Property  
  
End Class  
```  
  
 Inoltre, le definizioni di tipo anonimo contengono un costruttore predefinito.  Non è consentito l'uso di costruttori che richiedono parametri.  
  
 Se una dichiarazione di tipo anonimo contiene almeno una proprietà chiave, la definizione del tipo esegue l'override di tre membri ereditati da <xref:System.Object>: <xref:System.Object.Equals%2A>, <xref:System.Object.GetHashCode%2A>e <xref:System.Object.ToString%2A>.  Se non viene dichiarata alcuna proprietà chiave, viene eseguito l'override solo di <xref:System.Object.ToString%2A>.  L'override fornisce la seguente funzionalità:  
  
-   `Equals` restituisce `True` se due istanze di tipo anonimo sono la stessa istanza, o se soddisfano le condizioni seguenti:  
  
    -   Hanno lo stesso numero di proprietà.  
  
    -   Le proprietà vengono dichiarate nello stesso ordine, con gli stessi nomi e gli stessi tipi dedotti.  Nel confronto tra nomi non viene applicata la distinzione tra maiuscole e minuscole.  
  
    -   Almeno una delle proprietà è una proprietà chiave e la parola chiave `Key` si applica alle stesse proprietà.  
  
    -   Il confronto di ogni coppia corrispondente di proprietà chiave restituisce `True`.  
  
     Ad esempio, `Equals` restituisce `True` solo per `employee01` e `employee08`, come illustrato nell'esempio seguente.  Il commento che precede ogni riga specifica la ragione per cui la nuova istanza nuova non corrisponde a `employee01` .  
  
     [!code-vb[VbVbalrAnonymousTypes#24](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-type-definition_2.vb)]  
  
-   `GetHashcode` fornisce un algoritmo di GetHashCode adeguatamente univoco.  L'algoritmo utilizza solo le proprietà chiave per calcolare il codice hash.  
  
-   `ToString` restituisce una stringa di valori concatenati della proprietà, come illustrato nell'esempio seguente.  Sono incluse sia le proprietà chiave che quelle non chiave.  
  
     [!code-vb[VbVbalrAnonymousTypes#29](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-type-definition_3.vb)]  
  
 Le proprietà denominate in modo esplicito di un tipo anonimo non devono essere in conflitto con questi metodi generati.  Ovvero, non è possibile utilizzare `.Equals`, `.GetHashCode` o `.ToString` per denominare una proprietà.  
  
 Le definizioni di tipo anonimo che includono almeno una proprietà chiave implementano anche l'interfaccia <xref:System.IEquatable%601?displayProperty=fullName>, dove `T` è il tipo del tipo anonimo.  
  
> [!NOTE]
>  Dichiarazioni di tipo anonimo creano lo stesso tipo anonimo solo se si verificano nello stesso assembly, le proprietà hanno gli stessi nomi e gli stessi tipi dedotti, le proprietà vengono dichiarate nello stesso ordine e le stesse proprietà vengono contrassegnate come proprietà chiave.  
  
## Vedere anche  
 [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)