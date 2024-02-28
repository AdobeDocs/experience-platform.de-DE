---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Handbuch zur Richtlinien-Service-API
description: Die Richtlinien-Service-API ermöglicht es Entwicklern, Datennutzungskennzeichnungen und -richtlinien in Experience Platform zu verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
role: Developer
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 100%

---

# [!DNL Policy Service]-API-Handbuch

Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, beispielsweise bei der Katalogisierung, bei der Ermittlung der Datenherkunft, bei Datennutzungskennzeichnungen, bei Datennutzungsrichtlinien und bei der Steuerung der Nutzung von Daten für Marketing-Aktionen.

Die [!DNL Policy Service]-API bietet mehrere Endpunkte, mit denen Sie Datennutzungskennzeichnungen und -richtlinien programmgesteuert verwalten und Marketing-Aktionen für Richtlinienverletzungen auswerten können. Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge zu sehen, besuchen Sie den [[!DNL Policy Service] API-Swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Beschriftungen

Wenden Sie Datennutzungskennzeichnungen auf Schemata an, um Datensätze und Felder anhand der für diese Daten geltenden Nutzungsrichtlinien zu kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in [!DNL Experience Platform] oder ab dem Zeitpunkt ihrer Nutzbarkeit in [!DNL Platform] mit einer Kennzeichnung zu versehen. Sie können Kennzeichnungen mit dem Endpunkt `/labels` erstellen, ansehen, bearbeiten und löschen. Informationen zur Verwendung dieses Endpunkts finden Sie im [Kennzeichnungsendpunkt-Handbuch](./labels.md).

## Marketing-Aktionen

Marketing-Aktionen (auch als Marketing-Anwendungsfälle bezeichnet) im Rahmen des Data Governance-Frameworks sind Maßnahmen, die ein [!DNL Experience Platform]-Datenbenutzer ausführen kann und die Ihr Unternehmen in Bezug auf die Datennutzung möglicherweise einschränken möchte. Ausführliche Informationen zum Arbeiten mit Marketing-Aktionen finden Sie im [Endpunkthandbuch zu Marketing-Aktionen](./marketing-actions.md).

## Richtlinien

Data-Governance-Richtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, welche Sie mit Daten innerhalb von [!DNL Experience Platform] durchführen dürfen bzw. nicht durchführen dürfen.

>[!NOTE]
>
>Data-Governance-Richtlinien sind nicht zu verwechseln mit Zugriffssteuerungsrichtlinien, die die spezifischen Datenattribute festlegen, auf die bestimmte Benutzende von Platform in Ihrer Organisation zugreifen können. Weitere Informationen finden Sie im Handbuch zur [attributbasierten Zugriffssteuerung](../../access-control/abac/overview.md).

Eine Data-Governance-Richtlinie ist durch Folgendes definiert:

1. Eine bestimmte Marketing-Aktion
1. Die Datennutzungsbeschriftung(en), für die diese Aktion nicht ausgeführt werden darf

Informationen zum Verwalten von Richtlinien in der API finden Sie im [Handbuch zu Richtlinienendpunkten](./policies.md)

## Auswertung

Sobald Datennutzungskennzeichnungen auf Platform-Schemata angewendet und Datennutzungsrichtlinien entsprechend für Marketing-Aktionen definiert wurden, können Sie diese Richtlinien mithilfe von Data-Governance-Funktionen durchsetzen und Datenvorgänge verhindern, bei denen die Richtlinien verletzt werden.

Die [!DNL Policy Service]-API stellt Endpunkte bereit, mit denen Sie Marketing-Aktionen für Datensätze oder beliebige Kombinationen von Datennutzungskennzeichnungen testen können, um festzustellen, ob Richtlinien verletzt werden. Je nach API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung von Datennutzungsrichtlinien richtig durchzusetzen. Weiterführende Informationen dazu finden Sie im [Handbuch zu Auswertungsendpunkten](./evaluation.md).

## Nächste Schritte

Um mit Aufrufen mit der [!DNL Policy Service]-API zu beginnen, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) und wählen Sie dann eins der Endpunkthandbücher aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden. Informationen zum Arbeiten mit Kennzeichnungen und Richtlinien über die Benutzeroberfläche von [!DNL Experience Platform] finden Sie im [Benutzerhandbuch zu Kennzeichnungen](../labels/user-guide.md) und im [Benutzerhandbuch zu Richtlinien](../policies/user-guide.md).
