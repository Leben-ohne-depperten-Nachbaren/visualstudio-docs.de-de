---
title: IDebugEngine3::SetJustMyCodeState | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetJustMyCodeState
helpviewer_keywords:
- IDebugEngine3::SetJustMyCodeState
ms.assetid: 8ec17fbf-df93-424a-b2ed-fd1e5ee51256
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f53b0eb95a2a91f34917b05cadffda2f4aa9a8b1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322328"
---
# <a name="idebugengine3setjustmycodestate"></a>IDebugEngine3::SetJustMyCodeState
Diese Methode teilt die Debug-Engine zu den JustMyCode-Status-Informationen.

## <a name="syntax"></a>Syntax

```cpp
HRESULT SetJustMyCodeState(
   BOOL           fUpdate,
   DWORD          dwModules,
   JMC_CODE_SPEC* rgJMCSpec
);
```

```csharp
int SetJustMyCodeState(
   int             fUpdate,
   uint            dwModules,
   JMC_CODE_SPEC[] rgJMCSpec
);
```

## <a name="parameters"></a>Parameter
`fUpdate`\
[in] Ungleich Null (`TRUE`) um aktuelle Informationen zu aktualisieren, NULL (`FALSE`) alle Informationen, die (wird ignoriert, alle zuvor festgelegten) zurücksetzen.

`dwModules`\
[in] Anzahl der Informationsstrukturen in `rgJMCSpec.`

`rgJMCSpec`\
[in] Array von [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md) Strukturen verwenden.

## <a name="return-value"></a>Rückgabewert
 Wenn erfolgreich, wird `S_OK`ist, andernfalls gibt den Fehlercode zurück.

## <a name="remarks"></a>Hinweise
 JustMyCode ist das Konzept der nur den Code Debuggen, der zu einem Benutzer gehört, und wird ignoriert, alle temporären Code wie z. B. Systemcode – selbst wenn der Quellcode für diesen Systemcode verfügbar ist.

## <a name="see-also"></a>Siehe auch
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
- [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)