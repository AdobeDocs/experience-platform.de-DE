---
title: Übersicht über Datenströme
description: Erfahren Sie, wie Sie mithilfe von Datenströmen Ihre Client-seitige Experience Platform SDK-Integration mit Adobe-Produkten und Zielen von Drittanbietern verbinden können.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 79d724eec4903b8a3eee6f717d94fcd70a4ffcb7
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 48%

---

# Übersicht über Datenströme

Ein Datenstrom stellt die Server-seitige Konfiguration für die [!DNL Adobe Experience Platform] Web- und Mobile-SDKs dar. Während Client-seitige Einstellungen (z. B. die `edgeDomain`) mit dem [`configure`](/help/collection/js/commands/configure/overview.md)-Befehl in der SDK verarbeitet werden, verwalten Datenströme alle anderen Konfigurationen.

Wenn Sie eine Anfrage an die [!DNL Edge Network] senden, verweist die `datastreamId` auf den Datenstrom, an den die Daten gesendet werden. Sie können die Server-seitige Konfiguration aktualisieren, ohne den Code Ihrer Website zu ändern.

Sie können Datenströme erstellen und verwalten, indem Sie im linken Navigationsbereich der [!DNL Adobe Experience Platform]-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche **[!UICONTROL Datastreams]** auswählen.

![Screenshot der Registerkarte „Datenströme“ in der Adobe Experience Platform-Benutzeroberfläche.](assets/overview/datastreams-tab.png)

Weitere Informationen zum Konfigurieren eines Datenstroms in der Benutzeroberfläche finden Sie im [Konfigurationshandbuch](/help/datastreams/configure.md).

## Handhabung sensibler Daten in Datenströmen {#sensitive}

>[!IMPORTANT]
>
>Der Inhalt dieses Dokuments ist keine Rechtsberatung und soll keine Rechtsberatung ersetzen. Wenden Sie sich an die Rechtsabteilung Ihres Unternehmens, um sich über den Umgang mit sensiblen Daten zu beraten.

Unternehmensrichtlinien zur Datenverwaltung und gesetzliche Vorschriften schränken die Erfassung, Verarbeitung und Nutzung sensibler Kundendaten zunehmend ein. Dazu gehört die Erfassung, Verarbeitung und Nutzung geschützter Gesundheitsdaten (PHI), die Vorschriften wie dem Health Insurance Portability and Accountability Act (HIPAA) unterliegen.

Datenströme bieten drei Methoden, mit denen Sie Ihre sensiblen Daten sicher verarbeiten können:

* [Verbesserte Verschlüsselung](#encryption)
* [Data Governance](#governance)
* [Auditprotokolle](#audit-logs)

### Verbesserte Verschlüsselung {#encryption}

Alle Daten, die über die [!DNL Edge Network] übertragen werden, werden über sichere, verschlüsselte Verbindungen mit ([&#x200B; TLS 1.2) &#x200B;](https://datatracker.ietf.org/doc/html/rfc5246). Wenn der Datenstrom Daten in Experience Platform einbringt, werden die Daten im Ruhezustand im Experience Platform Data Lake verschlüsselt. Weitere Informationen finden Sie im Dokument über [Datenverschlüsselung in Experience Platform](/help/landing/governance-privacy-security/encryption.md).

### Data Governance {#governance}

Datenströme verwenden die integrierten Data Governance-Funktionen von Experience Platform, um zu verhindern, dass sensible Daten an nicht HIPAA-fähige Services gesendet werden. Durch die Kennzeichnung bestimmter Felder, die sensible Daten in Ihren Datenstromschemata enthalten, können Sie genau steuern, welche Datenfelder für bestimmte Zwecke verwendet werden können.

Das folgende Video bietet einen kurzen Überblick darüber, wie Datennutzungsbeschränkungen für Datenspeicher in der Benutzeroberfläche konfiguriert und durchgesetzt werden:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

In Experience Platform können Sie [sensible Datennutzungs-Labels](/help/data-governance/labels/reference.md#sensitive) auf Schemata und Felder anwenden, die Daten enthalten, welche Ihr Unternehmen als sensibel einstuft. So wird beispielsweise das Label `RHD` für geschützte Gesundheitsinformationen (PHI) verwendet, und das Label `S1` steht für Geolokalisierungsdaten.

>[!NOTE]
>
>Weitere Informationen zum Anwenden von Datennutzungskennzeichnungen auf der Registerkarte &quot;[!UICONTROL Schemas]&quot; in der Experience Platform-Benutzeroberfläche oder Datenerfassungs-Benutzeroberfläche finden Sie im [Tutorial zu Schemakennzeichnungen](/help/xdm/tutorials/labels.md).

Wenn Sie beim Erstellen eines Datenstroms das ausgewählte Schema vertrauliche Datennutzungskennzeichnungen enthält, können Sie den Datenstrom nur so konfigurieren, dass diese Daten an HIPAA-fähige Ziele gesendet werden. Derzeit ist das einzige HIPAA-fähige Ziel, das von Datenströmen unterstützt wird, [!DNL Adobe Experience Platform]. Andere Ziel-Services, einschließlich [!DNL Adobe Target]-, [!DNL Adobe Analytics]-, [!DNL Adobe Audience Manager]-, Ereignisweiterleitungs- und Edge-Zielen, sind für Datenströme mit sensiblen Datennutzungskennzeichnungen deaktiviert.

Wenn ein Schema in einem vorhandenen Datenstrom mit nicht HIPAA-fähigen Diensten verwendet wird, führt der Versuch, dem Schema ein sensibles Datennutzungs-Label hinzuzufügen, zu einer Richtlinienverletzungsmeldung und die Aktion wird verhindert. Die Meldung gibt an, welcher Datenstrom die Verletzung ausgelöst hat, und schlägt vor, alle nicht HIPAA-fähigen Services aus dem Datenstrom zu entfernen, um das Problem zu beheben.

### Auditprotokolle {#audit-logs}

In Experience Platform können Datenstrom-Aktivitäten in Form von Administratorprotokollen überwacht werden. Audit-Protokolle geben an **wer** welche **ausgeführt** und **wann** sowie andere kontextuelle Daten, mit denen Sie Probleme im Zusammenhang mit Datenströmen beheben können, damit Ihr Unternehmen die Richtlinien zur Unternehmensdatenverwaltung und die gesetzlichen Anforderungen erfüllen kann.

Jedes Mal, wenn eine Benutzerin oder ein Benutzer einen Datenstrom erstellt, aktualisiert oder löscht, wird ein Administratorprotokoll erstellt, um die Aktion aufzuzeichnen. Dasselbe erfolgt, wenn jemand über die [Datenvorbereitung für die Datenerfassung](/help/datastreams/data-prep.md) eine Zuordnung erstellt, aktualisiert oder löscht. Unabhängig davon, ob es sich um einen Datenstrom oder eine Zuordnung handelte, die aktualisiert wurde, wird das resultierende Auditprotokoll unter dem [!UICONTROL Datastreams] Ressourcentyp kategorisiert.

Weitere Informationen zur Interpretation von Protokollen aus Datenströmen und anderen unterstützten Diensten finden Sie in der Dokumentation zu [Administratorprotokollen](/help/landing/governance-privacy-security/audit-logs/overview.md).

## Nächste Schritte {#next-steps}

Dieses Handbuch bietet einen allgemeinen Überblick über Datenströme und deren Verwendung bei der Datenerfassung und der Verarbeitung sensibler Daten. Wie Sie einen neuen Datenstrom einrichten, erfahren Sie im [Handbuch zur Konfiguration von Datenströmen](/help/datastreams/configure.md).
