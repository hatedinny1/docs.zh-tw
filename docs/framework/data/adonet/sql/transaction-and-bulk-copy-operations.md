---
title: "交易和大量複製作業 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 交易和大量複製作業
大量複製作業可做為隔離作業或多步驟交易的其中一個執行步驟。  第二種選項可讓您在同一交易內執行多個大量複製作業，並執行其他資料庫作業 \(例如插入、更新及刪除\)，同時仍然能夠認可或回復整個交易。  
  
 根據預設，大量複製作業會做為隔離作業執行。  大量複製作業會以非交易性方式進行，而且無法回復。  如果需要在發生錯誤時，復原全部或部分大量複製，您可以使用 <xref:System.Data.SqlClient.SqlBulkCopy> 管理的交易，在現有交易內執行大量複製作業，或在 **System.Transactions** <xref:System.Transactions.Transaction> 中登記。  
  
## 執行非交易大量複製作業  
 下列主控台應用程式 \(Console Application\) 會顯示非交易大量複製作業在作業過程中發生錯誤時的狀況。  
  
 在範例中，來源資料表及目標資料表都包含名為 **ProductID** 的 `Identity` 資料行。  首先，程式碼會透過刪除所有資料列然後插入其 **ProductID** 已存在於來源資料表中的單一資料列，來準備目標資料表。  依預設會在目標資料表中，為每個加入之資料列的 `Identity` 資料行產生新的值。  在此範例中，開啟連接時會設定選項，以強制大量載入處理序使用來源資料表中的 `Identity` 值。  
  
 執行大量複製作業時，其 <xref:System.Data.SqlClient.SqlBulkCopy.BatchSize%2A> 屬性會設定為 10。  當作業遇到無效的資料列時，系統會擲回例外狀況 \(Exception\)。  在第一個範例中，大量複製作業是非交易的。  發生錯誤前複製的所有批次作業都會得到認可；處理任何其他批次作業之前，會復原包含重複索引鍵的批次作業，並中止大量複製作業。  
  
> [!NOTE]
>  除非您已依照[大量複製範例設定](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)所述來建立工作資料表，否則此範例將無法執行。  這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。  如果來源及目的地資料表位於相同的 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 執行個體中，則使用 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
 [!code-csharp[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/VB/source.vb#1)]  
  
## 在交易中執行專用大量複製作業  
 根據預設，大量複製作業是自己的交易。  當您要執行專用大量複製作業時，請建立具有連接字串的新 <xref:System.Data.SqlClient.SqlBulkCopy> 執行個體，或使用不含作用中交易的現有 <xref:System.Data.SqlClient.SqlConnection> 物件。  在每個案例中，會先建立大量複製作業，然後認可或復原交易。  
  
 您可以在 <xref:System.Data.SqlClient.SqlBulkCopy> 類別建構函式 \(Constructor\) 中明確指定 <xref:System.Data.SqlClient.SqlBulkCopyOptions> 選項，以便明確地讓大量複製作業在自己的交易中執行，進而讓每個大量複製作業的批次在個別的交易內執行。  
  
> [!NOTE]
>  由於是在不同的交易中執行不同的批次作業，因此如果在大量複製作業期間發生錯誤，則將復原目前批次作業中的所有資料列，但是先前批次作業的資料列將保留在資料庫中。  
  
 下列主控台應用程式類似於先前的範例，但有一個例外狀況：在此範例中，大量複製作業會管理其本身的交易。  發生錯誤前複製的所有批次作業都會得到認可；處理任何其他批次作業之前，會復原包含重複索引鍵的批次作業，並中止大量複製作業。  
  
> [!IMPORTANT]
>  除非您已依照[大量複製範例設定](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)所述來建立工作資料表，否則此範例將無法執行。  這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。  如果來源及目的地資料表位於相同的 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 執行個體中，則使用 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
 [!code-csharp[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/VB/source.vb#1)]  
  
## 使用現有交易  
 您可指定現有 <xref:System.Data.SqlClient.SqlTransaction> 物件做為 <xref:System.Data.SqlClient.SqlBulkCopy> 建構函式中的參數。  在此情況下，系統會在現有交易中執行大量複製作業，而且不會變更交易狀態 \(亦即，它尚未認可或中止\)。  這可讓應用程式使用其他資料庫作業來將大量複製作業併入交易中。  不過，如果您不指定 <xref:System.Data.SqlClient.SqlTransaction> 物件及傳遞 Null 參考，而且連接具有作用中的交易，則會擲回例外狀況。  
  
 如果因為發生錯誤而需要回復整個大量複製作業，或者大量複製作業應做為可回復之較大處理序的一部分執行，則可提供 <xref:System.Data.SqlClient.SqlTransaction> 物件給 <xref:System.Data.SqlClient.SqlBulkCopy> 建構函式。  
  
 下列主控台應用程式類似於第一個 \(非交易\) 範例，但有一個例外狀況：在此範例中，大量複製作業包含在較大的外部交易中。  當發生主索引鍵違規錯誤時，會復原整個交易，並且不會將任何資料列加入目標資料表中。  
  
> [!IMPORTANT]
>  除非您已依照[大量複製範例設定](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)所述來建立工作資料表，否則此範例將無法執行。  這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。  如果來源及目的地資料表位於相同的 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 執行個體中，則使用 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
 [!code-csharp[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/VB/source.vb#1)]  
  
## 請參閱  
 [SQL Server 中的大量複製作業](../../../../../docs/framework/data/adonet/sql/bulk-copy-operations-in-sql-server.md)   
 [ADO.NET Managed 提供者和資料集開發人員中心](http://go.microsoft.com/fwlink/?LinkId=217917)