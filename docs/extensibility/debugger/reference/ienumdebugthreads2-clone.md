---
title: IEnumDebugThreads2::Clone | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2::Clone
helpviewer_keywords:
- IEnumDebugThreads2::Clone
ms.assetid: d774322c-e72d-4df3-b317-928da39dadc5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 98ed0d58aeec5b26216366d84661bf42b304e2cb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350859"
---
# <a name="ienumdebugthreads2clone"></a>IEnumDebugThreads2::Clone
Gibt eine Kopie der aktuellen Enumeration als ein separates Objekt zurück.

## <a name="syntax"></a>Syntax

```cpp
HRESULT Clone(
   IEnumDebugThreads2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugThreads2 ppEnum
);
```

## <a name="parameters"></a>Parameter
`ppEnum`\
[out] Gibt eine Kopie dieser Enumeration als ein separates Objekt zurück.

## <a name="return-value"></a>Rückgabewert
 Wenn erfolgreich, wird `S_OK`ist, andernfalls ein Fehlercode zurückgegeben.

## <a name="remarks"></a>Hinweise
 Die Kopie der Enumeration hat den gleichen Zustand wie die ursprüngliche, zu dem Zeitpunkt, die diese Methode aufgerufen wird. Allerdings wird der Kopiervorgangs des und den ursprünglichen Zustand sind getrennt und einzeln geändert werden können.

## <a name="see-also"></a>Siehe auch
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)