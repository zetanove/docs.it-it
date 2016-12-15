---
title: "Namespace Statement | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Namespace"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "namespaces, root"
  - "Namespace statement"
  - "namespaces, nested"
  - "declaring namespaces, syntax"
  - "namespaces, declaring"
  - "root namespaces"
  - "declarations, namespaces"
ms.assetid: a31fbd95-9ace-4c3d-bbb1-51222a2272b2
caps.latest.revision: 39
caps.handback.revision: 39
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Namespace Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di dichiarare il nome di uno spazio dei nomi e provoca la compilazione del codice sorgente che segue la dichiarazione all'interno di tale spazio dei nomi.  
  
## Sintassi  
  
```  
Namespace [Global.] { name | name.name }  
    [ componenttypes ]  
End Namespace  
```  
  
## Parti  
 Global  
 Parametro facoltativo.  Consente di definire uno spazio dei nomi dallo spazio dei nomi radice del progetto.  Vedere [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md).  
  
 `name`  
 Obbligatorio.  Nome univoco che identifica lo spazio dei nomi.  È necessario che sia un identificativo valido di Visual Basic.  Per ulteriori informazioni, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
 `componenttypes`  
 Parametro facoltativo.  Elementi che compongono lo spazio dei nomi.  Questi includono, tra l'altro, enumerazioni, strutture, interfacce, classi, moduli, delegati e altri spazi dei nomi.  
  
 `End Namespace`  
 Consente di terminare un blocco `Namespace`.  
  
## Note  
 Gli spazi dei nomi vengono utilizzati come sistema organizzativo  in quanto forniscono un metodo di classificazione e presentazione degli elementi di programmazione esposti ad altri programmi e applicazioni.  Si noti che uno spazio dei nomi non corrisponde a *tipo* nel senso che una classe o una struttura essere\-non possibile dichiarare un elemento di programmazione per disporre il tipo di dati dello spazio dei nomi.  
  
 Tutti gli elementi di programmazione dichiarati dopo un'istruzione `Namespace` appartengono a tale spazio dei nomi.  Gli elementi continuano ad essere compilati nello spazio dei nomi dichiarato per ultimo fino a quando non viene rilevata un'istruzione `End Namespace` o un'altra istruzione `Namespace`.  
  
 Se uno spazio dei nomi è già definito, anche all'esterno del progetto, è possibile aggiungere elementi di programmazione.  A tale scopo, utilizzare un oggetto `Namespace` istruzione per eseguire Visual Basic per compilare gli elementi nello spazio dei nomi.  
  
 L'istruzione `Namespace` può essere utilizzata solo a livello del file o dello spazio dei nomi.  Il altri termini, il *contesto della dichiarazione* per uno spazio dei nomi deve essere costituito di un file di origine o uno spazio dei nomi e non può essere una classe, una struttura, un modulo, un'interfaccia o una routine.  Per ulteriori informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 È possibile dichiarare uno spazio dei nomi all'interno di un altro.  Non esiste un limite rigoroso ai livelli di annidamento che è possibile dichiarare. Tenere presente comunque che quando altro codice accede agli elementi dichiarati nello spazio dei nomi più interno, è necessario utilizzare una stringa di qualificazione contenente tutti i nomi degli spazi dei nomi della gerarchia di annidamento.  
  
## Livello di accesso  
 Gli spazi dei nomi vengono considerati come se fossero a `Public` livello di accesso.  È possibile accedere a uno spazio dei nomi dal codice in un punto qualsiasi nello stesso progetto, da altri progetti che fanno riferimento al progetto e da qualsiasi assembly compilato dal progetto.  
  
 Gli elementi di programmazione dichiarati a livello di spazio dei nomi, ovvero in uno spazio dei nomi ma non all'interno di altri elementi, possono disporre di accesso `Public` o `Friend`.  Se non viene specificato, il livello di accesso di tale elemento utilizza  `Friend` per impostazione predefinita.  Tra gli elementi che è possibile dichiarare a livello dello spazio dei nomi sono compresi classi, strutture, moduli, interfacce, enumerazioni e delegati.  Per ulteriori informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
## Spazio dei nomi radice  
 Tutti i nomi degli spazi dei nomi del progetto sono basati su uno *spazio dei nomi radice*.  In Visual Studio il nome del progetto viene assegnato come spazio dei nomi di primo livello predefinito per tutto il codice all'interno del progetto.  Se il progetto è denominato `Payroll` ad esempio, i relativi elementi di programmazione apparterranno allo spazio dei nomi `Payroll`.  Se si dichiara `Namespace funding`, il nome completo di quello spazio dei nomi sarà `Payroll.funding`.  
  
 Se si desidera specificare uno spazio dei nomi esistente in un'istruzione `Namespace`, come nell'esempio della classe elenco generica, è possibile impostare lo spazio dei nomi di primo livello su un valore null.  A questo scopo, scegliere **Proprietà progetto** dal menu **Progetto**, quindi eliminare il contenuto della voce **Spazio dei nomi di primo livello** in modo che la casella risulti vuota.  Se non si è eseguita questa operazione nell'esempio della classe elenco generica, `System.Collections.Generic` verrebbe considerato come nuovo spazio dei nomi all'interno del progetto `Payroll`, con il nome completo di `Payroll.System.Collections.Generic`.  
  
 In alternativa, è possibile utilizzare la parola chiave `Global` per fare riferimento agli elementi degli spazi dei nomi definiti all'esterno del progetto.  In questo modo è possibile mantenere il nome del progetto come spazio dei nomi di primo livello.  In questo modo si riduce la possibilità di unire in modo non intenzionale gli elementi di programmazione a quelli degli spazi dei nomi esistenti.  Per ulteriori informazioni, vedere “parola chiave globale la sezione in nomi completi„ in [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md).  
  
 `Global` la parola chiave può essere utilizzata in un'istruzione dello spazio dei nomi.  Ciò consente di definire uno spazio dei nomi dallo spazio dei nomi radice del progetto.  Per ulteriori informazioni, vedere “parola chiave globale la sezione in istruzioni dello spazio dei nomi„ in [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md).  
  
 **Risoluzione dei problemi.** Lo spazio dei nomi di primo livello può condurre a concatenazioni impreviste di nomi degli spazi dei nomi.  Se si fa riferimento agli spazi dei nomi definiti all'esterno del progetto, il compilatore di Visual Basic può interpretarli come spazi dei nomi annidati nello spazio dei nomi di primo livello.  In casi di questo tipo, il compilatore non riconosce i tipi che sono già stati definiti negli spazi dei nomi esterni.  Per evitare questo problema, impostare lo spazio dei nomi radice con un valore null come descritto in “nello spazio dei nomi radice,„ o utilizzare `Global` parola chiave per accedere agli elementi degli spazi dei nomi esterni.  
  
## Attributi e modificatori  
 Non è possibile applicare gli attributi a uno spazio dei nomi.  Un attributo fornisce informazioni ai metadati dell'assembly, che non è significativo per i classificatori di origine come gli spazi dei nomi.  
  
 Non è possibile applicare modificatori di accesso o di routine o qualsiasi altro modificatore a uno spazio dei nomi.  Poiché non si tratta di un tipo, questi modificatori non sono significativi.  
  
## Esempio  
 Nell'esempio illustrato di seguito vengono dichiarati due spazi dei nomi, uno annidato nell'altro.  
  
 [!code-vb[VbVbalrStatements#43](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/namespace-statement_1.vb)]  
  
## Esempio  
 Nell'esempio illustrato di seguito vengono dichiarati più spazi dei nomi annidati in un'unica riga in modo equivalente all'esempio precedente.  
  
 [!code-vb[VbVbalrStatements#41](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/namespace-statement_2.vb)]  
  
## Esempio  
 Nell'esempio illustrato di seguito si accede alla classe definita negli esempi precedenti.  
  
 [!code-vb[VbVbalrStatements#42](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/namespace-statement_3.vb)]  
  
## Esempio  
 Nell'esempio seguente viene definito lo scheletro di una nuova classe elenco e viene aggiunta questa classe allo spazio dei nomi <xref:System.Collections.Generic?displayProperty=fullName>.  
  
```vb  
Namespace System.Collections.Generic  
    Class specialSortedList(Of T)  
        Inherits List(Of T)  
        ' Insert code to define the special generic list class.  
    End Class  
End Namespace  
```  
  
## Vedere anche  
 [Imports Statement \(.NET Namespace and Type\)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)