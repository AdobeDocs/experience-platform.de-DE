---
title: Erste Schritte mit der Ereignisweiterleitung
description: In diesem Schritt-für-Schritt-Tutorial erfahren Sie, wie Sie mit der Ereignisweiterleitung in Adobe Experience Platform beginnen.
source-git-commit: da7696d288543abd21ff8a1402e81dcea32efbc2
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 48%

---

# Erste Schritte mit der Ereignisweiterleitung

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Um die Ereignisweiterleitung in Adobe Experience Platform zu verwenden, müssen Daten mit einer oder mehreren der folgenden drei Optionen an das Adobe Experience Platform Edge Network gesendet werden:

* [Adobe Experience Platform Web SDK](../../extensions/web/sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [Server-zu-Server-API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>Das Platform Web SDK und Platform Mobile SDK erfordern keine Implementierung über Tags in Adobe Experience Platform. Es wird jedoch empfohlen, Tags zur Bereitstellung dieser SDKs zu verwenden.

Nachdem Sie Daten an das Edge-Netzwerk gesendet haben, können Sie die Adobe-Lösungen einschalten, um Daten dorthin zu senden. Um Daten an eine Nicht-Adobe-Lösung zu senden, richten Sie diese in der Ereignisweiterleitung ein.

## Voraussetzungen

* Adobe Experience Platform Collection Enterprise (Preise erhalten Sie von Ihrem Account Manager)
* Ereignisweiterleitung in Adobe Experience Platform
* Adobe Experience Platform Web oder Mobile SDK, konfiguriert zum Senden von Daten an Edge Network
* Daten dem Experience-Datenmodell (XDM) zuordnen (diese Zuordnung kann mithilfe von Tags erfolgen)

## Erstellen eines XDM-Schemas

Erstellen Sie in Adobe Experience Platform Ihr Schema.

1. Erstellen Sie ein Schema, indem Sie auf **[!UICONTROL Schemas]** > **[!UICONTROL Schema erstellen]** klicken und die Option **[!UICONTROL XDM ExperienceEvent]** auswählen.

1. Versehen Sie das Schema mit einem Namen und einer Kurzbeschreibung.

1. Sie können die Feldergruppe &quot;ExperienceEvent web details&quot;hinzufügen, indem Sie **[!UICONTROL Hinzufügen]** neben **[!UICONTROL Feldergruppen]** auswählen.

   >[!NOTE]
   >
   >Bei Bedarf können mehrere Feldergruppen hinzugefügt werden.

1. Speichern Sie das Schema und notieren Sie sich den Namen, den Sie ihm gegeben haben.

Weitere Informationen zu Schemata finden Sie unter [Experience-Datenmodell (XDM) – Systemhilfe](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de).

## Erstellen einer Ereignisweiterleitungseigenschaft

Erstellen Sie in der Datenerfassungs-Benutzeroberfläche eine Eigenschaft vom Typ &quot;Edge&quot;.

1. Wählen Sie **[!UICONTROL Neue Eigenschaft]** aus.

1. Benennen Sie die Eigenschaft.

1. Wählen Sie den Plattformtyp „Edge“ aus.

1. Wählen Sie **[!UICONTROL Speichern]** aus.

Nachdem Sie die Eigenschaft erstellt haben, wechseln Sie zum Tab **[!UICONTROL Umgebungen]** für die neue Eigenschaft und
notieren Sie sich die Umgebungs-IDs. Wenn sich die im Datastream verwendete Adobe Org von der in der Ereignisweiterleitung verwendeten Adobe unterscheidet, können Sie die Umgebungs-ID aus dem Tab **[!UICONTROL Umgebungen]** kopieren und beim Erstellen eines Datastreams einfügen. Andernfalls können Sie die Umgebung aus einem Dropdown-Menü auswählen.

## Erstellen eines Datenspeichers

Verwenden Sie zum Erstellen Ihres Datenspeichers in Adobe Experience Platform die Umgebungs-ID, die beim Erstellen der Ereignisweiterleitungseigenschaft generiert wurde.

1. Verwenden Sie den Link in der linken Leiste der Datenerfassungs-Benutzeroberfläche, um die Oberfläche für Datastraams zu öffnen.

1. Wählen Sie **[!UICONTROL Datastreams]** aus.

1. Benennen Sie die Konfiguration und geben Sie eine optionale Beschreibung ein.
Die Beschreibung hilft, Konfigurationen in einer Liste mehrerer Konfigurationen zu identifizieren.

1. Wählen Sie **[!UICONTROL Speichern]** aus.



## Ereignisweiterleitung aktivieren

Konfigurieren Sie als Nächstes das Edge Network, um Daten an die Ereignisweiterleitung und an andere Adobe-Produkte zu senden.

1. Wählen Sie in der Benutzeroberfläche &quot;datastreams&quot;die von Ihnen erstellte Eigenschaft aus.

1. Wählen Sie die Entwicklungs-, Betreibungs- oder Staging-Umgebung.

   Wenn Sie Daten auch an eine Ereignisweiterleitungsumgebung außerhalb der Adobe-Organisation senden möchten, wählen Sie **[!UICONTROL Wechseln Sie in den erweiterten Modus]** und fügen Sie eine ID ein. Die ID wird bereitgestellt, wenn Sie eine Ereignisweiterleitungs-Eigenschaft erstellen.

1. Schalten Sie die erforderlichen Werkzeuge ein und konfigurieren Sie sie nach Bedarf.

   * Adobe Analytics benötigt eine Report Suite-ID.

   * Für die Ereignisweiterleitung in Adobe Experience Platform sind eine Eigenschaften-ID und eine Umgebungs-ID erforderlich. Dies ist der Veröffentlichungspfad für die Ereignisweiterleitungseigenschaft.

Notieren Sie sich nach der Konfiguration die Umgebungs-IDs für die neue Eigenschaft.

## Konfigurieren der Web SDK-Erweiterung des Tags, um Daten an den zuvor erstellten Datastream zu senden

Erstellen Sie Ihre Eigenschaft in der Datenerfassungs-Benutzeroberfläche und konfigurieren Sie sie dann mit der Adobe Experience Platform Web SDK-Erweiterung.

1. Benennen Sie die Eigenschaft.

   Sie können mehrere Alloy-Instanzen haben. Sie können beispielsweise verschiedene Tracking-Eigenschaften vor und hinter einer Paywall haben.

1. Wählen Sie die Org-ID aus.

1. Wählen Sie die Edge-Domäne aus.

Weitere Konfigurationsoptionen finden Sie in der [Dokumentation zur Web SDK-Erweiterung](../../extensions/web/sdk/overview.md).

## Erstellen einer Tag-Regel zum Senden von Daten an das Platform Web SDK

Erstellen Sie nach dem oben beschriebenen Verfahren Datendefinitionen, Regeln usw., die die Ereignisweiterleitung und -tags verwenden, aber nur eine einzige Anfrage von der Seite benötigen.

Erstellen Sie eine Seitenladeregel mit der Platform Web SDK-Erweiterung und dem Aktionstyp „Ereignis senden“:

1. Öffnen Sie die Registerkarte **[!UICONTROL Regeln]** und wählen Sie **[!UICONTROL Neue Regel erstellen]** aus.

1. Geben Sie einen Namen für die Regel ein.

1. Wählen Sie **[!UICONTROL Ereignis hinzufügen]** aus.

1. Fügen Sie ein Ereignis hinzu, indem Sie eine Erweiterung und einen der für diese Erweiterung verfügbaren Ereignistypen auswählen und dann die Einstellungen für das Ereignis konfigurieren. Wählen Sie beispielsweise **[!UICONTROL Core - Window Loaded]** aus.

1. Fügen Sie eine Aktion hinzu, indem Sie die Platform Web SDK-Erweiterung verwenden. Wählen Sie **[!UICONTROL Ereignis senden]** aus der Liste **[!UICONTROL Aktionstyp]** aus, wählen Sie die gewünschte Instanz aus (Alloy-Instanz, die zuvor konfiguriert wurde) und wählen Sie dann ein Datenelement aus, das zum XDM-Datenblock innerhalb des Alloy-Treffers hinzugefügt werden soll.

1. Belassen Sie den Rest der Einstellungen für dieses Beispiel als Standard und wählen Sie **[!UICONTROL Speichern]**.

Sie können beispielsweise eine Regel erstellen, die die Datenschicht an Edge sendet, wenn der Mauszeiger über einen bestimmten Button bewegt wird.

## Zusammenfassung

Nachdem Sie Folgendes eingerichtet haben, können Sie nun Ereignisweiterleitungsregeln erstellen, um Daten an Nicht-Adobe-Ziele weiterzuleiten.

* Schema des Experience-Datenmodells (notieren Sie sich den Namen, den Sie ihm gegeben haben).
* Eine Ereignisweiterleitungseigenschaft (verfolgen Sie die Eigenschaften-ID und Umgebungs-IDs.)
* Ein Datastream (Beachten Sie die Umgebungs-ID, nicht zu verwechseln mit der Umgebungs-ID aus der Ereignisweiterleitung.)
* Eine Tag-Eigenschaft
