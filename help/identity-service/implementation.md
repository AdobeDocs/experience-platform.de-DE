---
title: Implementierungshandbuch für Identity Service
description: Erfahren Sie, wie an Adobe Experience Platform bereitgestellte Daten verarbeitet werden, bevor sie von Identity Service zum Erstellen von Identitätsdiagrammen verwendet werden.
source-git-commit: bdda234c44b63999d7582857975afa64fdb93605
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 66%

---

# Implementierungshandbuch für Identity Service

Dieses Dokument enthält Informationen dazu, wie an Adobe Experience Platform bereitgestellte Daten verarbeitet werden, bevor sie von Identity Service zum Erstellen eines Identitätsdiagramms für einen bestimmten Kunden verwendet werden.

## Identitätsfelder bestimmen

Je nach der Strategie Ihres Unternehmens zur Datenerfassung bestimmen die Datenfelder, die Sie als Identitäten kennzeichnen, darüber, welche Daten in Ihre Identitätszuordnung aufgenommen werden. Um den größtmöglichen Nutzen aus Experience Platform und den umfassendsten Kundenidentitäten zu ziehen, sollten Sie sowohl Online- als auch Offline-Daten hochladen.

* Online-Daten sind Daten, die die Präsenz und das Verhalten im Internet beschreiben, z. B. Benutzernamen und E-Mail-Adressen.

* Offline-Daten beziehen sich auf Daten, die nicht direkt mit einer Online-Präsenz zusammenhängen, wie z. B. Kennungen aus CRM-Systemen. Solche Daten macht Ihre Identitäten robuster und fördern die Kohärenz von Daten in verschiedenen Systemen.

## Zusätzliche Identitäts-Namespaces erstellen

Zwar bietet Experience Platform eine Vielzahl von Standard-Namespaces, doch müssen Sie möglicherweise zusätzliche Namespaces erstellen, um Ihre Identitäten korrekt zu kategorisieren. Weitere Informationen finden Sie im Handbuch unter [Erstellen benutzerdefinierter Namespaces für Ihre Organisation](./namespaces.md).

>[!NOTE]
>
>Identitäts-Namespaces sind ein Qualifizierer für Identitäten. Nachdem ein Namespace erstellt wurde, kann er daher nicht mehr gelöscht werden.

## Identitätsdaten in Experience-Datenmodell (XDM) einschließen

Als standardisiertes Framework, mit dem Experience Platform Kundendaten organisiert, ermöglicht das Experience-Datenmodell (XDM) die Freigabe und Verstehen von Daten über Experience Platform und andere Dienste hinweg, die mit Experience Platform interagieren. Weitere Informationen finden Sie unter [XDM-System - Übersicht](../xdm/home.md).

Sowohl Datensatz- als auch Zeitreihenschemas bieten die Möglichkeit, Identitätsdaten einzubeziehen. Beim Erfassen von Daten erstellt das Identitätsdiagramm neue Beziehungen zwischen Datenfragmenten aus verschiedenen Namespaces, wenn festgestellt wird, dass sie gemeinsame Identitätsdaten aufweisen.

## Beschriften von XDM-Feldern als Identität

Jedes Feld vom Typ `string` in Schemas, die XDM-Klassen für Datensätze oder Zeitreihen implementieren, kann als Identitätsfeld gekennzeichnet werden. In der Folge würden alle in diesem Feld erfassten Daten als Identitätsdaten betrachtet.

Identitätsfelder erlauben auch eine Verknüpfung von Identitäten, wenn diese gemeinsame personenbezogene Daten aufweisen.
Wenn Sie beispielsweise Telefonnummernfelder als Identitätsfelder kennzeichnen, stellt Identity Service die Beziehungen zu den anderen Personen, bei denen dieselbe Telefonnummer ermittelt wurde, automatisch grafisch dar.

>[!NOTE]
>
>* Felder vom Typ Array und Zuordnung werden nicht unterstützt und können nicht als Identitätsfelder markiert und gekennzeichnet werden.
>* Der Namespace der resultierenden Identitäten wird zum Zeitpunkt der Kennzeichnung des Felds bereitgestellt.

## Datensatz für Identity Service konfigurieren

Während der Streaming-Erfassung extrahiert Identity Service automatisch Identitätsdaten aus Datensatz- und Zeitreihendaten. Bevor Daten erfasst werden können, müssen sie jedoch für Identity Service aktiviert werden. Tutorial lesen unter  [Datensatz für Echtzeit-Kundenprofil und Identity Service mithilfe von APIs konfigurieren](../profile/tutorials/dataset-configuration.md) für weitere Informationen.

## Daten in Identity Service einbeziehen

Identity Service nutzt XDM-konforme Daten, die entweder von an Experience Platform gesendet werden [Batch-Erfassung](../ingestion/batch-ingestion/overview.md) oder [Streaming-Erfassung](../ingestion/streaming-ingestion/overview.md).

Das folgende Video soll Ihnen das Verständnis für Identity Service erleichtern. In diesem Video erfahren Sie, wie Sie Datenfelder als Identitäten kennzeichnen, Identitätsdaten aufnehmen und dann überprüfen, ob die Daten in das private Diagramm von Adobe Experience Platform Identity Service gelangt sind.

>[!WARNING]
>
>Die im folgenden Video dargestellte Experience Platform-Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)