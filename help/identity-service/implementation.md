---
title: Implementierungshandbuch für Identity Service
description: Erfahren Sie, wie an Adobe Experience Platform bereitgestellte Daten verarbeitet werden, bevor sie von Identity Service zum Erstellen von Identitätsdiagrammen verwendet werden.
exl-id: c961bbf6-6b46-470f-a671-93ff4173876c
source-git-commit: 4ba25ed684ff126ab1c4f1a33e6503f0342e8720
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 62%

---

# Implementierungshandbuch für Identity Service

In diesem Dokument erfahren Sie, wie an Adobe Experience Platform bereitgestellte Daten verarbeitet werden, bevor sie vom Identity Service zum Erstellen eines Identitätsdiagramms für einen bestimmten Kunden verwendet werden.

## Identitätsfelder bestimmen

Je nach der Strategie Ihres Unternehmens zur Datenerfassung bestimmen die Datenfelder, die Sie als Identitäten kennzeichnen, darüber, welche Daten in Ihre Identitätszuordnung aufgenommen werden. Um den größtmöglichen Nutzen aus dem Experience Platform und einer möglichst umfassenden Kundenidentität zu ziehen, sollten Sie sowohl Online- als auch Offline-Daten hochladen.

* Online-Daten sind Daten, die die Präsenz und das Verhalten im Internet beschreiben, z. B. Benutzernamen und E-Mail-Adressen.

* Offline-Daten beziehen sich auf Daten, die nicht direkt mit einer Online-Präsenz zusammenhängen, wie z. B. Kennungen aus CRM-Systemen. Solche Daten macht Ihre Identitäten robuster und fördern die Kohärenz von Daten in verschiedenen Systemen.

## Zusätzliche Identitäts-Namespaces erstellen

Zwar bietet Experience Platform eine Vielzahl von Standard-Namespaces, doch müssen Sie möglicherweise zusätzliche Namespaces erstellen, um Ihre Identitäten korrekt zu kategorisieren. Weitere Informationen finden Sie im Handbuch unter [Erstellen benutzerdefinierter Namespaces für Ihre Organisation](./features/namespaces.md).

>[!NOTE]
>
>Identitäts-Namespaces sind ein Qualifizierer für Identitäten. Nachdem ein Namespace erstellt wurde, kann er daher nicht mehr gelöscht werden.

## Identitätsdaten in Experience-Datenmodell (XDM) einschließen

Als standardisiertes Framework, mit dem Experience Platform Kundendaten organisiert, ermöglicht das Experience-Datenmodell (XDM) das Teilen und Verstehen von Daten über Experience Platform und andere Services hinweg, die mit Experience Platform interagieren. Weitere Informationen finden Sie unter [XDM-System - Übersicht](../xdm/home.md).

Sowohl Datensatz- als auch Zeitreihenschemata bieten die Möglichkeit, Identitätsdaten einzubeziehen. Beim Erfassen von Daten erstellt das Identitätsdiagramm neue Beziehungen zwischen Datenfragmenten aus verschiedenen Namespaces, wenn festgestellt wird, dass sie gemeinsame Identitätsdaten aufweisen.

## Kennzeichnen von XDM-Feldern als Identität

Jedes Feld vom Typ `string` in Schemata, die XDM-Klassen für Datensätze oder Zeitreihen implementieren, kann als Identitätsfeld gekennzeichnet werden. In der Folge würden alle in diesem Feld erfassten Daten als Identitätsdaten betrachtet.

Identitätsfelder erlauben auch eine Verknüpfung von Identitäten, wenn diese gemeinsame personenbezogene Daten aufweisen.
Wenn Sie beispielsweise Telefonnummernfelder als Identitätsfelder kennzeichnen, stellt Identity Service die Beziehungen zu den anderen Personen, bei denen dieselbe Telefonnummer ermittelt wurde, automatisch grafisch dar.

>[!NOTE]
>
>* Felder vom Typ Array und Zuordnung werden nicht unterstützt und können nicht als Identitätsfelder markiert und gekennzeichnet werden.
>* Der Namespace der resultierenden Identitäten wird zum Zeitpunkt der Kennzeichnung des Felds bereitgestellt.
>* Ein Feld kann als Identität markiert werden, solange sich dieses Feld nicht unter einem Array-Objekt befindet.

Weitere Informationen finden sich im Handbuch unter [Definieren von Identitätsfeldern in der Benutzeroberfläche](../xdm/ui/fields/identity.md).

## Datensatz für Identity Service konfigurieren

Während der Streaming-Erfassung extrahiert Identity Service automatisch Identitätsdaten aus Datensatz- und Zeitreihendaten. Bevor Daten erfasst werden können, müssen sie jedoch für Identity Service aktiviert werden. Lesen Sie das Tutorial unter [Konfigurieren eines Datensatzes für Echtzeit-Kundenprofil und Identity Service mit APIs](../profile/tutorials/dataset-configuration.md) für weitere Informationen.

## Daten in Identity Service einbeziehen

Identity Service nutzt XDM-konforme Daten, die entweder per [Batch-Aufnahme](../ingestion/batch-ingestion/overview.md) oder [Streaming-Aufnahme](../ingestion/streaming-ingestion/overview.md) an Experience Platform gesendet werden.

Das folgende Video soll Ihnen das Verständnis für Identity Service erleichtern. In diesem Video erfahren Sie, wie Sie Datenfelder als Identitäten kennzeichnen, Identitätsdaten aufnehmen und dann überprüfen, ob die Daten in das private Diagramm von Adobe Experience Platform Identity Service gelangt sind.

>[!WARNING]
>
>Die im folgenden Video angezeigte Experience Platform-Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)
