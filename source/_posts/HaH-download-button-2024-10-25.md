---
title: Add a download button for ExHentai search page!
date: 2024-10-25 03:49:24
tags:
---

ExHentai is a great place for hentai manga, the only problem is that it's been too popular to be targeted by copyright strike all the time.
I cannot remember how many times I click into a favorated gallery only to find it was removed by FAKKU/irodori... you name it, in those theoretically uncensored Comic X-EROS chapters you will only find lightsaberred penis.
While I was fiddling with my NAS, I was wondering if I could build a library for my already downloaded manga, and I ran into [LANraragi](https://github.com/Difegue/LANraragi), which starts a server for archival and reading of manga/doujinshi.
I was running on a QNAP and recently moved to a mini PC with Unraid, both systems have decent support of docker, so it is quite easy to get LANraragi running, just map the library directory to your folder storing your manga/doujinshi, it should start and scan your library and you should see your manga at the port you mapped to.

Now that we have the server ready, it's time to populate it with Trying to create my own collection, I was bulk downloading from E-Hentai recently.
I first tried to create a simple [Tempermonkey script](https://greasyfork.org/scripts/510654-exhentai-archive-download-button) to allow me download the archive using the given archive download directly from the search page.

No surprise, problems arose. The problems come from the followings:

- E-Hentai put a lot of restrictions on downloading. First of all your downloader has to be limited to 4 threads, or it will just throw you an error. Even if you have done that, bulk downloading too short time between each download can still give you HTTP `429 Too Many Requests` error. Not good.
- The other problem comes from LANraragi, specificly the E-Hentai plugin to retrieve metadata for the archive. Sometimes, it just failed to retrieve anything. Enabling "Fetch using thumbnail first" can somewhat alleviate it but the mismatch is annoying, my raws were marked as Korean translation, nonsense.
- What caught my attention was the HentaiAtHome plugin came with LANraragi, that it reads the `galleryinfo.txt` which contains the metadata, especially tags for the gallary. There is usually very little mislabeled tag, without uncertainty and mismatches, this approach is certainly a more appropriate to sort my library out.

The next steps were easy, since in the earlier version of the script I have handled the archive download, initiating H@H download is simply simulating clicking a button.
It was even easier since I didn't need to handle the download link (there was waiting before the link was generated).

Finally! The script is up and run without major issue.
By just clicking the button, the archive will automatically be downloaded to my Hentai@Home server for me to sort them out later, it looks like this:

![Screenshot of the download button in action](download-button.png)

Each gallery downloaded by Hentai@Home is stored as a folder.
Therefore, we will need to set up a program to watch the download and automatically zip it.
It's another long story and I haven't found a solution for it yet, maybe we can save it for another post.