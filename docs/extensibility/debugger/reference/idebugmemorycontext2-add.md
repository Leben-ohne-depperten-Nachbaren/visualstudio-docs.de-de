---
title: IDebugMemoryContext2::Add | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Add
helpviewer_keywords:
- IDebugMemoryContext2::Add method
- Add method
ms.assetid: 3c47e646-ce9e-4dd3-8f1a-6dbd3827d407
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c1cafbf22e51f867948491e2925c085bd387ea84
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66347087"
---
# <a name="idebugmemorycontext2add"></a>IDebugMemoryContext2::Add
Fügt den angegebenen Wert für den aktuellen Kontext aus, und gibt Sie einen neuen Kontext zurück.

## <a name="syntax"></a>Syntax

```cpp
HRESULT Add( 
   UINT64                 dwCount,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int Add(
   ulong                    dwCount,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>Parameter
`dwCount`\
[in] Der Wert für den aktuellen Kontext hinzugefügt.

`ppMemCxt`\
[out] Gibt eine neue [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) Objekt.

## <a name="return-value"></a>Rückgabewert
 Wenn erfolgreich, wird `S_OK`ist, andernfalls ein Fehlercode zurückgegeben.

## <a name="remarks"></a>Hinweise
 Ein Arbeitsspeicher-Kontext ist eine Adresse, daher Hinzufügen eines Werts zu einer Adresse generiert eine neue Adresse, die eine neue Kontextschnittstelle erforderlich sind.

 Diese Methode muss immer einen neuen Kontext, erzeugen, auch wenn die resultierende Adresse außerhalb des Speicherbereichs, der diesem Kontext zugeordnet ist. Die einzige Ausnahme hierbei ist, wenn kein Arbeitsspeicher kann, für den neuen Kontext belegt werden oder `ppMemCxt` ist ein null-Wert (der ein Fehler ist).

## <a name="see-also"></a>Siehe auch
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)