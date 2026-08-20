# Cafe Craze

A pixel-art barista sim for the phone. One shift, one clock, two views: the **window** where customers queue with tickets, and the **bar** where you actually pull the shots. The timer never stops — stepping between the two costs you seconds you don't have.

Runs from a single file (`index.html`). Save/load, high scores, barista names and tutorial progress live in the browser's local storage.

## The loop

1. A customer shows up at the window with a ticket. Tap it to accept.
2. Switch to the bar and build the drink: beans into the grinder, hold GRIND, dose the portafilter, tamp, set a cup, dock the portafilter, BREW.
3. Stop the brew inside the gold band for an espresso. Run it long in a latte cup for a lungo. Miss the band with a demitasse or a glass and the shot is binned.
4. Milk: open the FRIDGE, take whole, oat or cashew, drag the carton into the frother tin, put the tin on the steam wand, hold STEAM and release inside the green band.
5. Combine on the tray (espresso + steamed milk = latte, + cocoa = mocha, espresso in a glass + milk = cortado).
6. Drag the finished drink onto the customer's accepted ticket to ring it up.

Miss five tickets and the run is over — unless **You're Fired!** is switched off in GAMEPLAY. Patience, modifications and day length are also house rules you control there.

## Money

Every drink and every modifier turns a profit at default prices. Ingredient costs per use, from Supplies:

| Ingredient | Pack | Cost per use |
| --- | --- | --- |
| Beans | $6 / 5 grinds (3 doses each) | $0.40 per shot |
| Whole milk | $4 / 3 | $1.33 |
| Oat or cashew milk | $5 / 3 | $1.67 |
| Cocoa | $4 / 6 | $0.67 |
| Cinnamon | $3 / 6 | $0.50 |
| Sugar cubes | $3 / 12 | $0.25 |

Modifier surcharges added to the ticket: extra shot **+$1.25**, alt milk **+$0.75**, cocoa on top **+$1.00**, cinnamon dust **+$0.75**, each sugar cube **+$0.35**. Serving with more than half the ticket timer left pays a **+$0.50** speed bonus, and tips are a percentage of the whole ticket set by your reputation.

## Pricing and reputation

There is **no price cap**. Every drink's price is yours to set in **RECIPES** &mdash; type any figure from $0.25 to $99, or nudge it in 25&cent; steps. What reputation buys you is not permission, it is **tolerance**: how much the street will happily pay before it starts to feel robbed.

### The fair price

Each drink has a menu default. Your reputation scales that into a **fair price** &mdash; the number the neighbourhood currently considers reasonable:

fair price = default &times; (0.88 + 0.06 &times; stars)

| Stars | Fair price is | Espresso ($3.50) | Latte ($5.00) | Mocha ($5.50) |
| --- | --- | --- | --- | --- |
| 0 | 88% of default | $3.08 | $4.40 | $4.84 |
| 1 | 94% of default | $3.29 | $4.70 | $5.17 |
| 2 | 100% of default | $3.50 | $5.00 | $5.50 |
| 3 | 106% of default | $3.71 | $5.30 | $5.83 |
| 4 | 112% of default | $3.92 | $5.60 | $6.16 |
| 5 | 118% of default | $4.13 | $5.90 | $6.49 |

A no-name shop can't charge what a beloved one can. A beloved one can charge nearly 20% over the menu and nobody blinks.

### What happens when you go over

Nothing is forbidden. Four separate consequences simply get worse the further past fair you go, and each one is visible in play:

- **The crowd thins.** Above fair there is an **8% grace band** &mdash; a few cents over and nobody notices. Past that, demand decays on a curve (quadratic, so it is gentle at first and brutal later) until at some point nobody orders that drink at all.
- **People walk out.** When your menu is overpriced, customers show up in the log by name and leave without ordering: *"Marcus read the board and kept walking."* No life lost, no penalty &mdash; just the sound of money not being made.
- **Tips dry up.** Tips are unaffected until you are 12% over fair, then fall away fast and hit zero around 40% over. Go the other way and they swell: a genuine bargain can more than double the tip.
- **Your stars slip.** Past 18% over fair, each serve costs up to &#8722;0.14 reputation. That is the self-correcting part &mdash; gouging erodes the very tolerance that let you gouge, and the fair price drops out from under you.

### Why you should still charge over fair

Because the money peaks **above** fair, not at it. Every drink has its own elasticity &mdash; how price-sensitive its buyers are &mdash; so the profitable markup differs by drink:

| Drink | Elasticity | Best price is about | Best take vs. default |
| --- | --- | --- | --- |
| Ice water | 2.8 (very sensitive) | +19% over fair | +14% |
| Espresso | 1.9 | +24% over fair | +16% |
| Americano | 1.7 | +26% over fair | +17% |
| Lungo | 1.6 | +27% over fair | +17% |
| Latte | 1.3 | +30% over fair | +19% |
| Cortado | 1.2 | +32% over fair | +20% |
| Mocha | 1.05 (a treat) | +35% over fair | +22% |

Treats absorb a markup; commodities don't. Charging $2.50 for a glass of ice water is a different crime than charging $7.40 for a mocha, and the game agrees with you about which is worse.

### Charging under fair

Underpricing is a real strategy, not just a loss. Below fair, demand rises up to +40% and tips grow, and staying under fair drifts reputation upward. A cheap opening menu is a fast way out of the low-star hole where traffic is slow and nobody tips.

### Reading the card

Every recipe card shows the whole picture live as you type:

- **FAIR $x.xx** &mdash; the fair price at your current reputation.
- **A mood line** &mdash; GIVING IT AWAY / BARGAIN &middot; THEY TELL FRIENDS / FAIR PRICE / A LITTLE PRICEY / STEEP &middot; EYEBROWS RAISED / GOUGING &middot; WORD GETS AROUND / DAYLIGHT ROBBERY. Green is safe, amber is a warning, orange means you are losing money.
- **CROWD %** and a bar &mdash; how much traffic this price pulls versus normal.
- **TAKE &plusmn;%** &mdash; the honest answer: total revenue at this price versus the menu default, crowd loss already accounted for. If TAKE is negative, the price rise is costing you money, however good the number on the board looks.

Hunt the peak of TAKE. It is always somewhere past FAIR, and it moves every time your stars change.

### Everything else reputation does

| Stars | Traffic | Tips | Patience |
| --- | --- | --- | --- |
| 0 | 50% slower | none | normal |
| 1 | 30% slower | none | normal |
| 2 | 15% slower | ~5% | normal |
| 2.5 | baseline | ~10% | normal |
| 3 | 15% faster | ~15% | 10% slower |
| 4 | 30% faster | ~25% | 20% slower |
| 5 | 50% faster | ~50% | 40% slower |

Reputation climbs with fast, accurate service and falls on missed or wrong orders &mdash; and now on greedy ones too.
