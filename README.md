# Suno Music Generation API Integration Guidance

As AI applications become more widespread, various AI programs have gradually become popular. AI has increasingly penetrated into many aspects of people's work and life. The industries involved in AI are also growing, from initial writing to healthcare education, and now to music.

Suno is a professional high-quality AI song and music creation platform. Users only need to input simple text prompts to generate songs with vocals based on genre style and lyrics. This AI music generator has been developed by team members from well-known technology companies such as Meta, TikTok, and Kensho, with the aim of allowing everyone to create wonderful music without the need for any musical instruments.

Suno has recently upgraded its music generation model to version V3, capable of generating songs of 2 minutes in length.

However, Suno does not officially provide an API; AceDataCloud provides a set of Suno APIs that simulate the official Suno interface, allowing users to conveniently and quickly generate desired music.

## Application and Usage

To use the Suno Audios API, first visit the [Suno Audios Generation API](https://platform.acedata.cloud/documents/4da95d9d-7722-4a72-857d-bf6be86036e9) page and click the "Acquire" button to obtain the necessary credentials for the request:

![](https://cdn.acedata.cloud/nyq0xz.png)

If you are not logged in or registered, you will be automatically redirected to the login page inviting you to register and log in; after logging in or registering, you will be returned to the current page.

Upon the first application, there will be a free quota provided to use the API for free.

## Basic Usage

For any song ideas, you can freely input a piece of text. For example, if I want to generate a song about Christmas, I can enter `a song for Christmas`, as shown in the image:

![](https://cdn.acedata.cloud/tsragd.png)

The generated code is as follows:

<p><img src="https://cdn.acedata.cloud/ohgrs3.png" width="500" class="m-auto"></p>

You can click the "Try" button to directly test the API, wait for 1-2 minutes, and the result is as follows:

```json
{
  "success": true,
  "data": [
    {
      "id": "2f16f7bc-4135-42c6-b3c5-6d6c49dc8cd5",
      "title": "Winter Wonderland",
      "image_url": "https://cdn1.suno.ai/image_2f16f7bc-4135-42c6-b3c5-6d6c49dc8cd5.png",
      "lyric": "[Verse]\nSnowflakes falling all around\nGlistening white\nCovering the ground\nChildren laughing\nFull of delight\nIn this winter wonderland tonight\nSanta's sleigh\nUp in the sky\nRudolph's nose shining bright\nOh my\nHear the jingle bells\nRinging so clear\nBringing joy and holiday cheer\n[Verse 2]\nRoasting chestnuts by the fire's glow\nChristmas lights\nThey twinkle and show\nFamilies gathering with love and cheer\nSpreading warmth to everyone near",
      "audio_url": "https://cdn1.suno.ai/2f16f7bc-4135-42c6-b3c5-6d6c49dc8cd5.mp3",
      "video_url": "https://cdn1.suno.ai/2f16f7bc-4135-42c6-b3c5-6d6c49dc8cd5.mp4",
      "created_at": "2024-05-10T16:21:37.624Z",
      "model": "chirp-v3",
      "prompt": "A song for Christmas",
      "style": "holiday"
    },
    {
      "id": "5dca232b-17cc-4896-a2d1-4b59178bf410",
      "title": "Winter Wonderland",
      "image_url": "https://cdn1.suno.ai/image_5dca232b-17cc-4896-a2d1-4b59178bf410.png",
      "lyric": "[Verse]\nSnowflakes falling all around\nGlistening white\nCovering the ground\nChildren laughing\nFull of delight\nIn this winter wonderland tonight\nSanta's sleigh\nUp in the sky\nRudolph's nose shining bright\nOh my\nHear the jingle bells\nRinging so clear\nBringing joy and holiday cheer\n[Verse 2]\nRoasting chestnuts by the fire's glow\nChristmas lights\nThey twinkle and show\nFamilies gathering with love and cheer\nSpreading warmth to everyone near",
      "audio_url": "https://cdn1.suno.ai/5dca232b-17cc-4896-a2d1-4b59178bf410.mp3",
      "video_url": "https://cdn1.suno.ai/5dca232b-17cc-4896-a2d1-4b59178bf410.mp4",
      "created_at": "2024-05-10T16:21:37.624Z",
      "model": "chirp-v3",
      "prompt": "A song for Christmas",
      "style": "holiday"
    }
  ]
}
```

At this point, we have obtained the content of two songs, including titles, preview images, lyrics, audio, videos, and other information.

Field descriptions are as follows:

- success: Indicates whether the generation was successful, if successful it is `true`, otherwise it is `false`
- data: A list containing detailed information about the generated songs.
  - id: Song ID
  - title: Title of the song
  - image_url: Cover image of the song
  - lyric: Lyrics of the song
  - audio_url: Audio file of the song, opening it will yield an mp3 audio.
  - video_url: Video file of the song, opening it will yield an mp4 video.
  - created_at: Creation time
  - model: The model used, usually the latest v3 model
  - style: Style

## Custom Generation

If you want to customize the lyrics, you can enter the lyrics:

At this time, the `lyric` field can receive content similar to the following:

```
[Verse]\nSnowflakes falling all around\nGlistening white\nCovering the ground\nChildren laughing\nFull of delight\nIn this winter wonderland tonight\nSanta's sleigh\nUp in the sky\nRudolph's nose shining bright\nOh my\nHear the jingle bells\nRinging so clear\nBringing joy and holiday cheer\n[Verse 2]\nRoasting chestnuts by the fire's glow\nChristmas lights\nThey twinkle and show\nFamilies gathering with love and cheer\nSpreading warmth to everyone near
```

> Note, that `\n` in the lyrics indicates a line break. If you are unsure how to generate lyrics, you can use the lyrics generation API provided by AceDataCloud to generate lyrics through prompts, the API is [Suno Lyrics Generation API](https://platform.acedata.cloud/documents/514d82dc-f7ab-4638-9f21-8b9275916b08).

Next, to customize the song generation based on lyrics, title, and style, you can specify the following content:

- lyric: Lyric text
- custom: Fill in as `true` to indicate custom generation; this parameter defaults to false, which means using prompt generation.
- file: Title of the song.
- style: The style of the song, optional.

An example of a filled-in form is shown below:

![](https://cdn.acedata.cloud/quw76r.png)

After filling it out, the generated code is as follows:

<p><img src="https://cdn.acedata.cloud/d1jv3i.png" width="500" class="m-auto"></p>

Corresponding code:
```python
curl -X POST 'https://api.acedata.cloud/suno/audios' \
-H 'authorization: Bearer {token}' \
-H 'accept: application/json' \
-H 'content-type: application/json' \
-d '{
"lyric": "[Verse]\\nSnowflakes falling all around\\nGlistening white\\nCovering the ground\\nChildren laughing\\nFull of delight\\nIn this winter wonderland tonight\\nSanta's sleigh\\nUp in the sky\\nRudolph's nose shining bright\\nOh my\\nHear the jingle bells\\nRinging so clear\\nBringing joy and holiday cheer\\n[Verse 2]\\nRoasting chestnuts by the fire's glow\\nChristmas lights\\nThey twinkle and show\\nFamilies gathering with love and cheer\\nSpreading warmth to everyone near",
"custom": true
}'
```

Testing is allowed, and the generated effect is similar.

## Continue Generating

If you want to continue generating the song, you can set the `action` parameter to `extend`, and input the ID of the song to continue generating. The song ID can be obtained based on the basic usage as shown in the image below:

<p><img src="https://cdn.acedata.cloud/8vehrn.png" width="500" class="m-auto"></p>

At this time, the song ID can be seen as:

```
"id": "b9e9fa11-0bf3-47cd-a3d7-85735aee3e07"
```

> Note that the `id` in the lyrics is the ID of the generated song. If you do not know how to generate a song, you can refer to the basic usage above to generate a song.

Next, we must fill in the lyrics and customize the generation of the song. You can specify the following content:

- lyric: Lyric text
- custom: Fill in as `true`, representing custom generation. This parameter defaults to false, representing generation using `prompt`.
- style: The style of the song, optional.
- continue_at: The time in seconds to continue the existing audio. For example, 213.5 means continue to 3 minutes and 33.5 seconds.

An example of how to fill it out is shown below:

<p><img src="https://cdn.acedata.cloud/tbdaqu.png" width="500" class="m-auto"></p>

After filling it out, the code is automatically generated as follows:

<p><img src="https://cdn.acedata.cloud/zftqj4.png" width="500" class="m-auto"></p>

The corresponding Python code:

```python
import requests

url = "https://api.acedata.cloud/suno/audios"

headers = {
    "accept": "application/json",
    "authorization": "Bearer {token}",
    "content-type": "application/json"
}

payload = {
    "action": "extend",
    "prompt": "A song for Christmas",
    "audio_id": "b9e9fa11-0bf3-47cd-a3d7-85735aee3e07",
    "continue_at": 10,
    "style": "cute",
    "lyric": "la la la"
}

response = requests.post(url, json=payload, headers=headers)
print(response.text)
```

Click to run, and you can get a result as follows:

```json
{
  "success": true,
  "task_id": "baf55c32-1207-4bdf-bd00-32a864f0474d",
  "data": [
    {
      "id": "5a3d0054-a6c5-43a9-a348-eae22d1f0efe",
      "title": "",
      "image_url": "https://cdn2.suno.ai/image_5a3d0054-a6c5-43a9-a348-eae22d1f0efe.jpeg",
      "lyric": "la la la",
      "audio_url": "https://cdn1.suno.ai/5a3d0054-a6c5-43a9-a348-eae22d1f0efe.mp3",
      "video_url": "https://cdn1.suno.ai/5a3d0054-a6c5-43a9-a348-eae22d1f0efe.mp4",
      "created_at": "2024-07-25T11:15:49.320Z",
      "model": "chirp-v3.5",
      "prompt": null,
      "style": "cute",
      "duration": 7.96
    },
    {
      "id": "9ae90c96-adcf-4aad-a591-361485168f13",
      "title": "",
      "image_url": "https://cdn2.suno.ai/image_9ae90c96-adcf-4aad-a591-361485168f13.jpeg",
      "lyric": "la la la",
      "audio_url": "https://cdn1.suno.ai/9ae90c96-adcf-4aad-a591-361485168f13.mp3",
      "video_url": "https://cdn1.suno.ai/9ae90c96-adcf-4aad-a591-361485168f13.mp4",
      "created_at": "2024-07-25T11:15:49.321Z",
      "model": "chirp-v3.5",
      "prompt": null,
      "style": "cute",
      "duration": 4.2
    }
  ]
}
```

As can be seen, the result content is consistent with the above text, thus achieving the function of continuing song generation.

## Asynchronous Callback

Since the time it takes for Suno to generate music is relatively long, about 1-2 minutes, if the API does not respond for a long time, the HTTP request will keep the connection open, leading to extra system resource consumption. Therefore, this API also provides support for asynchronous callbacks.

The overall process is: When the client initiates a request, an additional `callback_url` field needs to be specified. After the client initiates the API request, the API will immediately return a result containing a field for `task_id`, representing the current task ID. When the task is completed, the generated music result will be sent to the client-specified `callback_url` via POST JSON format, which also includes the `task_id` field, thus allowing the task result to be associated through the ID.

Next, let’s understand in detail how to operate through an example.

First, the Webhook callback is a service that can receive HTTP requests, and developers should replace it with the URL of their own HTTP server. For demonstration purposes, we will use a public Webhook sample website https://webhook.site/. Opening this site will provide a Webhook URL, as shown in the image below:

![](https://cdn.acedata.cloud/fwfqin.png)

Copy this URL, and it can be used as the Webhook. The example here is https://webhook.site/03e60575-3d96-4132-b681-b713d78116e2.

Next, we can set the `callback_url` field to the above Webhook URL, and fill in the `prompt`, as shown below:

![](https://cdn.acedata.cloud/x8xql1.png)

Click to run, and you will immediately see a result as follows:

```
{
  "task_id": "44472ab8-783b-4054-b861-5bf14e462f60"
}
```

After a while, we can observe the generated song results at https://webhook.site/03e60575-3d96-4132-b681-b713d78116e2, as shown in the image below:

![](https://cdn.acedata.cloud/f9kosb.png)

The content is as follows:
```json
{
  "success": true,
  "task_id": "44472ab8-783b-4054-b861-5bf14e462f60",
  "data": [
    {
      "id": "da4324e5-84b2-484b-b0e9-dd261381c594",
      "title": "Winter Whispers",
      "image_url": "https://cdn1.suno.ai/image_da4324e5-84b2-484b-b0e9-dd261381c594.png",
      "lyric": "[Verse]\nSnow falling gently from the sky\nChildren giggling as they pass by\nFire crackling\nCozy and warm\nChristmas spirit begins to swarm\n[Verse 2]\nTwinkling lights\nA sight to behold\nStockings hung\nWaiting to be filled with gold\nGifts wrapped with love\nPiled high\nExcitement in the air\nYou can't deny\n[Chorus]\nWinter whispers in the wind\nJoy and love it brings\nLet's celebrate this season\nWith the ones we're missing",
      "audio_url": "https://cdn1.suno.ai/da4324e5-84b2-484b-b0e9-dd261381c594.mp3",
      "video_url": "https://cdn1.suno.ai/da4324e5-84b2-484b-b0e9-dd261381c594.mp4",
      "created_at": "2024-05-11T07:33:05.430Z",
      "model": "chirp-v3",
      "prompt": "A song for Christmas",
      "style": "pop"
    },
    {
      "id": "b878a87b-a0db-4046-8ccd-ecd2fb3d4372",
      "title": "Winter Whispers",
      "image_url": "https://cdn1.suno.ai/image_b878a87b-a0db-4046-8ccd-ecd2fb3d4372.png",
      "lyric": "[Verse]\nSnow falling gently from the sky\nChildren giggling as they pass by\nFire crackling\nCozy and warm\nChristmas spirit begins to swarm\n[Verse 2]\nTwinkling lights\nA sight to behold\nStockings hung\nWaiting to be filled with gold\nGifts wrapped with love\nPiled high\nExcitement in the air\nYou can't deny\n[Chorus]\nWinter whispers in the wind\nJoy and love it brings\nLet's celebrate this season\nWith the ones we're missing",
      "audio_url": "https://cdn1.suno.ai/b878a87b-a0db-4046-8ccd-ecd2fb3d4372.mp3",
      "video_url": "https://cdn1.suno.ai/b878a87b-a0db-4046-8ccd-ecd2fb3d4372.mp4",
      "created_at": "2024-05-11T07:33:05.430Z",
      "model": "chirp-v3",
      "prompt": "A song for Christmas",
      "style": "pop"
    }
  ]
}
```
