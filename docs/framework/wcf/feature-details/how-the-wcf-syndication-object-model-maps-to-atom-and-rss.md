---
title: "Modalit&#224; di mapping del modello a oggetti di diffusione WCF ad Atom e RSS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0365eb37-98cc-4b13-80fb-f1e78847a748
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Modalit&#224; di mapping del modello a oggetti di diffusione WCF ad Atom e RSS
Quando si sviluppa un servizio di diffusione [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], vengono creati feed ed elementi utilizzando le classi seguenti:  
  
-   <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
-   <xref:System.ServiceModel.Syndication.TextSyndicationContent>  
  
-   <xref:System.ServiceModel.Syndication.UrlSyndicationContent>  
  
-   <xref:System.ServiceModel.Syndication.XmlSyndicationContent>  
  
 Un oggetto <xref:System.ServiceModel.Syndication.SyndicationFeed> può essere serializzato in qualsiasi formato di diffusione per il quale è definito un formattatore.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene fornito con due formattatori: <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> e <xref:System.ServiceModel.Syndication.Rss20FeedFormatter>.  
  
 Il modello a oggetti basato su <xref:System.ServiceModel.Syndication.SyndicationFeed> e <xref:System.ServiceModel.Syndication.SyndicationItem> è più strettamente conforme alla specifica Atom 1.0 che non alla specifica RSS 2.0.Ciò è dovuto al fatto che Atom 1.0 è una specifica più sostanziale e definisce elementi ambigui o che sono stati omessi dalla specifica RSS 2.0.Di conseguenza, numerosi elementi nel modello a oggetti di diffusione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non hanno rappresentazione diretta nella specifica RSS 2.0.Quando si serializzano oggetti <xref:System.ServiceModel.Syndication.SyndicationFeed> e <xref:System.ServiceModel.Syndication.SyndicationItem> in RSS 2.0, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente di serializzare gli elementi di dati specifici di Atom come elementi di estensione qualificati con lo spazio dei nomi conformi alla specifica Atom.Questa procedura può essere controllata con un parametro passato al costruttore <xref:System.ServiceModel.Syndication.Rss20FeedFormatter>.  
  
 Negli esempi di codice inclusi in questo argomento, per eseguire la serializzazione effettiva viene utilizzato uno dei due metodi illustrati qui.  
  
 `SerializeFeed` serializza un feed di diffusione.  
  
 [!code-csharp[SyndicationMapping#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#10)]
 [!code-vb[SyndicationMapping#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#10)]  
  
 `SerializeItem` serializza un elemento di diffusione.  
  
 [!code-csharp[SyndicationMapping#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#11)]
 [!code-vb[SyndicationMapping#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#11)]  
  
## SyndicationFeed  
 Nell'esempio di codice seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.SyndicationFeed> in Atom 1.0 e RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#0)]
 [!code-vb[SyndicationMapping#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#0)]  
  
 Nel codice XML seguente viene mostrato come serializzare <xref:System.ServiceModel.Syndication.SyndicationFeed> per il formato Atom 1.0.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<feed xml:lang="EN-US" xmlns="http://www.w3.org/2005/Atom">  
  <title type="text">My Feed Title</title>  
  <subtitle type="text">My Feed Description</subtitle>  
  <id>FeedID</id>  
  <rights type="text">Copyright 2007</rights>  
  <updated>2007-08-29T13:57:17-07:00</updated>  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <logo>http://server/image.jpg</logo>  
  <generator>Sample Code</generator>  
  <link rel="alternate" href="http://myfeeduri/" />  
  <entry>  
    <id>ItemID</id>  
    <title type="text">Item Title</title>  
    <summary type="text">Item Summary</summary>  
    <published>2007-08-29T00:00:00-07:00</published>  
    <updated>2007-08-29T13:57:17-07:00</updated>  
    <author>  
      <name>Jesper Aaberg</name>  
      <uri>http://Jesper/Aaberg</uri>  
      <email>Jesper@Aaberg.com</email>  
    </author>  
    <contributor>  
      <name>Lene Aaling</name>  
      <uri>http://Lene/Aaling</uri>  
      <email>Lene@Aaling.com</email>  
    </contributor>  
    <link rel="alternate" href="http://myitemuri/" />  
    <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
    <content type="text">Item Content</content>  
    <rights type="text">Copyright 2007</rights>  
    <source>  
      <title type="text">My Feed Title</title>  
      <subtitle type="text">My Feed Description</subtitle>  
      <id>FeedID</id>  
      <rights type="text">Copyright 2007</rights>  
      <updated>2007-08-29T13:57:17-07:00</updated>  
      <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
      <logo>http://server/image.jpg</logo>  
      <generator>Sample Code</generator>  
      <link rel="alternate" href="http://myfeeduri/" />  
    </source>  
  </entry>  
</feed>  
```  
  
 Nel codice XML seguente viene mostrato come serializzare <xref:System.ServiceModel.Syndication.SyndicationFeed> per il formato RSS 2.0.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<rss xmlns:a10="http://www.w3.org/2005/Atom" version="2.0">  
  <channel>  
    <title>My Feed Title</title>  
    <link>http://myfeeduri/</link>  
    <description>My Feed Description</description>  
    <language>EN-US</language>  
    <copyright>Copyright 2007</copyright>  
    <lastBuildDate>Wed, 29 Aug 2007 13:57:17 -0700</lastBuildDate>  
    <category domain="categoryScheme">categoryName</category>  
    <generator>Sample Code</generator>  
    <image>  
      <url>http://server/image.jpg</url>  
      <title>My Feed Title</title>  
      <link>http://myfeeduri/</link>  
    </image>  
    <a10:id>FeedID</a10:id>  
    <item>  
      <guid isPermaLink="false">ItemID</guid>  
      <link>http://myitemuri/</link>  
      <author>Jesper@Aaberg.com</author>  
      <category domain="categoryScheme">categoryName</category>  
      <title>Item Title</title>  
      <description>Item Summary</description>  
      <source>My Feed Title</source>  
      <pubDate>Wed, 29 Aug 2007 00:00:00 -0700</pubDate>  
      <a10:updated>2007-08-29T13:57:17-07:00</a10:updated>  
      <a10:rights type="text">Copyright 2007</a10:rights>  
      <a10:content type="text">Item Content</a10:content>  
      <a10:contributor>  
        <a10:name>Lene Aaling</a10:name>  
        <a10:uri>http://Lene/Aaling</a10:uri>  
        <a10:email>Lene@Aaling.com</a10:email>  
      </a10:contributor>  
    </item>  
  </channel>  
</rss>  
```  
  
## SyndicationItem  
 Nell'esempio di codice seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.SyndicationItem> per i formati Atom 1.0 e RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#1)]
 [!code-vb[SyndicationMapping#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#1)]  
  
 Nel codice XML seguente viene mostrato come serializzare <xref:System.ServiceModel.Syndication.SyndicationItem> per il formato Atom 1.0.  
  
```  
<entry xmlns="http://www.w3.org/2005/Atom">  
  <id>ItemID</id>  
  <title type="text">Item Title</title>  
  <summary type="text">Item Summary</summary>  
  <published>2007-08-29T00:00:00-07:00</published>  
  <updated>2007-08-29T14:07:09-07:00</updated>  
  <author>  
    <name>Jesper Aaberg</name>  
    <uri>http://Contoso/Aaberg</uri>  
    <email>Jesper.Aaberg@contoso.com</email>  
  </author>  
  <author>  
    <name>Syed Abbas</name>  
    <uri>http://Contoso/Abbas</uri>  
    <email>Syed.Abbas@contoso.com</email>  
  </author>  
  <contributor>  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
  <contributor>  
    <name>Kim Abercrombie</name>  
    <uri>http://Contoso/Abercrombie</uri>  
    <email>Kim.Abercrombie@contoso.com</email>  
  </contributor>  
  <link rel="alternate" href="http://myitemuri/" />  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <content type="text">Item Content</content>  
  <rights type="text">Copyright 2007</rights>  
  <source>  
    <title type="text">My Feed Title</title>  
    <subtitle type="text">My Feed Description</subtitle>  
    <link rel="alternate" href="http://myfeeduri/" />  
  </source>  
</entry>  
```  
  
 Nel codice XML seguente viene mostrato come serializzare <xref:System.ServiceModel.Syndication.SyndicationItem> per il formato RSS 2.0.  
  
```  
<item>  
  <guid isPermaLink="false">ItemID</guid>  
  <link>http://myitemuri/</link>  
  <author xmlns="http://www.w3.org/2005/Atom">  
    <name>Jesper Aaberg</name>  
    <uri>http://Jesper/Aaberg</uri>  
    <email>Jesper@Aaberg.com</email>  
  </author>  
  <author xmlns="http://www.w3.org/2005/Atom">  
    <name>Syed Abbas</name>  
    <uri>http://Contoso/Abbas</uri>  
    <email>Syed.Abbas@contoso.com</email>  
  </author>  
  <category domain="categoryScheme">categoryName</category>  
  <category domain="categoryScheme">categoryName</category>  
  <title>Item Title</title>  
  <description>Item Summary</description>  
  <source>My Feed Title</source>  
  <pubDate>Wed, 29 Aug 2007 00:00:00 -0700</pubDate>  
  <updated xmlns="http://www.w3.org/2005/Atom">2007-08-29T14:07:09-07:00</updated>  
  <rights type="text" xmlns="http://www.w3.org/2005/Atom">Copyright 2007</rights>  
  <content type="text" xmlns="http://www.w3.org/2005/Atom">Item Content</content>  
  <contributor xmlns="http://www.w3.org/2005/Atom">  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
  <contributor xmlns="http://www.w3.org/2005/Atom">  
    <name>Kim Abercrombie</name>  
    <uri>http://Contoso/Abercrombie</uri>  
    <email>Kim.Abercrombie@contoso.com</email>  
  </contributor>  
</item>  
```  
  
## SyndicationPerson  
 Nell'esempio di codice seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.SyndicationPerson> per i formati Atom 1.0 e RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#2)]
 [!code-vb[SyndicationMapping#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#2)]  
  
 Nel codice XML seguente viene mostrato come serializzare <xref:System.ServiceModel.Syndication.SyndicationPerson> per il formato Atom 1.0.  
  
```  
  <author>  
    <name>Jesper Aaberg</name>  
    <uri>http://Contoso/Aaberg</uri>  
    <email>Jesper.Aaberg@contoso.com</email>  
  </author>  
<contributor>  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
```  
  
 Nell'XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.SyndicationPerson> per il formato RSS 2.0 se esiste un solo <xref:System.ServiceModel.Syndication.SyndicationPerson> rispettivamente nelle raccolte `Authors` o `Contributors`.  
  
```  
<author>Jesper.Aaberg@contoso.com</author>  
<a10:contributor>  
    <a10:name>Lene Aaling</a10:name>  
    <a10:uri>http://Contoso/Aaling</a10:uri>  
    <a10:email>Lene.Aaling@contoso.com</a10:email>  
</a10:contributor>  
```  
  
 Nell'XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.SyndicationPerson> per il formato RSS 2.0 se esiste più di un <xref:System.ServiceModel.Syndication.SyndicationPerson> rispettivamente nelle raccolte `Authors` o `Contributors`.  
  
```  
<a10:author>  
    <a10:name>Jesper Aaberg</a10:name>  
    <a10:uri>http://Contoso/Aaberg</a10:uri>  
    <a10:email>Jesper.Aaberg@contoso.com</a10:email>  
</a10:author>  
<a10:author>  
    <a10:name>Syed Abbas</a10:name>  
    <a10:uri>http://Contoso/Abbas</a10:uri>  
    <a10:email>Syed.Abbas@contoso.com</a10:email>  
</a10:author>  
<a10:contributor>  
    <a10:name>Lene Aaling</a10:name>  
    <a10:uri>http://Contoso/Aaling</a10:uri>  
    <a10:email>Lene.Aaling@contoso.com</a10:email>  
</a10:contributor>  
<a10:contributor>  
    <a10:name>Kim Abercrombie</a10:name>  
    <a10:uri>http://Contoso/Abercrombie</a10:uri>  
    <a10:email>Kim.Abercrombie@contoso.com</a10:email>  
</a10:contributor>  
```  
  
## SyndicationLink  
 Nell'esempio di codice seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.SyndicationLink> per i formati Atom 1.0 e RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#3)]
 [!code-vb[SyndicationMapping#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#3)]  
  
 Nel codice XML seguente viene mostrato come serializzare <xref:System.ServiceModel.Syndication.SyndicationLink> per il formato Atom 1.0.  
  
 `<link rel="alternate" type="text/html" title="My Link Title" length="2048" href="http://contoso/MyLink" />`  
  
 Nel codice XML seguente viene mostrato come serializzare <xref:System.ServiceModel.Syndication.SyndicationLink> per il formato RSS 2.0.  
  
 `<a10:link rel="alternate" type="text/html" title="My Link Title" length="2048" href="http://contoso/MyLink" />`  
  
## SyndicationCategory  
 Nell'esempio di codice seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.SyndicationCategory> per i formati Atom 1.0 e RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#4)]
 [!code-vb[SyndicationMapping#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#4)]  
  
 Nel codice XML seguente viene mostrato come serializzare <xref:System.ServiceModel.Syndication.SyndicationCategory> per il formato Atom 1.0.  
  
 `<category term="categoryName" label="categoryLabel" scheme="categoryScheme" />`  
  
 Nel codice XML seguente viene mostrato come serializzare <xref:System.ServiceModel.Syndication.SyndicationCategory> per il formato RSS 2.0.  
  
 `<category domain="categoryScheme">categoryName</category>`  
  
## TextSyndicationContent  
 Nell'esempio di codice seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.TextSyndicationContent> per i formati Atom 1.0 e RSS 2.0 quando viene creato <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenuto HTML.  
  
 [!code-csharp[SyndicationMapping#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#5)]
 [!code-vb[SyndicationMapping#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#5)]  
  
 Nel codice XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenuto HTML per il formato Atom 1.0.  
  
 `<content type="html"><html> some html </html></content>`  
  
 Nel codice XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenuto HTML per il formato RSS 2.0.  
  
 `<description><html> some html </html></description>`  
  
 Nell'esempio di codice seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.TextSyndicationContent> per i formati Atom 1.0 e RSS 2.0 quando viene creato <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenuto di testo normale.  
  
 [!code-csharp[SyndicationMapping#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#6)]
 [!code-vb[SyndicationMapping#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#6)]  
  
 Nel codice XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenuto di testo normale per il formato Atom 1.0.  
  
 `<content type="text">Some Plain Text</content>`  
  
 Nel codice XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenuto di testo normale per il formato RSS 2.0.  
  
 `<description>Some Plain Text</description>`  
  
 Nell'esempio di codice seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.TextSyndicationContent> per i formati Atom 1.0 e RSS 2.0 quando viene creato <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenuto XHTML.  
  
 [!code-csharp[SyndicationMapping#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#7)]
 [!code-vb[SyndicationMapping#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#7)]  
  
 Nel codice XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenuto XHTML per il formato Atom 1.0.  
  
 `<content type="xhtml">`  
  
 `<html> some xhtml </html>`  
  
 `</content>`  
  
 Nel codice XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenuto XHTML per il formato RSS 2.0.  
  
 `<description><html> some xhtml </html></description>`  
  
## UrlSyndicationContent  
 Nell'esempio di codice seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.UrlSyndicationContent> per i formati Atom 1.0 e RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#8)]
 [!code-vb[SyndicationMapping#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#8)]  
  
 Nel codice XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.UrlSyndicationContent> per il formato Atom 1.0.  
  
 `<content type="audio" src="http://someurl/" />`  
  
 Nel codice XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.UrlSyndicationContent> con contenuto XHTML per il formato RSS 2.0.  
  
 `<description />`  
  
 `<content type="audio" src="http://Contoso/someurl/" xmlns="http://www.w3.org/2005/Atom" />`  
  
## XmlSyndicationContent  
 Nell'esempio di codice seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.XmlSyndicationContent> per i formati Atom 1.0 e RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#9)]
 [!code-vb[SyndicationMapping#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#9)]  
  
 Nel codice XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.XmlSyndicationContent> per il formato Atom 1.0.  
  
 `<content type="mytype">`  
  
 `<SomeData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/FeedMapping" />`  
  
 `</content>`  
  
 Nel codice XML seguente viene illustrato come serializzare la classe <xref:System.ServiceModel.Syndication.XmlSyndicationContent> con contenuto XHTML per il formato RSS 2.0.  
  
 `<content type="mytype" xmlns="http://www.w3.org/2005/Atom">`  
  
 `<SomeData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/FeedMapping" />`  
  
 `</content>`  
  
## Vedere anche  
 [Panoramica sulla diffusione WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)   
 [Architettura di diffusione](../../../../docs/framework/wcf/feature-details/architecture-of-syndication.md)   
 [Procedura: creare un feed RSS di base](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-rss-feed.md)   
 [Procedura: creare un feed Atom di base](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-atom-feed.md)   
 [Procedura: esporre un feed come Atom e RSS](../../../../docs/framework/wcf/feature-details/how-to-expose-a-feed-as-both-atom-and-rss.md)