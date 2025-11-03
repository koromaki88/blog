---
title: "V1t 2025 | OSINT"
date: 2025-11-02T22:20:00+07:00
draft: false
tags: ["OSINT", "V1t", "Geolocation"]
categories: ["CTF Writeups"]
summary: "Full guide on all OSINT challenges in V1t CTF 2025."
---
**Category**: OSINT\
**Note**: N/A

---

# Among USniversity
> Bro, I found "Among Us" at this school!
>
> Can you spot the hidden acronym?
> Wrap it in v1t{...} to submit your answer.
>
> Example: University of Economics Ho Chi Minh City => v1t{UEH}
> 
> ![amongus.png](amongus.png#center)

Just look up the text `truong dai hoc cong nghe thong tin` and it will be the first result: `v1t{UIT}`

# Duck Company
> I found this company selling this cute wooden duck for the halloween but i forgot where link web store :< can you help me find it
> 
> Flag format: v1t{example.com}
>
> ![duck_company.png](duck_company.png#center)

Reverse search the image on `images.google.com`, the first result is the flag: `v1t{dcuk.com}`

# The Forgotten Inventory
> In the summer of 2007, a massive archive quietly surfaced — a meticulous ledger of items that once rolled across desert sands under foreign command. The file was structured, line after line, page after page, each entry tied to a unit whose banners flew far from home.
>
> Someone wasn’t happy about its release. A message was sent, demanding its silence — a digital plea from a uniformed gatekeeper. The request was denied.
>
> Your task is to uncover the sender of that plea.
>
> Clues hide in old public archives — look for a tabular trail documenting what was once called Operation Freedom, catalogued in a comma-separated vault of** 1,996 pages** worth of equipment.
> 
> Some say the sands between two nations hold the real context — where east met west, and war turned into a spreadsheet.
>
> Find the **email address** of the official who tried to bury the list.
> 
> Format: v1t{hello.hi@ehatever.com}
>
> View Hint: Watch https://www.youtube.com/watch?v=dQw4w9WgXcQ

This challenge is entirely solvable using only AI and the description, but it is quite inconsistent and would not always yield the correct answer immediately on weaker models.

Fortunately, it gave many relevant information which helps significantly in the search for the flag. The riddle refers to an equipment data leak which happens to the US army during the Iraq war in 2007. The leak was requested to be taken down by an authority figure from the US side, and we must find the email address of said figure. The leak was published on the [WikiLeaks](https://wikileaks.org/) archive.

The description references a "spreadsheet", so we can input `"csv"` into WikiLeaks' as the main search keyword. The advanced search menu would then pop-up, allowing us to further curate our search query:

![inv1.png](inv1.png#center)

A result titled `Iraq OIF Property List.csv` will come up. Viewing it will immediately show us the takedown request we need along with the sender's email address which is the correct flag: `v1t{david.j.hoskins@us.army.mil}`

# 16th Duck
> Caught someone playing music at this place and here are their belonging, can you find the place ?
>
> Flag format: v1t{latitude, longitude}
> 
> Example: v1t{36.123456,18.789123}
>
> ![belonging.png](belonging.png#center)
> ![place.png](place.png#center)

Reverse search the insignia image, an [auction page](https://auction.ru/offer/krasnoznamennaja_vojskovaja_chast_v_ch_61608_100_let_svjaz_kosmos-i109496963498623.html) of the exact same items is found.

Google Translate `Краснознаменная войсковая часть в/ч 61608` to `Red Banner Military Unit 61608` and look the English result up, the first result is a [PDF document](https://checkfirst.network/wp-content/uploads/2025/07/OSINT_Phaleristics_Unveiling_FSB_16th_Center_SIGINT_Capabilities.pdf). Skim through to page 28 and the challenge's two images can be found along with the coordinates in the caption of the figure. Submit `v1t{55.592169,37.689097}` as the flag.

![ru1.png](ru1.png#center)


# Dusk Till Duck
> As the sun sets over a calm lake, a lone duck drifts across the fading light. The scene looks peaceful, but the park hides more than it seems. Can you figure out where this photo was taken before the night falls?
> 
> Format: v1t{place_name}
> 
> Example: v1t{Abc_Park}
>
> ![dusk_till_duck.jpg](dusk_till_duck.jpg#center)

Reverse search on the image will lead to a [shutterstock page](https://www.shutterstock.com/id/image-photo/stunning-evening-view-swimming-ducks-thames-1781586122). Looking at the "Image details" section gives us a clue: `Stunning evening view with swimming ducks in the Thames River`.

One's immediate thought would be the River Thames in London, UK - but don't be fooled. I filtered the images by date and quickly inspect photos that were taken around the same time period. Some of them will mention the location we are looking for: Thames River of London, Ontario, Canada (yes they outright stole the names).

Now, we will open Google Maps and begin searching. Since we only need the name of where this photo was taken, we can do some guessworks and don't have to find the exact location. The challenge description mentions that the sun is setting, we can confirm this is true by the previously found description mentioning `evening view`. This means the photographer is facing west, so we should look for locations situated on the eastern riverbank. It is also more intuitive to begin looking inside the city rather than its outskirts. From here, we just do some trial and error and found the correct location to be `v1t{Ivey_Park}` as shown below.

![dusk1.png](dusk1.png#center)

![dusk2.png](dusk2.png#center)

# Snowflake
> My friend sent me this picture, the snowflakes are so beautiful. Can you figure out where is this?
> 
> Flag format: v1t{latitude, longitude}
>
> Example: v1t{22.44385,-74.22042}
>
> https://drive.google.com/file/d/1BDD4-_E6397He7ZUsoV0e15TRwM2tUhY/view?usp=sharing 
>
> ![chall.png](chall.png#center)

This challenge is proven to be difficult right away as we cannot reverse the exact image. Search results and Google AI immediately shows that it is in Japan (possibly because Google recognizes its distinctive residential architecture), presumably a northern region like Hokkaido due to the heavy snow. 

Scanning through the image, I can quickly find that the license plate on the blue car is not fully blurred, with the top line still faintly visible. Throwing the text onto an online OCR/translator like Google Translate and we can confirm that this is `札幌` or Sapporo, Hokkaido.

![snow1.png](snow1.png#center)

I move my attention over to the other partially visible text on the utility pole. The information we want to pay attention to are the pairs of numbers.

![snow2.png](snow2.png#center)

These numbers are used to uniquely identify utility poles so that companies can easily locate and provide maintenance on them. This means that we can identify exactly where we are if we know the full numbers set.

The problem is that the Hokkaido region has 12 identification numbers on its utility pole, but only the larger 8 numbers are legible to us.

![plonkit.jpg](plonkit.jpg#center)

Here, I took a rather suboptimal approach of going into Google Street View and searching for shared patterns. Fortunately, I quickly noticed that all Sapporo poles have the identical first pair of number `41`. This narrows it down significantly to only having two remaining missing digits to fill in: `41XX73776507`

The search pivots to finding the tool that I can use to pinpoint the exact location of our pole and potentially brute force through it. Incredibly enough, there was a [website exactly for this purpose](https://haiden.hokuden-network.biz/denchu/). This may not be the intended solution, since the site is only accessible with a Japanese IP, forcing me to run a VPN to use it.

The coordinates don't scale linearly with the code, so it was a bit hard to roughly estimate how far off I am. I decided to take its API and whip up a script to output corresponding latitude and longitude of a given 12-digit code (I only needed at maximum 100 requests so this is acceptable for brute forcing):

```sh
#!/bin/bash

for i in $(seq -w 00 99); do
  num="41${i}73776507"
  json=$(curl -s "https://haiden.hokuden-network.biz/denchu/api/pole/${num}/latlng")
  
  if echo "$json" | grep -q '"lat"'; then
    latlng=$(echo "$json" | jq -r '"\(.lat),\(.lng)"')
    echo "$num -> $latlng"
  fi
done
```

Output: 
```
410073776507 -> 42.73386981268185,141.04269732195274
410173776507 -> 42.73387199568185,141.16768694157773
410273776507 -> 42.73387417868185,141.29267656120274
410373776507 -> 42.73387636168185,141.41766618082775
410473776507 -> 42.73387854468185,141.54265580045274
...
```

With some trial and error, I found `414273776507` with `43.067171862015186,141.29266121520274` to be the correct location by jumping into street view and confirming my surroundings.

![snow3.png](snow3.png#center)

The challenge SHOULD be considered solved by now, but I had to find the exact latitude and longitude to the 5th decimal place, which essentially means I need to look for exactly where the photographer stood. You can do this by right clicking on any spot in Google Maps and the coordinates is shown. After painstakingly trying 20+ different submissions for 15 minutes, the challenge was completed: `v1t{43.06743,141.29253}`.
