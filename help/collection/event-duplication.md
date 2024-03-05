---
title: Umgang mit Ereignisduplizierungen im Experience Platform
description: Erfahren Sie, wie Adobe Experience Platform mit der Ereignisduplizierung umgeht
source-git-commit: bc3ae849bd7fd8a9f50ba98528adc43d7282df90
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Umgang mit Ereignisduplizierungen in Adobe Experience Platform

Adobe Experience Platform ist ein hochverteiltes System, das die Zuverlässigkeit maximiert und gleichzeitig auf immer größere Datenmengen skaliert.

Für die Echtzeit-Datenerfassung: [Erlebnisereignisse](../xdm/classes/experienceevent.md) werden über die [Edge Network](../web-sdk/home.md#edge-network), aus clientseitigen Quellen, wie z. B. [Web SDK](../web-sdk/home.md) oder [Mobile SDK](https://developer.adobe.com/client-sdks/home/)und an Experience Platform-Verarbeitungs- und Speicherschichten geliefert werden. Diese Schichten bestehen aus Lösungen wie Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de), und [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de).

Um den Verlust von Erlebnisereignissen zu minimieren, erwarten Client-seitige SDKs und der interne Experience Platform-Bereitstellungsdienst eine Bestätigung, dass ein Ereignis erfolgreich erfasst wurde.

Wenn diese Bestätigung nicht empfangen wird, versuchen Sie es erneut mit den clientseitigen SDKs oder dem internen Platform-Bereitstellungsdienst und das Erlebnisereignis wird erneut gesendet.

Dies ist eine Best Practice für den Umgang mit Verlaufsfehlern. Die Nebenwirkung besteht darin, dass es möglich ist, doppelte Ereignisse einzuführen.

Informationen zu Best Practices für die Behandlung von Verlaufsfehlern finden Sie in diesem Artikel zu [vorübergehende Fehlerbehandlung](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Szenarien für die Ereignisduplizierung {#scenarios}

Eine Ereignisduplizierung kann in verschiedenen Szenarien auftreten, z. B. aber nicht ausschließlich:

* Netzwerkbezogene Probleme zwischen Client-seitigen SDKs und der [!DNL Edge Network]. Diese Probleme können aus Fehlern des Internet Service Providers, dem Verlust mobiler Signale oder anderen Netzwerkfehlern resultieren, da die Verbindung zwischen dem Kunden und dem Edge-Netzwerk über das öffentliche Internet hergestellt wird.
* Interne Experience Platform: Automatische Skalierung von Ereignissen. Gelegentlich können Daten aufgrund der Volatilität der Cloud-Infrastruktur neu ausgeglichen werden.

Die Adobe Experience Platform-Datenerfassungsschicht unterstützt die Verarbeitung mindestens einmal. Dementsprechend kann es in begrenzten, seltenen Fällen zu einer Duplizierung von Ereignissen kommen.

Weitere Informationen zur Verarbeitung &quot;mindestens einmal&quot;finden Sie in diesem Artikel zu [Versandgarantien](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Deduplizierungsoptionen für Ereignisse {#deduplication}

Für Geschäftsszenarios, die auf doppelte Ereignisse reagieren, verwendet Experience Platform mehrere Deduplizierungsmethoden für Ereignisse in seinen nachgelagerten Speichersystemen, wie die unten beschriebenen.

* Real-Time CDP-Profilspeicher legen Ereignisse ab, wenn ein Ereignis mit demselben `_id` bereits in der [!DNL Profile Store]. Siehe die Dokumentation unter [XDM ExperienceEvent-Klasse](../xdm/classes/experienceevent.md) für weitere Details.
* Mit Customer Journey Analytics können Benutzer eine Metrik so konfigurieren, dass nur Werte nicht wiederholt gezählt werden. Weitere Informationen hierzu finden Sie in der Dokumentation unter [Komponenteneinstellungen für Metrik-Deduplizierung](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=de).
* Experience Platform Query Service unterstützt die Deduplizierung von Daten, wenn eine ganze Zeile aus einer Berechnung entfernt oder ein bestimmter Feldsatz ignoriert werden muss, da nur ein Teil der Daten in der Zeile doppelte Informationen enthält. Die Dokumentation finden Sie hier: [Datendeduplizierung in Query Service](../query-service/key-concepts/deduplication.md) für weitere Informationen.

>[!NOTE]
>
>Wenn außerhalb der oben beschriebenen Anwendungsfälle Probleme mit der Ereignisduplizierung auftreten, wenden Sie sich an Ihren Adobe-Support-Mitarbeiter und geben Sie detaillierte Informationen zu Ihrem Anwendungsfall an.