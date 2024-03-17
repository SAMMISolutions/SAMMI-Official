# 2024.1.0 IS HERE, HI, WE'RE ALIVE :sparkles: 

It's been a while, @everyone! A lot has been going on since the beginning of this year, as we thought about the future of SAMMI and what 2024 will look like. We've decided to undertake an extremely daunting task to kick it all off. Primarily, Christinna has been instrumental in reworking the entire backend of our Twitch integration over to Twitch's newer EventSub structure.

We began work on this with our last update, moving some endpoints to test the waters. Now, we've fully shifted, and PubSub has been completely removed from SAMMI :boom:

This massive shift brings some significant upsides, along with a few minor downsides. Let's start with the upsides!

___Upsides___  

We now have access to new triggers such as when ads start, charity triggers, guest start triggers, and much more! Additionally, we've made changes to existing triggers, adding new data that wasn't present in PubSub.
New commands also join the mix, enabling you to snooze ads, block/unblock users, manage ad schedules, and more.

With EventSub, we can stay more up-to-date with Twitch's changes, moving away from a legacy system. This reduces the likelihood of features randomly breaking due to Twitch's gradual phasing out of PubSub.

___Downsides___  

Some triggers are temporarily unavailable as we transition to EventSub. We'll be adding them back as soon as possible, so please don't delete your buttons. Additionally, Twitch's decisions with EventSub might require some tweaks in your buttons, but rest assured, there are workarounds for everything. Check our patch notes for triggers that might need editing.

Twitch now limits listening to events to one account at a time, which is more a benefit for those who previously had triggers linked to their bot accounts. Streamers typically prefer events to be linked to their primary streaming account, not a secondary bot account.


# Important note about Twitch ⚠

Due to the EventSub changes, you'll need to re-link (i.e. remove and re-add) your Twitch account! This brings us to our next major announcement...

# NEW UI CHANGES :tada:

Digi_Bunny, our latest recruit, has been diligently redesigning and coding a new UI for SAMMI. Their first projects include the About page and, most importantly, the Twitch Connections page. The new design is exceptionally simple, intuitive, and eye-friendly.

# New Language :books:

Portuguese has been added by JzTurrini!!

# SAMMI Deck App Notice

As SAMMI has evolved, new third-party deck apps have emerged. We want to acknowledge that! With 2024.1.0, we're renaming the SAMMI Panel side menu to "Deck App." This aligns better with the various ways of connecting and interacting with decks on your devices. We're changing the recommended app for SAMMI Deck connections to the Deck Hopper app, developed independently by Christina. While not official, Deck Hopper is a fantastic alternative, offering a polished experience with SAMMI Decks. The SAMMI Panel hasn't met expectations, so we're suggesting this excellent alternative.

# Windows Smartscreen Warning

When running the new SAMMI version, you might see a Windows Smartscreen pop-up. This is because the exe is simply not verified by Microsoft, as our code signing certificate renewal is pending. We're working to resolve this.

The pop-up simply indicates this and nothing nefarious. To proceed, select "More Info," and you'll be able to run the program without further interruptions.

Full patch notes below, get out there, Sammies!!

PATCH NOTES: <https://sammi.solutions/docs/patch-notes>
