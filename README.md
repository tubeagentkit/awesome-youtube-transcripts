# Awesome YouTube Transcripts

A curated list of libraries, APIs, MCP servers, agent skills and apps for getting the transcript or subtitles of a YouTube video, plus speech-to-text tools for videos that have no captions.

Entries are open source unless they are in [Hosted APIs](#hosted-apis). Star counts change, so none are listed; every repo here had a commit in the last 12 months when it was added.

## Contents

- [Which tool should I use?](#which-tool-should-i-use)
- [Libraries](#libraries)
- [Speech-to-text for videos without captions](#speech-to-text-for-videos-without-captions)
- [Hosted APIs](#hosted-apis)
- [MCP servers](#mcp-servers)
- [Agent skills](#agent-skills)
- [Framework integrations](#framework-integrations)
- [Summarizers and apps](#summarizers-and-apps)
- [Bulk and archiving](#bulk-and-archiving)
- [Guides and references](#guides-and-references)

## Which tool should I use?

| You want to | Start with |
| --- | --- |
| Fetch captions from a script on your own machine | [youtube-transcript-api](https://github.com/jdepoix/youtube-transcript-api) (Python) or [YouTube.js](https://github.com/LuanRT/YouTube.js) (JavaScript) |
| Download subtitle files from the command line | [yt-dlp](https://github.com/yt-dlp/yt-dlp#subtitle-options) with `--write-subs --write-auto-subs --skip-download` |
| Transcribe a video that has no captions | [faster-whisper](https://github.com/SYSTRAN/faster-whisper) or [whisper.cpp](https://github.com/ggml-org/whisper.cpp) on the downloaded audio |
| Fetch transcripts from a server or cloud function | A [hosted API](#hosted-apis), or a library behind your own proxies. YouTube often blocks requests from cloud IP ranges ([details](https://github.com/jdepoix/youtube-transcript-api#working-around-ip-bans-requestblocked-or-ipblocked-exception)) |
| Let an AI assistant read YouTube videos | An [MCP server](#mcp-servers) or an [agent skill](#agent-skills) |

## Libraries

### Python

- [youtube-transcript-api](https://github.com/jdepoix/youtube-transcript-api) - Fetches manual and auto-generated transcripts, lists available languages and translates them. No API key or headless browser. Includes a CLI.
- [yt-dlp](https://github.com/yt-dlp/yt-dlp) - The standard video downloader. Its [subtitle options](https://github.com/yt-dlp/yt-dlp#subtitle-options) save captions as VTT, SRT or JSON3 without downloading the video.

### JavaScript and TypeScript

- [YouTube.js](https://github.com/LuanRT/YouTube.js) - Client for YouTube's internal InnerTube API. `getTranscript()` returns timed segments ([example](https://github.com/LuanRT/YouTube.js/tree/main/examples/transcript)).
- [youtube-transcript](https://github.com/Kakulukian/youtube-transcript) - Small npm package with a single `fetchTranscript()` call. Uses an unofficial endpoint, so it can break when YouTube changes.

## Speech-to-text for videos without captions

- [Whisper](https://github.com/openai/whisper) - OpenAI's open speech recognition model, the base most tools below build on.
- [faster-whisper](https://github.com/SYSTRAN/faster-whisper) - Whisper reimplemented on CTranslate2. Several times faster than the original with lower memory use.
- [whisper.cpp](https://github.com/ggml-org/whisper.cpp) - Whisper in C/C++. Runs on CPU, Apple Silicon and small devices.
- [WhisperX](https://github.com/m-bain/whisperX) - Adds word-level timestamps and speaker diarization to Whisper.
- [insanely-fast-whisper](https://github.com/Vaibhavs10/insanely-fast-whisper) - CLI for batched Whisper transcription on GPUs.

## Hosted APIs

Use these when you need transcripts from servers that YouTube blocks, or don't want to run proxies. All are commercial services; check each site for current pricing and limits.

- [GetYouTubeTranscript](https://getyoutubetranscript.com) - REST API and remote MCP server for transcripts, YouTube search, channels and playlists. Python and Node SDKs.
- [SearchAPI](https://www.searchapi.io/docs/youtube-transcripts) - YouTube transcripts endpoint inside a general search API.
- [Supadata](https://supadata.ai) - Transcripts and metadata for YouTube, TikTok, Instagram, X, Facebook and web pages.
- [TranscriptAPI](https://transcriptapi.com) - YouTube transcripts, search, channels and playlists, with an MCP server.
- [TranscriptOut](https://transcriptout.com) - YouTube transcript API with agent skills and an MCP server.
- [YouTube Transcript (youtube-transcript.io)](https://www.youtube-transcript.io) - Web tool and API for YouTube transcripts.

## MCP servers

[Model Context Protocol](https://modelcontextprotocol.io) servers let Claude, Cursor, VS Code and other MCP clients read YouTube videos.

- [jkawamoto/mcp-youtube-transcript](https://github.com/jkawamoto/mcp-youtube-transcript) - Transcripts and metadata, with automatic pagination for long videos and proxy settings.
- [kimtaeyoon83/mcp-server-youtube-transcript](https://github.com/kimtaeyoon83/mcp-server-youtube-transcript) - One `get_transcript` tool, installable through Smithery.
- [anaisbetts/mcp-youtube](https://github.com/anaisbetts/mcp-youtube) - Downloads subtitles with a local yt-dlp install.
- [tubeagentkit/youtube-mcp](https://github.com/tubeagentkit/youtube-mcp) - Transcripts, search, channels and playlists through the GetYouTubeTranscript API. Remote HTTP or local stdio.
- [ZeroPointRepo/youtube-mcp](https://github.com/ZeroPointRepo/youtube-mcp) - Transcripts, search, channels and playlists through the TranscriptAPI service.

## Agent skills

[Agent Skills](https://agentskills.io) are folders of instructions that Claude Code, Cursor, Codex and similar agents load when a task matches.

- [artemchuikin/youtube-skills](https://github.com/artemchuikin/youtube-skills) - Twelve skills for transcripts, search, channels and playlists through TranscriptOut.
- [JimmySadek/video-fetcher-to-markdown](https://github.com/JimmySadek/video-fetcher-to-markdown) - Turns YouTube, Instagram, TikTok and X video links into Obsidian-ready Markdown notes.
- [michalparkola/tapestry-skills](https://github.com/michalparkola/tapestry-skills) - Claude Code skills that download articles, PDFs and YouTube transcripts as sources.
- [tubeagentkit/youtube-transcript-skills](https://github.com/tubeagentkit/youtube-transcript-skills) - Transcripts, search, channels and playlists through the GetYouTubeTranscript API. Shell scripts, no runtime to install.
- [zarazhangrui/youtube-to-ebook](https://github.com/zarazhangrui/youtube-to-ebook) - Claude skill that turns transcripts from chosen channels into EPUB ebooks.
- [ZeroPointRepo/youtube-skills](https://github.com/ZeroPointRepo/youtube-skills) - Transcripts, search, channels and playlists through TranscriptAPI.

## Framework integrations

- [LlamaIndex YoutubeTranscriptReader](https://developers.llamaindex.ai/python/framework-api-reference/readers/youtube_transcript/) - Built-in LlamaIndex reader that loads transcripts as Documents.
- [llama-index-readers-getyoutubetranscript](https://github.com/tubeagentkit/llama-index-readers-getyoutubetranscript) - LlamaIndex reader backed by the GetYouTubeTranscript API.
- [getyoutubetranscript-haystack](https://github.com/tubeagentkit/getyoutubetranscript-haystack) - Haystack component that returns transcripts as Documents.
- [n8n-nodes-getyoutubetranscript](https://github.com/tubeagentkit/n8n-nodes-getyoutubetranscript) - n8n community node for transcripts, search, channels and playlists.
- [dify-plugin-getyoutubetranscript](https://github.com/tubeagentkit/dify-plugin-getyoutubetranscript) - Dify tool plugin for transcripts with timestamps.

## Summarizers and apps

- [martinopiaggi/summarize](https://github.com/martinopiaggi/summarize) - Summarizes videos from YouTube and 10 other sources into Markdown with any OpenAI-compatible model. CLI, Streamlit, HTTP API and Docker.
- [Milkshiift/YouTubeTLDR](https://github.com/Milkshiift/YouTubeTLDR) - Lightweight self-hosted YouTube summarizer using Gemini.
- [PaoloJN/recap](https://github.com/PaoloJN/recap) - YouTube summaries, a searchable transcript and chat about the video.
- [zarazhangrui/youtube-digest](https://github.com/zarazhangrui/youtube-digest) - Turns videos into study material with transcripts, bilingual translation and notes.
- [DevRico003/youtube_summarizer](https://github.com/DevRico003/youtube_summarizer) - Next.js app for AI summaries of YouTube videos.
- [jimmc414/onefilellm](https://github.com/jimmc414/onefilellm) - Combines GitHub repos, papers, web pages and YouTube transcripts into one text file for an LLM prompt.

## Bulk and archiving

- [openzim/youtube](https://github.com/openzim/youtube) - Packs a channel or playlist, with its subtitles, into an offline ZIM archive for Kiwix.
- [Ebrizzzz/Youtube-playlist-to-formatted-text](https://github.com/Ebrizzzz/Youtube-playlist-to-formatted-text) - Desktop app that pulls a playlist's transcripts and turns them into a formatted book with Gemini.
- [Dicklesworthstone/bulk_transcribe_youtube_videos_from_playlist](https://github.com/Dicklesworthstone/bulk_transcribe_youtube_videos_from_playlist) - Transcribes a whole playlist with Whisper.

## Guides and references

- [Working around IP bans](https://github.com/jdepoix/youtube-transcript-api#working-around-ip-bans-requestblocked-or-ipblocked-exception) - Why transcript requests from cloud servers get `RequestBlocked` or `IpBlocked`, and how proxies help.
- [yt-dlp subtitle options](https://github.com/yt-dlp/yt-dlp#subtitle-options) - Every flag for choosing subtitle languages and formats.
- [youtube-transcript-errors](https://github.com/tubeagentkit/youtube-transcript-errors) - What each transcript error means, what triggers it and what to do about it.
- [youtube-transcript-benchmark](https://github.com/tubeagentkit/youtube-transcript-benchmark) - Open, reproducible comparison of transcript methods by success rate and latency.

## Contributing

Pull requests are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

This list is maintained by the team behind GetYouTubeTranscript, so some entries are our own projects. Competing tools are listed on the same terms, and a PR that improves a description of ours is as welcome as any other.

## License

[CC0 1.0](LICENSE). To the extent possible under law, the contributors have waived all copyright to this list.
