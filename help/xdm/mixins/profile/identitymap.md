---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Identitätskarte;Identitätskarte;Schema-Design;Map;Vereinigung Schema;Vereinigung
solution: Experience Platform
title: IdentityMap-Mixin
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die XDM Individual Profil-Klasse.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

#  IdentityMapmixin

>[!NOTE]
>
>Die Namen mehrerer Mixins haben sich geändert. Weitere Informationen finden Sie im Dokument [mixin name updates](../name-updates.md).

 IdentityMapis ist ein Standardmixin für die  [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Das Mixin bietet ein einzelnes Kartenfeld, das eine Reihe von Benutzeridentitäten enthält, die vom Namensraum festgelegt werden.

>[!WARNING]
>
>Das Feld `IdentityMap` wird vom System automatisch aktualisiert, wenn Identitätsdaten erfasst werden. Um dieses Feld für [Kundendaten in Echtzeit](../../../profile/home.md) richtig zu verwenden, sollten Sie nicht versuchen, den Feldinhalt in Ihren Datenvorgängen manuell zu aktualisieren.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Weitere Informationen zum Anwendungsfall finden Sie im Abschnitt zu Identitätskarten in den [Grundlagen der Schema-Komposition](../../schema/composition.md#identityMap).
