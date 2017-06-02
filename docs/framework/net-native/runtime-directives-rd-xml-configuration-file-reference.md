---
title: "Riferimento a file di configurazione di direttive di runtime (rd.xml) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8241523f-d8e1-4fb6-bf6a-b29bfe07b38a
caps.latest.revision: 27
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 26
---
# Riferimento a file di configurazione di direttive di runtime (rd.xml)
Un file di direttive di runtime \(rd.xml\) è un file di configurazione XML che specifica se gli elementi del programma designato sono disponibili per la reflection.  Ecco un esempio di un file di direttive di runtime:  
  
```  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
<Application>  
  <Namespace Name="Contoso.Cloud.AppServices" Serialize="Required Public" />  
  <Namespace Name="ContosoClient.ViewModels" Serialize="Required Public" />  
  <Namespace Name="ContosoClient.DataModel" Serialize="Required Public" />  
  <Namespace Name="Contoso.Reader.UtilityLib" Serialize="Required Public" />  
  
  <Namespace Name="System.Collections.ObjectModel" >  
    <TypeInstantiation Name="ObservableCollection"   
          Arguments="ContosoClient.DataModel.ProductItem" Serialize="Public" />  
    <TypeInstantiation Name="ReadOnlyObservableCollection"   
          Arguments="ContosoClient.DataModel.ProductGroup" Serialize="Public" />  
  </Namespace>  
</Application>  
</Directives>  
  
```  
  
## La struttura di un file di direttive di runtime  
 Il file di direttive di runtime usa lo spazio dei nomi `http://schemas.microsoft.com/netfx/2013/01/metadata`.  
  
 L'elemento radice è l'elemento [Directives](../../../docs/framework/net-native/directives-element-net-native.md).  Può contenere zero o più elementi [Library](../../../docs/framework/net-native/library-element-net-native.md) e zero o uno elementi [Application](../../../docs/framework/net-native/application-element-net-native.md), come illustrato nella seguente struttura.  Gli attributi dell'elemento [Application](http://msdn.microsoft.com/it-it/2a038172-1ad5-47b7-a8db-79b2f1212f0a) possono definire i criteri di reflection di runtime a livello di applicazione, oppure possono fungere da contenitore per gli elementi figlio.  L'elemento [Library](../../../docs/framework/net-native/library-element-net-native.md), invece, è semplicemente un contenitore.  Gli elementi figlio degli elementi [Application](../../../docs/framework/net-native/application-element-net-native.md) e [Library](../../../docs/framework/net-native/library-element-net-native.md) definiscono i tipi, i metodi, i campi, le proprietà e gli eventi disponibili per la reflection.  
  
 Per le informazioni di riferimento, scegliere gli elementi dalla struttura seguente o vedere [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md).  Nella seguente gerarchia, i puntini di sospensione contrassegnano una struttura ricorsiva.  Le informazioni tra parentesi quadre indicano se tale elemento è facoltativo oppure obbligatorio e, se viene usato, il numero di istanze consentito \(una o molte\).  
  
 [Directives](../../../docs/framework/net-native/directives-element-net-native.md) \[1:1\]                        
 [Application](../../../docs/framework/net-native/application-element-net-native.md) \[0:1\]  
 [Assembly](../../../docs/framework/net-native/assembly-element-net-native.md) \[0:M\]  
 [Namespace](../../../docs/framework/net-native/namespace-element-net-native.md) \[0:M\]  
.  .  .    
 [Type](../../../docs/framework/net-native/type-element-net-native.md) \[0:M\]  
.  .  .    
 [TypeInstantiation](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) \(tipo generico costruito\) \[0:M\]  
.  .  .    
 [Namespace](../../../docs/framework/net-native/namespace-element-net-native.md) \[0:M\]  
 [Namespace](../../../docs/framework/net-native/namespace-element-net-native.md) \[0:M\]  
.  .  .    
 [Type](../../../docs/framework/net-native/type-element-net-native.md) \[0:M\]  
.  .  .    
 [TypeInstantiation](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) \(tipo generico costruito\) \[0:M\]   
.  .  .    
 [Type](../../../docs/framework/net-native/type-element-net-native.md) \[0:M\]  
 [Subtypes](../../../docs/framework/net-native/subtypes-element-net-native.md) \(sottoclassi di tipo contenitore\) \[O:1\]   
 [Type](../../../docs/framework/net-native/type-element-net-native.md) \[0:M\]  
.  .  .    
 [TypeInstantiation](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) \(tipo generico costruito\) \[0:M\]  
.  .  .    
 [AttributeImplies](../../../docs/framework/net-native/attributeimplies-element-net-native.md) \(il tipo contenitore è un attributo\) \[O:1\]   
 [GenericParameter](../../../docs/framework/net-native/genericparameter-element-net-native.md) \[0:M\]  
 [Method](../../../docs/framework/net-native/method-element-net-native.md) \[0:M\]  
 [Parameter](../../../docs/framework/net-native/parameter-element-net-native.md) \[0:M\]   
 [TypeParameter](../../../docs/framework/net-native/typeparameter-element-net-native.md) \[0:M\]  
 [GenericParameter](../../../docs/framework/net-native/genericparameter-element-net-native.md) \[0:M\]  
 [MethodInstantiation](../../../docs/framework/net-native/methodinstantiation-element-net-native.md) \(metodo generico costruito\) \[0:M\]   
 [Property](../../../docs/framework/net-native/property-element-net-native.md) \[0:M\]  
 [Field](../../../docs/framework/net-native/field-element-net-native.md) \[0:M\]  
 [Event](../../../docs/framework/net-native/event-element-net-native.md) \[0:M\]  
 [TypeInstantiation](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) \(tipo generico costruito\) \[0:M\]  
 [Type](../../../docs/framework/net-native/type-element-net-native.md) \[0:M\]  
.  .  .    
 [TypeInstantiation](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) \(tipo generico costruito\) \[0:M\]  
.  .  .    
 [Method](../../../docs/framework/net-native/method-element-net-native.md) \[0:M\]  
 [Parameter](../../../docs/framework/net-native/parameter-element-net-native.md) \[0:M\]   
 [TypeParameter](../../../docs/framework/net-native/typeparameter-element-net-native.md) \[0:M\]  
 [GenericParameter](../../../docs/framework/net-native/genericparameter-element-net-native.md) \[0:M\]  
 [MethodInstantiation](../../../docs/framework/net-native/methodinstantiation-element-net-native.md) \(metodo generico costruito\) \[0:M\]  
 [Property](../../../docs/framework/net-native/property-element-net-native.md) \[0:M\]  
 [Field](../../../docs/framework/net-native/field-element-net-native.md) \[0:M\]  
 [Event](../../../docs/framework/net-native/event-element-net-native.md) \[0:M\]  
 [Library](../../../docs/framework/net-native/library-element-net-native.md) \[0:M\]  
 [Assembly](../../../docs/framework/net-native/assembly-element-net-native.md) \[0:M\]  
 [Namespace](../../../docs/framework/net-native/namespace-element-net-native.md) \[0:M\]  
.  .  .    
 [Type](../../../docs/framework/net-native/type-element-net-native.md) \[0:M\]  
.  .  .    
 [TypeInstantiation](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) \(tipo generico costruito\) \[0:M\]  
.  .  .    
 [Namespace](../../../docs/framework/net-native/namespace-element-net-native.md) \[0:M\]  
 [Namespace](../../../docs/framework/net-native/namespace-element-net-native.md) \[0:M\]  
.  .  .    
 [Type](../../../docs/framework/net-native/type-element-net-native.md) \[0:M\]  
.  .  .    
 [TypeInstantiation](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) \(tipo generico costruito\) \[0:M\]   
.  .  .    
 [Type](../../../docs/framework/net-native/type-element-net-native.md) \[0:M\]  
 [Subtypes](../../../docs/framework/net-native/subtypes-element-net-native.md) \(sottoclassi di tipo contenitore\) \[O:1\]   
 [Type](../../../docs/framework/net-native/type-element-net-native.md) \[0:M\]  
.  .  .    
 [TypeInstantiation](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) \(tipo generico costruito\) \[0:M\]  
.  .  .    
 [AttributeImplies](../../../docs/framework/net-native/attributeimplies-element-net-native.md) \(il tipo contenitore è un attributo\) \[O:1\]   
 [GenericParameter](../../../docs/framework/net-native/genericparameter-element-net-native.md) \[0:M\]  
 [Method](../../../docs/framework/net-native/method-element-net-native.md) \[0:M\]  
 [MethodInstantiation](../../../docs/framework/net-native/methodinstantiation-element-net-native.md) \(metodo generico costruito\) \[0:M\]   
 [Property](../../../docs/framework/net-native/property-element-net-native.md) \[0:M\]  
 [Field](../../../docs/framework/net-native/field-element-net-native.md) \[0:M\]  
 [Event](../../../docs/framework/net-native/event-element-net-native.md) \[0:M\]  
 [TypeInstantiation](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) \(tipo generico costruito\) \[0:M\]  
 [Type](../../../docs/framework/net-native/type-element-net-native.md) \[0:M\]  
.  .  .    
 [TypeInstantiation](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) \(tipo generico costruito\) \[0:M\]  
.  .  .    
 [Method](../../../docs/framework/net-native/method-element-net-native.md) \[0:M\]  
 [MethodInstantiation](../../../docs/framework/net-native/methodinstantiation-element-net-native.md) \(metodo generico costruito\) \[0:M\]  
 [Property](../../../docs/framework/net-native/property-element-net-native.md) \[0:M\]  
 [Field](../../../docs/framework/net-native/field-element-net-native.md) \[0:M\]  
 [Event](../../../docs/framework/net-native/event-element-net-native.md) \[0:M\]  
  
 L'elemento [Application](../../../docs/framework/net-native/application-element-net-native.md) non può avere alcun attributo, oppure può avere attributi criteri descritti nella [sezione Direttive e criteri di runtime](#Directives).  
  
 Un elemento [Library](../../../docs/framework/net-native/library-element-net-native.md) ha un solo attributo, `Name`, che specifica il nome di una libreria o di un assembly, senza l'estensione del file.  Ad esempio, il seguente elemento [Library](../../../docs/framework/net-native/library-element-net-native.md) si applica a un assembly denominato Extensions.dll.  
  
```  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
     <!-- Child elements go here -->    
  </Application>  
  <Library Name="Extensions">  
     <!-- Child elements go here -->    
  </Library>  
</Directives>  
  
```  
  
<a name="Directives"></a>   
## Direttive e criteri di runtime  
 Lo stesso elemento [Application](../../../docs/framework/net-native/application-element-net-native.md) e gli elementi figlio degli elementi [Library](../../../docs/framework/net-native/library-element-net-native.md) e [Application](../../../docs/framework/net-native/application-element-net-native.md) esprimono criteri; vale a dire che definiscono il modo in cui un'applicazione può applicare reflection a un elemento del programma.  Il tipo di criterio è definito da un attributo dell'elemento \(ad esempio, `Serialize`\).  Il valore di criterio è definito dal valore dell'attributo \(ad esempio, `Serialize="Required"`\).  
  
 Qualsiasi criterio specificato da un attributo di un elemento si applica a tutti gli elementi figlio che non specificano un valore per tale criterio.  Ad esempio, se un criterio viene specificato da un elemento [Type](../../../docs/framework/net-native/type-element-net-native.md), tale criterio si applica a tutti i tipi e membri contenuti per i quali non è stato esplicitamente specificato un criterio.  
  
 Il criterio che può essere espresso dagli elementi [Application](../../../docs/framework/net-native/application-element-net-native.md), [Assembly](../../../docs/framework/net-native/assembly-element-net-native.md), [AttributeImplies](../../../docs/framework/net-native/attributeimplies-element-net-native.md), [Namespace](../../../docs/framework/net-native/namespace-element-net-native.md), [Subtypes](../../../docs/framework/net-native/subtypes-element-net-native.md) e [Type](../../../docs/framework/net-native/type-element-net-native.md) differisce dal criterio che può essere espresso per i singoli membri \(dagli elementi [Method](../../../docs/framework/net-native/method-element-net-native.md), [Property](../../../docs/framework/net-native/property-element-net-native.md), [Field](../../../docs/framework/net-native/field-element-net-native.md) ed [Event](../../../docs/framework/net-native/event-element-net-native.md)\).  
  
### Specifica di criteri per assembly, spazi dei nomi e tipi  
 Gli elementi [Application](../../../docs/framework/net-native/application-element-net-native.md), [Assembly](../../../docs/framework/net-native/assembly-element-net-native.md), [AttributeImplies](../../../docs/framework/net-native/attributeimplies-element-net-native.md), [Namespace](../../../docs/framework/net-native/namespace-element-net-native.md), [Subtypes](../../../docs/framework/net-native/subtypes-element-net-native.md) e [Type](../../../docs/framework/net-native/type-element-net-native.md) supportano i seguenti tipi di criteri:  
  
-   `Activate`.  Controlla l'accesso in fase di esecuzione ai costruttori per abilitare l'attivazione di istanze.  
  
-   `Browse`.  Controlla le query per le informazioni sugli elementi di programma, ma non abilita l'accesso in fase di esecuzione.  
  
-   `Dynamic`.  Controlla l'accesso in fase di esecuzione a tutti i membri dei tipi, inclusi costruttori, metodi, campi, proprietà ed eventi, per abilitare la programmazione dinamica.  
  
-   `Serialize`.  Controlla l'accesso in fase di esecuzione ai costruttori, ai campi e alle proprietà per abilitare la serializzazione e la deserializzazione delle istanze del tipo da parte di librerie di terze parti, ad esempio il serializzatore JSON di Newtonsoft.  
  
-   `DataContractSerializer`.  Controlla i criteri per la serializzazione che usano la classe <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName>.  
  
-   `DataContractJsonSerializer`.  Controlla i criteri per la serializzazione JSON che usano la classe <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName>.  
  
-   `XmlSerializer`.  Controlla i criteri per la serializzazione XML che usano la classe <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName>.  
  
-   `MarshalObject`.  Criteri di controlli per il marshalling dei tipi di riferimento per WinRT e COM.  
  
-   `MarshalDelegate`.  Controlla i criteri per il marshalling dei tipi delegati come puntatori a funzioni al codice nativo.  
  
-   `MarshalStructure` .  Controlla i criteri per il marshalling delle strutture al codice nativo.  
  
 Le impostazioni associate a questi tipi di criteri sono:  
  
-   `All`.  Attivare il criterio per tutti i tipi e membri che la catena di strumenti non riesce a rimuovere.  
  
-   `Auto`.  Usare il comportamento predefinito  \(non specificare un criterio è equivalente a impostare tale criterio su `Auto` a meno che tale criterio sia sottoposto a override, ad esempio da un elemento padre\).  
  
-   `Excluded`.  Disattivare il criterio per l'elemento di programma.  
  
-   `Public`.  Attivare i criteri per i tipi o i membri pubblici, a meno che la catena di strumenti non determini che il tipo o il membro non è necessario e lo rimuova  \(in quest'ultimo caso, è necessario usare `Required Public` per garantire che il membro venga mantenuto e abbia funzionalità di reflection.\)  
  
-   `PublicAndInternal`.  Attivare il criterio per i tipi o membri pubblici e interni se la catena di strumenti non li rimuove.  
  
-   `Required Public`.  Richiedere che la catena di strumenti mantenga i tipi e i membri pubblici, indipendentemente dal fatto che vengano usati o no, e attivare i relativi criteri.  
  
-   `Required PublicAndInternal`.  Richiedere che la catena di strumenti mantenga i tipi e i membri pubblici e interni, indipendentemente dal fatto che vengano usati o no, e attivare i relativi criteri.  
  
-   `Required All`.  Richiedere che la catena di strumenti mantenga tutti i tipi e i membri, indipendentemente dal fatto che vengano usati o no, e attivare i relativi criteri.  
  
 Il seguente file di direttive di runtime, ad esempio, definisce i criteri per tutti i tipi e membri nell'assembly DataClasses.dll.  Consente la reflection per la serializzazione di tutte le proprietà pubbliche, consente di cercare tutti i tipi e membri del tipo, consente l'attivazione per tutti i tipi \(a causa dell'attributo `Dynamic`\) e abilita la reflection per tutti i tipi e membri pubblici.  
  
```  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Assembly Name="DataClasses" Serialize="Required Public"   
                Browse="All" Activate="PublicAndInternal"   
                Dynamic="Public"  />  
   </Application>  
   <Library Name="UtilityLibrary">  
     <!-- Child elements go here -->    
   </Library>  
</Directives>  
  
```  
  
### Specifica di criteri per i membri  
 Gli elementi [Property](../../../docs/framework/net-native/property-element-net-native.md) e [Field](../../../docs/framework/net-native/field-element-net-native.md) supportano i seguenti tipi di criteri:  
  
-   `Browse`: controlla le query per le informazioni su questo membro, ma non abilita l'accesso in fase di esecuzione.  
  
-   `Dynamic`: controlla l'accesso in fase di esecuzione a tutti i membri dei tipi, inclusi costruttori, metodi, campi, proprietà ed eventi, per abilitare la programmazione dinamica.  Controlla anche la ricerca di informazioni sul tipo contenitore.  
  
-   `Serialize`: controlla l'accesso in fase di esecuzione al membro per abilitare istanze di tipi da serializzare e deserializzare da parte di librerie quali il serializzatore JSON di Newtonsoft.  Questi criteri possono essere applicati a costruttori, campi e proprietà.  
  
 Gli elementi [Method](../../../docs/framework/net-native/method-element-net-native.md) ed [Event](../../../docs/framework/net-native/event-element-net-native.md) supportano i seguenti tipi di criteri:  
  
-   `Browse`: controlla le query per le informazioni su questo membro, ma non abilita l'accesso in fase di esecuzione.  
  
-   `Dynamic`: controlla l'accesso in fase di esecuzione a tutti i membri dei tipi, inclusi costruttori, metodi, campi, proprietà ed eventi, per abilitare la programmazione dinamica.  Controlla anche la ricerca di informazioni sul tipo contenitore.  
  
 Le impostazioni associate a questi tipi di criteri sono:  
  
-   `Auto`: usare il comportamento predefinito  \(non specificare un criterio equivale a impostare tale criterio su `Auto` a meno che un elemento esegua l'override\).  
  
-   `Excluded`: non includere mai i metadati per il membro.  
  
-   `Included`: abilitare il criterio se il tipo padre è presente nell'output.  
  
-   `Required`: richiedere che la catena di strumenti conservi questo membro anche se sembra non essere in uso e abilitare i relativi criteri.  
  
## Semantica dei file di runtime direttive  
 È possibile definire criteri contemporaneamente per gli elementi di livello più alto e più basso.  Ad esempio, è possibile definire dei criteri per un assembly e per alcuni dei tipi di contenuti in tale assembly.  Se non è rappresentato un particolare elemento di livello inferiore, esso eredita i criteri del padre.  Ad esempio, se è presente un elemento `Assembly`, ma gli elementi `Type` sono assenti, il criterio specificato nell'elemento `Assembly` viene applicato a ciascun tipo nell'assembly.  Più elementi possono anche applicare criteri allo stesso elemento di programma.  Ad esempio, elementi [Assembly](../../../docs/framework/net-native/assembly-element-net-native.md) separati potrebbero definire lo stesso elemento di criterio per lo stesso assembly in modo diverso.  Le sezioni seguenti spiegano come risolvere il criterio per un determinato tipo in questi casi.  
  
 Un elemento [Type](../../../docs/framework/net-native/type-element-net-native.md) o [Method](../../../docs/framework/net-native/method-element-net-native.md) di un tipo o metodo generico applica i relativi criteri a tutte le istanze che non hanno un proprio criterio.  Ad esempio, un elemento `Type` che specifica i criteri per <xref:System.Collections.Generic.List%601> si applica a tutte le istanze costruite di tale tipo generico, a meno che non venga eseguito l'override per un particolare tipo generico costruito \(come `List<Int32>`\) da un elemento `TypeInstantiation`.  In caso contrario, gli elementi definiscono i criteri per l'elemento di programma denominato.  
  
 Quando un elemento è ambiguo, il motore ricerca corrispondenze e, se ne trova di esatte, le usa.  Se trova più corrispondenze, si riceverà un avviso o un errore.  
  
### Se due direttive applicano criteri allo stesso elemento di programma  
 Se due elementi in diversi file di direttive di runtime provano a impostare lo stesso tipo di criteri per lo stesso elemento di programma \(ad esempio un tipo o assembly\) su valori diversi, il conflitto viene risolto come segue:  
  
1.  Se l'elemento `Excluded` è presente, ha la precedenza.  
  
2.  `Required` ha la precedenza su non `Required`.  
  
3.  `All` ha la precedenza su `PublicAndInternal`, che a sua volta ha la precedenza su `Public`.  
  
4.  Qualsiasi impostazione esplicita ha la precedenza su `Auto`.  
  
 Ad esempio, se un singolo progetto include i due file di direttive di runtime seguenti, i criteri di serializzazione per DataClasses.dll vengono impostati su `Required Public` e `All`.  In questo caso, il criterio di serializzazione sarebbe risolto come `Required All`.  
  
```  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Assembly Name="DataClasses" Serialize="Required Public"/>  
   </Application>  
   <Library Name="DataClasses">  
      <!-- any other elements -->  
   </Library>  
</Directives>  
  
```  
  
```  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Assembly Name="DataClasses" Serialize="All" />  
   </Application>  
   <Library Name="DataClasses">  
      <!-- any other elements -->  
   </Library>  
</Directives>  
  
```  
  
 Tuttavia, se due direttive in un unico file di direttive di runtime prova a impostare lo stesso tipo di criteri per l'elemento del programma stesso, lo strumento di definizione di schema XML visualizza un messaggio di errore.  
  
### Se gli elementi figlio e padre applicano lo stesso tipo di criteri  
 Gli elementi figlio eseguono l'override dei relativi elementi padre, inclusa l'impostazione `Excluded`.  L'override è il motivo principale per cui è preferibile specificare `Auto`.  
  
 Nell'esempio seguente, l'impostazione dei criteri di serializzazione per tutto quanto presente in `DataClasses` ma assente in `DataClasses.ViewModels` corrisponderebbe a `Required Public`, e tutto quanto presente sia in `DataClasses` sia in `DataClasses.ViewModels` corrisponderebbe a `All`.  
  
```  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Assembly Name="DataClasses" Serialize="Required Public" >  
         <Namespace Name="DataClasses.ViewModels" Seralize="All" />  
      </Assembly>  
   </Appliction>  
   <Library Name="DataClasses">  
      <!-- any other elements -->  
   </Library>  
</Directives>  
  
```  
  
### Se i generics aperti e gli elementi di un'istanza applicano lo stesso tipo di criteri  
 Nell'esempio seguente, a `Dictionary<int,int>` viene assegnato il criterio `Browse` solo se il motore ha un motivo differente per assegnare il criterio `Browse` \(che altrimenti sarebbe il comportamento predefinito\). Per qualsiasi altra istanza di <xref:System.Collections.Generic.Dictionary%602> sarà possibile esplorare tutti i membri.  
  
```  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Assembly Name="DataClasses" Serialize="Required Public" >  
         <Namespace Name="DataClasses.ViewModels" Seralize="All" />  
      </Assembly>  
      <Namespace Name="DataClasses.Generics" />  
      <Type Name="Dictionary" Browse="All" />  
      <TypeInstantiation Name="Dictionary"   
                         Arguments="System.Int32,System.Int32" Browse="Auto" />  
   </Application>  
   <Library Name="DataClasses">  
      <!-- any other elements -->  
   </Library>  
</Directives>  
  
```  
  
### Come vengono dedotti i criteri  
 Ogni tipo di criteri ha un diverso insieme di regole che determinano in che modo la presenza di tale tipo di criterio ha effetto su altri costrutti.  
  
#### Effetto del criterio Browse  
 L'applicazione del criterio `Browse` a un tipo implica le seguenti modifiche:  
  
-   Il tipo di base del tipo viene contrassegnato con il criterio `Browse`.  
  
-   Se il tipo è un generico istanziato, la versione priva di istanze del tipo è contrassegnata con il criterio `Browse`.  
  
-   Se il tipo è un delegato, il metodo `Invoke` del tipo è contrassegnato con il criterio `Dynamic`.  
  
-   Ciascuna interfaccia del tipo viene contrassegnata con il criterio `Browse`.  
  
-   Il tipo di ciascun attributo applicato al tipo è contrassegnato con il criterio `Browse`.  
  
-   Se il tipo è generico, ogni tipo di vincolo è contrassegnato con il criterio `Browse`.  
  
-   Se il tipo è generico, i tipi su cui viene creata un'istanza del tipo sono contrassegnati con il criterio `Browse`.  
  
 L'applicazione del criterio `Browse` a un metodo implica le seguenti modifiche:  
  
-   Ogni tipo di parametro del metodo è contrassegnato con il criterio `Browse`.  
  
-   Il tipo restituito del metodo è contrassegnato con il criterio `Browse`.  
  
-   Il tipo contenitore del metodo è contrassegnato con il criterio `Browse`.  
  
-   Se il metodo è un metodo generico istanziato, il metodo generico privo di istanze è contrassegnato con il criterio `Browse`.  
  
-   Il tipo di ciascun attributo applicato al metodo è contrassegnato con il criterio `Browse`.  
  
-   Se il metodo è generico, ogni tipo di vincolo è contrassegnato con il criterio `Browse`.  
  
-   Se il metodo è generico, i tipi su cui viene creata un'istanza del metodo sono contrassegnati con il criterio `Browse`.  
  
 L'applicazione del criterio `Browse` a un campo implica le seguenti modifiche:  
  
-   Il tipo di ciascun attributo applicato al campo è contrassegnato con il criterio `Browse`.  
  
-   Il tipo del campo viene contrassegnato con il criterio `Browse`.  
  
-   Il tipo al quale appartiene il campo viene contrassegnato con il criterio `Browse`.  
  
#### Effetto dei criteri Dynamic  
 L'applicazione del criterio `Dynamic` a un tipo implica le seguenti modifiche:  
  
-   Il tipo di base del tipo viene contrassegnato con il criterio `Dynamic`.  
  
-   Se il tipo è un generico istanziato, la versione priva di istanze del tipo è contrassegnata con il criterio `Dynamic`.  
  
-   Se il tipo è un delegato, il metodo `Invoke` del tipo è contrassegnato con il criterio `Dynamic`.  
  
-   Ciascuna interfaccia del tipo viene contrassegnata con il criterio `Browse`.  
  
-   Il tipo di ciascun attributo applicato al tipo è contrassegnato con il criterio `Browse`.  
  
-   Se il tipo è generico, ogni tipo di vincolo è contrassegnato con il criterio `Browse`.  
  
-   Se il tipo è generico, i tipi su cui viene creata un'istanza del tipo sono contrassegnati con il criterio `Browse`.  
  
 L'applicazione del criterio `Dynamic` a un metodo implica le seguenti modifiche:  
  
-   Ogni tipo di parametro del metodo è contrassegnato con il criterio `Browse`.  
  
-   Il tipo restituito del metodo è contrassegnato con il criterio `Dynamic`.  
  
-   Il tipo contenitore del metodo è contrassegnato con il criterio `Dynamic`.  
  
-   Se il metodo è un metodo generico istanziato, il metodo generico privo di istanze è contrassegnato con il criterio `Browse`.  
  
-   Il tipo di ciascun attributo applicato al metodo è contrassegnato con il criterio `Browse`.  
  
-   Se il metodo è generico, ogni tipo di vincolo è contrassegnato con il criterio `Browse`.  
  
-   Se il metodo è generico, i tipi su cui viene creata un'istanza del metodo sono contrassegnati con il criterio `Browse`.  
  
-   Il metodo può essere richiamato da `MethodInfo.Invoke` e la creazione del delegato è resa possibile da <xref:System.Reflection.MethodInfo.CreateDelegate%2A?displayProperty=fullName>.  
  
 L'applicazione del criterio `Dynamic` a un campo implica le seguenti modifiche:  
  
-   Il tipo di ciascun attributo applicato al campo è contrassegnato con il criterio `Browse`.  
  
-   Il tipo del campo viene contrassegnato con il criterio `Dynamic`.  
  
-   Il tipo al quale appartiene il campo viene contrassegnato con il criterio `Dynamic`.  
  
#### Effetto del criterio Activation  
 L'applicazione del criterio Activation a un tipo implica le seguenti modifiche:  
  
-   Se il tipo è un generico istanziato, la versione priva di istanze del tipo è contrassegnata con il criterio `Browse`.  
  
-   Se il tipo è un delegato, il metodo `Invoke` del tipo è contrassegnato con il criterio `Dynamic`.  
  
-   I costruttori del tipo vengono contrassegnati con il criterio `Activation`.  
  
 L'applicazione del criterio `Activation` a un metodo implica le seguenti modifiche:  
  
-   Il costruttore può essere richiamato dai metodi <xref:System.Reflection.ConstructorInfo.Invoke%2A?displayProperty=fullName> e <xref:System.Activator.CreateInstance%2A?displayProperty=fullName>.  Per i metodi, il criterio `Activation` influisce solo sui costruttori.  
  
 L'applicazione del criterio `Activation` a un campo non ha alcun effetto.  
  
#### Effetto del criterio Serialize  
 Il criterio `Serialize` consente l'utilizzo dei serializzatori basati su reflection più comuni.  Tuttavia, poiché gli schemi di accesso alla reflection esatti dei serializzatori non Microsoft non sono noti a Microsoft, questo criterio potrebbe non essere completamente efficace.  
  
 L'applicazione del criterio `Serialize` a un tipo implica le seguenti modifiche:  
  
-   Il tipo di base del tipo viene contrassegnato con il criterio `Serialize`.  
  
-   Se il tipo è un generico istanziato, la versione priva di istanze del tipo è contrassegnata con il criterio `Browse`.  
  
-   Se il tipo è un delegato, il metodo `Invoke` del tipo è contrassegnato con il criterio `Dynamic`.  
  
-   Se il tipo è un'enumerazione, una matrice del tipo è contrassegnata con il criterio `Serialize`.  
  
-   Se il tipo implementa <xref:System.Collections.Generic.IEnumerable%601>, `T` viene contrassegnato con il criterio `Serialize`.  
  
-   Se il tipo è <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.Generic.IList%601>, <xref:System.Collections.Generic.ICollection%601>, <xref:System.Collections.Generic.IReadOnlyCollection%601> o <xref:System.Collections.Generic.IReadOnlyList%601>, `T[]` e <xref:System.Collections.Generic.List%601> vengono contrassegnati con il criterio `Serialize`, ma nessuno membro del tipo di interfaccia viene contrassegnato con il criterio `Serialize`.  
  
-   Se il tipo è <xref:System.Collections.Generic.List%601>, nessun membro del tipo viene contrassegnato con il criterio `Serialize`.  
  
-   Se il tipo è <xref:System.Collections.Generic.IDictionary%602>, <xref:System.Collections.Generic.Dictionary%602> viene contrassegnato con il criterio `Serialize`,  ma nessun membro del tipo viene contrassegnato con il criterio `Serialize`.  
  
-   Se il tipo è <xref:System.Collections.Generic.Dictionary%602>, nessun membro del tipo viene contrassegnato con il criterio `Serialize`.  
  
-   Se il tipo implementa <xref:System.Collections.Generic.IDictionary%602>, `TKey` e `TValue` vengono contrassegnati con il criterio `Serialize`.  
  
-   Ogni costruttore, ogni funzione di accesso della proprietà e ogni campo è contrassegnato con il criterio `Serialize`.  
  
 L'applicazione del criterio `Serialize` a un metodo implica le seguenti modifiche:  
  
-   Il tipo contenitore è contrassegnato con il criterio `Serialize`.  
  
-   Il tipo restituito del metodo è contrassegnato con il criterio `Serialize`.  
  
 L'applicazione del criterio `Serialize` a un campo implica le seguenti modifiche:  
  
-   Il tipo contenitore è contrassegnato con il criterio `Serialize`.  
  
-   Il tipo del campo viene contrassegnato con il criterio `Serialize`.  
  
#### Effetto dei criteri XmlSerializer, DataContractSerializer e DataContractJsonSerialier  
 A differenza del criterio `Serialize`, destinato ai serializzatori basati sulla reflection, i criteri `XmlSerializer`, `DataContractSerializer` e `DataContractJsonSerializer` sono usati per abilitare un set di serializzatori noti alla catena di strumenti [!INCLUDE[net_native](../../../includes/net-native-md.md)].  Questi serializzatori non vengono implementati tramite reflection, ma l'insieme di tipi che possono essere serializzati in fase di esecuzione è determinato in modo simile come tipi soggetti a reflection.  
  
 L'applicazione di uno di questi criteri a un tipo consente di serializzare il tipo con il serializzatore corrispondente.  Inoltre, eventuali tipi che il motore di serializzazione determina come serializzabili saranno indicati come tali.  
  
 Questi criteri non hanno alcun effetto sui metodi o campi.  
  
 Per altre informazioni, vedere la sezione "Differenze nei serializzatori" in [Migrazione dell'app di Windows Store a .NET Native](../../../docs/framework/net-native/migrating-your-windows-store-app-to-net-native.md).  
  
## Vedere anche  
 [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [Reflection e .NET Native](../../../docs/framework/net-native/reflection-and-net-native.md)