---
title: HaH-zip-file
tags:
---
Since the H@H download was a folder and personally I don't like fragmented small files, I would need to compress the folder once the download was finished. 
The next step was to set up a script to watch the download and compress it when the download is done.
Fortunately the `galleryinfo.txt` was the last file created for a gallery download, we can use the creation of this file as an indication for the finish of the download.