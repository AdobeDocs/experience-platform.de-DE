---
title: Erste Schritte mit der Ereignisweiterleitung
description: In diesem Schritt-für-Schritt-Tutorial erfahren Sie, wie Sie mit der Ereignisweiterleitung in Adobe Experience Platform beginnen.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 87%

---

# Erste Schritte mit der Ereignisweiterleitung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Um die Ereignisweiterleitung in Adobe Experience Platform zu verwenden, müssen Daten mit einer oder mehreren der folgenden drei Optionen an das Adobe Experience Platform Edge Network gesendet werden:

* [Adobe Experience Platform Web SDK](../../extensions/client/sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [Server-zu-Server-API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=de)

>[!NOTE]
>Das Platform Web SDK und das Platform Mobile SDK erfordern keine Bereitstellung über Tags in Adobe Experience Platform. Es wird jedoch empfohlen, Tags zur Bereitstellung dieser SDKs zu verwenden.

Nachdem Sie Daten an das Edge-Netzwerk gesendet haben, können Sie die Adobe-Lösungen einschalten, um Daten dorthin zu senden. Um Daten an eine Drittanbieter-Lösung zu senden, richten Sie diese in der Ereignisweiterleitung ein.

## Voraussetzungen

* Adobe Experience Platform Collection Enterprise (Informationen zu Preisen erhalten Sie von Ihrem Adobe-Kundenbetreuungsteam)
* Ereignisweiterleitung in Adobe Experience Platform
* Adobe Experience Platform Web oder Mobile SDK, konfiguriert zum Senden von Daten an Edge Network
* Zuordnen von Daten zum Experience-Datenmodell (XDM) (diese Zuordnung kann über Tags erfolgen)

## Erstellen eines XDM-Schemas

Erstellen Sie in Adobe Experience Platform Ihr Schema.

1. Erstellen Sie ein Schema, indem Sie auf **[!UICONTROL Schemas]** > **[!UICONTROL Schema erstellen]** klicken und die Option **[!UICONTROL XDM ExperienceEvent]** auswählen.

1. Versehen Sie das Schema mit einem Namen und einer Kurzbeschreibung.

1. Sie können die Feldergruppe &quot;ExperienceEvent web details&quot;hinzufügen, indem Sie **[!UICONTROL Hinzufügen]** neben **[!UICONTROL Feldergruppen]**.

   >[!NOTE]
   >
   >Bei Bedarf können mehrere Feldgruppen hinzugefügt werden.

1. Speichern Sie das Schema und notieren Sie sich den Namen, den Sie ihm gegeben haben.

Weitere Informationen zu Schemata finden Sie unter [Experience-Datenmodell (XDM) – Systemhilfe](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de).

## Erstellen einer Ereignisweiterleitungseigenschaft

Im **[!UICONTROL Tags]** Workspace erstellen Sie eine Eigenschaft vom Typ **[!UICONTROL Edge]**.

1. Wählen Sie **[!UICONTROL Neue Eigenschaft]** aus.

1. Benennen Sie die Eigenschaft.

1. Wählen Sie den Plattformtyp &quot;Edge&quot;aus.

1. Wählen Sie **[!UICONTROL Speichern]** aus.

Nachdem Sie die Eigenschaft erstellt haben, wechseln Sie zum Tab **[!UICONTROL Umgebungen]** für die neue Eigenschaft und
notieren Sie sich die Umgebungs-IDs. Wenn sich die im Daten-Stream verwendete Adobe-Organisation von der in der Ereignisweiterleitung verwendeten unterscheidet, können Sie die Umgebungs-ID aus der Registerkarte **[!UICONTROL Umgebungen]** kopieren und beim Erstellen eines Daten-Streams einfügen. Andernfalls können Sie die Umgebung aus einem Dropdown-Menü auswählen.

## Erstellen eines Datenspeichers

Verwenden Sie zum Erstellen Ihres Daten-Streams in Adobe Experience Platform die Umgebungs-ID, die beim Erstellen der Ereignisweiterleitungseigenschaft generiert wurde.

1. Auswählen **[!UICONTROL Datenspeicher]** in der linken Navigation.

1. Benennen Sie die Konfiguration und geben Sie eine optionale Beschreibung ein.
Die Beschreibung hilft, Konfigurationen in einer Liste mehrerer Konfigurationen zu identifizieren.

1. Wählen Sie **[!UICONTROL Speichern]** aus.

## Aktivieren der Ereignisweiterleitung

Konfigurieren Sie als Nächstes Edge Network, um Daten an die Ereignisweiterleitung und andere Adobe-Produkte zu senden.

1. Im **[!UICONTROL Datenspeicher]** Arbeitsbereich die von Ihnen erstellte Eigenschaft aus.

1. Wählen Sie die Entwicklungs-, Betreibungs- oder Staging-Umgebung.

   Oder wählen Sie, um Daten an eine Ereignisweiterleitungsumgebung außerhalb der Adobe-Organisation zu senden, **[!UICONTROL In den fortgeschrittenen Modus wechseln]** aus und fügen Sie eine ID ein. Die ID wird bereitgestellt, wenn Sie eine Ereignisweiterleitungseigenschaft erstellen.

1. Schalten Sie die erforderlichen Werkzeuge ein und konfigurieren Sie sie nach Bedarf.

   * Adobe Analytics benötigt eine Report Suite-ID.

   * Für die Ereignisweiterleitung in Adobe Experience Platform sind eine Eigenschaften-ID und eine Umgebungs-ID erforderlich. Dies ist der Veröffentlichungspfad für die Ereignisweiterleitungseigenschaft.

Notieren Sie sich nach der Konfiguration die Umgebungs-IDs für die neue Eigenschaft.

## Konfigurieren der Platform Web SDK-Erweiterung, um Daten an den zuvor erstellten Daten-Stream zu senden

Erstellen Sie Ihre Eigenschaft im **[!UICONTROL Tags]** Arbeitsbereich und navigieren Sie dann zu **[!UICONTROL Erweiterungen]** und wählen Sie die Experience Platform Web SDK-Erweiterung aus dem Katalog aus, um sie zu konfigurieren und zu installieren.

Siehe [Dokumentation zur Web SDK-Erweiterung](../../extensions/client/sdk/overview.md) für Details zu Konfigurationsoptionen.

## Erstellen einer Tag-Regel zum Senden von Daten an das Platform Web SDK

Nachdem alle oben genannten Elemente eingerichtet sind, können Sie die erforderlichen Datendefinitionen, Regeln usw. erstellen, die sowohl Ereignisweiterleitung als auch Tags nutzen, für die jedoch nur eine einzige Anfrage von der Seite benötigt wird.

Erstellen Sie eine Seitenladeregel mit der Platform Web SDK-Erweiterung und dem Aktionstyp &quot;Ereignis senden&quot;:

1. Öffnen Sie die Registerkarte **[!UICONTROL Regeln]** und wählen Sie **[!UICONTROL Neue Regel erstellen]** aus.

1. Geben Sie einen Namen für die Regel ein.

1. Wählen Sie **[!UICONTROL Ereignis hinzufügen]** aus.

1. Fügen Sie ein Ereignis hinzu, indem Sie eine Erweiterung und einen der für diese Erweiterung verfügbaren Ereignistypen auswählen und dann die Einstellungen für das Ereignis konfigurieren. Wählen Sie beispielsweise **[!UICONTROL Core - Window Loaded]** aus.

1. Fügen Sie eine Aktion hinzu, indem Sie die Platform Web SDK-Erweiterung verwenden. Wählen Sie **[!UICONTROL Ereignis senden]** aus der Liste **[!UICONTROL Aktionstyp]** aus, wählen Sie die gewünschte Instanz aus (Alloy-Instanz, die zuvor konfiguriert wurde) und wählen Sie dann ein Datenelement aus, das zum XDM-Datenblock innerhalb des Alloy-Treffers hinzugefügt werden soll.

1. Belassen Sie den Rest der Einstellungen für dieses Beispiel als Standard und wählen Sie **[!UICONTROL Speichern]**.

Sie können beispielsweise eine Regel erstellen, die die Datenschicht an Edge sendet, wenn der Mauszeiger über einen bestimmten Button bewegt wird.

## Zusammenfassung

Wenn Folgendes eingerichtet ist, können Sie jetzt Ereignisweiterleitungsregeln erstellen, um Daten an Drittanbieter-Ziele weiterzuleiten.

* Schema des Experience-Datenmodells (notieren Sie sich den Namen, den Sie ihm gegeben haben).
* Eine Ereignisweiterleitungseigenschaft (verfolgen Sie die Eigenschaften-ID und die Umgebungs-IDs.)
* Ein Daten-Stream (beachten Sie die Umgebungs-ID, nicht zu verwechseln mit der Umgebungs-ID aus der Ereignisweiterleitung.)
* Eine Tag-Eigenschaft
