---
title: "Procedura: importare asserzioni di criteri personalizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f41d787-accb-4a10-bfc6-a807671d1581
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: importare asserzioni di criteri personalizzati
Le asserzioni di criteri descrivono le funzionalità e i requisiti di un endpoint del servizio.  Le applicazioni client possono utilizzare asserzioni di criteri nei metadati del servizio per configurare l'associazione del client o per personalizzare il contratto di servizio per un endpoint del servizio.  
  
 Asserzioni di criteri personalizzate vengono importate implementando il <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=fullName> interfaccia e passando l'oggetto al sistema di metadati o registrando l'implementazione del tipo nel file di configurazione dell'applicazione.  Le implementazioni di <xref:System.ServiceModel.Description.IPolicyImportExtension> interfaccia deve fornire un costruttore predefinito.  
  
### <a name="to-import-custom-policy-assertions"></a>Per importare asserzioni di criteri personalizzati  
  
1.  Implementare il <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=fullName> interfaccia in una classe. Vedere le procedure seguenti.  
  
2.  Inserire l'unità di importazione dei criteri personalizzati tramite uno dei modi seguenti:  
  
3.  Utilizzando un file di configurazione. Vedere le procedure seguenti.  
  
4.  Utilizzando un file di configurazione con [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md). Vedere le procedure seguenti.  
  
5.  Inserendo a livello di programmazione l'unità di importazione dei criteri. Vedere le procedure seguenti.  
  
### <a name="to-implement-the-systemservicemodeldescriptionipolicyimportextension-interface-on-any-class"></a>Per implementare l'interfaccia System.ServiceModel.Description.IPolicyImportExtension in qualsiasi classe  
  
1.  Nel <xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=fullName> (metodo), per ogni oggetto criterio a cui si è interessati, individuare le asserzioni di criteri che si desidera importare chiamando il metodo appropriato (in base all'ambito dell'asserzione desiderata) nel <xref:System.ServiceModel.Description.PolicyConversionContext?displayProperty=fullName> oggetto passato al metodo. Esempio di codice seguente viene illustrato come utilizzare il <xref:System.ServiceModel.Description.PolicyAssertionCollection.Remove%2A?displayProperty=fullName> metodo per individuare l'asserzione di criteri personalizzata e rimuoverla dalla raccolta in un unico passaggio. Se si utilizza il metodo di rimozione per individuare e rimuovere l'asserzione, non è necessario eseguire il passaggio 4.  
  
     [!code-csharp[CustomPolicySample#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/policyimporter.cs#9)]
     [!code-vb[CustomPolicySample#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/policyimporter.vb#9)]  
  
2.  Elaborare le asserzioni dei criteri. Si noti che il sistema del criterio non normalizza i criteri annidati e `wsp:optional`. È necessario elaborare questi costrutti nell'implementazione di un'estensione di importazione del criterio.  
  
3.  Eseguire la personalizzazione dell'associazione o del contratto che supporta la funzionalità o il requisito specificato dall'asserzione del criterio. In genere, le asserzioni indicano che un'associazione richiede una particolare configurazione o uno specifico elemento di associazione. Apportare queste modifiche accedendo il <xref:System.ServiceModel.Description.PolicyConversionContext.BindingElements%2A?displayProperty=fullName> proprietà. Le altre asserzioni richiedono che si modifichi il contratto.  È possibile accedere e modificare il contratto utilizzando il <xref:System.ServiceModel.Description.PolicyConversionContext.Contract%2A?displayProperty=fullName> proprietà.  Si noti che l'unità di importazione dei criteri può venire chiamata più volte per la stessa associazione e per lo stesso contratto, ma per alternative criteri diverse se l'importazione di un'alternativa criterio non riesce. Il codice deve adattarsi a questo comportamento.  
  
4.  Rimuovere l'asserzione di criteri personalizzata dalla raccolta di asserzioni. Se l'asserzione non viene rimossa, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] presuppone che l'importazione del criterio non sia stata completata correttamente e non importa l'associazione associata. Se è stata utilizzata la <xref:System.ServiceModel.Description.PolicyAssertionCollection.Remove%2A?displayProperty=fullName> metodo per individuare l'asserzione di criteri personalizzata e rimuoverla dalla raccolta in un passaggio non è necessario eseguire questo passaggio.  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-using-a-configuration-file"></a>Per inserire l'unità di importazione di criteri personalizzata nel sistema di metadati utilizzando un file di configurazione  
  
1.  Aggiungere il tipo di unità di importazione di `<extensions>` elemento all'interno di [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/policyimporters.md) elemento nel file di configurazione client.  
  
     [!code[CustomPolicySample#7](../../../../samples/snippets/common/VS_Snippets_CFX/custompolicysample/common/client.exe.config#7)]
     [!code-csharp[CustomPolicySample#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/client.exe.config#7)]
     [!code-vb[CustomPolicySample#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/client.exe.config#7)]  
  
2.  Nell'applicazione client, utilizzare il <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=fullName> o <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName> per risolvere i metadati e l'utilità di importazione viene richiamata automaticamente.  
  
     [!code-csharp[CustomPolicySample#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/client.cs#10)]
     [!code-vb[CustomPolicySample#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/client.vb#10)]  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-using-svcutilexe"></a>Per inserire l'unità di importazione di criteri personalizzata nel sistema di metadati utilizzando Svcutil.exe  
  
1.  Aggiungere il tipo di unità di importazione di `<extensions>` elemento all'interno di [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/policyimporters.md) elemento nel file di configurazione Svcutil.exe.config. È anche possibile puntare a Svcutil.exe per caricare tipi di unità di importazione di criteri registrati in un file di configurazione diverso, utilizzando l'opzione `/svcutilConfig`.  
  
2.  Utilizzare [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per importare i metadati e l'utilità di importazione viene richiamata automaticamente.  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-programmatically"></a>Per inserire l'unità di importazione di criteri personalizzata nel sistema di metadati a livello di programmazione  
  
1.  Aggiungere l'unità di importazione per il <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A?displayProperty=fullName> proprietà (ad esempio, se si utilizza il <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName>) prima di importare i metadati.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=fullName>   
 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName>   
 <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=fullName>   
 [Estensione del sistema di metadati](../../../../docs/framework/wcf/extending/extending-the-metadata-system.md)