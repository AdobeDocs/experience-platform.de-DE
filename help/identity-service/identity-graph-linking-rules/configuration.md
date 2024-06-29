---
title: Konfigurationshandbuch für Regeln zur Verknüpfung von Identitätsdiagrammen
description: Erfahren Sie mehr über die empfohlenen Schritte zur Implementierung Ihrer Daten mit Regelkonfigurationen für die Identitätsdiagrammzuordnung.
badge: Beta
source-git-commit: d8a36650b2cd3ec9683763f536ea5c2c2e27455c
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 5%

---

# Konfigurationshandbuch für Regeln zur Verknüpfung von Identitätsdiagrammen

Lesen Sie dieses Dokument, um eine schrittweise Anleitung zur Implementierung Ihrer Daten mit dem Adobe Experience Platform Identity-Dienst zu erhalten.

Schrittweise Anleitung:

1. [Erstellen der erforderlichen Identitäts-Namespaces](#namespace)
2. [Verwenden Sie das Tool zur Diagrammsimulation, um sich mit dem Identitätsoptimierungsalgorithmus vertraut zu machen.](#graph-simulation)
3. [Verwenden Sie das Tool für Identitätseinstellungen, um Ihre eindeutigen Namespaces zu bestimmen und die Prioritätseinstufung für Ihre Namespaces zu konfigurieren](#identity-settings)
4. [Erstellen eines Experience-Datenmodell (XDM)-Schemas](#schema)
5. [Erstellen eines Datensatzes](#dataset)
6. [Daten auf Experience Platform erfassen](#ingest)

## Voraussetzungen für die Implementierung

Bevor Sie beginnen können, müssen Sie zunächst sicherstellen, dass authentifizierte Ereignisse in Ihrem System immer eine Personenkennung enthalten.

<!-- ## Set permissions {#set-permissions}

The first step in the implementation process for Identity Service is to ensure that your Experience Platform account is added to a role that is provisioned with the necessary permissions. Your administrator can configure permissions for your account by navigating to the Permissions UI in Adobe Experience Cloud. From there, your account must be added to a role with the following permissions:

* manage-identity-settings
* view-identity-dashboard
* view-identity-simulation

For more information on permissions, read the [permissions guide](../../access-control/abac/ui/permissions.md). -->

## Erstellen Ihrer Identitäts-Namespaces {#namespace}

Wenn Ihre Daten dies erfordern, müssen Sie zunächst die entsprechenden Namespaces für Ihre Organisation erstellen. Anweisungen zum Erstellen eines benutzerdefinierten Namespace finden Sie im Handbuch unter [Erstellen eines benutzerdefinierten Namespace in der Benutzeroberfläche](../features/namespaces.md#create-custom-namespaces).

## Tool zur Diagrammsimulation verwenden {#graph-simulation}

Navigieren Sie dann zum [Tool zur Diagrammsimulation](./graph-simulation.md) im UI-Arbeitsbereich des Identity Service. Mit dem Simulationstool für Diagramme können Sie Identitätsdiagramme simulieren, die mit einer Vielzahl verschiedener eindeutiger Namespace- und Namespace-Prioritätskonfigurationen erstellt wurden.

Durch die Erstellung verschiedener Konfigurationen können Sie mit dem Tool für die Diagrammsimulation erfahren, wie der Identitätsoptimierungsalgorithmus und bestimmte Konfigurationen das Verhalten Ihres Diagramms beeinflussen können.

## Identitätseinstellungen konfigurieren {#identity-settings}

Sobald Sie eine bessere Vorstellung davon haben, wie sich Ihr Diagramm verhalten soll, navigieren Sie zum [Identitäts-Einstellungswerkzeug](./identity-settings-ui.md) im UI-Arbeitsbereich des Identity Service.

Verwenden Sie das Tool für Identitätseinstellungen, um Ihre eindeutigen Namespaces zu bestimmen und Ihre Namespaces nach Priorität zu konfigurieren. Sobald Sie mit der Anwendung Ihrer Einstellungen fertig sind, müssen Sie mindestens sechs Stunden warten, bis Sie mit der Datenerfassung fortfahren können, da es mindestens sechs Stunden dauert, bis neue Einstellungen in Identity Service angezeigt werden.

## Erstellen eines XDM-Schemas {#schema}

Nachdem Sie Ihre eindeutigen Namespaces und Namespace-Prioritäten festgelegt haben, können Sie jetzt mit der erforderlichen Einrichtung fortfahren, um Ihre Daten zu erfassen. Zunächst müssen Sie ein XDM-Schema erstellen. Abhängig von Ihren Daten müssen Sie möglicherweise ein Schema für sowohl XDM Individual Profile als auch XDM ExperienceEvent erstellen.

Um Daten in das Echtzeit-Kundenprofil zu erfassen, müssen Sie sicherstellen, dass Ihr Schema mindestens ein Feld enthält, das als primäre Identität ausgewiesen wurde. Durch Festlegen einer primären Identität können Sie ein bestimmtes Schema für die Profilerfassung aktivieren.

Anweisungen zum Erstellen eines Schemas finden Sie im Handbuch unter [Erstellen eines XDM-Schemas in der Benutzeroberfläche](../../xdm/tutorials/create-schema-ui.md).

## Erstellen eines Datensatzes {#dataset}

Erstellen Sie anschließend einen Datensatz, um eine Struktur für die Daten bereitzustellen, die Sie erfassen werden. Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Datensätze funktionieren gemeinsam mit Schemas und zur Aufnahme von Daten in das Echtzeit-Kundenprofil muss Ihr Datensatz für die Profilaufnahme aktiviert sein. Damit Ihr Datensatz für Profil aktiviert werden kann, muss er auf ein Schema verweisen, das für die Profilaufnahme aktiviert ist.

Anweisungen zum Erstellen eines Datensatzes finden Sie in der [Handbuch zur Datensatz-Benutzeroberfläche](../../catalog/datasets/user-guide.md).

## Daten erfassen {#ingest}

An dieser Stelle sollten Sie Folgendes haben:

* Die erforderlichen Berechtigungen für den Zugriff auf Identity Service-Funktionen.
* Namespaces für Ihre Daten.
* Ausgewählte eindeutige Namespaces und konfigurierte Prioritäten für Ihre Namespaces.
* Mindestens ein XDM-Schema. (Abhängig von Ihren Daten und Ihrem spezifischen Anwendungsfall müssen Sie möglicherweise sowohl Profil- als auch Erlebnisereignisschemas erstellen.)
* Ein Datensatz, der auf Ihrem Schema basiert.

Sobald Sie alle oben aufgelisteten Elemente haben, können Sie mit der Erfassung Ihrer Daten zu Experience Platform beginnen. Sie können die Datenerfassung auf verschiedene Arten durchführen. Sie können die folgenden Dienste verwenden, um Ihre Daten zum Experience Platform zu bringen:

* [Batch- und Streaming-Erfassung](../../ingestion/home.md)
* [Datenerfassung in Experience Platform](../../collection/home.md)
* [Experience Platform-Quellen](../../sources/home.md)

>[!TIP]
>
>Nach der Erfassung Ihrer Daten ändert sich die XDM-Rohdaten-Payload nicht mehr. Möglicherweise werden Ihre primären Identitätskonfigurationen weiterhin in der Benutzeroberfläche angezeigt. Diese Konfigurationen werden jedoch durch Identitätseinstellungen überschrieben.

Verwenden Sie für jedes Feedback die **[!UICONTROL Beta-Feedback]** in der Benutzeroberfläche des Identity Service-Arbeitsbereichs.