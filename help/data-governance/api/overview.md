---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Handbuch zur Richtlinien-Service-API
topic-legacy: developer guide
description: Die Richtlinien-Service-API ermöglicht es Entwicklern, Datennutzungskennzeichnungen und -richtlinien in Experience Platform zu verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: ht
source-wordcount: '500'
ht-degree: 100%

---

# [!DNL Policy Service]-API-Handbuch

Mit Adobe Experience Platform [!DNL Data Governance] können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von relevanten Vorschriften, Einschränkungen und Richtlinien sicherstellen. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, beispielsweise bei der Katalogisierung, bei der Ermittlung der Datenherkunft, bei Datennutzungskennzeichnungen, bei Datennutzungsrichtlinien und bei der Steuerung der Nutzung von Daten für Marketing-Aktionen.

Die [!DNL Policy Service]-API bietet mehrere Endpunkte, mit denen Sie Datennutzungskennzeichnungen und -richtlinien programmgesteuert verwalten und Marketing-Aktionen für Richtlinienverletzungen auswerten können. Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge zu sehen, besuchen Sie den [[!DNL Policy Service] API-Swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Beschriftungen

Mit Datennutzungsbeschriftungen können Sie Datensätze anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in [!DNL Experience Platform] oder ab dem Zeitpunkt ihrer Nutzbarkeit in [!DNL Platform] mit einer Kennzeichnung zu versehen. Sie können Kennzeichnungen mit dem Endpunkt `/labels` erstellen, ansehen, bearbeiten und löschen. Informationen zur Verwendung dieses Endpunkts finden Sie im [Kennzeichnungsendpunkt-Handbuch](./labels.md).

## Marketing-Aktionen

Marketing-Aktionen (auch als Marketing-Anwendungsfälle bezeichnet) im Kontext des [!DNL Data Governance]-Frameworks sind Aktionen, die ein [!DNL Experience Platform]-Datenbenutzer ausführen kann und für die Ihr Unternehmen die Datennutzung einschränken möchte. Ausführliche Informationen zum Arbeiten mit Marketing-Aktionen finden Sie im [Endpunkthandbuch zu Marketing-Aktionen](./marketing-actions.md).

## Richtlinien

Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in [!DNL Experience Platform] ausführen bzw. nicht ausführen dürfen. Eine Richtlinie wird wie folgt definiert:

1. Eine bestimmte Marketing-Aktion
1. Die Datennutzungsbeschriftung(en), für die diese Aktion nicht ausgeführt werden darf

Informationen zum Verwalten von Richtlinien in der API finden Sie im [Handbuch zu Richtlinienendpunkten](./policies.md)

## Auswertung

Sobald Datennutzungskennzeichnungen auf [!DNL Platform]-Datensätze angewendet und somit Datennutzungsrichtlinien für Marketing-Aktionen mit diesen Kennzeichnungen definiert wurden, können Sie die Richtlinien mithilfe von Data-Governance-Funktionen durchsetzen und Datenvorgänge verhindern, bei denen Richtlinien verletzt werden.

Die [!DNL Policy Service]-API stellt Endpunkte bereit, mit denen Sie Marketing-Aktionen für Datensätze oder beliebige Kombinationen von Datennutzungskennzeichnungen testen können, um festzustellen, ob Richtlinien verletzt werden. Je nach API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung von Datennutzungsrichtlinien richtig durchzusetzen. Weiterführende Informationen dazu finden Sie im [Handbuch zu Bewertungsendpunkten](./evaluation.md).

## Nächste Schritte

Um mit Aufrufen mit der [!DNL Policy Service]-API zu beginnen, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) und wählen Sie dann eins der Endpunkthandbücher aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden. Informationen zum Arbeiten mit Kennzeichnungen und Richtlinien über die Benutzeroberfläche von [!DNL Experience Platform] finden Sie im [Benutzerhandbuch zu Kennzeichnungen](../labels/user-guide.md) und im [Benutzerhandbuch zu Richtlinien](../policies/user-guide.md).
