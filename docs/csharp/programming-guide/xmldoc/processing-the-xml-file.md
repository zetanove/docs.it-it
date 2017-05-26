---
title: Elaborazione del file XML (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- XML processing [C#]
- XML [C#], processing
ms.assetid: 60c71193-9dac-4cd3-98c5-100bd0edcc42
caps.latest.revision: 16
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a780a11d8dd238187eb82933359bbb151bb3c333
ms.openlocfilehash: 3a585025063847f93dc2c3b3747bd3406f89eae4
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="processing-the-xml-file-c-programming-guide"></a>Elaborazione del file XML (Guida per programmatori C#)
Il compilatore genera una stringa identificativa (ID) per ciascun costrutto del codice che contiene tag per la creazione della documentazione. Per informazioni sull'applicazione di tag al codice, vedere [Tag consigliati per i commenti relativi alla documentazione ](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md). L'ID identifica in modo univoco il costrutto. I programmi che elaborano il file XML possono usare la stringa ID per identificare il corrispondente elemento di metadati/reflection di .NET Framework a cui si applica la documentazione.  
  
 Il file XML non è una rappresentazione gerarchica del codice, bensì un normale elenco contenente un ID generato per ogni elemento.  
  
 Per generare gli ID, il compilatore applica le regole seguenti:  
  
-   La stringa non deve contenere spazi vuoti.  
  
-   La prima parte della stringa ID specifica il tipo di membro da identificare, con un singolo carattere seguito dai due punti. Vengono usati i tipi di membri seguenti:  
  
    |Carattere|Descrizione|  
    |---------------|-----------------|  
    |N|namespace<br /><br /> Non è possibile aggiungere a uno spazio dei nomi commenti relativi alla documentazione, ma, se supportati, è possibile creare riferimenti cref a tali commenti.|  
    |T|tipo: classe, interfaccia, struct, enum, delegato|  
    |F|campo|  
    |P|proprietà (compresi gli indicizzatori o altre proprietà indicizzate)|  
    |M|metodo (compresi i metodi speciali, ad esempio costruttori, operatori e così via)|  
    |E|event|  
    |!|stringa di errore<br /><br /> Nella parte restante della stringa vengono fornite informazioni sull'errore. Il compilatore C# genera informazioni sugli errori per tutti i collegamenti che non è possibile risolvere.|  
  
-   La seconda parte della stringa identifica il nome completo dell'elemento, a partire dalla radice dello spazio dei nomi. Il nome dell'elemento, i tipi che lo contengono e lo spazio dei nomi sono separati da punti. Se il nome dell'elemento contiene dei punti, questi verranno sostituiti con il segno di cancelletto ('#'), in base al presupposto che nessun nome di elemento contiene direttamente tale segno. Ad esempio, il nome completo del costruttore String è "System.String.#ctor".  
  
-   Per le proprietà e i metodi, se il metodo ha degli argomenti, verrà incluso di seguito l'elenco degli argomenti racchiuso tra parentesi. Se non sono presenti argomenti, non verranno usate le parentesi. Gli argomenti sono separati da virgole. La codifica di ciascun argomento è del tutto simile alla modalità di codifica usata in una firma .NET Framework:  
  
    -   Tipi di base. I tipi regolari (ELEMENT_TYPE_CLASS o ELEMENT_TYPE_VALUETYPE) vengono rappresentati con il nome completo del tipo.  
  
    -   Tipi intrinseci (ad esempio, ELEMENT_TYPE_I4, ELEMENT_TYPE_OBJECT, ELEMENT_TYPE_STRING, ELEMENT_TYPE_TYPEDBYREF. ed ELEMENT_TYPE_VOID) vengono rappresentati come nome completo del tipo completo corrispondente, ad esempio System.Int32 o System.TypedReference.  
  
    -   ELEMENT_TYPE_PTR viene rappresentato con '*' dopo il tipo modificato.  
  
    -   ELEMENT_TYPE_BYREF viene rappresentato con '@' dopo il tipo modificato.  
  
    -   ELEMENT_TYPE_PINNED viene rappresentato con '^' dopo il tipo modificato. Non viene mai generato dal compilatore C#.  
  
    -   ELEMENT_TYPE_CMOD_REQ viene rappresentato con '&#124;' seguito dal nome completo della classe di modificatori dopo il tipo modificato. Non viene mai generato dal compilatore C#.  
  
    -   ELEMENT_TYPE_CMOD_OPT viene rappresentato con '!' seguito dal nome completo della classe di modificatori dopo il tipo modificato.  
  
    -   ELEMENT_TYPE_SZARRAY viene rappresentato con "[]" dopo il tipo di elemento della matrice.  
  
    -   ELEMENT_TYPE_GENERICARRAY viene rappresentato con "[?]" dopo il tipo di elemento della matrice. Non viene mai generato dal compilatore C#.  
  
    -   ELEMENT_TYPE_ARRAY viene rappresentato con [*limite inferiore*:`size`,*limite inferiore*:`size`], dove il numero di virgole indica il numero di dimensioni - 1. I limiti inferiori e le dimensioni di ogni dimensione, qualora noti, vengono rappresentati con valori decimali. Se non è specificato alcun valore, il limite o la dimensione inferiore viene omesso. Se vengono omessi il limite inferiore e la dimensione per una dimensione specifica, viene omesso anche ':'. Ad esempio, una matrice a due dimensioni con limiti inferiori pari a 1 e dimensioni non specificate viene rappresentata con [1:,1:].  
  
    -   ELEMENT_TYPE_FNPTR viene rappresentato con "=FUNC:`type`(*signature*)", dove `type` rappresenta il tipo restituito e *signature* identifica gli argomenti del metodo. Se non vi sono argomenti, le parentesi vengono omesse. Non viene mai generato dal compilatore C#.  
  
     I seguenti componenti della firma non vengono rappresentati in quanto non vengono mai usati per differenziare i metodi di overload:  
  
    -   convenzione di chiamata  
  
    -   tipo restituito  
  
    -   ELEMENT_TYPE_SENTINEL  
  
-   Limitatamente agli operatori di conversione (op_Implicit e op_Explicit), il valore restituito del metodo viene codificato con '~' seguito dal tipo restituito, codificato come descritto in precedenza.  
  
-   Nel caso di tipi generici, il nome del tipo verrà seguito da un apice inverso e quindi da un numero che indica il numero di parametri di tipo generici.  Ad esempio,  
  
     `<member name="T:SampleClass`2">` is the tag for a type that is defined as `public class SampleClass\<T, U>`.  
  
     Nel caso di metodi che accettano tipi generici come parametri, i parametri dei tipi generici sono caratterizzati da numeri preceduti da apici inversi, ad esempio \`0,`1).  Ogni numero rappresenta la notazione della matrice in base zero per i parametri generici del tipo.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato come vengono generate le stringhe di ID per una classe e i relativi membri:  
  
 [!code-cs[csProgGuidePointers#21](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/processing-the-xml-file_1.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [/doc (opzioni del compilatore C#)](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [Commenti relativi alla documentazione XML](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)
