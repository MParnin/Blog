---
title: "Blog Initial Configuration"
description: "Brief walkthrough of the steps taken to create this blog in Linux"
date: 2023-03-02
#weight: 1
author: MP
---
## Installing/Updating Hugo
1. Make sure installed version of Go is >= 1.18: 
	1. Check Go version: `go version`
		1. Install/update Go: https://go.dev/doc/install
	2. Check Hugo: `hugo version`
		1. Update Hugo:
			1. Download latest version: https://github.com/gohugoio/hugo/releases
			2. Install .deb file: `sudo dpkg --install ./hugo_0.110.0_linux-amd64.deb`

## Creating a New Site
1. Install Hugo and prerequisites: https://gohugo.io/installation/
2. Create two repositories on Github:
	1. "Blog Repository" - Repository for storing website code: "Blog"
		1. Make Public, no README, simply click "Create repository"
	2. "Production Repository" - Repository for deploying website that's hosted through Github Pages: "MParnin.github.io"
		1. Make Public, no README, simply click "Create repository"
3. Choose theme for site: https://themes.gohugo.io/ (PaperMod was used for this site)
4. Clone "Blog" to local machine: `git clone git@github.com:MParnin/Blog.git`
5. Change to "Blog" directory: `cd Blog`
6. Create a new Hugo site: `hugo new site MParnin.github.io`
7. Change to new directory: `cd MParnin.github.io`
8. Clone theme to newly created boiler plate code for website: `git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1`
9. Setup the config file:
	1. Open the config file in a text editor: `code config.toml`
	2. Add the theme to the end of the config file: `theme = "PaperMod"`
	3. Change the title: `MP`
	4. Change the base URL to match Github production repo: `baseURL = https://MParnin.github.io/`
	5. Save changes and exit code editor
10. Preview site locally:
	1. Make sure in directory with config.toml
	2. Run Hugo server: `hugo server`
	3. Visit the address of the local site: `http://localhost:1313/` (can ctrl-click link in terminal)
	4. Stop server when finished viewing: `Ctrl+c`
11. Test creating a new post: 
	1. Create file: `hugo new posts/hellomom.md`
	2. Edit file: `code /content/posts/hellomom.md`
		1. 1. Set title of post: `title: "Hello Mom!"`
		2. Delete draft mode line
		3. Add content below second "---": 
			1. Add plaintext: `Hey Mom checkout my new site!`
			2. Add code: 
			```Python
			print("Hello Mom!")
			```
			3. Save and exit
12. Add "Blog" as submodule to store static assets for website:
	1. Need one commit for "MParnin.github.io" repo and set the main branch to "main":
		1. Make a temp directory to clone repo to: `mkdir ~/tmp`
		2. Change to temp directory: `cd ~/tmp`
		3. Clone Production repository: `git clone git@github.com:MParnin/MParnin.github.io.git`
		4. Change to cloned directory: `cd MParnin.github.io`
		5. Checkout a new branch: `git checkout -b main`
		6. Create a readme file: `touch README.md`
		7. Check status to see untracked files: `git status`
		8. Add new all new files to be tracked: `git add .`
		9. Commit tracked files: `git commit -m "Adding README"`
		10. Push to Main branch on Github: `git push origin main`
		11. Confirm on Github the file was added and branch is set to "main"
		12. Delete temp files: `rm -rf tmp`
	2. Add a git submodule which will reference "Production" repository:
		1. Change to root site directory: `cd ~/Documents/Blog/MParnin.github.io`
		2. Create submodule within root to deploy site from (site deployed from "public" submodule directory; static files that Hugo generates get added to this directory): `git submodule add -b main git@github.com:MParnin/MParnin.github.io.git public`
13. Review site before deploying: `hugo server`
14. Generate static files into "public": 
	1. Change to root site directory: `cd ~/Documents/Blog/MParnin.github.io`
	2. Create files for selected theme: `hugo -t PaperMod`
	3. Confirm files were generated: `cd public`
	4. Confirm origin is directed to Production repository: `git remote -v`
	5. Check status of files: `git status`
	6. Add all static files: `git add .`
	7. Commit static files: `git commit -m "Initial commit"`
	8. Push the origin files to the main branch: `git push origin main`
		1. Confirm all static files are in Production repo on Github.  These files are now automatically deployed to `https://MParnin.github.io`.  This site is published because it is hosted through Github Pages which can be seen in "Settings > Pages" for the Production repositories settings.

## Creating a New Post
1. Create a new post:
	1. Navigate to root of site: `cd /Documents/Blog/MParnin.github.io`
	2. Create new post file: `hugo new posts/<name.md>`
	3. Edit post: `code /content/posts/<post-title>.md`
		1. Set title of post: `title: "Hello Mom!"`
		2. Delete draft mode
		3. Save and exit
2. Generate static files into "public" and push to github to update site: 
	1. Change to root site directory: `cd ~/Documents/Blog/MParnin.github.io`
	2. Create files for selected theme: `hugo -t PaperMod`
	3. Confirm files were generated: `cd public`
	4. Confirm origin is directed to Production repository: `git remote -v`
	5. Check status of files: `git status`
	6. Add all static files: `git add .`
	7. Commit static files: `git commit -m "Initial commit"`
	8. Push the origin files to the main branch: `git push origin main`

## Modifications
1. Moved table of contents to left side of page:
	1. Replace the contents of `themes/PaperMod/layouts/partials/toc.html` with the following (comment out what is currently in the file):
	```html
	{{- $headers := findRE "<h[1-6].*?>(.|\n])+?</h[1-6]>" .Content -}}
	{{- $has_headers := ge (len $headers) 1 -}}
	{{- if $has_headers -}}
	<aside id="toc-container" class="toc-container wide">
		<div class="toc">
			<details {{if (.Param "TocOpen") }} open{{ end }}>
				<summary accesskey="c" title="(Alt + C)">
					<span class="details">{{- i18n "toc" | default "Table of Contents" }}</span>
				</summary>

				<div class="inner">
					{{- $largest := 6 -}}
					{{- range $headers -}}
					{{- $headerLevel := index (findRE "[1-6]" . 1) 0 -}}
					{{- $headerLevel := len (seq $headerLevel) -}}
					{{- if lt $headerLevel $largest -}}
					{{- $largest = $headerLevel -}}
					{{- end -}}
					{{- end -}}

					{{- $firstHeaderLevel := len (seq (index (findRE "[1-6]" (index $headers 0) 1) 0)) -}}

					{{- $.Scratch.Set "bareul" slice -}}
					<ul>
						{{- range seq (sub $firstHeaderLevel $largest) -}}
						<ul>
							{{- $.Scratch.Add "bareul" (sub (add $largest .) 1) -}}
							{{- end -}}
							{{- range $i, $header := $headers -}}
							{{- $headerLevel := index (findRE "[1-6]" . 1) 0 -}}
							{{- $headerLevel := len (seq $headerLevel) -}}

							{{/* get id="xyz" */}}
							{{- $id := index (findRE "(id=\"(.*?)\")" $header 9) 0 }}

							{{- /* strip id="" to leave xyz, no way to get regex capturing groups in hugo */ -}}
							{{- $cleanedID := replace (replace $id "id=\"" "") "\"" "" }}
							{{- $header := replaceRE "<h[1-6].*?>((.|\n])+?)</h[1-6]>" "$1" $header -}}

							{{- if ne $i 0 -}}
							{{- $prevHeaderLevel := index (findRE "[1-6]" (index $headers (sub $i 1)) 1) 0 -}}
							{{- $prevHeaderLevel := len (seq $prevHeaderLevel) -}}
							{{- if gt $headerLevel $prevHeaderLevel -}}
							{{- range seq $prevHeaderLevel (sub $headerLevel 1) -}}
							<ul>
								{{/* the first should not be recorded */}}
								{{- if ne $prevHeaderLevel . -}}
								{{- $.Scratch.Add "bareul" . -}}
								{{- end -}}
								{{- end -}}
								{{- else -}}
								</li>
								{{- if lt $headerLevel $prevHeaderLevel -}}
								{{- range seq (sub $prevHeaderLevel 1) -1 $headerLevel -}}
								{{- if in ($.Scratch.Get "bareul") . -}}
							</ul>
							{{/* manually do pop item */}}
							{{- $tmp := $.Scratch.Get "bareul" -}}
							{{- $.Scratch.Delete "bareul" -}}
							{{- $.Scratch.Set "bareul" slice}}
							{{- range seq (sub (len $tmp) 1) -}}
							{{- $.Scratch.Add "bareul" (index $tmp (sub . 1)) -}}
							{{- end -}}
							{{- else -}}
						</ul>
						</li>
						{{- end -}}
						{{- end -}}
						{{- end -}}
						{{- end }}
						<li>
							<a href="#{{- $cleanedID -}}" aria-label="{{- $header | plainify -}}">{{- $header | safeHTML -}}</a>
							{{- else }}
						<li>
							<a href="#{{- $cleanedID -}}" aria-label="{{- $header | plainify -}}">{{- $header | safeHTML -}}</a>
							{{- end -}}
							{{- end -}}
							<!-- {{- $firstHeaderLevel := len (seq (index (findRE "[1-6]" (index $headers 0) 1) 0)) -}} -->
							{{- $firstHeaderLevel := $largest }}
							{{- $lastHeaderLevel := len (seq (index (findRE "[1-6]" (index $headers (sub (len $headers) 1)) 1) 0)) }}
						</li>
						{{- range seq (sub $lastHeaderLevel $firstHeaderLevel) -}}
						{{- if in ($.Scratch.Get "bareul") (add . $firstHeaderLevel) }}
					</ul>
					{{- else }}
					</ul>
					</li>
					{{- end -}}
					{{- end }}
					</ul>
				</div>
			</details>
		</div>
	</aside>
	<script>
		let activeElement;
		let elements;
		window.addEventListener('DOMContentLoaded', function (event) {
			checkTocPosition();

			elements = document.querySelectorAll('h1[id],h2[id],h3[id],h4[id],h5[id],h6[id]');
			// Make the first header active
			activeElement = elements[0];
			const id = encodeURI(activeElement.getAttribute('id')).toLowerCase();
			document.querySelector(`.inner ul li a[href="#${id}"]`).classList.add('active');
		}, false);

		window.addEventListener('resize', function(event) {
			checkTocPosition();
		}, false);

		window.addEventListener('scroll', () => {
			// Check if there is an object in the top half of the screen or keep the last item active
			activeElement = Array.from(elements).find((element) => {
				if ((getOffsetTop(element) - window.pageYOffset) > 0 && 
					(getOffsetTop(element) - window.pageYOffset) < window.innerHeight/2) {
					return element;
				}
			}) || activeElement

			elements.forEach(element => {
				const id = encodeURI(element.getAttribute('id')).toLowerCase();
				if (element === activeElement){
					document.querySelector(`.inner ul li a[href="#${id}"]`).classList.add('active');
				} else {
					document.querySelector(`.inner ul li a[href="#${id}"]`).classList.remove('active');
				}
			})
		}, false);

		const main = parseInt(getComputedStyle(document.body).getPropertyValue('--article-width'), 10);
		const toc = parseInt(getComputedStyle(document.body).getPropertyValue('--toc-width'), 10);
		const gap = parseInt(getComputedStyle(document.body).getPropertyValue('--gap'), 10);

		function checkTocPosition() {
			const width = document.body.scrollWidth;

			if (width - main - (toc * 2) - (gap * 4) > 0) {
				document.getElementById("toc-container").classList.add("wide");
			} else {
				document.getElementById("toc-container").classList.remove("wide");
			}
		}

		function getOffsetTop(element) {
			if (!element.getClientRects().length) {
				return 0;
			}
			let rect = element.getBoundingClientRect();
			let win = element.ownerDocument.defaultView;
			return rect.top + win.pageYOffset;   
		}
	</script>
	{{- end }}
	```