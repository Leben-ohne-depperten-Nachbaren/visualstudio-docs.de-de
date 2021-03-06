---
title: 'CA1403: automatische Layouttypen sollten nicht com-sichtbar sein | Microsoft-Dokumentation'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AutoLayoutTypesShouldNotBeComVisible
- CA1403
helpviewer_keywords:
- CA1403
- AutoLayoutTypesShouldNotBeComVisible
ms.assetid: a7007714-f9b4-4730-94e0-67d3dc68991f
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5f39540cb23d86dda4244604da8a9ff764594e11
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661334"
---
# <a name="ca1403-auto-layout-types-should-not-be-com-visible"></a>CA1403: Typen mit automatischem Layout sollten nicht für COM sichtbar sein
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AutoLayoutTypesShouldNotBeComVisible|
|CheckId|CA1403|
|Kategorie|Microsoft. Interoperabilität|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
 Ein sichtbarer Component Object Model (com)-Werttyp ist mit dem Attribut <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName> gekennzeichnet, das auf <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=fullName> festgelegt ist.

## <a name="rule-description"></a>Regelbeschreibung
 <xref:System.Runtime.InteropServices.LayoutKind> Layouttypen werden vom Common Language Runtime verwaltet. Das Layout dieser Typen kann sich zwischen den Versionen der .NET Framework ändern, wodurch com-Clients, die ein bestimmtes Layout erwarten, unterbricht werden. Beachten Sie, dass C#, wenn das <xref:System.Runtime.InteropServices.StructLayoutAttribute>-Attribut nicht angegeben ist, die C++ -, [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]-und-Compiler das <xref:System.Runtime.InteropServices.LayoutKind> Layout für Werttypen angeben.

 Sofern nicht anders gekennzeichnet, sind alle öffentlichen nicht generischen Typen für com sichtbar. alle nicht öffentlichen und generischen Typen sind für com nicht sichtbar. Um falsch positive Ergebnisse zu reduzieren, erfordert diese Regel jedoch, dass die COM-Sichtbarkeit des Typs explizit angegeben wird. die enthaltende Assembly muss mit dem <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> als `false` markiert werden, und der Typ muss mit dem <xref:System.Runtime.InteropServices.ComVisibleAttribute> auf `true` festgelegt sein.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
 Um einen Verstoß gegen diese Regel zu beheben, ändern Sie den Wert des <xref:System.Runtime.InteropServices.StructLayoutAttribute> Attributs in <xref:System.Runtime.InteropServices.LayoutKind> oder <xref:System.Runtime.InteropServices.LayoutKind>, oder machen Sie den Typ für COM unsichtbar.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
 Unterdrücken Sie keine Warnung dieser Regel.

## <a name="example"></a>Beispiel
 Das folgende Beispiel zeigt einen Typ, der gegen die Regel verstößt, und einen Typ, der die Regel erfüllt.

 [!code-csharp[FxCop.Interoperability.AutoLayout#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/cs/FxCop.Interoperability.AutoLayout.cs#1)]
 [!code-vb[FxCop.Interoperability.AutoLayout#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/vb/FxCop.Interoperability.AutoLayout.vb#1)]

## <a name="related-rules"></a>Verwandte Regeln
 [CA1408: AutoDual ClassInterfaceType nicht verwenden](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>Siehe auch
 [Einführung in die Klassen Schnittstelle](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024) [qualifizieren von .NET-Typen für die Interoperation](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd) [mit nicht verwaltetem Code](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
