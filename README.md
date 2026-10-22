# Build notes

I build games and practical tools for streaming, video, and job search. These notes explain the problems behind a few of them, the choices I made, and what still needs work.

## Start here

### [Making a chat game work over stream delay](chat-vs-meteors/)

In Chat vs. Meteors, the game, the stream, and the viewer's answer run on different clocks. How I handle late answers without making everyone wait for the slowest connection.

### [4K60 Native Ingest: why my uploader uses an iPhone](4k60-native-ingest/)

My browser uploads kept losing the video quality I had exported. What I found when I compared upload routes, and why I built around the native phone apps.

### [Keeping AI resume edits tied to real experience](how-i-built-pathos/)

An application tool can make a resume sound stronger while quietly making it less true. How Pathos checks imported details and proposed edits against the person's own record.

## More implementation notes

- [Keeping stream overlays in sync](scaling-streamer-online/) — Sharing updates across Streamer Online's browser sources, including the music display.
- [Giving a Twitch bot useful memory](chat-bot-memory/) — What ForgetMeNot keeps, how it chooses context, and where its memory can go wrong.

[My projects](https://github.com/thedevmark) · [Website](https://deutschmark.online) · [Twitch](https://twitch.tv/thedeutschmark)
