---
title: "Access Levels in Visual Basic | Microsoft Docs"
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
  - "members, accessing in Visual Basic"
  - "Friend access modifier"
  - "access levels, declared elements"
  - "access levels"
  - "access modifiers"
  - "Public access modifier"
  - "Protected access modifier"
  - "Protected Friend access modifier"
  - "Private access modifier"
  - "declared elements, access level"
ms.assetid: 6e06c1ab-fd78-47f0-83a8-1152780b5e1a
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Access Levels in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il *livello di accesso* di un elemento dichiarato indica l'ampiezza della capacità di accesso all'elemento, ossia specifica le parti di codice che dispongono delle autorizzazioni di lettura o scrittura sull'elemento.  Questo valore dipende non solo dal modo in cui viene dichiarato l'elemento stesso ma anche dal livello di accesso del relativo contenitore.  Un codice che non può accedere a un elemento contenitore non può accedere ai relativi elementi contenuti, inclusi quelli dichiarati come `Public`.  Ad esempio, è possibile accedere a una variabile `Public` in una struttura `Private` dall'interno della classe contenente la struttura, ma non dall'esterno della classe.  
  
## Public  
 La parola chiave [Public](../../../../visual-basic/language-reference/modifiers/public.md) nell'istruzione di dichiarazione indica che è possibile accedere agli elementi da qualsiasi codice all'interno dello stesso progetto, da altri progetti che fanno riferimento al progetto e da qualsiasi assembly compilato dal progetto.  Nel codice riportato di seguito è illustrato un esempio di dichiarazione `Public`.  
  
```  
Public Class classForEverybody  
```  
  
 È possibile utilizzare la parola chiave `Public` solo a livello di modulo, di interfaccia o di spazio dei nomi.  Questo significa che è possibile dichiarare un elemento Public a livello di file di origine o di spazio dei nomi oppure all'interno di un'interfaccia, di un modulo, di una classe o di una struttura, ma non in una routine.  
  
## Protected  
 La parola chiave [Protected](../../../../visual-basic/language-reference/modifiers/protected.md) nell'istruzione di dichiarazione indica che è possibile accedere agli elementi solo dall'interno della stessa classe o da una classe da essa derivata.  Nel codice riportato di seguito è illustrato un esempio di dichiarazione `Protected`.  
  
```  
Protected Class classForMyHeirs  
```  
  
 È possibile utilizzare la parola chiave `Protected` solo a livello di classe e solo quando si dichiara un membro di una classe.  Questo significa che è possibile dichiarare un elemento Protected in una classe ma non a livello di file di origine o di spazio dei nomi né all'interno di un'interfaccia, di un modulo, di una struttura o di una routine.  
  
## Friend  
 La parola chiave [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) nell'istruzione di dichiarazione indica che è possibile accedere agli elementi dall'interno dello stesso assembly, ma non dall'esterno dell'assembly.  Nel codice riportato di seguito è illustrato un esempio di dichiarazione `Friend`.  
  
```  
Friend stringForThisProject As String  
```  
  
 È possibile utilizzare la parola chiave `Friend` solo a livello di modulo, di interfaccia o di spazio dei nomi.  Questo significa che è possibile dichiarare un elemento Friend a livello di file di origine o di spazio dei nomi oppure all'interno di un'interfaccia, di un modulo, di una classe o di una struttura, ma non in una routine.  
  
## Protected Friend  
 L'utilizzo di entrambe le parole chiave `Protected` e `Friend` nell'istruzione di dichiarazione indica che è possibile accedere agli elementi dalle classi derivate e\/o dall'interno dello stesso assembly.  Nel codice riportato di seguito è illustrato un esempio di dichiarazione `Protected` `Friend`.  
  
```  
Protected Friend stringForProjectAndHeirs As String  
```  
  
 È possibile utilizzare `Protected` `Friend` solo a livello di classe e solo quando si dichiara un membro di una classe.  Questo significa che è possibile dichiarare un elemento Protected Friend in una classe ma non a livello di file di origine o di spazio dei nomi né all'interno di un'interfaccia, di un modulo, di una struttura o di una routine.  
  
## Private  
 La parola chiave [Private](../../../../visual-basic/language-reference/modifiers/private.md) nell'istruzione di dichiarazione indica che è possibile accedere agli elementi solo dall'interno dello stesso modulo, classe o struttura.  Nel codice riportato di seguito è illustrato un esempio di dichiarazione `Private`.  
  
```  
Private numberForMeOnly As Integer  
```  
  
 È possibile utilizzare la parola chiave `Private` solo a livello di modulo.  Questo significa che è possibile dichiarare un elemento Private all'interno di un modulo, di una classe o di una struttura ma non a livello di file di origine o di spazio dei nomi né dall'interno di un'interfaccia o di una routine.  
  
 A livello di modulo, l'istruzione `Dim` senza alcuna parola chiave relativa al livello di accesso equivale a una dichiarazione `Private`.  È possibile comunque utilizzare la parola chiave `Private` per rendere più semplice la lettura e l'interpretazione del codice.  
  
## Modificatori di accesso  
 Le parole chiave che specificano il livello di accesso sono dette *modificatori di accesso*.  Nella seguente tabella viene effettuato un confronto tra i vari modificatori di accesso.  
  
|Modificatore di accesso|Livello di accesso concesso|Elementi che è possibile dichiarare con questo livello di accesso|Contesto della dichiarazione all'interno del quale è possibile utilizzare questo modificatore|  
|-----------------------------|---------------------------------|-----------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|  
|`Public`|Illimitato<br /><br /> L'accesso a un elemento Public è consentito a qualsiasi parte di codice in cui tale elemento è visibile.|Interfacce<br /><br /> Moduli<br /><br /> Classi<br /><br /> Strutture<br /><br /> Membri di struttura<br /><br /> Procedure<br /><br /> Proprietà<br /><br /> Variabili membro<br /><br /> Costanti<br /><br /> Enumerazioni<br /><br /> Eventi<br /><br /> Dichiarazioni esterne<br /><br /> Delegati|File di origine<br /><br /> Spazio dei nomi<br /><br /> Interfaccia<br /><br /> Modulo<br /><br /> Classe<br /><br /> Struttura|  
|`Protected`|Derivazionale<br /><br /> L'accesso a un elemento Protected è consentito al codice della classe che dichiara tale elemento o di una classe da essa derivata.|Interfacce<br /><br /> Classi<br /><br /> Strutture<br /><br /> Procedure<br /><br /> Proprietà<br /><br /> Variabili membro<br /><br /> Costanti<br /><br /> Enumerazioni<br /><br /> Eventi<br /><br /> Dichiarazioni esterne<br /><br /> Delegati|Classe|  
|`Friend`|Assembly:<br /><br /> L'accesso a un elemento Friend è consentito al codice dell'assembly che dichiara tale elemento.|Interfacce<br /><br /> Moduli<br /><br /> Classi<br /><br /> Strutture<br /><br /> Membri di struttura<br /><br /> Procedure<br /><br /> Proprietà<br /><br /> Variabili membro<br /><br /> Costanti<br /><br /> Enumerazioni<br /><br /> Eventi<br /><br /> Dichiarazioni esterne<br /><br /> Delegati|File di origine<br /><br /> Spazio dei nomi<br /><br /> Interfaccia<br /><br /> Modulo<br /><br /> Classe<br /><br /> Struttura|  
|`Protected` `Friend`|Unione di `Protected` e `Friend`<br /><br /> L'accesso a un elemento Protected Friend è consentito al codice della stessa classe o dello stesso assembly di tale elemento oppure al codice di una qualsiasi classe derivata dalla classe dell'elemento.|Interfacce<br /><br /> Classi<br /><br /> Strutture<br /><br /> Procedure<br /><br /> Proprietà<br /><br /> Variabili membro<br /><br /> Costanti<br /><br /> Enumerazioni<br /><br /> Eventi<br /><br /> Dichiarazioni esterne<br /><br /> Delegati|Classe|  
|`Private`|Contesto della dichiarazione<br /><br /> L'accesso a un elemento Private è consentito al codice del tipo che dichiara tale elemento, incluso il codice dei tipi contenuti.|Interfacce<br /><br /> Classi<br /><br /> Strutture<br /><br /> Membri di struttura<br /><br /> Procedure<br /><br /> Proprietà<br /><br /> Variabili membro<br /><br /> Costanti<br /><br /> Enumerazioni<br /><br /> Eventi<br /><br /> Dichiarazioni esterne<br /><br /> Delegati|Modulo<br /><br /> Classe<br /><br /> Struttura|  
  
## Vedere anche  
 [Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Static](../../../../visual-basic/language-reference/modifiers/static.md)   
 [Declared Element Names](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Declared Element Characteristics](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [Lifetime in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [How to: Control the Availability of a Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-availability-of-a-variable.md)   
 [Variables](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)