---
title: Eigenschaften
description: Erfahren Sie, wie Erweiterungen, Umgebung und Bibliotheken für Ihr Unternehmen in Adobe Experience Platform organisiert und gruppiert werden.
exl-id: e5b4a853-c23e-498c-9e20-e773ea1de88b
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 97%

---

# Eigenschaften

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

## Web-Eigenschaften

Eine Web-Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Jede Web-Eigenschaft verfügt über einen eigenen Satz von Einbettungs-Codes und kann auf beliebig vielen verschiedenen Websites (verschiedene Domains) bereitgestellt werden.

## Mobile-Eigenschaften

Mobile-Eigenschaften können mehrere Anwendungen enthalten. In einer Mobile-Eigenschaft können Sie beispielsweise dieselben Regeln und Erweiterungen für mehrere iOS- und Android-Mobile-Apps verwalten.

## Best Practices für die Planung von Eigenschaften {#best-practices-for-planning-properties}

Tag-Implementierungen in Adobe Experience Platform können sehr unterschiedlich sein. Sie haben verschiedensten Anforderungen bezüglich Datenerfassung, Variablennutzung, Erweiterungen, Drittanbieter-Tags, anderer Systeme und Technologien, Personen, Teams, geografischer Regionen usw. Sie sollten Ihre Eigenschaften so strukturieren, dass sie dem Workflow und den Prozessen Ihres Unternehmens entsprechen.

Beachten Sie bei der Planung von Eigenschaften Folgendes:

* Code-Struktur
* Daten
* Variablen
* Erweiterungen, Tags und Systeme
* „Personen“

### Code-Struktur

Sites basieren auf HTML, Apps auf Code. Wenn die zugrunde liegenden HTML-Vorlagen oder Code-Basen für mehrere Sites und Programme gleich sind, sollten Sie in Erwägung ziehen, mehrere Sites oder Programme mit einer einzigen Tag-Eigenschaft zu verwalten.

### Daten

Sind die Daten, die Sie für alle Ihre Websites oder Anwendungen erfassen möchten, sehr ähnlich, in gewissem Maße ähnlich oder komplett verschieden?

Wenn die Daten, die Sie erfassen müssen, ähnlich sind, kann es sinnvoll sein, diese Websites oder Anwendungen in einer Eigenschaft zu gruppieren, um die Duplizierung von Regeln und das Kopieren von Regeln von einer Eigenschaft zur nächsten zu vermeiden.

Wenn Sie für jede Website oder jedes Programm komplett verschiedene Daten erfassen müssen, kann es sinnvoll sein, sie in eigene Eigenschaften zu unterteilen. Mit dieser Methode können Sie die Datenerfassung präziser steuern, ohne Unmengen von Bedingungslogik in benutzerdefinierten Skripten zu verwenden.

### Variablen

Sind die Variablen, die Sie in Ihrer [!DNL Analytics]- und anderen Erweiterungen einrichten werden, sehr ähnlich, in gewissem Maße ähnlich oder komplett verschieden?

Wenn beispielsweise über all Ihre Websites und Anwendungen hinweg eVar27 für denselben Quellenwert verwendet wird, kann es sinnvoll sein, diese Sites oder Anwendungen zu gruppieren, sodass Sie diese gemeinsamen Variablen in nur einer Eigenschaft festlegen können.

### Erweiterungen, Tags und Systeme

Sind die Erweiterungen, Tags und Systeme, die Sie bereitstellen werden, sehr ähnlich, in gewissem Maße ähnlich oder komplett verschieden?

Wenn sich die Erweiterungen, Tags und Systeme, die Sie bereitstellen, sehr ähnlich sind, empfiehlt es sich möglicherweise, sie derselben Eigenschaft hinzuzufügen.

Wenn Sie [!DNL Adobe Analytics] nur auf einer Website oder in einer Anwendung bereitstellen und Ihre anderen Erweiterungen und Tags ebenfalls eindeutig sind, empfiehlt es sich möglicherweise, separate Eigenschaften zu erstellen, um mehr Kontrolle zu erhalten.

Wenn Sie z. B. [!DNL Adobe Analytics], [!DNL Target] sowie dieselben Drittanbietererweiterungen für alle Ihre Sites oder Anwendungen bereitstellen, ist das ein guter Grund für eine Gruppierung.

### „Personen“

Benötigen die Personen, Teams und Organisationen, die in Adobe Experience Platform arbeiten, Zugriff auf all Ihre Websites und Programme, auf einige oder nur auf eine(s)?

Mit der User-Management-Funktion können Sie verschiedenen Personen unterschiedliche Rollen zuweisen – entweder für alle oder für einzelne Properties. Wenn jemand über ausreichende Rechte verfügt, kann diese Person administrative Aktionen für alle Eigenschaften in dieser Platform-Organisation durchführen. Alle anderen Rollen können pro Eigenschaft zugewiesen werden. Sie können eine Eigenschaft sogar für bestimmte Benutzer (nicht Administratoren) ausblenden, indem Sie ihnen in der betreffenden Eigenschaft keine Rolle zuweisen.

## Eigenschaften-Seite

Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Bei Web-Eigenschaften gibt es nur einen Einbettungs-Code für die Veröffentlichung. Bei Mobile gibt es eine Konfigurations-App-ID pro Eigenschaften.

Es kann sich bei einer Eigenschaft um eine beliebige Gruppierung einer oder mehrerer Domains bzw. Subdomains handeln. Sie können diese Assets auf ähnliche Weise verwalten und verfolgen. Angenommen, Sie haben mehrere Websites, die auf einer Vorlage basieren, und Sie möchten auf all diesen Websites dieselben Assets verfolgen. Sie können eine Eigenschaft auf mehrere Domains anwenden.

Auf der linken Seite des Bildschirms werden die Unternehmen Ihrer Organisation angezeigt. Dies ist besonders hilfreich, wenn Sie mehrere Konten verwalten. Wählen Sie ein Unternehmen aus, um die Eigenschaften und Audit-Protokolle für dieses Unternehmen anzuzeigen.

Jede Eigenschaft wird in der Liste „Eigenschaften“ angezeigt.

Diese Liste enthält folgende Informationen:

* Eigenschaftsname
* Plattform
* Status

Klicken Sie auf eine Eigenschaft, um eine Übersicht über diese zu erhalten. Die Übersicht zeigt alle Aktivitäten an, die für die Eigenschaft durchgeführt wurden. Außerdem werden die Metriken und Erweiterungen für die Eigenschaft aufgeführt.

## Erstellen und Konfigurieren von Eigenschaften

Dieser Abschnitt enthält Anleitungen zum Erstellen oder Konfigurieren einer Tag-Eigenschaft in Adobe Experience Platform.

>[!NOTE]
>
>Nur Benutzer mit ausreichenden Rechten können eine Eigenschaft erstellen. Siehe [User Management](user-permissions.md).

Bevor Sie beginnen, lesen Sie zunächst den Abschnitt [Best Practices für die Planung von Eigenschaften](companies-and-properties.md#best-practices-for-planning-properties).

Navigieren Sie zu Ihrer Firmenseite und klicken Sie auf **[!UICONTROL Eigenschaft hinzufügen]**, oder wählen Sie eine vorhandene Eigenschaft aus der Liste aus und klicken Sie auf **[!UICONTROL Konfigurieren]**.

![](../../images/property-settings.png)

### Bei Web-Properties

Befolgen Sie die Anweisungen zum Erstellen einer Web-Eigenschaft.

1. Füllen Sie die Felder aus:

   **Name:** Der Name Ihrer Eigenschaft.

   **Domains:** Die Basis-URL aller Sites, für die Sie diese Eigenschaft bereitstellen möchten.

1. (Erweitert) **[!UICONTROL Regelkomponenten nacheinander ausführen]**: Aktivieren Sie dieses Kontrollkästchen, damit Bedingungen und Aktionen vor der Ausführung auf den Abschluss der vorherigen Aktion warten.
1. (Erweitert) **[!UICONTROL Geben Sie eine leere Zeichenfolge für fehlende Datenelemente zurück:]** Wenn Sie auf ein Datenelement verweisen, das nicht in einer Bibliothek vorhanden ist, wird normalerweise `undefined` zurückgegeben. Aktivieren Sie dieses Kontrollkästchen, wenn bei diesem Szenario stattdessen eine leere Zeichenfolge zurückgegeben werden soll.
1. (Erweitert) **[!UICONTROL Für die Entwicklung von Erweiterungen konfigurieren:]** Aktivieren Sie dieses Kontrollkästchen, wenn Sie Entwicklungserweiterungen installieren möchten, die aktiv von Ihrem Unternehmen entwickelt werden.
1. Wählen Sie **[!UICONTROL Speichern]** aus.

### Bei mobilen Properties

Befolgen Sie die Anweisungen zum Erstellen einer Mobile-Eigenschaft.

1. Füllen Sie die Felder aus:

   * **Name:** Der Name Ihrer Eigenschaft.
   * **Datenschutz:** Standardmäßig ist die Datenschutzeinstellung aktiviert, d. h., das SDK soll Daten erfassen und an Lösungen senden. Wenn Sie sie deaktivieren, sendet das SDK standardmäßig KEINE Daten an Lösungen. Wenn Sie als Einstellung „Unbekannt“ auswählen, verlangt das SDK, dass das Programm zunächst die Einwilligung des Benutzers zur Datenerfassung und -freigabe einholt.

      >[!NOTE]
      >
      >In der Mobile App können Sie mittels API zusätzliche Steuerungen für diese Einstellungen einrichten.

   * **HTTPS verwenden:** Wählen Sie aus, ob die gesamte Datenkommunikation über HTTP oder HTTPS gesendet werden soll.

1. Wählen Sie **[!UICONTROL Speichern]** aus.

Nachdem Sie die Eigenschaft erstellt haben, fügt Platform automatisch einen Standard-Host, die nötigen Umgebungen (Entwicklung, Staging und Produktion) sowie die Standarderweiterungen hinzu.

## Löschen von Properties

Gehen Sie wie folgt vor, um eine Tag-Eigenschaft zu löschen.

>[!NOTE]
>
>Das Löschen von Eigenschaften kann nicht rückgängig gemacht werden. Der Anfragende muss ein Benutzer auf Administratorebene sein. Diese Anfrage kann nicht rückgängig gemacht werden.

1. Wählen Sie in der Liste „Eigenschaften“ die zu löschende Eigenschaft aus.

   Sie können mehrere Eigenschaften zum Löschen auswählen.

1. Klicken Sie auf **[!UICONTROL Löschen]** und bestätigen Sie, dass Sie die Eigenschaft löschen möchten.
