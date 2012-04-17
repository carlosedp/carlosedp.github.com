---
layout: post
title: "Kindle 4 review, eBook management and removing DRM"
published: false
---


# Separate into two parts

## Kindle 4 review


## eBook and content management

RSS feeds on Calibre

Instapaper

## Bonus topic on removing DRM

In my experience, you can find pretty much everything on Amazon Kindle store. Also they have great prices and almost beat the rest of the market.

But of course you may want an option of getting ebooks from other sources like Barnes and Noble, booksamillion or bookstores outside U.S. like Livraria Cultura or Saraiva for Brazilian portuguese titles. All of these retailers sells ebooks with Adobe DRM.

The easiest way to handle ebooks from another sources is installing a plugin into Calibre itself. After installing it, the plugin will automatically import the DRM'ed epub, remove the DRM and convert to Kindle format.

First, you need to download and install [Calibre](http://calibre-ebook.com/). 

After it, get [Adobe Digital Editions](http://www.adobe.com/products/digitaleditions/). ADE is an ebook reader software that already comes with it's own certificate key. This key will be used by the plugin to remove DRM and successfully convert the ebook to Kindle. Install it as well.

Then, download plugin file: [ineptepub_v01.7_plugin.zip](http://carlosedp.com/files/ineptepub_v01.7_plugin).

### Plugins Installation:

Go to Calibre's Preferences page. Under "Advanced" click on the Plugins button.

Use the "Load plugin from file" button to select the plugin's zip file (ineptepub_v01.7_plugin.zip) and click the 'Add' button. you're done.

<img src="/images/2012-04-16-a-brief-kindle-4-review-and-ebook-management/advanced-plugins.jpg" alt="Adv Prefs" class="center">

<img src="/images/2012-04-16-a-brief-kindle-4-review-and-ebook-management/apply.jpg" alt="Apply" class="center">

Please note:  Adding the plugin was a success, Calibre will show the item in File Type plugins--Inept Epub DeDRM(0.1.7) by DiapDealer(as the images show). You can always click on the File-Type plugins to see if the plugin was added.

## Configuration:

When first run, the plugin will attempt to find your Adobe Digital Editions installation (on Windows and Mac OS's). If successful, it will create an 'adeptkey.der' file and save it in Calibre's configuration directory. It will use that file on subsequent runs. If there are already '*.der' files in the directory, the plugin won't attempt to find the Adobe Digital Editions installation installation.

After this, all you do is add a new epub book with DRM into Calibre, convert it into MOBI (Kindle format) and send to yout device. The conversion should work without errors.


