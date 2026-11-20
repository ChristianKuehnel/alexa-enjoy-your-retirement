# Alexa, Enjoy Your Retirement!

*Replacing Amazon Echo with Home Assistant Voice – one use case at a time.*

After years of faithful service, it's time for Alexa to retire.

Let's face it: Alexa is getting a bit long in the tooth. What once felt revolutionary now feels rather dated, and the ongoing **enshittification** of cloud-based services isn't exactly making me more enthusiastic about keeping Amazon microphones around the house.

So I've decided to replace our Echo devices with a self-hosted voice assistant based on Home Assistant.

I'm not trying to recreate every Alexa feature. In fact, we only use a handful of things regularly:

- **Timers and alarms**
- **Radio and Spotify**
- **News briefings:** Deutschlandfunk, BR24, and heise online's *kurz informiert*
- **To-do lists and shopping lists**

Sounds simple enough, right?

There's just one catch: **Alexa has set a pretty high bar.** Voice commands need to work reliably from several meters away, even with music playing. And music needs to sound at least as good as it does on our Echo Dots.

Otherwise, Alexa's retirement might have to be postponed.

## What's already working?

My Home Assistant setup already includes Music Assistant and local Whisper-based speech recognition.

For hardware, I'm currently experimenting with:

- **2 × Home Assistant Voice Preview Edition**
- **1 × Futureproof Homes Satellite1**

Some things are looking promising:

✅ **Timers, to-do lists, and shopping lists** already work.

✅ **Voice recognition on the Home Assistant Voice Preview Edition** is actually pretty good.

✅ **Sound quality on the Satellite1** is already quite decent.

🟡 **News briefings** work using REST sensors and a few Home Assistant scripts.

🔧 **Alarms:** I'm currently working on an implementation that runs the alarm locally on the satellite, so it doesn't depend on a permanent connection to Home Assistant.

## What's still missing (or driving me crazy)?

**1. News without endless scripting**

I can already play the latest news bulletins, but I don't want to create a separate REST sensor and a bunch of scripts for every news provider.

What I'd really like is a generic solution integrated with Music Assistant that automatically finds and plays the latest episode of a news bulletin.

**2. The Satellite1 has trouble hearing me**

While the Home Assistant Voice Preview Edition does a surprisingly good job, voice recognition on the Futureproof Homes Satellite1 is still pretty unreliable – especially when music is playing.

There's definitely room for improvement here.

**3. A custom wake word**

I'm not particularly fond of the default wake words. I'd like to configure my own and have it work reliably across all satellites, ideally without waking up every time someone says something vaguely similar.

**4. Radio and Spotify**

I haven't tested voice control of radio stations or Spotify through Music Assistant yet.

Fortunately, there seem to be existing solutions for both, so hopefully this won't involve too much reinventing the wheel.

**5. Sound quality – pick your compromise**

Interestingly, the two devices have almost opposite strengths:

- **Futureproof Homes Satellite1:** Pretty decent sound quality, but voice recognition needs work.
- **Home Assistant Voice Preview Edition:** Good voice recognition, but music playback is rather underwhelming.

Ideally, I'd like the voice recognition of the Voice Preview Edition combined with the audio quality of the Satellite1.

## So, when can Alexa finally retire?

When all the everyday features work reliably, voice recognition is at least as good as Alexa's, and music sounds at least as good as it does on the Echo Dots.

I'd prefer to build on existing, actively maintained open-source solutions rather than inventing everything from scratch.

I'll use this thread to document my progress, including the things that don't work on the first (or fifth) attempt.

**Is anyone else working on something similar?**

I'd be particularly interested in experiences with the Satellite1 while music is playing, and ideas for a generic news briefing integration with Music Assistant.

Hopefully, we can get Alexa her well-deserved retirement party sooner rather than later. 🎉
