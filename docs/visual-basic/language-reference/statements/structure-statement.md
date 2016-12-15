---
title: "Structure Statement | Microsoft Docs"
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
  - "vb.Structure"
  - "Structure"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "user-defined types, Structure statement"
  - "compound data types"
  - "Structure keyword"
  - "Structure statement"
  - "UDT (user-defined types)"
  - "types [Visual Basic], user-defined"
ms.assetid: 9bd1deea-2a89-4cdc-812c-6dcbb947c391
caps.latest.revision: 28
caps.handback.revision: 28
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Structure Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di dichiarare il nome di una struttura e introduce la definizione di variabili, proprietà, eventi e routine comprese dalla struttura.  
  
## Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Partial ] _  
Structure name [ ( Of typelist ) ]  
    [ Implements interfacenames ]  
    [ datamemberdeclarations ]  
    [ methodmemberdeclarations ]  
End Structure  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`attributelist`|Parametro facoltativo.  Vedere [Elenco degli attributi](../../../visual-basic/language-reference/statements/attribute-list.md).|  
|`accessmodifier`|Parametro facoltativo.  ad esempio uno dei seguenti:<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).|  
|`Shadows`|Parametro facoltativo.  Vedere [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md).|  
|`Partial`|Parametro facoltativo.  Indica una definizione parziale della struttura.  Vedere [Partial](../../../visual-basic/language-reference/modifiers/partial.md).|  
|`name`|Obbligatorio.  Nome di questa struttura.  Per informazioni, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`Of`|Parametro facoltativo.  Specifica che si tratta di una struttura generica.|  
|`typelist`|Obbligatoria se si utilizza la parola chiave [Of](../../../visual-basic/language-reference/statements/of-clause.md).  Elenco di parametri di tipo per la struttura.  Vedere [Elenco dei tipi](../../../visual-basic/language-reference/statements/type-list.md).|  
|`Implements`|Parametro facoltativo.  Indica che la struttura consente di implementare i membri di una o più interfacce.  Vedere [Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md).|  
|`interfacenames`|Obbligatoria se si utilizza l'istruzione `Implements`.  Nomi delle interfacce implementate dalla struttura.|  
|`datamemberdeclarations`|Obbligatorio.  Zero o più istruzioni `Const`, `Dim`, `Enum` o `Event` che dichiarano i *membri dei dati* della struttura.|  
|`methodmemberdeclarations`|Parametro facoltativo.  Nessuna o più dichiarazioni di routine `Function`, `Operator`, `Property` o `Sub` che fungono da *membri di metodo* della struttura.|  
|`End Structure`|Obbligatorio.  Consente di terminare la definizione `Structure`.|  
  
## Note  
 L'istruzione `Structure` definisce un tipo di valore composto personalizzabile.  Una *struttura* rappresenta una generalizzazione del tipo definito dall'utente \(UDT, User\-Defined Type\) supportato dalle precedenti versioni di Visual Basic.  Per ulteriori informazioni, vedere [Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md).  
  
 Le strutture supportano molte delle funzionalità supportate dalle classi.  Le strutture che ad esempio possono contenere proprietà e routine, sono in grado di implementare interfacce e possono disporre di costruttori parametrizzati.  Le differenze tra strutture e classi sono tuttavia significative a livello di ereditarietà, dichiarazione e utilizzo.  Inoltre le classi sono tipi di riferimenti mentre le strutture sono tipi di valori.  Per ulteriori informazioni, vedere [Structures and Classes](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md).  
  
 È possibile utilizzare `Structure` solo a livello di modulo o di spazio dei nomi.  Il altri termini, il *contesto della dichiarazione* per una struttura deve essere costituito di un file di origine, uno spazio dei nomi, una classe, una struttura, un modulo o un'interfaccia, ma non una routine o un blocco.  Per ulteriori informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 L'impostazione predefinita della struttura è l'accesso [Friend](../../../visual-basic/language-reference/modifiers/friend.md).  È possibile modificarne i livelli di accesso mediante gli appositi modificatori.  Per ulteriori informazioni, vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## Regole  
  
-   **Annidamento.** È possibile definire una struttura all'interno di un altra.  La struttura esterna viene definita *struttura contenente*, mentre la struttura interna viene definita *struttura annidata*.  Attraverso la struttura contenente non è tuttavia possibile accedere ai membri di una struttura annidata.  È invece necessario dichiarare una variabile del tipo di dati della struttura annidata.  
  
-   **Dichiarazione di membro.** È necessario dichiarare tutti i membri di una struttura.  Un membro di struttura non può essere [Protected](../../../visual-basic/language-reference/modifiers/protected.md) o `Protected Friend` in quanto la struttura non prevede ereditarietà.  La struttura stessa tuttavia, può essere `Protected` o `Protected Friend`.  
  
     È possibile dichiarare zero o più variabili non condivise oppure eventi non condivisi o non personalizzati in una struttura.  Non è possibile che siano presenti solo costanti, proprietà e routine, anche se alcune di esse sono di tipo non condiviso.  
  
-   **Inizializzazione.** Non è possibile inizializzare il valore di un membro dati non condiviso di una struttura nell'ambito della relativa dichiarazione.  È invece necessario che tale membro dati venga inizializzato per mezzo di un costruttore con parametri nella struttura oppure che gli venga assegnato un valore dopo la creazione di un'istanza della struttura.  
  
-   **Ereditarietà.** Una struttura non può ereditare da qualsiasi tipo diverso da <xref:System.ValueType>, dal quale ereditano tutte le strutture.  In particolare, una struttura non può ereditare da un'altra.  
  
     Non è possibile utilizzare l'[Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md) nella definizione di una struttura, anche per specificare <xref:System.ValueType>.  
  
-   **Implementazione.** Se la struttura utilizza l'[Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md), è necessario implementare ogni membro definito da ogni interfaccia specificata in `interfacenames`.  
  
-   **Proprietà predefinita.** Una struttura è in grado di specificare al massimo una proprietà come *proprietà predefinita*, utilizzando il modificatore [Default](../../../visual-basic/language-reference/modifiers/default.md).  Per ulteriori informazioni, vedere [Default](../../../visual-basic/language-reference/modifiers/default.md).  
  
## Comportamento  
  
-   **Livello di accesso.** All'interno di una struttura è possibile dichiarare ogni membro con il suo livello di accesso personale.  L'impostazione predefinita dei membri della struttura è l'accesso [Public](../../../visual-basic/language-reference/modifiers/public.md).  Si noti che se la struttura stessa ha un livello di accesso più ristretto, questo restringe automaticamente l'accesso ai suoi membri, anche se si regolano i livelli di accesso dei membri con i modificatori di accesso.  
  
-   **Ambito.** Una struttura si trova nell'area di validità tramite lo spazio dei nomi, la classe, la struttura o il modulo che la contiene.  
  
     L'ambito di un membro di ogni struttura è l'intera struttura.  
  
-   **Durata.** Una struttura non dispone di una propria durata,  ma ogni istanza di quella struttura dispone di una durata indipendente da tutte le altre.  
  
     La durata di un'istanza comincia quando viene creata da una clausola [New Operator](../../../visual-basic/language-reference/operators/new-operator.md).  e termina quando termina la durata della variabile che la contiene.  
  
     Non è possibile estendere la durata di un'istanza della struttura.  Un'approssimazione alla funzionalità statica della struttura è fornita da un modulo.  Per ulteriori informazioni, vedere [Module Statement](../../../visual-basic/language-reference/statements/module-statement.md).  
  
     La durata dei membri della struttura dipende da come e dove sono stati dichiarati.  Per ulteriori informazioni, vedere "Durata" in [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md).  
  
-   **Qualificazione.** È necessario che il codice all'esterno di una struttura qualifichi un nome del membro con il nome di tale struttura.  
  
     Se il codice all'interno di una struttura annidata fa un riferimento non completo a un elemento di programmazione, l'elemento verrà innanzitutto cercato nella struttura annidata, quindi nella sua struttura contenente e via di seguito fino all'elemento contenente più esterno.  Per ulteriori informazioni, vedere [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
-   **Consumo di memoria.** Come nel caso di tutti i tipi di dati compositi, il calcolo del consumo di memoria totale di una struttura in base alla somma delle allocazioni di memoria nominali dei relativi membri presenta alcuni rischi.  Non è inoltre possibile supporre con certezza che l'ordine di archiviazione in memoria corrisponda esattamente all'ordine di dichiarazione.  Se è necessario controllare il layout di archiviazione di una struttura, è possibile applicare l'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute> all'istruzione `Structure`.  
  
## Esempio  
 Nell'esempio seguente l'istruzione `Structure` viene utilizzata per definire un insieme di dati correlati per un dipendente.  Viene illustrato l'utilizzo di membri `Public`, `Friend` e `Private` per riflettere la riservatezza degli elementi di dati.  Vengono inoltre illustrati membri di routine, proprietà ed eventi.  
  
 [!code-vb[VbVbalrStatements#57](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/structure-statement_1.vb)]  
  
## Vedere anche  
 [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Module Statement](../../../visual-basic/language-reference/statements/module-statement.md)   
 [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Const Statement](../../../visual-basic/language-reference/statements/const-statement.md)   
 [Enum Statement](../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Structures and Classes](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)