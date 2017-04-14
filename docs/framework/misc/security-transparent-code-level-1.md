---
title: "Security-Transparent Code, Level 1 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "transparent"
  - "SecurityTreatAsSafeAttribute"
  - "SecurityTransparentAttribute"
  - "SecurityCriticalAttribute"
  - "security-transparent code"
  - "security [.NET Framework], security-transparent code"
ms.assetid: 5fd8f46d-3961-46a7-84af-2eb1f48e75cf
caps.latest.revision: 32
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 30
---
# Security-Transparent Code, Level 1
La trasparenza consente agli sviluppatori di scrivere in modo più sicuro le librerie .NET Framework che espongono funzionalità a codice parzialmente attendibile. La trasparenza di livello 1 è stata introdotta in .NET Framework versione 2.0 ed è stata usata principalmente solo all'interno di Microsoft. A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], è possibile usare la [trasparenza di livello 2](../../../docs/framework/misc/security-transparent-code-level-2.md). La trasparenza di livello 1 è tuttavia stata mantenuta per consentire di identificare il codice legacy che deve essere eseguito con regole di sicurezza meno recenti.  
  
> [!IMPORTANT]
>  È necessario specificare la trasparenza di livello 1 solo per ragioni di compatibilità, ovvero specificare il livello 1 solo per codice sviluppato con .NET Framework 3.5 o versioni precedenti che usa <xref:System.Security.AllowPartiallyTrustedCallersAttribute> o non usa il modello di trasparenza. Usare ad esempio la trasparenza di livello 1 per assembly .NET Framework 2.0 che consentono l'uso di chiamate da chiamanti parzialmente attendibili \(APTCA\). Per il codice sviluppato per [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], usare sempre la trasparenza di livello 2.  
  
> [!CAUTION]
>  Sicurezza dall'accesso di codice e codice parzialmente attendibile  
>   
>  .NET Framework fornisce un meccanismo denominato sicurezza dall'accesso di codice, che consente di applicare vari livelli di attendibilità a codice diverso in esecuzione nella stessa applicazione.  La sicurezza dall'accesso di codice in .NET Framework non va usata come limite di sicurezza con codice parzialmente attendibile, in particolare con codice di origine sconosciuta. Non è consigliabile caricare ed eseguire codice di origine sconosciuta in assenza di misure di sicurezza alternative.  
>   
>  Questi criteri si applicano a tutte le versioni di .NET Framework, ma non alla versione di .NET Framework inclusa in Silverlight.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Modello di trasparenza di livello 1](#the_level_1_transparency_model)  
  
-   [Attributi di trasparenza](#transparency_attributes)  
  
-   [Esempi di trasparenza della sicurezza](#security_transparency_examples)  
  
<a name="the_level_1_transparency_model"></a>   
## Modello di trasparenza di livello 1  
 Quando si usa la trasparenza di livello 1, si usa un modello di sicurezza che suddivide il codice in metodi SecurityTransparent, SecuritySafeCritical e SecurityCritical.  
  
 È possibile contrassegnare un intero assembly, alcune classi di un assembly o alcuni metodi di una classe. Il codice SecurityTransparent non può elevare il livello di privilegi. Questa restrizione implica tre conseguenze:  
  
-   Il codice SecurityTransparent non può eseguire azioni <xref:System.Security.Permissions.SecurityAction>.  
  
-   Tutte le richieste di collegamento soddisfatte dal codice SecurityTransparent diventano richieste complete.  
  
-   Il codice unsafe \(non verificabile\) che deve essere eseguito nel codice SecurityTransparent provoca una richiesta completa per l'autorizzazione di sicurezza <xref:System.Security.Permissions.SecurityPermissionFlag>.  
  
 Queste regole vengono applicate durante l'esecuzione da Common Language Runtime \(CLR\). Il codice SecurityTransparent passa tutti i requisiti di sicurezza del codice richiamato ai relativi chiamanti. Le richieste trasmesse con il codice SecurityTransparent non possono elevare il livello di privilegi. Se un'applicazione con attendibilità bassa chiama il codice SecurityTransparent e provoca una richiesta di un livello di privilegi più alto, la richiesta verrà trasferita di nuovo al codice con attendibilità bassa generando un errore. Il codice SecurityTransparent non può arrestare la richiesta perché non può eseguire azioni di asserzione. Se lo stesso codice SecurityTransparent viene chiamato dal codice con attendibilità totale, la richiesta avrà esito positivo.  
  
 SecurityCritical rappresenta l'opposto di SecurityTransparent. Il codice SecurityCritical viene eseguito con attendibilità totale e può eseguire tutte le operazioni con privilegi. Il codice SecuritySafeCritical è codice con privilegi che è stato sottoposto a un controllo di sicurezza completo per verificare che non consenta ai chiamanti parzialmente attendibili di usare risorse per le quali non dispongono di autorizzazioni di accesso.  
  
 È necessario applicare la trasparenza in modo esplicito. La maggior parte del codice che gestisce la logica e la modifica dei dati può in genere essere contrassegnata come SecurityTransparent, mentre una quantità minore di codice che esegue le elevazioni dei privilegi viene contrassegnata come SecurityCritical o SecuritySafeCritical.  
  
> [!IMPORTANT]
>  La trasparenza di livello 1 è limitata all'ambito degli assembly e non viene applicata tra assembly. La trasparenza di livello 1 veniva usata principalmente da Microsoft per i controlli di sicurezza. È possibile accedere ai tipi e ai membri SecurityCritical all'interno di un assembly di livello 1 dal codice SecurityTransparent di altri assembly. È importante eseguire richieste di collegamento per l'attendibilità totale in tutti i tipi e i membri SecurityCritical di livello 1. I tipi e i membri SecuritySafeCritical devono inoltre verificare che i chiamanti dispongano di autorizzazioni per le risorse protette a cui il tipo o il membro accede.  
  
 Per compatibilità con le versioni precedenti di .NET Framework, tutti i membri non annotati con attributi di trasparenza vengono considerati SecuritySafeCritical. Tutti i tipi non annotati vengono considerati Transparent. Non ci sono regole di analisi statica per convalidare la trasparenza. Potrebbe quindi essere necessario eseguire il debug degli errori di trasparenza in fase di esecuzione.  
  
<a name="transparency_attributes"></a>   
## Attributi di trasparenza  
 Nella tabella riportata di seguito vengono descritti i tre attributi da usare per annotare il codice per la trasparenza.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|<xref:System.Security.SecurityTransparentAttribute>|Consentito solo a livello di assembly. Identifica tutti i tipi e i membri nell'assembly come SecurityTransparent. L'assembly non può contenere codice SecurityCritical.|  
|<xref:System.Security.SecurityCriticalAttribute>|Se usato a livello di assembly, senza la proprietà <xref:System.Security.SecurityCriticalAttribute.Scope%2A>, identifica tutto il codice nell'assembly come SecurityTransparent per impostazione predefinita, ma indica che l'assembly può contenere codice SecurityCritical.<br /><br /> Se usato a livello di classe, identifica la classe o il metodo come SecurityCritical, ma non i membri della classe. Per impostare tutti i membri come SecurityCritical, impostare la proprietà <xref:System.Security.SecurityCriticalAttribute.Scope%2A> su <xref:System.Security.SecurityCriticalScope>.<br /><br /> Se usato a livello di membro, l'attributo si applica solo a tale membro.<br /><br /> La classe o il membro identificato come SecurityCritical può eseguire le elevazioni dei privilegi. **Important:**  Con la trasparenza di livello 1, i tipi e i membri SecurityCritical vengono trattati come SecuritySafeCritical quando vengono chiamati dall'esterno dell'assembly. È necessario proteggere i tipi e i membri SecurityCritical con una richiesta di collegamento per l'attendibilità totale, per evitare l'elevazione dei privilegi non autorizzata.|  
|<xref:System.Security.SecuritySafeCriticalAttribute>|Identifica codice SecurityCritical a cui è possibile accedere da codice SecurityTransparent nell'assembly. In caso contrario, il codice SecurityTransparent non può accedere ai membri SecurityCritical interni o privati nello stesso assembly. Questa operazione influisce sul codice SecurityCritical con conseguenti possibili elevazioni dei privilegi impreviste. Il codice SecuritySafeCritical deve essere sottoposto a un controllo di sicurezza rigido. **Note:**  I tipi e i membri SecuritySafeCritical devono convalidare le autorizzazioni dei chiamanti per determinare se il chiamante dispone dell'autorità per accedere alle risorse protette.|  
  
 L'attributo <xref:System.Security.SecuritySafeCriticalAttribute> consente al codice SecurityTransparent di accedere ai membri SecurityCritical nello stesso assembly. Considerare il codice SecurityTransparent e il codice SecurityCritical come se si trovassero in due assembly distinti. Il codice SecurityTransparent non riesce a vedere i membri privati o interni del codice SecurityCritical. Inoltre, il codice SecurityCritical viene generalmente controllato per l'accesso all'interfaccia pubblica. Uno stato privato o interno non è normalmente accessibile all'esterno dell'assembly, quindi è consigliabile mantenere lo stato isolato. L'attributo <xref:System.Security.SecuritySafeCriticalAttribute> mantiene l'isolamento dello stato tra il codice SecurityTransparent e il codice SecurityCritical fornendo allo stesso tempo la possibilità di eseguire l'override dell'isolamento quando è necessario. Il codice SecurityTransparent non può accedere al codice SecurityCritical privato o interno, a meno che i membri non siano stati contrassegnati con <xref:System.Security.SecuritySafeCriticalAttribute>. Prima di applicare l'attributo <xref:System.Security.SecuritySafeCriticalAttribute>, controllare il membro come se fosse esposto pubblicamente.  
  
### Annotazione a livello di assembly  
 La tabella seguente descrive gli effetti dell'uso di attributi di sicurezza a livello di assembly.  
  
|Assembly \(attributo\)|Stato dell'assembly|  
|----------------------------|-------------------------|  
|Nessun attributo su un assembly parzialmente attendibile|Tutti i tipi e i membri sono Transparent.|  
|Nessun attributo su un assembly completamente attendibile \(nella Global Assembly Cache o identificato come attendibilità totale in `AppDomain`\)|Tutti i tipi sono Transparent e tutti i membri sono SecuritySafeCritical.|  
|`SecurityTransparent`|Tutti i tipi e i membri sono Transparent.|  
|`SecurityCritical(SecurityCriticalScope.Everything)`|Tutti i tipi e i membri sono SecurityCritical.|  
|`SecurityCritical`|Tutto il codice è Transparent per impostazione predefinita. I singoli tipi e membri possono tuttavia avere altri attributi.|  
  
<a name="security_transparency_examples"></a>   
## Esempi di trasparenza della sicurezza  
 Per usare le regole di trasparenza di .NET Framework 2.0 \(trasparenza di livello 1\), usare l'annotazione di assembly seguente:  
  
```  
[assembly: SecurityRules(SecurityRuleSet.Level1)]  
```  
  
 Se si vuole rendere trasparente un intero assembly per indicare che l'assembly non contiene codice critico e non eleva in alcun modo i privilegi, è possibile aggiungere in modo esplicito la trasparenza all'assembly con l'attributo seguente:  
  
```  
[assembly: SecurityTransparent]  
```  
  
 Se si vuole combinare codice critico e codice trasparente nello stesso assembly, contrassegnare l'assembly con l'attributo <xref:System.Security.SecurityCriticalAttribute> per indicare che l'assembly può contenere codice critico, come segue:  
  
```  
[assembly: SecurityCritical]  
```  
  
 Se si vogliono eseguire azioni SecurityCritical, contrassegnare in modo esplicito il codice che eseguirà l'azione critica con un altro attributo <xref:System.Security.SecurityCriticalAttribute>, come illustrato nell'esempio di codice seguente:  
  
```  
[assembly: SecurityCritical] Public class A { [SecurityCritical] private void Critical() { // critical } public int SomeProperty { get {/* transparent */ } set {/* transparent */ } } } public class B { internal string SomeOtherProperty { get { /* transparent */ } set { /* transparent */ } } }  
```  
  
 Il codice precedente è trasparente a eccezione del metodo Critical che è contrassegnato in modo esplicito come `Critical`. La trasparenza rappresenta l'impostazione predefinita, anche con l'attributo <xref:System.Security.SecurityCriticalAttribute> a livello di assembly.  
  
## Vedere anche  
 [Security\-Transparent Code, Level 2](../../../docs/framework/misc/security-transparent-code-level-2.md)   
 [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md)