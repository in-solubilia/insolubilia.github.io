---
title: how this site was made
description: Some tips and tricks.
date: 2025-09-21T14:27:15+00:00
draft: false
---
I like [Neocities.](https://neocities.org/) Unfortunately, I am also lazy, and the (admittedly minimal) sequence of operations needed to upkeep [Zonelets](https://zonelets.net/) + [ZoneRSS](https://adamledoux.net/zoneRSS/) had me wondering if things could be easier.

4rkal has a [fantastic guide](https://4rkal.com/posts/obsidianhugo/) for publishing an [Obsidian vault](https://obsidian.md/) to a website via [Hugo](https://gohugo.io/), a Github repo, and [Render](https://render.com/), and this guide was pretty much all I needed, save for a few adjustments.

Obsidian is packed with features, which also leads to it having a reputation for a high learning curve; to either my own advantage or detriment, I hardly use any of them. I have some basic folders: one for highlights taken from books, one for highlights taken from articles, one for my own writing, and then one loose to-do document. Then, everything gets sorted into subfolders based on source, topic, or project. I use the tagging system somewhat frivolously to see the big mind map graphic float around, but that's it. I appreciate that Obsidian allows you to create multiple vaults for further organization, but I like having all of my stuff in one place for ease of searching and editing.

So, instead of syncing the whole vault, I opted to sync one new designated folder within the vault, and the contents of that folder will become the content on the website.

Fun fact: Github does not like it if you sign up with an alias email. Which makes sense as a spam prevention method; I should have thought of that before tossing one of my Proton aliases in there. However, it does not *stop* you from signing up with an alias; it identifies the fact that you used one 10-30 minutes later, and then they lock your account. The only indication that my account was locked was that I could not hook Render into my repo, because third-party integration was turned off. I was able to appeal-- though any ticket you make has commenting rights tied to the email you sent it with, so I had to submit a second ticket after I got the email addresses swapped around. So: don't use temp or alias email services when creating a Github account!

After getting Hugo set up, my Github repo set up, and my Render account set up as per the linked tutorial, I made some adjustments to the synchronization process. Of note is that I am doing all of this on Linux. My sync script is as follows: 

```
rsync -az --delete-after "Obsidian/MyNotes/WebsitePosts/" "MyWebsite/content/posts/"
cd quickstart
git init 
hugo --buildDrafts --cleanDestinationDir --baseURL=https://insolubilia.blog/ --appendPort=false 
git add . --all
git commit -a -m "new commit"
git branch -M main
git remote add origin https://github.com/path/to/my/repo
git push -f -u origin main
```

I don't particularly care about version control on my website, so I felt OK with just having the repo folder directly match the Hugo build, and to have the Hugo posts folder directly match the Obsidian folder, and with having Hugo clean up the ten billion CSS files it made as I was messing around with the layout. I also ran into the default Hugo settings plugging my baseURL in correctly about 75% of the time and having a few links still go to localhost after publishing, so the extra commands on the Hugo server line are to fix that. These commands may be redundant or badly constructed. I am totally new to using Hugo + an amateur at Linux, so I am here primarily by the good graces of the tutorial and a mosiac of search results.

After that, I saved that sync script and configured it to run in response to a keyboard shortcut. So, I can update my website by just pressing ctrl+H. 

I also bought a domain off [Porkbun](https://porkbun.com/). The branding is a bit twee, but the pricing felt much more straightforward than some of the other options that I looked at, and they were given positive (and not astroturf-seeming) reviews on Reddit. Unless things change, this website will cost me a little under 30$/year (with a severe discount on the first year, which a lot of other sites offer, as well; it cost about 2.50\$ to start.) The DNS setup (they partner with [Cloudflare](https://www.cloudflare.com/) for it) is pretty comparable to what's described in the [additional tutorial](https://4rkal.com/posts/thisblog?utm_source=internal&utm_campaign=obsidianhugo); I added CNAME and alias records that pointed towards the Render publish. I also really like that on Render's side, it has a clear UI that tells you if the DNS records are configured correctly + if certificates are in place. Speaking of which, as per Render's recommendation, I did also add CAA records for letsencrypt and google. There's a tutorial on the DNS section of Render's site management page that shows how to do it. 

This site's theme is an adjusted version of [Archie](https://github.com/athul/archie). I just added the Flammarion engraving as a new div called "logo" in the theme's head layout (`MyWebsite/themes/archie/layouts/partials/head.html`) Like so: 

```
<header>
	<div class="main">
		<a href="{{ absLangURL "/" }}">{{ .Site.Title }}</a>
		<div class="logo"><img src="{{ absURL "../flammarion.png" }}"></img></div>
	</div>
	<nav>
		{{ range .Site.Menus.main }}
		<a href="{{ .URL }}">{{ .Name }}</a>
		{{ end }}
		{{ if eq .Site.Params.mode "toggle" -}}
	| <span id="dark-mode-toggle" onclick="toggleTheme()">{{template "feathericon" (dict "UseCDN" .Site.Params.useCDN "Icon" "sun") }}</span>
		<script src="{{ absURL "js/themetoggle.js" }}"></script>
		{{ end }}
	</nav>
</header>

```

And added to the css (`MyWebsite/themes/archie/assets/css/main.css)`:

```
.logo {
	position: absolute;
	right: 0;
	max-width: 200px;
	height: auto;
}

.logo img {
	outline: 10px outset var(--accent);
	}
```

I may update this document as I make further tweaks to the config.