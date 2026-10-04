# Go Lab

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

Fair and reasonable! But truth be told, I was *glad* to hear it, because it meant that I could make a stab at this with a clear conscience. Furthermore, the response on the forum post indicated that other people would find such an application useful.

## The Saga Begins

So I got to work. According to the git commits on my first draft, between 10-9-2023 and 10-19-2023, I worked somewhat feverishly, adding basic graphics, websocket communication, an SGF parser, and basic Go game logic. The proof-of-concept looked like this:

![20231019](assets/golab1.png)
