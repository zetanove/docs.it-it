---
title: "Raccolte di schemi ODBC | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1bb126a5-ceec-4649-a4bc-8aa19e801046
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Raccolte di schemi ODBC
Contenuto della sezione viene descritto il supporto delle raccolte di schemi per driver ODBC per Microsoft SQL Server, Oracle e Microsoft Jet.  
  
## Driver ODBC di Microsoft SQL Server  
 Il driver ODBC di Microsoft SQL Server, oltre alle raccolte di schemi comuni, supporta le seguenti raccolte di schemi specifici:  
  
-   Tabelle  
  
-   Indexes  
  
-   Colonne  
  
-   Procedure  
  
-   ProcedureColumns  
  
-   ProcedureParameters  
  
-   Visualizzazioni  
  
### Tables e Views  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|TABLE\_CAT|String|  
|TABLE\_SCHEM|String|  
|TABLE\_NAME|String|  
|TABLE\_TYPE|String|  
|REMARKS|String|  
  
### Indexes  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|TABLE\_CAT|String|  
|TABLE\_SCHEM|String|  
|TABLE\_NAME|String|  
|NON\_UNIQUE|Int16|  
|INDEX\_QUALIFIER|String|  
|INDEX\_NAME|String|  
|TYPE|Int16|  
|ORDINAL\_POSITION|Int16|  
|COLUMN\_NAME|String|  
|ASC\_OR\_DESC|String|  
|CARDINATLITY|Int32|  
|PAGES|Int32|  
|FILTER\_CONDITION|String|  
|SS\_TYPE\_SCHEMA|String|  
|SS\_DATA\_TYPE|Byte|  
  
### Colonne  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|TABLE\_CAT|String|  
|TABLE\_SCHEM|String|  
|TABLE\_NAME|String|  
|COLUMN\_NAME|String|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|COLUMN\_SIZE|Int32|  
|BUFFER\_LENGTH|Int32|  
|DECIMAL\_DIGITS|Int16|  
|NUM\_PREC\_RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|COLUMN\_DEF|String|  
|SQL\_DATA\_TYPE|Int16|  
|SQL\_DATETIME\_SUB|Int16|  
|CHAR\_OCTET\_LENGTH|Int32|  
|ORDINAL\_POSITION|Int32|  
|IS\_NULLABLE|String|  
|SS\_TYPE\_CATALOG|String|  
|SS\_TYPE\_SCHEMA|String|  
|SS\_DATA\_TYPE|Byte|  
  
### Procedure  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|PROCEDURE\_CAT|String|  
|PROCEDURE\_SCHEM|String|  
|PROCEDURE\_NAME|String|  
|NUM\_INPUT\_PARAMS|Int32|  
|NUM\_OUTPUT\_PARAMS|Int32|  
|NUM\_RESULT\_SETS|Int32|  
|REMARKS|String|  
|PROCEDURE\_TYPE|Int16|  
  
### ProcedureColumns  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|PROCEDURE\_CAT|String|  
|PROCEDURE\_SCHEM|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_TYPE|Int16|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|COLUMN\_SIZE|Int32|  
|BUFFER\_LENGTH|Int32|  
|DECIMAL\_DIGITS|Int16|  
|NUM\_PREC\_RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|COLUMN\_DEF|String|  
|SQL\_DATA\_TYPE|Int16|  
|SQL\_DATETIME\_SUB|Int16|  
|CHAR\_OCTET\_LENGTH|Int32|  
|ORDINAL\_POSITION|Int32|  
|IS\_NULLABLE|String|  
|SS\_TYPE\_CATALOG|String|  
|SS\_TYPE\_SCHEMA|String|  
|SS\_DATA\_TYPE|Byte|  
  
### ProcedureParameters  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|PROCEDURE\_CAT|String|  
|PROCEDURE\_SCHEM|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_TYPE|Int16|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|COLUMN\_SIZE|Int32|  
|BUFFER\_LENGTH|Int32|  
|DECIMAL\_DIGITS|Int16|  
|NUM\_PREC\_RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|COLUMN\_DEF|String|  
|SQL\_DATA\_TYPE|Int16|  
|SQL\_DATETIME\_SUB|Int16|  
|CHAR\_OCTET\_LENGTH|Int32|  
|ORDINAL\_POSITION|Int32|  
|IS\_NULLABLE|String|  
|SS\_TYPE\_CATALOG|String|  
|SS\_TYPE\_SCHEMA|String|  
|SS\_DATA\_TYPE|Byte|  
  
## Driver Microsoft ODBC per Oracle  
 Il driver ODBC di Microsoft SQL Server per Oracle, oltre alle raccolte di schemi comuni, supporta le seguenti raccolte di schemi specifici:  
  
-   Tabelle  
  
-   Colonne  
  
-   Procedure  
  
-   ProcedureColumns  
  
-   ProcedureParameters  
  
-   Visualizzazioni  
  
-   Indexes  
  
### Tables e Views  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|TABLE\_QUALIFIER|String|  
|TABLE\_OWNER|String|  
|TABLE\_NAME|String|  
|TABLE\_TYPE|String|  
|REMARKS|String|  
  
### Colonne  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|TABLE\_QUALIFIER|String|  
|TABLE\_OWNER|String|  
|TABLE\_NAME|String|  
|COLUMN\_NAME|String|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|PRECISION|Int32|  
|LENGTH|Int32|  
|SCALE|Int16|  
|RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|ORDINAL\_POSITION|Int32|  
  
### Procedure  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|PROCEDURE\_QUALIFIER|String|  
|PROCEDURE\_OWNER|String|  
|PROCEDURE\_NAME|String|  
|NUM\_INPUT\_PARAMS|Int16|  
|NUM\_OUTPUT\_PARAMS|Int16|  
|NUM\_RESULT\_SETS|Int16|  
|REMARKS|String|  
|PROCEDURE\_TYPE|Int16|  
  
### ProcedureColumns  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|PROCEDURE\_QUALIFIER|String|  
|PROCEDURE\_OWNER|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_TYPE|Int16|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|PRECISION|Int32|  
|LENGTH|Int32|  
|SCALE|Int16|  
|RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|OVERLOAD|Int32|  
|ORDINAL\_POSITION|Int32|  
  
## Driver ODBC per Microsoft Jet  
 Oltre alle raccolte di schemi comuni, il driver ODBC per Microsoft Jet supporta le raccolte di schemi specifici seguenti:  
  
-   Tabelle  
  
-   Indexes  
  
-   Colonne  
  
-   Procedure  
  
-   ProcedureColumns  
  
-   ProcedureParameters  
  
-   Visualizzazioni  
  
### Tables e Views  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|TABLE\_QUALIFIER|String|  
|TABLE\_OWNER|String|  
|TABLE\_NAME|String|  
|TABLE\_TYPE|String|  
|REMARKS|String|  
  
### Colonne  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|TABLE\_QUALIFIER|String|  
|TABLE\_OWNER|String|  
|TABLE\_NAME|String|  
|COLUMN\_NAME|String|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|PRECISION|Int32|  
|LENGTH|Int32|  
|SCALE|Int16|  
|RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|ORDINAL\_POSITION|Int32|  
  
### Procedure  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|PROCEDURE\_QUALIFIER|String|  
|PROCEDURE\_OWNER|String|  
|PROCEDURE\_NAME|String|  
|NUM\_INPUT\_PARAMS|Int16|  
|NUM\_OUTPUT\_PARAMS|Int16|  
|NUM\_RESULT\_SETS|Int16|  
|REMARKS|String|  
|PROCEDURE\_TYPE|Int16|  
  
### ProcedureColumns  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|PROCEDURE\_QUALIFIER|String|  
|PROCEDURE\_OWNER|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_TYPE|Int16|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|PRECISION|Int32|  
|LENGTH|Int32|  
|SCALE|Int16|  
|RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|OVERLOAD|Int32|  
|ORDINAL\_POSITION|Int32|  
  
### ProcedureParameters  
  
|Nome colonna|Tipo di dati|  
|------------------|------------------|  
|PROCEDURE\_CAT|String|  
|PROCEDURE\_SCHEM|String|  
|PROCEDURE\_NAME|String|  
|COLUMN\_NAME|String|  
|COLUMN\_TYPE|Int16|  
|DATA\_TYPE|Int16|  
|TYPE\_NAME|String|  
|COLUMN\_SIZE|Int32|  
|BUFFER\_LENGTH|Int32|  
|DECIMAL\_DIGITS|Int16|  
|NUM\_PREC\_RADIX|Int16|  
|NULLABLE|Int16|  
|REMARKS|String|  
|COLUMN\_DEF|String|  
|SQL\_DATA\_TYPE|Int16|  
|SQL\_DATETIME\_SUB|Int16|  
|CHAR\_OCTET\_LENGTH|Int32|  
|ORDINAL\_POSITION|Int32|  
|IS\_NULLABLE|String|  
  
## Vedere anche  
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)