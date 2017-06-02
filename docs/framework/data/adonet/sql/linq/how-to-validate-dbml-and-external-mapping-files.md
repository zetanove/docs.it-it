---
title: "Procedura: convalidare file DBML e file di mapping esterno | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d9ea37f5-0a9e-4401-8fc3-1e6fd44c49f9
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: convalidare file DBML e file di mapping esterno
I file di mapping esterno e i file con estensione dbml modificati devono essere convalidati in base alle rispettive definizioni dello schema.  In questo argomento vengono descritti i passaggi per l'implementazione del processo di convalida per gli utenti di [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
### Per convalidare un file con estensione dbml o un file XML  
  
1.  Scegliere **Apri** dal menu **File** di Visual Studio, quindi fare clic su **File**.  
  
2.  Nella finestra di dialogo **Apri file** fare clic sul file di mapping dbml o XML che si desidera convalidare.  
  
     Il file verrà aperto nell'**Editor XML**.  
  
3.  Fare clic con il pulsante destro del mouse sulla finestra, quindi scegliere **Proprietà**.  
  
4.  Nella finestra **Proprietà** fare clic sul pulsante con i puntini di sospensione accanto alla proprietà **Schemi**.  
  
     Verrà visualizzata la finestra di dialogo relativa agli schemi XML.  
  
5.  Notare la definizione dello schema adatta allo scopo.  
  
    -   DbmlSchema.xsd è la definizione dello schema per la convalida di un file dbml.  Per altre informazioni, vedere [Generazione di codice in LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md).  
  
    -   LinqToSqlMapping.xsd è la definizione dello schema per la convalida di un file di mapping XML esterno.  Per altre informazioni, vedere [Mapping esterno](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md).  
  
6.  Nella colonna **Use** della riga di definizione dello schema desiderato fare clic per aprire la casella a discesa, quindi fare clic **Use this schema**.  
  
     Il file di definizione dello schema è ora associato al file di mapping DBML o XML.  
  
     Assicurarsi che non siano selezionate altre definizioni dello schema.  
  
7.  Scegliere **Elenco errori** dal menu **Visualizza**.  
  
     Determinare se sono stati generati errori, avvisi o messaggi.  In caso contrario, il file XML è valido per la definizione dello schema.  
  
## Metodo alternativo per fornire la definizione dello schema  
 Se per qualsiasi motivo il file con estensione xsd appropriato non viene visualizzato nella finestra di dialogo relativa agli schemi XML, è possibile scaricarlo da un argomento della Guida.  I passaggi seguenti consentono di salvare il file scaricato nel formato Unicode richiesto dall'editor XML di [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
#### Per copiare un file di definizione dello schema da un argomento della Guida  
  
1.  Individuare l'argomento della Guida che contiene la definizione dello schema descritta in questo argomento.  
  
    -   Per i file con estensione dbml, vedere [Generazione di codice in LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md).  
  
    -   Per i file di mapping esterno, vedere [Mapping esterno](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md).  
  
2.  Fare clic su **Copia codice** per copiare il file di codice negli Appunti.  
  
3.  Avviare il Blocco note per creare un nuovo file.  
  
4.  Incollare il codice dagli Appunti nel file del Blocco note.  
  
5.  Nel Blocco note scegliere **Salva con nome**  dal menu **File**.  
  
6.  Nella casella **Codifica** selezionare **Unicode**.  
  
    > [!IMPORTANT]
    >  Questa selezione assicura che il file di testo sia preceduto dal marcatore dell'ordine di byte Unicode 16 \(`FFFE`\).  
  
7.  Nella casella **Nome file** creare un nome file con estensione xsd.  
  
## Vedere anche  
 [Riferimenti](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)