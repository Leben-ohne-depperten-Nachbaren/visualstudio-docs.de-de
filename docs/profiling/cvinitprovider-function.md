---
title: CvInitProvider-Funktion | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkers/CvInitProvider
helpviewer_keywords:
- CvInitProvider method
ms.assetid: ba1863ad-e35f-4d34-a2f2-5e68957d1915
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a97be63cd782397e984fd8dbce7da844efa07540
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62552666"
---
# <a name="cvinitprovider-function"></a>CvInitProvider-Funktion
Initialisiert Markeranbieter. Muss vor anderen Funktionen des SDK für die Nebenläufigkeitsschnellansicht aufgerufen werden.

## <a name="syntax"></a>Syntax

```C
HRESULT CvInitProvider(
   _In_ const GUID* pGuid,
   _Out_ PCV_PROVIDER* ppProvider
);
```

#### <a name="parameters"></a>Parameter
 `pGuid`: die Anbieter-GUID. Darf nicht NULL sein.

 `ppProvider`: die Adresse einer Ausgabevariablen, mit der der Anbieterkontext gespeichert wird. Darf nicht NULL sein.

## <a name="return-value"></a>Rückgabewert
 S_OK, wenn der Anbieter erfolgreich initialisiert wurde, oder Fehlercode, wenn Fehler aufgetreten sind. Prüfen Sie mit den Makros SUCCEEDED bzw. FAILED, ob Fehler vorliegen.

## <a name="requirements"></a>Anforderungen
 **Header:** *cvmarkers.h*

## <a name="see-also"></a>Siehe auch
- [C++-Bibliotheksreferenz](../profiling/cpp-library-reference.md)