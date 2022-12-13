---
title: Übersicht über Meta-Pixel-Erweiterung
description: Erfahren Sie mehr über die Meta-Pixel-Tag-Erweiterung in Adobe Experience Platform.
source-git-commit: 87376172f89858bfa883084461544a2c50ba5009
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 2%

---

# [!DNL Meta Pixel] Erweiterungsübersicht

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ist ein JavaScript-basiertes Analysetool, mit dem Sie die Besucheraktivität auf Ihrer Website verfolgen können. Von Ihnen verfolgte Besucheraktionen (so genannte Konversionen) werden an gesendet [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) wo sie zur Messung der Effektivität Ihrer Anzeigen, Kampagnen, Konversionstrichter und mehr verwendet werden können.

Die [!DNL Meta Pixel] Tag-Erweiterung ermöglicht Ihnen die Nutzung von [!DNL Pixel] -Funktionen in Ihren clientseitigen Tag-Bibliotheken. In diesem Dokument wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer [Regel](../../../ui/managing-resources/rules.md).

<!-- (To include when Conversions API extension doc is published)
>[!NOTE]
>
>If you are trying to send server-side events to [!DNL Meta] rather than from the client side, use the [[!DNL Meta Conversions API] extension](../../server/meta/overview.md) instead.
-->

## Voraussetzungen

Um die Erweiterung verwenden zu können, müssen Sie über eine gültige [!DNL Meta] Konto mit Zugriff auf [!DNL Ads Manager]. Insbesondere müssen Sie [eine neue [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) und kopieren sie [!DNL Pixel ID] damit die Erweiterung für Ihr Konto konfiguriert werden kann. Wenn Sie bereits eine [!DNL Meta Pixel], können Sie stattdessen die zugehörige ID verwenden.

## Installieren der Erweiterung

So installieren Sie die [!DNL Meta Pixel] Erweiterung, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder Experience Platform-Benutzeroberfläche und wählen Sie **[!UICONTROL Tags]** über die linke Navigation. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, wählen Sie **[!UICONTROL Erweiterungen]** Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Katalog]** Registerkarte. Suchen Sie nach [!UICONTROL Meta-Pixel] Karte, und wählen Sie **[!UICONTROL Installieren]**.

![Die [!UICONTROL Installieren] für die [!UICONTROL Meta-Pixel] -Erweiterung in der Datenerfassungs-Benutzeroberfläche.](../../../images/extensions/client/meta/install.png)

In der angezeigten Konfigurationsansicht müssen Sie die Variable [!DNL Pixel] ID, die Sie zuvor kopiert haben, um die Erweiterung mit Ihrem Konto zu verknüpfen. Sie können die ID direkt in die Eingabe einfügen oder stattdessen ein vorhandenes Datenelement auswählen.

>[!TIP]
>
>Mithilfe eines Datenelements können Sie die [!DNL Pixel] ID, die von anderen Faktoren wie der Build-Umgebung verwendet wird. Siehe den Anhang unter [mit verschiedenen [!DNL Pixel] IDs für verschiedene Umgebungen](#id-data-element) für weitere Informationen.

Sie können optional auch eine Ereignis-ID angeben, die mit der Erweiterung verknüpft werden soll. Damit werden identische Ereignisse zwischen [!DNL Meta Pixel] und [!DNL Meta Conversions API]. Siehe [!DNL Meta] Dokumentation zu [Verarbeiten von Duplikaten [!DNL Pixel] und [!DNL Conversions API] events](https://developers.facebook.com/docs/marketing-api/conversions-api/deduplicate-pixel-and-server-events/) für Details.

Klicken Sie abschließend auf **[!UICONTROL Speichern]**

![Die [!DNL Pixel] ID, die in der Erweiterungskonfigurationsansicht als Datenelement bereitgestellt wird.](../../../images/extensions/client/meta/configure.png)

Die -Erweiterung ist installiert und Sie können jetzt die verschiedenen Aktionen in Ihren Tag-Regeln verwenden.

## Tag-Regel konfigurieren {#rule}

[!DNL Meta Pixel] akzeptiert einen Satz vordefinierter [Standardereignisse](https://www.facebook.com/business/help/402791146561655), jeweils mit eigenen Kontexten und akzeptierten Eigenschaften. Die Regelaktionen, die von der [!DNL Pixel] Korrelation der Erweiterung mit diesen Ereignistypen erstellen, sodass Sie das Ereignis, das an gesendet wird, einfach kategorisieren und konfigurieren können [!DNL Meta] je nach Typ.

Zu Demonstrationszwecken wird in diesem Abschnitt gezeigt, wie eine Regel erstellt wird, die ein Seitenansichtsereignis an [!DNL Meta].

Beginnen Sie mit der Erstellung einer neuen Tag-Regel und konfigurieren Sie deren Bedingungen nach Bedarf. Wenn Sie die Aktionen für die Regel auswählen, wählen Sie **[!UICONTROL Meta-Pixel]** für die Erweiterung und wählen Sie dann **[!UICONTROL Seitenansicht senden]** für den Aktionstyp.

![Die [!UICONTROL Seitenansicht senden] Aktionstyp, der für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt wird.](../../../images/extensions/client/meta/select-action.png)

Es ist keine weitere Konfiguration erforderlich für die [!UICONTROL Seitenansicht senden] Aktion. Auswählen **[!UICONTROL Änderungen beibehalten]** , um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]**.

Veröffentlichen Sie abschließend ein neues Tag [build](../../../ui/publishing/builds.md) , um die Änderungen an der Bibliothek zu aktivieren.

## Vergewissern Sie sich, dass [!DNL Meta] empfängt Daten

Nachdem Ihr aktualisierter Build auf Ihrer Website bereitgestellt wurde, können Sie überprüfen, ob die Daten erwartungsgemäß gesendet werden, indem Sie Konversionsereignisse in Ihrem Browser generieren und überprüfen, ob diese Ereignisse in [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Daten an [!DNL Meta] mithilfe der [!DNL Meta Pixel] Tag-Erweiterung. Weiterführende Informationen zu Tags in Experience Platform finden Sie im Abschnitt [Tag-Übersicht](../../../home.md).

## Anhang: Unterschiedliche [!DNL Pixel] IDs für verschiedene Umgebungen {#id-data-element}

Wenn Sie Ihre Implementierung in Entwicklungs- oder Staging-Umgebungen testen und dabei Ihre Produktion beibehalten möchten [!DNL Meta Pixel] intakte Analyse verwenden, können Sie ein Datenelement verwenden, um eine geeignete [!DNL Pixel] Kennung abhängig von der verwendeten Umgebung.

Dies erreichen Sie mithilfe eines [!UICONTROL Benutzerspezifischer Code] Datenelement (bereitgestellt von der [[!UICONTROL Core] Erweiterung](../core/overview.md)) in Kombination mit dem [`turbine` freie Variable](../../../extension-dev/turbine.md). Verwenden Sie im JavaScript-Code des Datenelements den `turbine` -Objekt, um die aktuelle Umgebungsstufe zu finden, und geben Sie dann eine geeignete [!DNL Pixel] Kennung basierend auf dem Ergebnis.

Das folgende Beispiel gibt eine falsche Produktions-ID zurück `exampleProductionKey` bei Verwendung in der Produktionsumgebung und einer anderen ID `exampleTestKey` wenn eine andere Umgebung verwendet wird. Ersetzen Sie bei der Implementierung dieses Codes jeden Wert durch Ihre eigentliche Produktion und Ihren Test. [!DNL Pixel] IDs.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```

