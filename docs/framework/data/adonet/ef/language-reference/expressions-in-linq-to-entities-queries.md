---
title: "LINQ to Entities 查詢中的運算式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: d70b502f-6a15-4120-b4fe-500b173ad9cc
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# LINQ to Entities 查詢中的運算式
運算式是可以評估為單一值、物件、方法或命名空間的程式碼片段。  運算式可以包含常值、方法呼叫、運算子及其運算元，或是簡單名稱。  簡單名稱可以是變數、型別成員、方法參數、命名空間或型別的名稱。  運算式可以使用運算子 \(後者又可能使用其他運算式當做參數\) 或方法呼叫 \(它的參數又可能是其他方法呼叫\)。  因此，運算式可以很簡單，也可以非常複雜。  
  
 在 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 查詢中，運算式可以包含 <xref:System.Linq.Expressions> 命名空間中型別允許的任何項目，包括 Lambda 運算式。  [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 查詢中可以使用的運算式是可用於查詢 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 之運算式的超集。  針對 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 之查詢中所包含的運算式僅限於 `ObjectQuery<T>` 和基礎資料來源所支援的運算。  
  
 在以下範例中，`Where` 子句中的比較就是個運算式：  
  
 [!code-csharp[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#whereexpression)]
 [!code-vb[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#whereexpression)]  
  
> [!NOTE]
>  指定語言建構 \(例如 C\# `unchecked`\) 在 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 中沒有意義。  
  
## 本章節內容  
 [常數運算式](../../../../../../docs/framework/data/adonet/ef/language-reference/constant-expressions.md)  
  
 [比較運算式](../../../../../../docs/framework/data/adonet/ef/language-reference/comparison-expressions.md)  
  
 [Null 比較](../../../../../../docs/framework/data/adonet/ef/language-reference/null-comparisons.md)  
  
 [初始化運算式](../../../../../../docs/framework/data/adonet/ef/language-reference/initialization-expressions.md)  
  
 [Navigation Properties](http://msdn.microsoft.com/zh-tw/41e1e6b9-8a57-467d-99d9-1857d2ca2ea5)  
  
## 請參閱  
 [ADO.NET Entity Framework](../../../../../../docs/framework/data/adonet/ef/index.md)