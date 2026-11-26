---
layout: post
title: "The Low-Hanging Fruit"
---

Alexa's retirement is proceeding one voice command at a time. This week I went after the easy wins: news, Spotify, and faster speech recognition. Then I tried to make coffee.

![A Home Assistant speaker plays the news beside a steaming French press while a thumb starts a kitchen timer set to 2:30.]({{ '/assets/images/coffee-timer.webp' | relative_url }})

*The news is automated. The coffee is not.*

## The news, in three YAML snippets

Deutschlandfunk works pretty reliably. A REST sensor checks the RSS feed every five minutes, uses the latest episode's title as its state, and keeps the audio enclosure as an attribute.

{% raw %}
```yaml
rest:
  - resource: https://www.deutschlandfunk.de/nachrichten-108.xml
    scan_interval: 300
    timeout: 20
    sensor:
      - name: Deutschlandfunk Nachrichten
        unique_id: deutschlandfunk_nachrichten
        value_template: >-
          {{ value_json.rss.channel.item[0].title }}
        json_attributes_path: "$.rss.channel.item[0]"
        json_attributes:
          - enclosure
          - pubDate
```
{% endraw %}

When I say “Spiel die Nachrichten,” Assist answers and hands the requesting device ID to my playback script.

{% raw %}
```yaml
alias: Deutschlandfunk per Sprache
triggers:
  - trigger: conversation
    command:
      - Spiel[e] die Nachricht[e]n
      - Spiel[e] die Nachricht[e]n von Deutschlandfunk
actions:
  - set_conversation_response: Die Nachrichten von Deutschlandfunk.
  - action: script.spiele_deutschlandfunk_nachrichten
    data:
      voice_device_id: '{{ trigger.device_id }}'
mode: parallel
```
{% endraw %}

The script (`script.spiele_deutschlandfunk_nachrichten`) refreshes the sensor on demand, then plays the episode on the device I spoke to. No need to broadcast the headlines to the whole house.

{% raw %}
```yaml
alias: Spiele Deutschlandfunk Nachrichten
fields:
  voice_device_id:
    name: Auslösendes Voice-Gerät
    required: true
sequence:
  - action: homeassistant.update_entity
    target:
      entity_id: sensor.deutschlandfunk_nachrichten
  - variables:
      audio_url: |-
        {{ state_attr(
          'sensor.deutschlandfunk_nachrichten',
          'enclosure'
        )['@url'] }}
  - condition: template
    value_template: '{{ audio_url | default('''', true) != '''' }}'
  - action: media_player.play_media
    target:
      device_id: '{{ voice_device_id }}'
    data:
      media:
        media_content_id: '{{ audio_url }}'
        media_content_type: music
        metadata: {}
mode: parallel
```
{% endraw %}

The same approach works in principle for heise online's *kurz informiert*, which is a polite way of saying I don't trust it yet. BR24 does things differently: simple RSS feed parsing doesn't get me the latest bulletin.

## Spotify works. “Stop” doesn't.

Music Assistant's [Spotify Connect plugin](https://www.music-assistant.io/plugins/spotify-connect/) has worked well so far. Stopping playback is the odd bit: “music off” works for music *and* the news, but “stop” doesn't. I haven't figured out why.

I also swapped Whisper for [NVIDIA Parakeet](https://docs.nvidia.com/nemo-framework/user-guide/latest/nemotoolkit/asr/models.html#parakeet). Speech recognition is much faster on my Intel CPU and still good enough for me. No GPU needed, despite the name on the box.

## The kitchen is holding up retirement

I want to ask “What's two-thirds of 450?” or “How many grams is six ounces?” without putting down the mixing bowl. I found an LLM-based option, but I'd rather have a plain calculator and unit converter. Maybe currencies too, if I find a live source for exchange rates. How hard could that be? (Famous last words.)

My French press gets two minutes and thirty seconds. You may disagree with the recipe; I just want “OK Nabu, coffee timer” to start it. I haven't found a way to start an on-device timer from an automation, but the [Home Assistant roadmap proposes making Voice timers available to automations](https://github.com/OpenHomeFoundation/roadmap/issues/211).

So far, the news is on demand, the speech recognition is faster, and the coffee interface is still my thumb.
