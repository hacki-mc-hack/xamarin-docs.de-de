---
title: 'Xamarin.Essentials: Geocodierung'
description: Die Geocodierung-Klasse in Xamarin.Essentials bietet APIs zu beiden "Geocode" eine Placemark in eine mit Feldern fester Breite Koordinaten und Umkehren von Geocode-Koordinaten auf einer Placemark.
ms.assetid: 3ADC440C-B000-4708-A2CC-296F5160AF90
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: a4d6e4d9b32e665893d82693a3c858630b63d372
ms.sourcegitcommit: 51c274f37369d8965b68ff587e1c2d9865f85da7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2018
ms.locfileid: "39353674"
---
# <a name="xamarinessentials-geocoding"></a>Xamarin.Essentials: Geocodierung

![Vorabversionen von NuGet](~/media/shared/pre-release.png)

Die **Geocodierung** Klasse bietet APIs zu "Geocode" eine Placemark in eine mit Feldern fester Breite Koordinaten und Umkehren von Geocode-Koordinaten auf einer Placemark.

## <a name="getting-started"></a>Erste Schritte

Für den Zugriff auf die **Geocodierung** Funktionalität die folgende Plattform Einrichtung erforderlich ist.

# <a name="androidtabandroid"></a>[Android](#tab/android)

Ohne zusätzliche Einrichtung erforderlich.

# <a name="iostabios"></a>[iOS](#tab/ios)

Ohne zusätzliche Einrichtung erforderlich.

# <a name="uwptabuwp"></a>[UWP](#tab/uwp)

Ein Bing Maps-API-Schlüssel ist erforderlich, die geocodierung-Funktion nutzen. Melden Sie sich für ein kostenloses [Bing Maps](https://www.bingmapsportal.com/) Konto. Klicken Sie unter **Mein Konto > Meine Schlüssel** einen neuen Schlüssel erstellen und füllen Sie die Informationen basierend auf Ihren Anwendungstyp (sein sollten **öffentlichen Windows-App (UWP, 8.x und früher)** für UWP-apps).

Am Anfang in Ihrer Anwendung Leben vor dem Aufruf einer **Geocodierung** Methoden legen Sie den API-Schlüssel:

```csharp
Geocoding.MapKey = "YOUR-KEY-HERE";
```

-----

## <a name="using-geocoding"></a>Mithilfe der Geocodierung

Fügen Sie einen Verweis auf Xamarin.Essentials in Ihrer Klasse hinzu:

```csharp
using Xamarin.Essentials;
```

Erste [Speicherort](xref:Xamarin.Essentials.Location) Koordinaten für eine Adresse:

```csharp
try
{
    var address =  "Microsoft Building 25 Redmond WA USA";
    var locations = await Geocoding.GetLocationsAsync(address);

    var location = locations?.FirstOrDefault();
    if (location != null)
    {
        Console.WriteLine($"Latitude: {location.Latitude}, Longitude: {location.Longitude}, Altitude: {location.Altitude}");
    }
}
catch (FeatureNotSupportedException fnsEx)
{
    // Feature not supported on device
}
catch (Exception ex)
{
    // Handle exception that may have occurred in geocoding
}
```

Die Höhe nicht immer verfügbar ist. Wenn sie nicht verfügbar ist, die `Altitude` Eigenschaft möglicherweise `null` oder der Wert 0 (null) sein. Wenn die Höhe verfügbar ist, ist der Wert, in Metern über über Sea-Ebene.

Erste [Placemarks](xref:Xamarin.Essentials.Placemark) für einen vorhandenen Satz von Koordinaten:

```csharp
try
{
    var lat = 47.673988;
    var lon = -122.121513;

    var placemarks = await Geocoding.GetPlacemarksAsync(lat, lon);

    var placemark = placemarks?.FirstOrDefault();
    if (placemark != null)
    {
        var geocodeAddress =
            $"AdminArea:       {placemark.AdminArea}\n" +
            $"CountryCode:     {placemark.CountryCode}\n" +
            $"CountryName:     {placemark.CountryName}\n" +
            $"FeatureName:     {placemark.FeatureName}\n" +
            $"Locality:        {placemark.Locality}\n" +
            $"PostalCode:      {placemark.PostalCode}\n" +
            $"SubAdminArea:    {placemark.SubAdminArea}\n" +
            $"SubLocality:     {placemark.SubLocality}\n" +
            $"SubThoroughfare: {placemark.SubThoroughfare}\n" +
            $"Thoroughfare:    {placemark.Thoroughfare}\n";

        Console.WriteLine(geocodeAddress);
    }
}
catch (FeatureNotSupportedException fnsEx)
{
    // Feature not supported on device
}
catch (Exception ex)
{
    // Handle exception that may have occurred in geocoding
}
```

## <a name="distance-between-two-locations"></a>Abstand zwischen zwei Standorten

Die [ `Location` ](xref:Xamarin.Essentials.Location) und [ `LocationExtensions` ](xref:Xamarin.Essentials.LocationExtensions) Klassen definieren Methoden, um die Entfernung zwischen zwei Orten zu berechnen. Finden Sie im Artikel [ **Xamarin.Essentials: Geolocation** ](geolocation.md#calculate-distance) verdeutlicht.

## <a name="api"></a>API

- [Quellcode für die geocodierung](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Geocoding)
- [Geocoding-API-Dokumentation](xref:Xamarin.Essentials.Geocoding)
