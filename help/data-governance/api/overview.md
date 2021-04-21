---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Handbuch zur Policy Service API
topic-legacy: developer guide
description: Die Policy-Service-API ermöglicht es Entwicklern, Datenverwendungsbeschriftungen und -richtlinien in der Experience Platform zu verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 14%

---

# [!DNL Policy Service] API-Handbuch

Mit Adobe Experience Platform [!DNL Data Governance] können Sie Kundendaten verwalten und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sicherstellen. Es spielt eine Schlüsselrolle innerhalb von [!DNL Experience Platform] auf verschiedenen Ebenen, einschließlich Katalogisierung, Datenbindung, Datenverwendungsbeschriftung, Datenverwendungsrichtlinien und Steuerung der Verwendung von Daten für Marketingaktionen.

Die [!DNL Policy Service]-API bietet mehrere Endpunkte, mit denen Sie Datenverwendungsbeschriftungen und -richtlinien programmgesteuert verwalten und Marketingaktionen für Richtlinienverletzungen auswerten können. Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern.[](./getting-started.md)

Um alle verfügbaren Endpunkte und CRUD-Vorgänge Ansicht, besuchen Sie den [[!DNL Policy Service] API-Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Bezeichnungen

Mit Datennutzungsbeschriftungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Bewährte Verfahren fördern die Kennzeichnung von Daten, sobald diese in [!DNL Experience Platform] aufgenommen werden oder sobald Daten für die Verwendung in [!DNL Platform] verfügbar sind. Sie können Beschriftungen mit dem Endpunkt `/labels` erstellen, Ansicht, bearbeiten und löschen. Informationen zur Verwendung dieses Endpunkts finden Sie im Endpunktleitfaden [label](./labels.md).

## Marketing-Aktionen

Marketingaktionen (auch als Marketing-Anwendungsfälle bezeichnet) im Kontext des [!DNL Data Governance]-Frameworks sind Aktionen, die ein [!DNL Experience Platform]-Datenbenutzer ausführen kann und für die Ihr Unternehmen die Datenverwendung einschränken möchte. Ausführliche Informationen zum Arbeiten mit Marketingaktionen finden Sie im [Endpunkthandbuch zu Marketingaktionen](./marketing-actions.md).

## Richtlinien

Datenverwendungsrichtlinien sind Regeln, die die Arten von Marketingaktionen beschreiben, von denen Sie Daten innerhalb von [!DNL Experience Platform] ausführen dürfen oder von denen Sie eingeschränkt sind. Eine Richtlinie wird wie folgt definiert:

1. Eine bestimmte Marketingaktion
1. Die Datenverwendungs-Beschriftungen, die für diese Aktion eingeschränkt sind, gegen

Informationen zum Verwalten von Richtlinien in der API finden Sie im [policies endpoint guide](./policies.md)

## Auswertung

Sobald Datenverwendungsbezeichnungen auf [!DNL Platform]-Datensätze angewendet wurden und für Marketingaktionen mit diesen Bezeichnungen Datenverwendungsrichtlinien definiert wurden, können Sie mit den Datenverwaltungsfunktionen diese Richtlinien durchsetzen und Datenoperationen verhindern, die Richtlinienverletzungen darstellen.

Die [!DNL Policy Service]-API stellt Endpunkte bereit, mit denen Sie Marketingaktionen gegen Datasets oder beliebige Kombinationen von Datenverwendungsbeschriftungen testen können, um festzustellen, ob Richtlinienverletzungen auftreten. Je nach API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung von Datennutzungsrichtlinien richtig durchzusetzen. Weitere Informationen finden Sie im Leitfaden [Testendpunkte](./evaluation.md).

## Nächste Schritte

Um mit dem Aufrufen der API zu beginnen, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) und wählen Sie dann eine der Endpunktleitfäden aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden. [!DNL Policy Service] Informationen zum Arbeiten mit Beschriftungen und Richtlinien mithilfe der [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Benutzerhandbuch für Beschriftungen](../labels/user-guide.md) bzw. [Richtlinien-Benutzerhandbuch](../policies/user-guide.md).
