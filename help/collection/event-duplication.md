---
title: Behandlung von Ereignisduplikaten beim Experience Platform
description: Erfahren Sie, wie Adobe Experience Platform mit der Ereignisduplizierung umgeht
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Handhabung von Ereignisduplikaten in Adobe Experience Platform

Adobe Experience Platform ist ein hochgradig verteiltes System, das auf maximale Zuverlässigkeit bei gleichzeitiger Skalierung auf immer größere Datenmengen ausgelegt ist.

Bei der Echtzeit-Datenerfassung [Erlebnisereignisse](../xdm/classes/experienceevent.md) über das [Edge Network ](../web-sdk/home.md#edge-network) aus Client-seitigen Quellen wie [Web SDK](../web-sdk/home.md) oder [Mobile SDK](https://developer.adobe.com/client-sdks/home/) erfasst und an Experience Platform-Verarbeitungs- und Speicherebenen bereitgestellt. Diese Ebenen umfassen Lösungen wie Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de) und [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de).

Um den Verlust von Erlebnisereignissen zu minimieren, erwarten Client-seitige SDKs und der interne Experience Platform-Bereitstellungs-Service eine Bestätigung, dass ein Ereignis erfolgreich erfasst wurde.

Wenn diese Bestätigung nicht eingeht, wiederholen die Client-seitigen SDKs oder der interne Platform-Bereitstellungs-Service-Trigger den Vorgang und das Erlebnisereignis wird erneut gesendet.

Dies ist eine Best Practice für die Behandlung von vorübergehenden Fehlern. Der Nebeneffekt ist die Möglichkeit, doppelte Ereignisse einzuführen.

Informationen zu Best Practices für die Behandlung von vorübergehenden Fehlern finden Sie in diesem Artikel [vorübergehenden Fehlerbehandlung](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Szenarien für die Ereignisduplizierung {#scenarios}

Eine Ereignisduplizierung kann in verschiedenen Szenarien auftreten, z. B. unter anderem:

* Netzwerkbezogene Probleme zwischen Client-seitigen SDKs und der [!DNL Edge Network]. Diese Probleme können auf Ausfälle von Internet Service Providern, den Verlust von Mobilsignalen oder andere Netzwerkfehler zurückzuführen sein, da die Verbindung zwischen dem Kunden und dem Edge Network über das öffentliche Internet hergestellt wird.
* Interne automatische Experience Platform-Skalierung. Gelegentlich können Daten aufgrund der Volatilität der Cloud-Infrastruktur neu ausgerichtet werden.

Die Datenerfassungsschicht von Adobe Experience Platform unterstützt die „mindestens einmalige“ Verarbeitung. Daher kann es in seltenen Fällen zu einer Ereignisduplizierung kommen.

Weitere Informationen zur „mindestens einmaligen“ Verarbeitung finden Sie in diesem Artikel zu [Garantien für den Nachrichtenversand](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Optionen für die Ereignis-Deduplizierung {#deduplication}

Bei Geschäftsszenarien, die auf doppelte Ereignisse reagieren, verwendet Experience Platform in seinen nachgelagerten Speichersystemen mehrere Methoden zur Deduplizierung von Ereignissen, wie unten beschrieben.

* Der Real-Time CDP-Profilspeicher löscht Ereignisse, wenn im [!DNL Profile store] bereits ein Ereignis mit demselben `_id` vorhanden ist. Weitere Informationen finden Sie in der Dokumentation [XDM ExperienceEvent](../xdm/classes/experienceevent.md)Klasse).
* Beim Customer Journey Analytics können Benutzende eine Metrik so konfigurieren, dass Werte nicht wiederholt gezählt werden. Informationen dazu finden Sie in der Dokumentation unter [Metrik-Deduplizierung - Komponenteneinstellungen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=de).
* Der Experience Platform-Abfrage-Service unterstützt die Datendeduplizierung, wenn eine ganze Zeile aus einer Berechnung entfernt oder ein bestimmter Feldsatz ignoriert werden muss, da nur ein Teil der Daten in der Zeile doppelte Informationen enthält. Weitere Informationen finden Sie in der Dokumentation [Datendeduplizierung im Abfrage](../query-service/key-concepts/deduplication.md)Service).

>[!NOTE]
>
>Wenn Sie außerhalb der oben beschriebenen Anwendungsfälle Probleme mit der Duplizierung von Ereignissen haben, wenden Sie sich an Ihren Adobe-Support-Mitarbeiter und geben Sie detaillierte Informationen zu Ihrem Anwendungsfall an.
