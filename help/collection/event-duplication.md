---
title: Umgang mit Ereignisduplizierungen im Experience Platform
description: Erfahren Sie, wie Adobe Experience Platform mit der Ereignisduplizierung umgeht
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Umgang mit Ereignisduplizierungen in Adobe Experience Platform

Adobe Experience Platform ist ein hochverteiltes System, das die Zuverlässigkeit maximiert und gleichzeitig auf immer größere Datenmengen skaliert.

Bei der Echtzeit-Datenerfassung werden [Erlebnisereignisse](../xdm/classes/experienceevent.md) über das [Edge Network](../web-sdk/home.md#edge-network) aus clientseitigen Quellen wie [Web SDK](../web-sdk/home.md) oder dem [Mobile SDK](https://developer.adobe.com/client-sdks/home/) erfasst und an Experience Platform-Verarbeitungs- und Speicherschichten gesendet. Diese Ebenen bestehen aus Lösungen wie Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de) und [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de).

Um den Verlust von Erlebnisereignissen zu minimieren, erwarten Client-seitige SDKs und der interne Experience Platform-Bereitstellungsdienst eine Bestätigung, dass ein Ereignis erfolgreich erfasst wurde.

Wenn diese Bestätigung nicht empfangen wird, versuchen Sie es erneut mit den clientseitigen SDKs oder dem internen Platform-Bereitstellungsdienst und das Erlebnisereignis wird erneut gesendet.

Dies ist eine Best Practice für den Umgang mit Verlaufsfehlern. Die Nebenwirkung besteht darin, dass es möglich ist, doppelte Ereignisse einzuführen.

Informationen zu Best Practices für die Handhabung von Verlaufsfehlern finden Sie in diesem Artikel zur [Behebung vorübergehender Fehler](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Szenarien für die Ereignisduplizierung {#scenarios}

Eine Ereignisduplizierung kann in verschiedenen Szenarien auftreten, z. B. aber nicht ausschließlich:

* Netzwerkbezogene Probleme zwischen clientseitigen SDKs und dem [!DNL Edge Network]. Diese Probleme können aus Fehlern des Internet Service Providers, dem Verlust mobiler Signale oder anderen Netzwerkfehlern resultieren, da die Verbindung zwischen dem Kunden und dem Edge Network über das öffentliche Internet hergestellt wird.
* Interne Experience Platform: Automatische Skalierung von Ereignissen. Gelegentlich können Daten aufgrund der Volatilität der Cloud-Infrastruktur neu ausgeglichen werden.

Die Adobe Experience Platform-Datenerfassungsschicht unterstützt die Verarbeitung mindestens einmal. Dementsprechend kann es in begrenzten, seltenen Fällen zu einer Duplizierung von Ereignissen kommen.

Weitere Informationen zur Verarbeitung &quot;mindestens einmal&quot;finden Sie in diesem Artikel zu [Garantien für Nachrichtenversand](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Deduplizierungsoptionen für Ereignisse {#deduplication}

Für Geschäftsszenarios, die auf doppelte Ereignisse reagieren, verwendet Experience Platform mehrere Deduplizierungsmethoden für Ereignisse in seinen nachgelagerten Speichersystemen, wie die unten beschriebenen.

* Der Real-Time CDP-Profilspeicher legt Ereignisse ab, wenn ein Ereignis mit dem gleichen `_id` bereits im [!DNL Profile store] vorhanden ist. Weitere Informationen finden Sie in der Dokumentation zur [XDM ExperienceEvent-Klasse](../xdm/classes/experienceevent.md) .
* Mit Customer Journey Analytics können Benutzer eine Metrik so konfigurieren, dass nur Werte nicht wiederholt gezählt werden. Weiterführende Informationen dazu finden Sie in der Dokumentation zu den Einstellungen der Metrik-Deduplizierungskomponente ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=de).[
* Experience Platform Query Service unterstützt die Deduplizierung von Daten, wenn eine ganze Zeile aus einer Berechnung entfernt oder ein bestimmter Feldsatz ignoriert werden muss, da nur ein Teil der Daten in der Zeile doppelte Informationen enthält. Weitere Informationen finden Sie in der Dokumentation zur [Datendeduplizierung in Query Service](../query-service/key-concepts/deduplication.md) .

>[!NOTE]
>
>Wenn außerhalb der oben beschriebenen Anwendungsfälle Probleme mit der Ereignisduplizierung auftreten, wenden Sie sich an Ihren Adobe-Support-Mitarbeiter und geben Sie detaillierte Informationen zu Ihrem Anwendungsfall an.
