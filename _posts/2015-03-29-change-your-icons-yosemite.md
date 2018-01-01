---
title: "Change Your Icons on Yosemite with Scripting 🔧"
date: 2015-03-29
excerpt: I got tired of Yosemite's icons and decided to take some initiative without the usual dependency on an app. It took about 2 days for me to perfect this strategy and now it's time to make your process a lot easier than mine.
header:
    image: //fvcproductions.files.wordpress.com/2015/03/banner-new-icons.png?w=1024&h=435&crop=1
---

> for all you machines out there

**Index**

1. [Intro](#section-intro)
2. [Tools](#section-tools)
3. [Step 1 - Get Your Icons](#section-step1)
4.  [Step 2 - Get The Command](#section-step2)
5.  [Step 3 - Execute Command](#section-step3)

Intro
-----

So maybe you got tired of Yosemite's icons. That's cool.

Even without apps like the once legendary
[`CandyBar`](//www.panic.com/blog/candybar-mountain-lion-and-beyond/ "CandyBar")
or [`LiteIcon`](//www.freemacsoft.net/liteicon/ "LiteIcon"), you
can still change all your icons. No more dependencies!

I got tired of Yosemite's icons and decided to take some initiative
without the usual dependency on an app. It took about 2 days for me to
perfect this strategy and now it's time to make your process a lot
easier than mine.

Tools
-----

-   `Terminal`
-   your favorite set of icons
-   some patience

Step 1 - Get Your Icons
=======================

[DeviantArt](//www.deviantart.com "DeviantArt") is my go-to place
for icons sets, but you can also try
[IconArchive](//www.iconarchive.com/ "IconArchive") for a broader
range of options.

If you like the app icons I show in these pictures, then you're welcome
to download them from my Dropbox.

[![Bubble Icons - Default
Apps](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-27-11-32-49.png)](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-27-11-32-49.png)[![Bubble
Icons -
Utility](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-27-11-47-53.png)](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-27-11-47-53.png)

### [Here is a `ZIP` file of the icons and commands used in this tutorial.](//github.com/fvcproductions/customize-icons "Icons")

*A special thanks to these guys for the amazing circular icons that I
use in this how-to.*

- [Sebastian de With](//dewith.com/ "deWith")
- [All the contributors to `Yoios` on
    GitHub](//github.com/mmarfil/yoios "Yoios")

Step 2 - Get The Command
========================

I include this command file in the [`ZIP`
file](//github.com/fvcproductions/customize-icons "Icons")
mentioned in **Step 1**, but for reference, here is the code for the
`ChangeIcons.command`.

```
\#!/usr/bin/env ruby

require 'json'\
require 'shellwords'

if ENV\['USER'\] != 'root'\
puts "You'll be prompted once to enter you administrator password."\
end

Dir.chdir(File.dirname(\_\_FILE\_\_)) do

file = File.read(%Q(.set\_icons/icon\_data.json))\
icon\_data = JSON.parse(file)

icon\_data.each do |key, value|

app\_path = "/Applications/\#{key}"

if Dir.exists?(app\_path) and File.exists?("\#{value}.icns")\
puts "Changing icon for \#{app\_path}"\
\`sudo .set\_icons/setfileicon "\#{value}.icns" "\#{app\_path}"\`\
end

end

puts "Restarting Finder and the Dock"\
\# \`killall Dock\`\
\# \`killall Finder\`

puts %Q(Finished!)

end\


Now here comes the tricky part. This command relies on a `JSON` file
that is named `icon-data.json` and a `UNIX Executable File` called
`setfileicon`.

[![All The Icons Folder Screenshot -
1](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-28-23-10-54.png)](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-28-23-10-54.png)[![All
The Icons Screenshot -
2](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-28-23-11-18.png)](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-28-23-11-18.png)

These files are both included in a folder called `set_icon` in the
[`ZIP` file](//github.com/fvcproductions/customize-icons "Icons")
provided in **Step 1**.

The `icon-data.json` file looks something like this:

```{\
"1Password 5.app":"1Password 5",\
"Alfred 2.app":"Alfred 2",\
"Amphetamine.app":"Amphetamine"\
}\
```

It is formatted with the name of the app first in quotes followed by a
semi-colon and then the name of the `icns` file.

Edit this `icon-data.json` file to include your own apps or create it
yourself using your favorite text-editor.

Here is how the `JSON` file for the Utilities looks like.

[![JSON
file](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-28-23-49-06.png)](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-28-23-49-06.png)

It is `case-sensitive`, so make sure to type everything correctly to
suit what the app is called and what you named the corresponding `icns`
file.

> When you are editing this file to add on your own apps, make sure
> there's not a comma on the last line or there will be an error.

Now, using `Terminal`, type in the following:
`defaults write com.apple.finder AppleShowAllFiles YES`. Once you press
`Enter`, this command will show all the hidden files on your Mac. Don't
mess with any of these hidden files. The reason Apple hides them is so
that the user has less of a chance of messing things up.

> To make the files hidden again later, type in the same command but
> with a NO at the end like this:
> `defaults write com.apple.finder AppleShowAllFiles NO`.

After that, type in `killall Finder` into Terminal for the command to
restart the Finder and have the hidden files be revealed in your Finder.

[![Show Hidden Files Command in
Terminal](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-29-00-21-37.png)](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-29-00-21-37.png)

Now that you have your Finder revealing all the hidden files - in the
folder where you have all your icons properly named, copy and paste the
folder `set_icons` from the [`ZIP`
file](//github.com/fvcproductions/customize-icons "Icons")
mentioned in **Step 1**, and rename it to `.set_icons`. Adding a period
in front of the folder name makes it hidden and you will therefore not
be able to see it anymore.

It looks exactly like the `.set_icons` folder already included within
the folder called `Utilities` that can be found in the [`ZIP`
file](//github.com/fvcproductions/customize-icons "Icons").

[![Utility
Sub-Folder](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-28-23-11-42.png)](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-28-23-11-42.png)

So if you want to change your Utility icons as well, the `.set_icons`
folder located in the sub-folder `Utilities` already has the `json` file
with all the necessary modifications.

> The only difference between the `ChangeIcons.command` within the
> `All The Icons` folder and the
> `ChangeUtilityIcons.command located within the`Utilities
> folder`is that on Line 36, the app path is listed as`app\_path =
> "/Applications/Utilities/\#{key}"\`.

*A special thanks to [James
Moore](//twitter.com/foozmeat "James Moore"), who created the
`ChangeIcons.command` to replace all the icons and Damien Bobillot who
created the `setfileicon` UNIX Executable File.*

Step 3 - Execute Command
========================

> otherwise known as `TLDR`

Now you probably have something like the following:

-   a folder called `All The Icons` with
    -   all the icons you want to replace your old ones (in `icns`
        format)
    -   the `ChangeIcons.command` that was included in this [`ZIP`
        file](//github.com/fvcproductions/customize-icons "Icons")
    -   a *hidden* sub-folder called `.set_icons` with
        -   a modified `icon-data.json` file to include your own
            personal apps
        -   the `setfileicon` UNIX executable file

At this point, if you've done everything right, you can "hide" your
hidden files again in your Finder by executing the command
`defaults write com.apple.finder AppleShowAllFiles NO` in `Terminal`.
Make sure to execute `killall Finder` as well so that your Finder
restarts and shows the changes.

Now go ahead and click the `ChangeIcons.command` to change all your
icons simultaneously.

[![ChangeIcons.command in
Terminal](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-29-00-01-44.png)](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-29-00-01-44.png)

You will be prompted to enter your password and *walla* you have all
your snazzy new icons in place in seconds!

> If you want to change your Utility icons as well, go ahead and click
> `ChangeUtilityIcons.command` too within the sub-folder called
> `Utilities`, assuming you properly named all the icons so that it
> works with the `json` file that is shown in **Step 2**.

### **Possible Errors You May Encounter**

-   You tried to edit the command files and now have a syntax error,
    like in the form of quotes - just make sure to use *straight
    quotes*.
-   You have a syntax error in your `icon-data.json` file, like a comma
    on the last line.
-   You forgot to include a certain app in your `icon-data.json` file
    and so the icon does not change when you execute the command.
-   An app is locked and, therefore, the icon cannot be changed. To
    unlock an app, go to the app, right click,  `Get Info`. Uncheck the
    `Locked` button.

[![Locked App Error In
Terminal](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-29-00-01-54.png)](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-29-00-01-54.png)[![Locked
App -
Dropbox](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-29-00-09-37.png)](//fvcproductions.files.wordpress.com/2015/03/screenshot-2015-03-29-00-09-37.png)

### Have fun with your new icons! 😍

> Tips or tricks?
>
> > contact me
> > [@fvcproductions](//twitter.com/fvcproductions "FVCproductions")
