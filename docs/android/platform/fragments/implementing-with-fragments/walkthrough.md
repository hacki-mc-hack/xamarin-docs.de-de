---
title: Xamarin.Android Fragmente Exemplarische Vorgehensweise – Teil 1
ms.prod: xamarin
ms.topic: tutorial
ms.assetid: ED368FA9-A34E-DC39-D535-5C34C32B9761
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 04/26/2018
ms.openlocfilehash: 4dae59d113671c9ba1ac35dd8e4189d05a7c319a
ms.sourcegitcommit: e16517edcf471b53b4e347cd3fd82e485923d482
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2018
ms.locfileid: "33798485"
---
# <a name="fragments-walkthrough-ndash-phone"></a>Exemplarische Vorgehensweise Fragmenten &ndash; Phone]

Dies ist der erste Teil einer exemplarischen Vorgehensweise, die eine Xamarin.Android-app erstellen, die auf einem Android-Gerät im Hochformat abzielt. In dieser exemplarischen Vorgehensweise wird zum Erstellen von Fragmenten in Xamarin.Android und zum Hinzufügen, die einer Stichprobe erläutert.

[![](./images/intro-screenshot-phone-sml.png)](./images/intro-screenshot-phone.png#lightbox)

Die folgenden Klassen werden für diese app erstellt werden:

1. `PlayQuoteFragment` &nbsp; Dieses Fragment wird ein Angebot aus einer Prüfung von William Shakespeare angezeigt. Es wird von gehostet werden `PlayQuoteActivity`.
1. `Shakespeare` &nbsp; Diese Klasse wird als Eigenschaften zwei hartcodiert Arrays enthalten.
1. `TitlesFragment` &nbsp; Dieses Fragment zeigt eine Liste der Titel wiedergegeben wird, die von William Shakespeare geschrieben wurden. Es wird von gehostet werden `MainActivity`.
1. `PlayQuoteActivity` &nbsp; `TitlesFragment` Startet die `PlayQuoteActivity` als Antwort auf die Benutzer wählen ein Spiel in `TitlesFragment`.

## <a name="1-create-the-android-project"></a>1. Erstellen Sie das Android-Projekt

Erstellen Sie ein neue Xamarin.Android Projekt mit der Bezeichnung **FragmentSample**.
# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

[![Erstellen eines neuen Xamarin.Android-Projekts](./walkthrough-images/01-newproject.w157-sml.png)](./walkthrough-images/01-newproject.w157.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

[![Erstellen eines neuen Xamarin.Android-Projekts](./walkthrough-images/01-newproject.m742-sml.png)](./walkthrough-images/01-newproject.m742.png#lightbox)

Es wird empfohlen, wählen Sie **moderne Entwicklungsplattformen** für diese exemplarische Vorgehensweise.

Nach dem Erstellen des Projekts, benennen Sie die Datei **layout/Main.axml** auf **layout/activity_main.axml**.

-----

## <a name="2-add-the-data"></a>2. Fügen Sie die Daten

Die Daten für diese Anwendung werden in zwei hartcodierte Zeichenfolgenarrays, die Eigenschaften für einen Klassennamen sind gespeichert werden `Shakespeare`:

* `Shakespeare.Titles` &nbsp; Dieses Array wird eine Liste der spielt von William Shakespeare enthalten. Dies ist die Datenquelle für die `TitlesFragment`.
* `Shakespeare.Dialogue` &nbsp; Dieses Array wird eine Liste der von einem der Wiedergabe der in enthaltenen Anführungszeichen halten `Shakespeare.Titles`. Dies ist die Datenquelle für die `PlayQuoteFragment`.

Fügen Sie eine neue c#-Klasse, die **FragmentSample** Projekt, und nennen Sie sie **Shakespeare.cs**. Erstellen Sie eine neue C#-Klasse mit dem Namen innerhalb dieser Datei `Shakespeare` mit dem folgenden Inhalt

```csharp
class Shakespeare
{
    public static string[] Titles = {
                                      "Henry IV (1)",
                                      "Henry V",
                                      "Henry VIII",
                                      "Richard II",
                                      "Richard III",
                                      "Merchant of Venice",
                                      "Othello",
                                      "King Lear"
                                    };

    public static string[] Dialogue = {
                                        "So shaken as we are, so wan with care, Find we a time for frighted peace to pant, And breathe short-winded accents of new broils To be commenced in strands afar remote. No more the thirsty entrance of this soil Shall daub her lips with her own children's blood; Nor more shall trenching war channel her fields, Nor bruise her flowerets with the armed hoofs Of hostile paces: those opposed eyes, Which, like the meteors of a troubled heaven, All of one nature, of one substance bred, Did lately meet in the intestine shock And furious close of civil butchery Shall now, in mutual well-beseeming ranks, March all one way and be no more opposed Against acquaintance, kindred and allies: The edge of war, like an ill-sheathed knife, No more shall cut his master. Therefore, friends, As far as to the sepulchre of Christ, Whose soldier now, under whose blessed cross We are impressed and engaged to fight, Forthwith a power of English shall we levy; Whose arms were moulded in their mothers' womb To chase these pagans in those holy fields Over whose acres walk'd those blessed feet Which fourteen hundred years ago were nail'd For our advantage on the bitter cross. But this our purpose now is twelve month old, And bootless 'tis to tell you we will go: Therefore we meet not now. Then let me hear Of you, my gentle cousin Westmoreland, What yesternight our council did decree In forwarding this dear expedience.",
                                        "Hear him but reason in divinity, And all-admiring with an inward wish You would desire the king were made a prelate: Hear him debate of commonwealth affairs, You would say it hath been all in all his study: List his discourse of war, and you shall hear A fearful battle render'd you in music: Turn him to any cause of policy, The Gordian knot of it he will unloose, Familiar as his garter: that, when he speaks, The air, a charter'd libertine, is still, And the mute wonder lurketh in men's ears, To steal his sweet and honey'd sentences; So that the art and practic part of life Must be the mistress to this theoric: Which is a wonder how his grace should glean it, Since his addiction was to courses vain, His companies unletter'd, rude and shallow, His hours fill'd up with riots, banquets, sports, And never noted in him any study, Any retirement, any sequestration From open haunts and popularity.",
                                        "I come no more to make you laugh: things now, That bear a weighty and a serious brow, Sad, high, and working, full of state and woe, Such noble scenes as draw the eye to flow, We now present. Those that can pity, here May, if they think it well, let fall a tear; The subject will deserve it. Such as give Their money out of hope they may believe, May here find truth too. Those that come to see Only a show or two, and so agree The play may pass, if they be still and willing, I'll undertake may see away their shilling Richly in two short hours. Only they That come to hear a merry bawdy play, A noise of targets, or to see a fellow In a long motley coat guarded with yellow, Will be deceived; for, gentle hearers, know, To rank our chosen truth with such a show As fool and fight is, beside forfeiting Our own brains, and the opinion that we bring, To make that only true we now intend, Will leave us never an understanding friend. Therefore, for goodness' sake, and as you are known The first and happiest hearers of the town, Be sad, as we would make ye: think ye see The very persons of our noble story As they were living; think you see them great, And follow'd with the general throng and sweat Of thousand friends; then in a moment, see How soon this mightiness meets misery: And, if you can be merry then, I'll say A man may weep upon his wedding-day.",
                                        "First, heaven be the record to my speech! In the devotion of a subject's love, Tendering the precious safety of my prince, And free from other misbegotten hate, Come I appellant to this princely presence. Now, Thomas Mowbray, do I turn to thee, And mark my greeting well; for what I speak My body shall make good upon this earth, Or my divine soul answer it in heaven. Thou art a traitor and a miscreant, Too good to be so and too bad to live, Since the more fair and crystal is the sky, The uglier seem the clouds that in it fly. Once more, the more to aggravate the note, With a foul traitor's name stuff I thy throat; And wish, so please my sovereign, ere I move, What my tongue speaks my right drawn sword may prove.",
                                        "Now is the winter of our discontent Made glorious summer by this sun of York; And all the clouds that lour'd upon our house In the deep bosom of the ocean buried. Now are our brows bound with victorious wreaths; Our bruised arms hung up for monuments; Our stern alarums changed to merry meetings, Our dreadful marches to delightful measures. Grim-visaged war hath smooth'd his wrinkled front; And now, instead of mounting barded steeds To fright the souls of fearful adversaries, He capers nimbly in a lady's chamber To the lascivious pleasing of a lute. But I, that am not shaped for sportive tricks, Nor made to court an amorous looking-glass; I, that am rudely stamp'd, and want love's majesty To strut before a wanton ambling nymph; I, that am curtail'd of this fair proportion, Cheated of feature by dissembling nature, Deformed, unfinish'd, sent before my time Into this breathing world, scarce half made up, And that so lamely and unfashionable That dogs bark at me as I halt by them; Why, I, in this weak piping time of peace, Have no delight to pass away the time, Unless to spy my shadow in the sun And descant on mine own deformity: And therefore, since I cannot prove a lover, To entertain these fair well-spoken days, I am determined to prove a villain And hate the idle pleasures of these days. Plots have I laid, inductions dangerous, By drunken prophecies, libels and dreams, To set my brother Clarence and the king In deadly hate the one against the other: And if King Edward be as true and just As I am subtle, false and treacherous, This day should Clarence closely be mew'd up, About a prophecy, which says that 'G' Of Edward's heirs the murderer shall be. Dive, thoughts, down to my soul: here Clarence comes.",
                                        "To bait fish withal: if it will feed nothing else, it will feed my revenge. He hath disgraced me, and hindered me half a million; laughed at my losses, mocked at my gains, scorned my nation, thwarted my bargains, cooled my friends, heated mine enemies; and what's his reason? I am a Jew. Hath not a Jew eyes? hath not a Jew hands, organs, dimensions, senses, affections, passions? fed with the same food, hurt with the same weapons, subject to the same diseases, healed by the same means, warmed and cooled by the same winter and summer, as a Christian is? If you prick us, do we not bleed? if you tickle us, do we not laugh? if you poison us, do we not die? and if you wrong us, shall we not revenge? If we are like you in the rest, we will resemble you in that. If a Jew wrong a Christian, what is his humility? Revenge. If a Christian wrong a Jew, what should his sufferance be by Christian example? Why, revenge. The villany you teach me, I will execute, and it shall go hard but I will better the instruction.",
                                        "Virtue! a fig! 'tis in ourselves that we are thus or thus. Our bodies are our gardens, to the which our wills are gardeners: so that if we will plant nettles, or sow lettuce, set hyssop and weed up thyme, supply it with one gender of herbs, or distract it with many, either to have it sterile with idleness, or manured with industry, why, the power and corrigible authority of this lies in our wills. If the balance of our lives had not one scale of reason to poise another of sensuality, the blood and baseness of our natures would conduct us to most preposterous conclusions: but we have reason to cool our raging motions, our carnal stings, our unbitted lusts, whereof I take this that you call love to be a sect or scion.",
                                        "Blow, winds, and crack your cheeks! rage! blow! You cataracts and hurricanoes, spout Till you have drench'd our steeples, drown'd the cocks! You sulphurous and thought-executing fires, Vaunt-couriers to oak-cleaving thunderbolts, Singe my white head! And thou, all-shaking thunder, Smite flat the thick rotundity o' the world! Crack nature's moulds, an germens spill at once, That make ingrateful man!" 
                                    };
}
```

## <a name="3-create-the-playquotefragment"></a>3. Erstellen Sie die PlayQuoteFragment

Die `PlayQuoteFragment` ist ein Android-Fragment, in denen ein Angebot für eine Shakespeare Play angezeigt wird, die vom Benutzer weiter oben in der Anwendung ausgewählt wurde dieses Fragment wird keine Android Layoutdatei verwenden, wird stattdessen die Benutzeroberfläche dynamisch erstellt. Fügen Sie einen neuen `Fragment` Klasse mit dem Namen `PlayQuoteFragment` zum Projekt:

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

[![Fügen Sie eine neue C#-Klasse](./walkthrough-images/04-addfragment.w157-sml.png)](./walkthrough-images/02-addclass.w157.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

[![Fügen Sie eine neue C#-Klasse](./walkthrough-images/04-addfragment.m742-sml.png)](./walkthrough-images/02-addclass.m742.png#lightbox)

-----

Ändern Sie dann den Code für das Fragment, damit Sie diesen Ausschnitt ähneln:

```csharp
public class PlayQuoteFragment : Fragment
{
    public int PlayId => Arguments.GetInt("current_play_id", 0);

    public static PlayQuoteFragment NewInstance(int playId)
    {
        var bundle = new Bundle();
        bundle.PutInt("current_play_id", playId);
        return new PlayQuoteFragment {Arguments = bundle};
    }

    public override View OnCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState)
    {
        if (container == null)
        {
            return null;
        }

        var textView = new TextView(Activity);
        var padding = Convert.ToInt32(TypedValue.ApplyDimension(ComplexUnitType.Dip, 4, Activity.Resources.DisplayMetrics));
        textView.SetPadding(padding, padding, padding, padding);
        textView.TextSize = 24;
        textView.Text = Shakespeare.Dialogue[PlayId];

        var scroller = new ScrollView(Activity);
        scroller.AddView(textView);

        return scroller;
    }
}
```

Es ist ein allgemeines Muster in der Android-apps, um eine Factorymethode bereitzustellen, die ein Fragment instanziiert wird. Dadurch wird sichergestellt, dass das Fragment mit den erforderlichen Parametern für das ordnungsgemäße Funktionieren erstellt werden soll. In dieser exemplarischen Vorgehensweise muss die app verwendet die `PlayQuoteFragment.NewInstance` Methode, um ein neues Fragment bei jedem erstellen ein Angebots ausgewählt ist. Die `NewInstance` -Methode einen einzelnen Parameter akzeptiert &ndash; den Index des Angebots angezeigt.

Die `OnCreateView` Methode wird von Android aufgerufen werden, wenn das Fragment auf dem Bildschirm gerendert werden. Wird zurückgegeben, die ein Android `View` -Objekt, das Fragment ist. Dieses Fragment verwendet eine Layoutdatei nicht, eine Sicht erstellt. Stattdessen wird sie die Ansicht programmgesteuert erstellen, indem Sie Instanziieren einer **TextView** zum Speichern des Angebots und zeigt diese Widgets in einer **ScrollView**.

> [!NOTE]
> Unterklassen Fragment müssen einen öffentlichen Standardkonstruktor verfügen, der keine Parameter hat.

## <a name="4-create-the-playquoteactivity"></a>4. Erstellen Sie die PlayQuoteActivity

Fragmente müssen innerhalb einer Aktivität gehostet werden, damit diese app eine Aktivität erforderlich ist, der als host der `PlayQuoteFragment`. Die Aktivität wird das zugehörige Layout zur Laufzeit dynamisch des Fragments hinzugefügt. Die Anwendung eine neue Aktivität hinzu, und nennen Sie sie `PlayQuoteActivity`:

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

[![Android-Aktivität zum Projekt hinzufügen](./walkthrough-images/03-addactivity.w157-sml.png)](./walkthrough-images/03-addactivity.w157.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

[![Android-Aktivität zum Projekt hinzufügen](./walkthrough-images/03-addactivity.m742-sml.png)](./walkthrough-images/03-addactivity.m742.png#lightbox)

-----

Bearbeiten Sie den Code in `PlayQuoteActivity`:

```csharp
[Activity(Label = "PlayQuoteActivity")]
public class PlayQuoteActivity : Activity
{
    protected override void OnCreate(Bundle savedInstanceState)
    {
        base.OnCreate(savedInstanceState);

        var playId = Intent.Extras.GetInt("current_play_id", 0);

        var detailsFrag = PlayQuoteFragment.NewInstance(playId);
        FragmentManager.BeginTransaction()
                        .Add(Android.Resource.Id.Content, detailsFrag)
                        .Commit();
    }
}
```

Wenn `PlayQuoteActivity` ist erstellt, instanziiert es dann ein neues `PlayQuoteFragment` und Laden Sie dieses Fragment in der Stammansicht im Rahmen einer `FragmentTransaction`. Beachten Sie, dass diese Aktivität eine Android Layoutdatei für die Benutzeroberfläche nicht geladen werden kann. Stattdessen ein neues `PlayQuoteFragment` ist der Stammansicht der Anwendung hinzugefügt. Der Ressourcenbezeichner `Android.Resource.Id.Content` wird verwendet, um auf die Stammansicht einer Aktivität zu verweisen, ohne die versionsspezifischen Bezeichner.

## <a name="5-create-titlesfragment"></a>5. Erstellen von TitlesFragment

Die `TitlesFragment` wird Unterklasse ein spezielles Fragments genannt eine `ListFragment` die kapselt der Logik für die Anzeige von einer `ListView` in einem Fragment. Ein `ListFragment` macht eine `ListAdapter` Eigenschaft (von verwendet die `ListView` zum Anzeigen des Inhalts) und einen Ereignishandler namens `OnListItemClick` , sodass das Fragment auf Klicks auf eine Zeile zu reagieren, die vom angezeigt wird der `ListView`. 

Um zu beginnen, fügen Sie dem Projekt ein neues Fragment hinzu, und nennen Sie sie **TitlesFragment**:

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

[![Hinzufügen von Android Fragment-Projekt](./walkthrough-images/04-addfragment.w157-sml.png)](./walkthrough-images/04-addfragment.w157.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

[![Hinzufügen von Android Fragment-Projekt](./walkthrough-images/04-addfragment.m742-sml.png)](./walkthrough-images/04-addfragment.m742.png#lightbox)

-----

Bearbeiten Sie den Code innerhalb des Fragments:

```csharp
public class TitlesFragment : ListFragment
{
    int selectedPlayId;

    public TitlesFragment()
    {
        // Being explicit about the requirement for a default constructor.
    }

    public override void OnActivityCreated(Bundle savedInstanceState)
    {
        base.OnActivityCreated(savedInstanceState);
        ListAdapter = new ArrayAdapter<String>(Activity, Android.Resource.Layout.SimpleListItemActivated1, Shakespeare.Titles);

        if (savedInstanceState != null)
        {
            selectedPlayId = savedInstanceState.GetInt("current_play_id", 0);
        }
    }

    public override void OnSaveInstanceState(Bundle outState)
    {
        base.OnSaveInstanceState(outState);
        outState.PutInt("current_play_id", selectedPlayId);
    }

    public override void OnListItemClick(ListView l, View v, int position, long id)
    {
        ShowPlayQuote(position);
    }

    void ShowPlayQuote(int playId)
    {
        var intent = new Intent(Activity, typeof(PlayQuoteActivity));
        intent.PutExtra("current_play_id", playId);
        StartActivity(intent);
    }
}
```

Android wird aufgerufen, wenn die Aktivität erstellt wird die `OnActivityCreated` Methode des Fragments; Dies ist, wenn die Liste-Netzwerkadapter für die `ListView` wird erstellt.  Die `ShowQuoteFromPlay` Methode startet eine Instanz von der `PlayQuoteActivity` das Angebot für die ausgewählten Play angezeigt.

## <a name="display-titlesfragment-in-mainactivity"></a>TitlesFragment in der Verwendung des Layoutnamens anzeigen

Der letzte Schritt besteht anzuzeigende `TitlesFragment` in `MainActivity`. Die Aktivität wird das Fragment nicht dynamisch geladen. Stattdessen das Fragment wird statisch geladen sein deklarieren Sie es in der Layoutdatei der Aktivität mit einem `fragment` Element. Das Fragment geladen wird durch Festlegen von identifiziert die `android:name` -Attribut der Klasse Fragment (einschließlich der Namespace des Typs). Beispielsweise verwenden die `TitlesFragment`, klicken Sie dann `android:name` wäre `FragmentSample.TitlesFragment`.

Bearbeiten Sie die Layoutdatei **activity_mail.axml**, die vorhandenen XML-Code durch Folgendes ersetzen:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:orientation="horizontal"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <fragment
        android:name="FragmentSample.TitleFragment"
        android:id="@+id/titles"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</LinearLayout>
```

> [!NOTE]
> Die `class` -Attribut ist ein gültiger Ersatz für `android:name`. Es gibt keine formale allgemeinen Vorgaben auf welche Form bevorzugt wird, es gibt viele Beispiele für Codebasen, die verwendet werden `class` austauschbar mit `android:name`.

Es sind keine Änderungen am Code für die Verwendung des Layoutnamens erforderlich sind. Der Code in dieser Klasse sollten diesen Ausschnitt sehr ähnlich sein:

```csharp
[Activity(Label = "@string/app_name", Theme = "@style/AppTheme", MainLauncher = true)]
public class MainActivity : Activity
{
    protected override void OnCreate(Bundle savedInstanceState)
    {
        base.OnCreate(savedInstanceState);
        SetContentView(Resource.Layout.activity_main);
    }
}
```

## <a name="run-the-app"></a>Ausführen der App

Nun, dass der Code abgeschlossen ist, führen Sie die app auf einem Gerät, in Aktion sehen.

[![Screenshots der Anwendung auf einem Telefon ausgeführt wird.](./walkthrough-images/05-app-screenshots-sml.png)](./walkthrough-images/05-app-screenshots.png#lightbox)

[Teil 2 dieser exemplarischen Vorgehensweise](./walkthrough-landscape.md) Optimtize-diese Anwendung für Geräte, die im Querformat ausgeführt wird.