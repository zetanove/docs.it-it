---
title: "Impostazione degli attributi dell&#39;assembly | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assembly [.NET Framework], attributi"
  - "associazione di assembly, attributi"
  - "manifesto assembly, attributi"
ms.assetid: 36a98a81-b5b5-4c19-912a-11f91eff7f4e
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Impostazione degli attributi dell&#39;assembly
Gli attributi dell'assembly sono valori che forniscono informazioni relative a un assembly. Tali attributi sono suddivisi nei seguenti gruppi di informazioni:  
  
-   Attributi relativi all'identità dell'assembly.  
  
-   Attributi informativi.  
  
-   Attributi relativi al manifesto dell'assembly.  
  
-   Attributi relativi al nome sicuro.  
  
## Attributi relativi all'identità dell'assembly  
 Tre attributi, insieme a un nome sicuro \(se disponibile\), consentono di determinare l'identità di un assembly: il nome, la versione e le impostazioni cultura. Il nome completo dell'assembly è costituito da questi attributi, che risultano necessari per creare riferimenti all'assembly nel codice. È possibile usare gli attributi per impostare la versione e le impostazioni cultura di un assembly. Il valore relativo al nome viene impostato dal compilatore o da [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md) quando l'assembly viene creato ed è basato sul file contenente il manifesto dell'assembly.  
  
 Nella tabella seguente vengono descritti gli attributi relativi alla versione e alle impostazioni cultura.  
  
|Attributi relativi all'identità dell'assembly|Descrizione|  
|---------------------------------------------------|-----------------|  
|<xref:System.Reflection.AssemblyCultureAttribute>|Campo elenco in cui vengono indicate le impostazioni cultura supportate dall'assembly. È possibile specificare anche l'indipendenza dalle impostazioni cultura per l'assembly, indicando che nell'assembly sono presenti le risorse per le impostazioni cultura predefinite. **Note:**  Tutti gli assembly il cui attributo relativo alle impostazioni cultura non è impostato su null vengono considerati dal runtime come assembly satellite e sono soggetti alle regole di associazione degli assembly satellite. Per altre informazioni, vedere [Modalità di individuazione di assembly del runtime](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md).|  
|<xref:System.Reflection.AssemblyFlagsAttribute>|Valore che consente di impostare gli attributi relativi all'assembly, indicando ad esempio se è consentita l'esecuzione affiancata di più versioni.|  
|<xref:System.Reflection.AssemblyVersionAttribute>|Valore numerico in formato *principale*.*secondario*.*build*.*revisione* \(ad esempio, 2.4.0.0\). Questo valore viene usato da Common Language Runtime per eseguire operazioni di associazione in assembly con nome sicuro. **Note:**  Se l'attributo <xref:System.Reflection.AssemblyInformationalVersionAttribute> non viene applicato a un assembly, il numero di versione specificato dall'attributo <xref:System.Reflection.AssemblyVersionAttribute> viene usato dalle proprietà  <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=fullName>, <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=fullName> e <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=fullName>.|  
  
 Nel seguente esempio di codice viene mostrato come applicare a un assembly gli attributi relativi alla versione e alle impostazioni cultura.  
  
 [!code-cpp[AssemblyDelaySignAttribute#3](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cpp/source2.cpp#3)]
 [!code-csharp[AssemblyDelaySignAttribute#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cs/source2.cs#3)]
 [!code-vb[AssemblyDelaySignAttribute#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyDelaySignAttribute/vb/source2.vb#3)]  
  
## Attributi informativi  
 Gli attributi informativi consentono di fornire informazioni aggiuntive relative alla società o al prodotto per un assembly. Nella tabella seguente vengono descritti gli attributi informativi che è possibile applicare a un assembly.  
  
|Attributo informativo|Descrizione|  
|---------------------------|-----------------|  
|<xref:System.Reflection.AssemblyCompanyAttribute>|Valore stringa in cui viene specificato un nome di società.|  
|<xref:System.Reflection.AssemblyCopyrightAttribute>|Valore stringa in cui vengono specificate informazioni relative al copyright.|  
|<xref:System.Reflection.AssemblyFileVersionAttribute>|Valore stringa in cui viene specificato il numero di versione del file Win32. L'impostazione predefinita è solitamente la versione dell'assembly.|  
|<xref:System.Reflection.AssemblyInformationalVersionAttribute>|Valore stringa in cui vengono specificate informazioni relative alla versione non usate da Common Language Runtime, quale il numero di versione del prodotto completo. **Note:**  Se questo attributo viene applicato a un assembly, è possibile ottenere la stringa che specifica in fase di esecuzione tramite la proprietà <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=fullName>. La stringa viene usata anche nel percorso e nella chiave del Registro di sistema forniti dalle proprietà <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=fullName> e <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=fullName>.|  
|<xref:System.Reflection.AssemblyProductAttribute>|Valore stringa in cui vengono specificate informazioni relative al prodotto.|  
|<xref:System.Reflection.AssemblyTrademarkAttribute>|Valore stringa in cui vengono specificate informazioni relative al marchio registrato.|  
  
 È possibile visualizzare questi attributi nella pagina delle proprietà di Windows o sostituirli usando l'opzione del compilatore **\/win32res** per specificare un file di risorsa Win32 personalizzato.  
  
## Attributi relativi al manifesto dell'assembly  
 Gli attributi relativi al manifesto dell'assembly consentono di fornire informazioni nel manifesto dell'assembly, inclusi il titolo, la descrizione, l'alias predefinito e la configurazione. Nella tabella seguente vengono descritti gli attributi relativi al manifesto dell'assembly.  
  
|Attributo relativo al manifesto dell'assembly|Descrizione|  
|---------------------------------------------------|-----------------|  
|<xref:System.Reflection.AssemblyConfigurationAttribute>|Valore stringa che indica la configurazione dell'assembly, ad esempio finale o di debug. Questo valore non viene usato da Common Language Runtime.|  
|<xref:System.Reflection.AssemblyDefaultAliasAttribute>|Valore stringa in cui viene specificato l'alias predefinito che verrà usato dagli assembly contenenti riferimenti all'assembly corrente. Questo valore consente di fornire un nome descrittivo nel caso in cui il nome dell'assembly non sia descrittivo, ma corrisponda ad esempio a un valore GUID. È inoltre possibile usare questo valore come forma abbreviata del nome completo dell'assembly.|  
|<xref:System.Reflection.AssemblyDescriptionAttribute>|Valore stringa in cui viene specificata una breve descrizione che riassume la natura e lo scopo dell'assembly.|  
|<xref:System.Reflection.AssemblyTitleAttribute>|Valore stringa in cui viene specificato un nome descrittivo per l'assembly. È ad esempio possibile che il titolo di un assembly denominato comdlg sia Controllo della finestra di dialogo comune Microsoft.|  
  
## Attributi relativi al nome sicuro  
 Gli attributi relativi al nome sicuro consentono di impostare un nome sicuro per un assembly. Nella tabella seguente vengono descritti gli attributi relativi al nome sicuro.  
  
|Attributo relativo al nome sicuro|Descrizione|  
|---------------------------------------|-----------------|  
|<xref:System.Reflection.AssemblyDelaySignAttribute>|Valore booleano che indica che viene usato il ritardo della firma.|  
|<xref:System.Reflection.AssemblyKeyFileAttribute>|Valore stringa che indica il nome del file contenente la chiave pubblica \(se si usa il ritardo della firma\) o la chiave pubblica e privata passate come parametro al costruttore di questo attributo. Si noti che il nome del file è relativo al percorso del file di output \(il file EXE o DLL\), non al percorso del file di origine.|  
|<xref:System.Reflection.AssemblyKeyNameAttribute>|Indica il contenitore di chiave contenente la coppia di chiavi passata come parametro al costruttore dell'attributo.|  
  
 Nell'esempio di codice seguente vengono mostrati gli attributi da applicare quando si usa il ritardo della firma per creare un assembly con nome sicuro con un file di chiave pubblica denominato `myKey.snk`.  
  
 [!code-cpp[AssemblyDelaySignAttribute#4](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cpp/source2.cpp#4)]
 [!code-csharp[AssemblyDelaySignAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cs/source2.cs#4)]
 [!code-vb[AssemblyDelaySignAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyDelaySignAttribute/vb/source2.vb#4)]  
  
## Vedere anche  
 [Creazione degli assembly](../../../docs/framework/app-domains/create-assemblies.md)   
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)