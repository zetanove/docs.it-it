---
title: "Recupero di informazioni memorizzate negli attributi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "attributi [.NET Framework], recupero"
  - "istanze multiple di attributi"
  - "recupero di attributi"
ms.assetid: 37dfe4e3-7da0-48b6-a3d9-398981524e1c
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Recupero di informazioni memorizzate negli attributi
Il recupero di un attributo personalizzato è un'operazione semplice.  Dichiarare innanzitutto un'istanza dell'attributo che si desidera recuperare.  Utilizzare quindi il metodo <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=fullName> per inizializzare il nuovo attributo sul valore dell'attributo da recuperare.  Al termine dell'inizializzazione del nuovo attributo sarà sufficiente utilizzarne le proprietà per ottenere i valori.  
  
> [!IMPORTANT]
>  In questo argomento viene descritto come recuperare gli attributi per il codice caricato nel contesto di esecuzione.  Per recuperare gli attributi per il codice caricato nel contesto di sola reflection, è necessario utilizzare la classe <xref:System.Reflection.CustomAttributeData>, come illustrato in [How to: Load Assemblies into the Reflection\-Only Context](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md).  
  
 In questa sezione verranno descritti i seguenti metodi per il recupero degli attributi:  
  
-   [Recupero di una singola istanza di un attributo](#cpconretrievingsingleinstanceofattribute)  
  
-   [Recupero di più istanze di un attributo applicate allo stesso ambito](#cpconretrievingmultipleinstancesofattributeappliedtosamescope)  
  
-   [Recupero di più istanze di un attributo applicate ad ambiti diversi](#cpconretrievingmultipleinstancesofattributeappliedtodifferentscopes)  
  
<a name="cpconretrievingsingleinstanceofattribute"></a>   
## Recupero di una singola istanza di un attributo  
 Nell'esempio che segue l'attributo `DeveloperAttribute`, descritto nella sezione precedente, viene applicato a livello della classe `MainApp`.  Nel metodo `GetAttribute` si utilizza **GetCustomAttribute** per recuperare a livello di classe i valori memorizzati in `DeveloperAttribute` prima di visualizzarli nella console.  
  
 [!code-cpp[Conceptual.Attributes.Usage#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#18)]
 [!code-csharp[Conceptual.Attributes.Usage#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#18)]
 [!code-vb[Conceptual.Attributes.Usage#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#18)]  
  
 All'esecuzione di questo programma viene visualizzato il seguente testo.  
  
```  
The Name Attribute is: Joan Smith.  
The Level Attribute is: 42.  
The Reviewed Attribute is: True.  
```  
  
 Se non è possibile individuare l'attributo, il metodo **GetCustomAttribute** inizializza `MyAttribute` sul valore Null.  In questo esempio viene verificata la presenza di un'istanza di `MyAttribute` e l'utente viene informato qualora non venisse individuato alcun attributo.  Se non è possibile trovare l'attributo `DeveloperAttribute` nell'ambito della classe, nella console verrà visualizzato il seguente messaggio:  
  
```  
The attribute was not found.   
```  
  
 In questo esempio si presuppone che la definizione dell'attributo sia contenuta nello spazio dei nomi corrente.  Importare lo spazio dei nomi in cui si trova la definizione dell'attributo se non si tratta dello spazio dei nomi corrente.  
  
<a name="cpconretrievingmultipleinstancesofattributeappliedtosamescope"></a>   
## Recupero di più istanze di un attributo applicate allo stesso ambito  
 Nell'esempio precedente la classe da analizzare e l'attributo specifico da trovare vengono passati a <xref:System.Attribute.GetCustomAttribute%2A>.  Tale codice funziona correttamente solo se a livello di classe viene applicata un'unica istanza di un attributo.  Se vengono invece applicate più istanze di uno stesso attributo a livello della stessa classe il metodo **GetCustomAttribute** non è in grado di recuperare tutte le informazioni.  Nei casi in cui più istanze dello stesso attributo vengono applicate al medesimo ambito è possibile utilizzare <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=fullName> per inserire tutte le istanze di un attributo in una matrice.  Se ad esempio due istanze di `DeveloperAttribute` sono applicate a livello di classe per la stessa classe, sarà possibile modificare il metodo `GetAttribute` in modo da visualizzare le informazioni presenti in entrambi gli attributi.  Per applicare più attributi allo stesso livello, è necessario che l'attributo sia definito con la proprietà **AllowMultiple** impostata su **true** in <xref:System.AttributeUsageAttribute>.  
  
 Nell'esempio di codice riportato di seguito si illustra come utilizzare il metodo **GetCustomAttributes** per creare una matrice che faccia riferimento a tutte le istanze di `DeveloperAttribute` in qualsiasi classe fornita.  I valori di tutti gli attributi verranno quindi visualizzati nella console.  
  
 [!code-cpp[Conceptual.Attributes.Usage#19](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#19)]
 [!code-csharp[Conceptual.Attributes.Usage#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#19)]
 [!code-vb[Conceptual.Attributes.Usage#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#19)]  
  
 Se non viene individuato alcun attributo verrà generato un messaggio di avviso.  In caso contrario verranno visualizzate le informazioni contenute in entrambe le istanze di `DeveloperAttribute`.  
  
<a name="cpconretrievingmultipleinstancesofattributeappliedtodifferentscopes"></a>   
## Recupero di più istanze di un attributo applicate ad ambiti diversi  
 I metodi <xref:System.Attribute.GetCustomAttributes%2A> e <xref:System.Attribute.GetCustomAttribute%2A> non effettuano ricerche in un'intera classe per restituire tutte le istanze di un attributo presenti nella classe.  Questi metodi consentono invece di eseguire ricerche all'interno di un unico metodo o membro alla volta.  Se si utilizza una classe in cui lo stesso attributo è applicato a ciascun membro e si desidera recuperare i valori di tutti gli attributi applicati ai membri è necessario specificare in **GetCustomAttributes** e **GetCustomAttribute**ogni metodo o membro singolarmente.  
  
 Nell'esempio di codice riportato di seguito viene accettata una classe come parametro e viene effettuata la ricerca dell'attributo `DeveloperAttribute` definito in precedenza, a livello di classe e per ciascun singolo metodo della classe.  
  
 [!code-cpp[Conceptual.Attributes.Usage#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#20)]
 [!code-csharp[Conceptual.Attributes.Usage#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#20)]
 [!code-vb[Conceptual.Attributes.Usage#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#20)]  
  
 Se non viene individuata alcuna istanza di `DeveloperAttribute` a livello di metodo o di classe, l'utente verrà informato dal metodo `GetAttribute` che non è stato trovato alcun attributo e verrà visualizzato il nome del metodo o della classe in cui l'attributo non è presente.  Se viene invece individuato un attributo, nella console verranno visualizzati i campi `Name`, `Level` e `Reviewed`.  
  
 È possibile utilizzare i membri della classe <xref:System.Type> per accedere ai singoli metodi e membri della classe passata.  Nell'esempio viene innanzitutto eseguita una query all'oggetto **Type** per ottenere informazioni sull'attributo a livello di classe.  Viene quindi utilizzato <xref:System.Type.GetMethods%2A?displayProperty=fullName> per inserire le istanze di tutti i metodi in una matrice di oggetti <xref:System.Reflection.MemberInfo?displayProperty=fullName> al fine di recuperare le informazioni sugli attributi a livello di metodo.  È inoltre possibile utilizzare il metodo <xref:System.Type.GetProperties%2A?displayProperty=fullName> per cercare eventuali attributi a livello di proprietà o il metodo <xref:System.Type.GetConstructors%2A?displayProperty=fullName> per cercare eventuali attributi a livello di costruttore.  
  
## Vedere anche  
 <xref:System.Type?displayProperty=fullName>   
 <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=fullName>   
 <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=fullName>   
 [Attributi](../../../docs/standard/attributes/index.md)