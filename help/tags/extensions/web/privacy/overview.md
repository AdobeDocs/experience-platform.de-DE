---
title: Adobe-Datenschutzerweiterung – Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Adobe Privacy“ in Adobe Experience Platform vertraut.
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: 285e7ff1a1cd6c9790c526ca27ffafc60e94218d
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 11%

---

# Adobe-Datenschutzerweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Mit der Datenschutz-Tag-Erweiterung der Adobe können Sie Benutzer-IDs erfassen und entfernen, die Endbenutzern von Adobe-Lösungen auf Client-seitigen Geräten zugewiesen wurden. Die erfassten IDs können dann an [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md) , um in unterstützten Adobe Experience Cloud-Anwendungen auf die personenbezogenen Daten der betreffenden Person zuzugreifen oder sie zu löschen.

In diesem Handbuch wird beschrieben, wie Sie die Adobe Privacy-Erweiterung in der Datenerfassungs-Benutzeroberfläche installieren und konfigurieren.

>[!NOTE]
>
>Wenn Sie diese Funktionen lieber ohne Tags installieren möchten, lesen Sie den Abschnitt [Übersicht über die Privacy JavaScript Library](../../../../privacy-service/js-library.md) für Schritte zur Implementierung mit Rohcode.

## Installieren und Konfigurieren der Erweiterung

Wählen Sie in der Datenerfassungs-Benutzeroberfläche die Option **[!UICONTROL Erweiterungen]** im linken Navigationsbereich, gefolgt von der **[!UICONTROL Katalog]** Registerkarte. Verwenden Sie die Suchleiste, um die Liste der verfügbaren Erweiterungen einzuschränken, bis Sie Adobe Privacy finden. Auswählen **[!UICONTROL Installieren]** , um fortzufahren.

![Installieren der Erweiterung](../../../images/extensions/privacy/install.png)

Im nächsten Bildschirm können Sie konfigurieren, aus welchen Quellen und Lösungen die Erweiterung IDs erfassen soll. Die folgenden Lösungen werden für die -Erweiterung unterstützt:

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Adobe Experience Cloud Identity-Dienst (Besucher oder ECID)
* Adobe Advertising Cloud (AdCloud)

Wählen Sie mindestens eine Lösung aus und wählen Sie dann **[!UICONTROL Aktualisieren]**.

![Lösungen auswählen](../../../images/extensions/privacy/select-solutions.png)

Der Bildschirm wird aktualisiert und zeigt die Eingaben für die erforderlichen Konfigurationsparameter basierend auf den von Ihnen ausgewählten Lösungen an.

![Erforderliche Eigenschaften](../../../images/extensions/privacy/required-properties.png)

Über das Dropdown-Menü unten können Sie der Konfiguration auch zusätzliche lösungsspezifische Parameter hinzufügen.

![Optionale Eigenschaften](../../../images/extensions/privacy/optional-properties.png)

>[!NOTE]
>
>Siehe Abschnitt zu [Konfigurationsparameter](../../../../privacy-service/js-library.md#config-params) in der Übersicht zur Privacy JavaScript Library finden Sie Details zu den akzeptierten Konfigurationswerten für die einzelnen unterstützten Lösungen.

Nachdem Sie die Parameter für Ihre ausgewählten Lösungen hinzugefügt haben, wählen Sie **[!UICONTROL Speichern]** , um die Konfiguration zu speichern.

![Optionale Eigenschaften](../../../images/extensions/privacy/save-config.png)

## Verwenden der Erweiterung {#using}

Die Adobe Privacy-Erweiterung bietet drei Aktionstypen, die in einer [Regel](../../../ui/managing-resources/rules.md) wenn ein bestimmtes Ereignis eintritt und Bedingungen erfüllt sind:

* **[!UICONTROL Abrufen von Identitäten]**: Die gespeicherten Identitätsdaten des Benutzers werden abgerufen.
* **[!UICONTROL Identitäten entfernen]**: Die gespeicherten Identitätsdaten des Benutzers werden entfernt.
* **[!UICONTROL Abrufen und Entfernen von Identitäten]**: Die gespeicherten Identitätsdaten des Benutzers werden abgerufen und dann entfernt.

Für jede der oben genannten Aktionen müssen Sie eine Callback-JavaScript-Funktion bereitstellen, die die abgerufenen Identitätsdaten als Objektparameter akzeptiert und verarbeitet. Von hier aus können Sie diese Identitäten speichern, anzeigen oder an die [Privacy Service-API](../../../../privacy-service/api/overview.md) wie Sie benötigen.

Bei Verwendung der Datenschutz-Tag-Erweiterung der Adobe müssen Sie die erforderliche Callback-Funktion in Form eines Datenelements bereitstellen. Anweisungen zum Konfigurieren dieses Datenelements finden Sie im nächsten Abschnitt .

### Definieren eines Datenelements zur Verarbeitung von Identitäten

Starten Sie in der Datenerfassungs-Benutzeroberfläche den Prozess der Erstellung eines neuen Datenelements durch Auswahl von **[!UICONTROL Datenelemente]** im linken Navigationsbereich, gefolgt von **[!UICONTROL Datenelement hinzufügen]**. Wählen Sie im Konfigurationsbildschirm die Option **[!UICONTROL Core]** für die Erweiterung und **[!UICONTROL Benutzerspezifischer Code]** für den Datenelementtyp. Wählen Sie von hier aus **[!UICONTROL Editor öffnen]** im rechten Bereich.

![Datenelementtyp auswählen](../../../images/extensions/privacy/data-element-type.png)

Definieren Sie im angezeigten Dialogfeld eine JavaScript-Funktion, die die abgerufenen Identitäten verarbeitet. Der Rückruf muss ein einzelnes Objekt (`ids` im Beispiel unten). Die Funktion kann dann die IDs beliebig verarbeiten und auch alle Variablen und Funktionen aufrufen, die auf Ihrer Site global für die weitere Verarbeitung verfügbar sind.

>[!NOTE]
>
>Weitere Informationen zur Struktur der `ids` -Objekt, das die Callback-Funktion verarbeiten soll, siehe [Codebeispiele](../../../../privacy-service/js-library.md#samples) in der Übersicht zur Privacy JavaScript Library bereitgestellt.

Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![Callback-Funktion definieren](../../../images/extensions/privacy/define-custom-code.png)

Sie können mit der Erstellung anderer Datenelemente mit benutzerdefiniertem Code fortfahren, wenn Sie für verschiedene Ereignisse unterschiedliche Rückrufe benötigen.

### Erstellen einer Regel mit einer Datenschutzaktion

Nachdem Sie ein Callback-Datenelement zur Verarbeitung der abgerufenen IDs konfiguriert haben, können Sie eine Regel erstellen, die die Adobe-Datenschutzerweiterung aufruft, sobald auf Ihrer Site ein bestimmtes Ereignis eintritt, sowie alle anderen erforderlichen Bedingungen.

Wählen Sie beim Konfigurieren der Aktion für die Regel **[!UICONTROL Datenschutz bei Adoben]** für die Erweiterung. Wählen Sie für den Aktionstyp eine der [drei Funktionen](#using) bereitgestellt von der -Erweiterung.

![Aktionstyp auswählen](../../../images/extensions/privacy/action-type.png)

Im rechten Bereich werden Sie aufgefordert, ein Datenelement auszuwählen, das als Rückruf der Aktion dient. Wählen Sie das Datenbanksymbol (![Datenbanksymbol](../../../images/extensions/privacy/database.png)) und wählen Sie aus der Liste das zuvor erstellte Datenelement aus. Auswählen **[!UICONTROL Änderungen beibehalten]** , um fortzufahren.

![Datenelement auswählen](../../../images/extensions/privacy/add-data-element.png)

Von hier aus können Sie mit der Regelkonfiguration fortfahren, sodass die Datenschutzaktion für Adoben unter den von Ihnen benötigten Ereignissen und Bedingungen ausgelöst wird. Wenn Sie zufrieden sind, wählen Sie **[!UICONTROL Speichern]**.

![Speichern Sie die Regel](../../../images/extensions/privacy/save-rule.png)

Sie können die Regel jetzt einer Bibliothek hinzufügen, um sie zum Testen als Build auf Ihrer Website bereitzustellen. Die Übersicht finden Sie auf der [Tagpublishing-Fluss](../../../ui/publishing/overview.md) für weitere Informationen.

## Erweiterung deaktivieren oder deinstallieren

Nach dem Installieren der Erweiterung können Sie sie deaktivieren oder löschen. Klicken Sie in der Adobe-Datenschutzkarte in Ihren installierten Erweiterungen auf **[!UICONTROL Konfigurieren]** und wählen Sie **[!UICONTROL Deaktivieren]** oder **[!UICONTROL Deinstallieren]** aus.

## Nächste Schritte

In diesem Handbuch wurde die Verwendung der Datenschutz-Tag-Erweiterung der Adobe in der Datenerfassungs-Benutzeroberfläche behandelt. Weitere Informationen zu den von der Erweiterung bereitgestellten Funktionen, einschließlich Beispielen für die Verwendung mit Rohcode, finden Sie in der [Übersicht über die Privacy JavaScript Library](../../../../privacy-service/js-library.md) in der Dokumentation zum Privacy Service.
