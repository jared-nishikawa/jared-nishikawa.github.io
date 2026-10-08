# Go Lab

TL;DR [Go Lab](https://github.com/golab/board) is the first big project that I carried through from beginning to end, becoming half research project and half public service.

## Backstory

I play [Go](https://en.wikipedia.org/wiki/Go_(game)).

In person, it's common to review games. The review process is (naturally) a multi-person event. One may even find a group of three to five people huddled around a board, nodding their heads, or taking it in turns to put variations on the board. It's hardly worth mentioning that this is a "low-friction" process, in the sense that there are no physical barriers to placing and removing stones, or pointing at various areas of the board.

Enter: the digital Go board. Of course, there are plenty of servers where users can play Go online. During a game these servers enforce obvious control policies (like, "if it's Alice's turn, then Bob can't place a stone"). Duh, right? But then the game ends, and the players may opt to begin a review. The prevailing design choice is: **During a review, one user has control of the board at a time. Furthermore, one user is the host and is responsible for passing control around to other users.**

Now, I started playing Go in 2010, and it didn't even occur to me to question this design choice until 2023. I had just gotten back from US Go Congress, having enjoyed a spirited week of playing and reviewing games. I was reviewing online with some Go-playing friends, and the sudden shift from "enjoyable frictionless in-person reviewing" to asking "Hey can I get control real quick?" a thousand times made it clear to me that something was missing.

Due diligence. I shouldn't just start making a new service from scratch if one of the online servers would simply implement it, right? The most popular western Go Server is [OGS](https://online-go.com/), so I [posted in the forums](https://forums.online-go.com/t/why-do-reviews-only-allow-one-party-with-control-at-a-time/49341), asking if they would consider implementing "shared" review control. (10-7-2023)

Amidst all the side-chatter I got a polite and technical response from one of the OGS devs (flovo):
> tldr: It eats up a big chunk of development time to change the way the reviews work. To allow multiple users to interact with the same board at the same time introduces a bunch of new issues to consider.

> [in-depth explanation of network considerations]

> All these concerns can be handled, but it will require big changes in the code. This asks for extra care to not risk the integrity of the whole service.

> It can be done, but it’s not just flipping a switch. My estimation is it would take as much time as any new major feature.

Technically, not a "no" but we should read this as "we will almost certainly not do this."

Fair and reasonable! But truth be told, I was *glad* to hear it, because it meant that I could make a stab at this with a clear conscience. Furthermore, the response on the forum post indicated that other people would find such an application useful. I was convinced, since I wasn't planning to make a "Go server" in the traditional sense, that I could build the project **around** managing the network issues.

## The Saga Begins

So I got to work. According to the git commits on my first draft, between 10-9-2023 and 10-19-2023, I worked somewhat feverishly, adding basic graphics, websocket communication, an SGF parser, and basic Go game logic. The board looked like this:

![20231019]({{ site.baseurl }}/assets/golab1.png)

If I remember right, the arrow buttons were cosmetic only, there was no logic to allow for moving through a game tree (besides adding stones). But I could load the same board state in two different browser windows, and (through the magic of websockets) input from one window would be reflected in the other. 

## Catastrophe Strikes

Unfortunately, just over a month later, I was unceremoniously [laid off](https://investors.broadcom.com/news-releases/news-release-details/broadcom-acquire-vmware-approximately-61-billion-cash-and-stock) during an acquisition. To keep this section brief, as it's only tangential to the main story, I found a new job in 2024 but I didn't have the same time or energy to devote to the "Go board with shared control" project.

## Renewed Energy

We pick up the story again in January of 2025 (the project lay dormant through all of 2024, though I think I showed a demo to couple of Go friends).

January 7, I started working on the project again in earnest. Looking back, I think I would attribute this to three things:
  - Dissatisfaction with my job, and a desire to put my engineering skill to use
  - The continued annoyance with "one user control" while reviewing on Go servers. (After all, now that I had noticed, I couldn't *stop* noticing how much it bothered me).
  - My partner and I were planning to have kids soon, and I wanted to get this idea on its feet and out the door, if possible.

From then until to the end of February, I was working on this almost every evening (evenings which I could have spent studying Go!). There are too many features to list, but suffice to say that I just kept adding features as I thought of them. I had deployed it and was using it with friends on a weekly basis, gathering ideas and implementing them as fast as I could.

Here are a few snapshots that showed major design changes in these two months:

![20250110]({{ site.baseurl }}/assets/golab2.png)

![20250130]({{ site.baseurl }}/assets/golab3.png)

![20250218]({{ site.baseurl }}/assets/golab4.png)

## Beta Release

At some point, it felt like I had something worth sharing with the Go community. I [made another post on the OGS forums](https://forums.online-go.com/t/an-online-go-board-with-shared-control/55610).

## Heads Down

From this point on, I simply kept working at a more normal pace, and there are fewer major plot points, but some of the major ones are:
  - Sync with live OGS games (3-14-2025)
  - Integration with Twitch (9-3-2025)
  - Textured shell stones (12-13-2025
  - Branding and name change (12-30-2025)

Some more snapshots along the way:

![20250522]({{ site.baseurl }}/assets/golab5.png)

![20250601]({{ site.baseurl }}/assets/golab6.png)

![20251018]({{ site.baseurl }}/assets/golab7.png)

![20251213]({{ site.baseurl }}/assets/golab8.png)

### Tangent: Colors

I had a fun few days in December implementing customizable colors, and I discovered an interesting [page on color contrast](https://ux.stackexchange.com/questions/107318/formula-for-color-contrast-between-text-and-background):

![color1]({{ site.baseurl }}/assets/color1.png)

![color1]({{ site.baseurl }}/assets/color2.png)

![color1]({{ site.baseurl }}/assets/color3.png)

![color1]({{ site.baseurl }}/assets/color4.png)

## Full Release

I really wanted to have the textured shell stones and finalized branding before I made another announcement. I agonized for months over the right name (I think it's a good sign that nearly a year on I still feel very happy about the name Go Lab), and then commissioned a graphic designer to create the logo, as well as the textured shell stone image files.

[Final post to the OGS forums](https://forums.online-go.com/t/go-lab-an-online-multi-user-go-board/59244). (1-30-2026).

Concluding thoughts:

  - I accomplished what I set out to do, and I learned a LOT in the process.
  - I've been programming since I was a kid, but this was the first project that I felt a deep connection to, and I very much wanted to see it through to a public launch.
  - This project was academically fulfilling, as it gave me the chance to implement interesting algorithms (for example, DFS features heavily in the game logic, and I'm rather proud of the SGF parser).
  - I wrote this by hand, no vibe-coding.
  - Despite an essentially silent discord community, my logs tell me I have daily active users.

Development has slowed and other priorities have taken front seat in my life, but I plan to keep the server going and do occasional bug fixes and patches in the future!

Thanks for reading!

## Appendix: Lessons Learned

### Canvas vs SVG

Canvas is an HTML element used for drawing graphics on webpages. At first I assumed this would be the natural choice for the Go board. But it turns out that using SVG elements was more performant.

### Websockets

Websockets are awesome. But they can be annoying.

The server sits behind Cloudflare, which accepts websocket connections, fortunately. However, websocket connections to Cloudflare get disconnected after 60 seconds, so I have to ping every 30 seconds to keep the connection alive.

Websockets on firefox have a built-in exponential backoff on reconnections. This drove me (somewhat) crazy while testing: I couldn't figure out why my reconnections just get slower and slower while I was trying to troubleshoot. [1](https://stackoverflow.com/questions/59548618/firefox-doesnt-close-websocket-immediately-on-connection-error) [2](https://bugzilla.mozilla.org/show_bug.cgi?id=711793) [3](https://bug711793.bmoattachments.org/attachment.cgi?id=637655)

### The Game Tree

![explorer]({{ site.baseurl }}/assets/explorer.png)

If implemented suboptimally, the game tree explorer is the most graphic-intensive part of the whole website. Hundreds (or potentially even thousands) of nodes may slow down the website to a crawl.

Solution: only render the nodes that are actually visible.

Another problem I ran into: constantly deleting and adding new nodes to the DOM causes massive memory use until garbage is collected.

Solution: reuse elements from an "element pool." Expand the pool when necessary.

For stress testing this, I have a zip file (about 100KB) containing around 150 SGF files. Altogether, the game tree has more than 30,000 nodes. This should be an order of magnitude more than anyone will load, and Go Lab is able to handle it.

### Client/Server Sync

This one was a huge pain. Basically, the way I initially hacked it together, the frontend and backend were doing simultaneous calculations on the board state and game tree, and it was written in a way that they SHOULD always match. But they didn't always match, and this caused many annoying bugs.

The original model is a fundamentally flawed paradigm. The backend should do the computation, and the frontend should receive the results and display them.

I finally ripped this out and redesigned it in August 2025. The backend now stores state and the frontend simply queries it.

### Android + Chrome

When uploading a file, the file picker is opened and Chrome gets sent to the background. After about 5 seconds, the websocket connection closes. (So, if you picked a file fast enough, you wouldn't encounter this bug).

Solution: await the successful websocket connection before uploading.

### String Builders

This is probably obvious to veteran string manipulators, but during parsing I was doing tons of string allocations (starting out with `result := "("` and growing arbitrarily). This became slow when the strings were very large (I only noticed while running benchmarks of hundreds or thousands of merged SGFs).

Solution: use string builders. Strings are inherently immutable, so doing a bunch of concatenations make new objects in memory. String builders use mutable internal buffers.
