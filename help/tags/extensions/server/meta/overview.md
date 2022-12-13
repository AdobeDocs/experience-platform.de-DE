---
title: Übersicht über die API-Erweiterung für Meta Conversions
description: Erfahren Sie mehr über die Meta Conversions API-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
source-git-commit: a47e35a1b8c7ce2b0fa4ffe30fcdc7d22fc0f4c5
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 2%

---

# [!DNL Meta Conversions API] Erweiterungsübersicht

Die [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) ermöglicht es Ihnen, Ihre Server-seitigen Marketing-Daten mit [!DNL Meta] Technologien zur Optimierung Ihres Anzeigen-Targeting, Senkung der Kosten pro Aktion und Messung der Ergebnisse. Ereignisse sind mit einer [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID und werden ähnlich wie clientseitige Ereignisse verarbeitet.

Verwenden der [!DNL Meta Conversions API] -Erweiterung verwenden, können Sie die API-Funktionen in Ihrer [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) Regeln zum Senden von Daten an [!DNL Meta] vom Adobe Experience Platform Edge Network aus. In diesem Dokument wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in der Ereignisweiterleitung verwenden. [Regel](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Wenn Sie versuchen, Ereignisse an zu senden [!DNL Meta] Verwenden Sie auf der Clientseite anstelle der Server-Seite die [[!DNL Meta Pixiel] Tag-Erweiterung](../../client/meta/overview.md) anstatt.

## Voraussetzungen

Um die Erweiterung verwenden zu können, müssen Sie auf die Ereignisweiterleitung zugreifen und über eine gültige [!DNL Meta] Konto mit Zugriff auf [!DNL Ad Manager] und [!DNL Event Manager]. Insbesondere müssen Sie die Kennung eines vorhandenen [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (oder [eine neue [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) ), damit die Erweiterung für Ihr Konto konfiguriert werden kann.

## Installieren der Erweiterung

So installieren Sie die [!DNL Meta Conversions API] Erweiterung, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder Experience Platform-Benutzeroberfläche und wählen Sie **[!UICONTROL Ereignisweiterleitung]** über die linke Navigation. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, wählen Sie **[!UICONTROL Erweiterungen]** Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Katalog]** Registerkarte. Suchen Sie nach [!UICONTROL Meta Conversions-API] Karte, und wählen Sie **[!UICONTROL Installieren]**.

![Die [!UICONTROL Installieren] für die [!UICONTROL Meta Conversions-API] -Erweiterung in der Datenerfassungs-Benutzeroberfläche.](../../../images/extensions/server/meta/install.png)

In der angezeigten Konfigurationsansicht müssen Sie die Variable [!DNL Pixel] ID, die Sie zuvor kopiert haben, um die Erweiterung mit Ihrem Konto zu verknüpfen. Sie können die ID direkt in die Eingabe einfügen oder stattdessen ein Datenelement verwenden.

Sie müssen außerdem ein Zugriffstoken bereitstellen, um die [!DNL Conversions API] speziell. Siehe Abschnitt [!DNL Conversions API] Dokumentation zu [Zugriffstoken generieren](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) für Schritte zum Abrufen dieses Werts.

Klicken Sie abschließend auf **[!UICONTROL Speichern]**

![Die [!DNL Pixel] ID, die in der Erweiterungskonfigurationsansicht als Datenelement bereitgestellt wird.](../../../images/extensions/server/meta/configure.png)

Die -Erweiterung ist installiert und Sie können jetzt ihre Funktionen in Ihren Tag-Regeln nutzen.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

Beginnen Sie mit der Erstellung einer neuen Ereignisweiterleitungsregel und konfigurieren Sie deren Bedingungen nach Bedarf. Wenn Sie die Aktionen für die Regel auswählen, wählen Sie **[!UICONTROL API-Erweiterung für Meta Conversions]** für die Erweiterung und wählen Sie dann **[!UICONTROL Ereignis der Konversions-API senden]** für den Aktionstyp.

![Die [!UICONTROL Seitenansicht senden] Aktionstyp, der für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt wird.](../../../images/extensions/server/meta/select-action.png)

Es werden Steuerelemente angezeigt, mit denen Sie die Ereignisdaten konfigurieren können, die an [!DNL Meta] über die [!DNL Conversions API]. Diese Optionen können direkt in die bereitgestellten Eingaben eingegeben werden oder Sie können vorhandene Datenelemente auswählen, um die Werte stattdessen darzustellen. Die Konfigurationsoptionen sind wie unten beschrieben in vier Hauptabschnitte unterteilt.

| Konfigurationsabschnitt | Beschreibung |
| --- | --- |
| [!UICONTROL Server-Ereignisparameter] | Allgemeine Informationen zum Ereignis, einschließlich der Zeit, zu der es aufgetreten ist, und der Quellaktion, die es ausgelöst hat. Siehe Abschnitt [[!DNL Conversions API] Dokumentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) für weitere Informationen zu diesen Parametern.<br><br>Sie haben auch die Möglichkeit, **[!UICONTROL Eingeschränkte Datenverwendung aktivieren]** um die Einhaltung von Kunden-Opt-outs zu unterstützen. Siehe [!DNL Conversions API] Dokumentation zu [Datenverarbeitungsoptionen](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) für Details zu dieser Funktion. |
| [!UICONTROL Parameter für Kundeninformationen] | Benutzeridentitätsdaten, mit denen das Ereignis einem Kunden zugeordnet wird. Einige dieser Werte müssen gehasht werden, bevor sie an die API gesendet werden können. Siehe Abschnitt [[!DNL Conversions API] Dokumentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) für weitere Informationen zu diesen Parametern. |
| [!UICONTROL Benutzerdefinierte Daten] | Zusätzliche Daten, die zur Optimierung der Anzeigenbereitstellung verwendet werden und in Form eines JSON-Objekts bereitgestellt werden. Siehe Abschnitt [[!DNL Conversions API] Dokumentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) für weitere Informationen zu den zulässigen Eigenschaften für dieses Objekt.<br><br>Wenn Sie ein Kaufereignis senden, müssen Sie in diesem Abschnitt die erforderlichen Attribute angeben `currency` und `value`. |
| [!UICONTROL Testereignis] | Diese Option wird verwendet, um zu überprüfen, ob Ihre Konfiguration dazu führt, dass Serverereignisse von empfangen werden [!DNL Meta] wie erwartet. Um diese Funktion zu verwenden, wählen Sie die **[!UICONTROL Als Testereignis senden]** und geben Sie dann in der unten stehenden Eingabe einen Test-Ereigniscode Ihrer Wahl ein. Nachdem die Ereignisweiterleitungsregel bereitgestellt wurde, sollten bei der korrekten Konfiguration der Erweiterung und Aktion Aktivitäten angezeigt werden, die im **[!DNL Test Events]** Ansicht in [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Änderungen beibehalten]** , um die Aktion zur Regelkonfiguration hinzuzufügen.

![[!UICONTROL Änderungen beibehalten] für die Aktionskonfiguration ausgewählt werden.](../../../images/extensions/server/meta/keep-changes.png)

Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]**. Veröffentlichen Sie schließlich eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) um die Änderungen zu aktivieren, die an der Bibliothek vorgenommen wurden.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie serverseitige Ereignisdaten an senden [!DNL Meta] mithilfe der [!DNL Meta Conversions API] -Erweiterung. Weiterführende Informationen zu Tags und zur Ereignisweiterleitung finden Sie im Abschnitt [Tag-Übersicht](../../../home.md).
