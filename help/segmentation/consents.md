---
keywords: Experience Platform; Startseite; beliebte Themen; Opt-out; Segmentierung; Segmentierungsdienst; Segmentierungsdienst; berücksichtigt Opt-outs; Opt-out; Opt-out; Opt-outs; Einverständnis; Freigabe; Sammeln;
solution: Experience Platform
title: Einverständnis in Segmenten
topic-legacy: overview
description: Erfahren Sie, wie Sie die Zustimmungseinstellungen von Kunden für die Erfassung und Freigabe personenbezogener Daten in Segmentvorgängen berücksichtigen.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 2%

---

# Einverständniserklärung in Segmenten

Rechtliche Datenschutzbestimmungen wie die [!DNL California Consumer Privacy Act] (CCPA) bieten Verbrauchern das Recht, sich gegen die Erfassung oder Weitergabe personenbezogener Daten an Dritte zu entscheiden. Adobe Experience Platform bietet standardmäßige XDM-Komponenten (Experience Data Model), mit denen diese Voreinstellungen bezüglich der Kundenzustimmung in Echtzeit-Kundenprofildaten erfasst werden sollen.

Wenn ein Kunde die Freigabe seiner personenbezogenen Daten widerrufen oder verweigert hat, muss Ihr Unternehmen diese Voreinstellung beim Generieren von Zielgruppen für Marketingaktivitäten berücksichtigen. In diesem Dokument wird beschrieben, wie Sie mithilfe der Experience Platform-Benutzeroberfläche Kundenzustimmungswerte in Ihre Segmentdefinitionen integrieren.

## Erste Schritte

Die Einhaltung der Zustimmungswerte von Kunden erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] beteiligte Dienste. Bevor Sie mit diesem Tutorial beginnen, sollten Sie mit den folgenden Diensten vertraut sein:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten ordnet.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ermöglicht das Erstellen von Zielgruppensegmenten aus [!DNL Real-Time Customer Profile] Daten.

## Einverständnisschemafelder

Um Kundeneinwilligungen und -präferenzen zu berücksichtigen, ist eines der Schemas, das Teil Ihrer [!UICONTROL XDM Individual Profile] Das Vereinigungsschema muss die Standardfeldgruppe enthalten. **[!UICONTROL Einverständnis und Voreinstellungen]**.

Weitere Informationen zur Struktur und zum vorgesehenen Anwendungsfall der einzelnen Attribute, die von der Feldergruppe bereitgestellt werden, finden Sie in der [Referenzhandbuch zu Einverständnissen und Voreinstellungen](../xdm/field-groups/profile/consents.md). Eine schrittweise Anleitung zum Hinzufügen einer Feldergruppe zu einem Schema finden Sie im Abschnitt [Handbuch zur XDM-Benutzeroberfläche](../xdm/ui/resources/schemas.md#add-field-groups).

Nachdem die Feldergruppe zu einem [Profil-aktiviertes Schema](../xdm/ui/resources/schemas.md#profile) und ihre Felder zum Erfassen von Einwilligungsdaten aus Ihrer Erlebnisanwendung verwendet wurden, können Sie die erfassten Zustimmungsattribute in Ihren Segmentregeln verwenden.

## Umgang mit Zustimmung in der Segmentierung

Um sicherzustellen, dass Opt-out-Profile nicht in Segmenten enthalten sind, müssen vorhandenen Segmenten spezielle Felder hinzugefügt und bei der Erstellung neuer Segmente einbezogen werden.

Die folgenden Schritte zeigen, wie Sie die entsprechenden Felder für zwei Arten von Opt-out-Flags hinzufügen:

1. [!UICONTROL Datenerfassung]
1. [!UICONTROL Daten freigeben]

>[!NOTE]
>
>Während sich dieses Handbuch auf die beiden oben genannten Opt-out-Flags konzentriert, können Sie Ihre Segmente so konfigurieren, dass auch zusätzliche Zustimmungssignale einbezogen werden. Die [Referenzhandbuch zu Einverständnissen und Voreinstellungen](../xdm/field-groups/profile/consents.md) enthält weitere Informationen zu den einzelnen Optionen und den vorgesehenen Anwendungsfällen.

Beim Erstellen eines Segments in der Benutzeroberfläche finden Sie unter **[!UICONTROL Attribute]**, navigieren Sie zu **[!UICONTROL XDM Individual Profile]**, wählen Sie **[!UICONTROL Einverständnis und Voreinstellungen]**. Von hier aus können Sie die Optionen für **[!UICONTROL Datenerfassung]** und **[!UICONTROL Daten freigeben]**.

![](./images/opt-outs/consents.png)

Wählen Sie zunächst **[!UICONTROL Datenerfassung]** Kategorie, dann ziehen **[!UICONTROL Auswahlwert]** in den Segment-Builder. Beim Hinzufügen des Attributs zum Segment können Sie die [Zustimmungswerte](../xdm/field-groups/profile/consents.md#choice-values) die ein- oder ausgeschlossen werden müssen.

![](./images/opt-outs/consent-values.png)

Ein Ansatz besteht darin, alle Kunden auszuschließen, die sich gegen die Erfassung ihrer Daten entschieden haben. Setzen Sie dazu den Operator auf **[!UICONTROL ist nicht gleich]** und wählen Sie die folgenden Werte aus:

* **[!UICONTROL Nein (Opt-out)]**
* **[!UICONTROL Standardwert Nein (Opt-out)]**
* **[!UICONTROL unbekannt]** (wenn davon ausgegangen wird, dass die Einwilligung verweigert wird, sofern nicht anderweitig unbekannt ist)

![](./images/opt-outs/collect.png)

under **[!UICONTROL Attribute]** Navigieren Sie in der linken Leiste zurück zur **[!UICONTROL Einverständnis und Voreinstellungen]** und wählen Sie **[!UICONTROL Daten freigeben]**. Ziehen Sie die entsprechenden **[!UICONTROL Auswahlwert]** in die Arbeitsfläche ein und wählen Sie dieselben Werte wie für die [!UICONTROL Datenerfassung] Auswahlwert. Stellen Sie sicher, dass **[!UICONTROL Oder]** Beziehung wird zwischen den beiden Attributen hergestellt.

![](./images/opt-outs/share.png)

Mit beiden **[!UICONTROL Datenerfassung]** und **[!UICONTROL Daten freigeben]** Zustimmungswerte, die zum Segment hinzugefügt wurden, werden alle Kunden, die sich gegen die Verwendung ihrer Daten entschieden haben, von der resultierenden Zielgruppe ausgeschlossen. Von hier aus können Sie die Segmentdefinition weiter anpassen, bevor Sie **[!UICONTROL Speichern]** , um den Prozess abzuschließen.

## Nächste Schritte

Durch Befolgung dieses Tutorials sollten Sie jetzt ein besseres Verständnis dafür haben, wie Sie Kundenzustimmungen und -präferenzen beim Erstellen von Segmenten in Experience Platform berücksichtigen können.

Weitere Informationen zur Verwaltung von Einwilligungen in Platform finden Sie in der folgenden Dokumentation:

* [Einverständnisverarbeitung mit dem Adobe-Standard](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Einverständnisverarbeitung mit dem IAB TCF 2.0-Standard](../landing/governance-privacy-security/consent/iab/overview.md)