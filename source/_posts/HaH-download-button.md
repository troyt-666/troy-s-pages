---
title: Add a download button for ExHentai search page!
date: 2024-10-25 03:49:24
tags:
---
Trying to create my own LANraragi collection, I was bulk downloading from E-Hentai recently.
I first tried to create a simple [Tempermonkey script](https://greasyfork.org/scripts/510654-exhentai-archive-download-button) to allow me download the archive using the given archive download directly from the search page.

No surprise, problems arised. The problems come from the followings:

- E-Hentai put a lot of restrictions on downloading. First of all your downloader has to be limited to 4 threads, or it will just throw you an error. Even if you have done that, bulk downloading too short time between each download can still give you HTTP `429 Too Many Requests` error. Not good.
- The other problem comes from LANraragi, or more specificly the E-Hentai pluging to retrieve metadata for the archive. Some times it just strait failed to retrieve anything. Enabling "Fetch using thumbnail first" can somewhat alleviate it but the mismatch is annoying, my raws were marked as Korean translation, nonsense.
- What caught my attention was the HentaiAtHome plugin came with LANraragi, that it reads the `galleryinfo.txt` which contains the metadata, especially tags for the gallary. There is usually very little mislabeled tag, without uncertainty and mismatches, this approach is certainly a more appropriate to sort my library out.

The next steps were easy, since in the earlier version of the script I have handled the archive download, initiating H@H download is simply simulating clicking a button.
It was even easier since I didn't need to handle the download link (there was waiting before the link was generated).

Since the H@H download was a folder and personally I don't like fragmented small files, I would need to compress the folder once the download was finished. 
The next step was to set up a script to watch the download and compress it when the download is done.
Fortunately the `galleryinfo.txt` was the last file created for a gallery download, we can use the creation of this file as an indication for the finish of the download.