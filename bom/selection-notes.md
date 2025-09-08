Why these picks (Budget Friendly)

1) Use SMD SAW filters (they’re a few dollars each)

RF360/TDK B3728 (915 MHz ISM SAW, ~26 MHz PBW): typically $1–$1.30 in singles. 

[DigiKey](https://www.digikey.com/en/products/detail/qualcomm-rf-front-end-rffe-filters/B39921B3728U410/3492653?utm_source=chatgpt.com)

[Mouser Electronics](https://www.mouser.com/ProductDetail/RF360/B39921B3728U410?qs=7N3YgXRJ4GVja%252BRYuIWLgQ%3D%3D&srsltid=AfmBOooQhY0-WVcHYT0M3J-b706EPw9e3oGBkMpXi3Xh5iL15iHp73O_&utm_source=chatgpt.com)

Taiyo Yuden FAR-F5QA-915M00-M2AK-J (915 MHz SAW): often well under $1 (Mouser list shows $0.44 in stock). 

[Mouser Electronics](https://www.mouser.com/c/passive-components/signal-conditioning/?frequency=915+MHz&product=SAW+Filters&srsltid=AfmBOoqbBp-8d57FrRV7PLv69CuX6yVa7Jv6hv23vjEA5FvVmbFS5qD_&utm_source=chatgpt.com)

Murata SF2053E (915 MHz SAW): common, low cost, widely stocked. 

[Mouser Electronics](https://www.mouser.com/datasheet/2/281/sf2053e-784918.pdf?srsltid=AfmBOorQgwD6R5gGecbr9x_D5bxmcLGXyujuyG6xPwo9g9PETaZcn14F&utm_source=chatgpt.com)

Trick: Cascade two SAWs in each path (TX and RX). Two cheap SAWs often give you ~double the out-of-band rejection for just a few dollars more—far cheaper than a cavity filter.

2) Keep the LO / mixer / LNA inexpensive

LNA: Mini-Circuits PSA4-5043+ is a solid 900 MHz LNA; small-qty price is a few dollars (Digi-Key shows volume pricing around ~$3–$4; single-qty more, but LCSC lists ~$1.28 in stock). 
[DigiKey](https://www.digikey.com/en/products/detail/mini-circuits/PSA4-5043/13928200?utm_source=chatgpt.com)
[LCSC Electronics](https://www.lcsc.com/product-detail/RF-Amplifiers_Mini-Circuits-PSA4-5043_C5240848.html?utm_source=chatgpt.com)

Mixer: Mini-Circuits ADE-12+ (SMD) is widely used and cheap; surplus listings can be ≈$2 each in small lots. 
[eBay](https://www.ebay.com/itm/284286521849?utm_source=chatgpt.com)

LO/Synth: ADF4351 dev boards (clones) are plentiful—typically $20–$60 each depending on vendor. 
[eBay](https://www.ebay.com/itm/365633079796?utm_source=chatgpt.com)


3) Audio chain stays dirt-cheap

Little class-D amps like PAM8302 are ~$4. 
[Adafruit](https://www.adafruit.com/product/2130?srsltid=AfmBOoqqXIxNtP6KtorKYou7HwLzlEXtVJUqRe3vv2Opyclyq9JDjrHk&utm_source=chatgpt.com)
[Jameco](https://www.jameco.com/z/2130-Adafruit-Industries-Adafruit-Mono-Class-D-Audio-Amplifier-2-5W-PAM8302_2294911.html?srsltid=AfmBOorQLiqpoITF-n0NnSZJEIuh1FLJvWH3LXu8qwvWoyDPE-c7plWp&utm_source=chatgpt.com)
[Micro Center](https://www.microcenter.com/product/668757/adafruit-industries-stemma-audio-amp-mono-25w-class-d-pam8302?utm_source=chatgpt.com)

4) Antennas and mechanics

Start with ¼-wave wires cut for ~915 MHz (~8.2 cm). That’s $0.

If you want connectors, use edge-launch SMA footprints and a pair of $2–$4 whips later.

5) Design moves that save money

Big frequency split (e.g., 906/920 MHz) + low TX power (0 to +3 dBm) + two SAWs in cascade per path + antenna spacing/cross-pol. This stacks isolation without expensive iron.

Add shield cans only on the final PCB (skip during bring-up).

If you ever need more rejection, you can add a DIY microstrip hairpin BPF on your PCB (cost = copper + FR-4).

What your per-node RF spend can look like (rough)

4× SAW filters (2 in TX path, 2 in RX path): ~$4–$6 total. 
[DigiKey](https://www.digikey.com/en/products/detail/qualcomm-rf-front-end-rffe-filters/B39921B3728U410/3492653?utm_source=chatgpt.com)

1× LNA PSA4-5043+: $2–$4 (or ~$1.30 at LCSC). 
[DigiKey](https://www.digikey.com/en/products/detail/mini-circuits/PSA4-5043/13928200?utm_source=chatgpt.com)
[LCSC Electronics](https://www.lcsc.com/product-detail/RF-Amplifiers_Mini-Circuits-PSA4-5043_C5240848.html?utm_source=chatgpt.com)

1× Mixer ADE-12+: $2–$10 depending on source. 
[eBay](https://www.ebay.com/itm/284286521849?utm_source=chatgpt.com)

1× ADF4351 board: $20–$60 (many vendors). 
[eBay](https://www.ebay.com/itm/365633079796?utm_source=chatgpt.com)
[Amazon](https://www.amazon.com/Development-35M-4-4GHz-Synthesizer-Controller-Compatible/dp/B0F9FXQCG8?utm_source=chatgpt.com)

Passives, SMA edge, board, audio amp, etc.: $10–$20.

Ballpark: You can keep the core RF+audio parts under ~$50–$80 per node (not counting general lab gear). Compare that to a single $289 cavity filter—big savings.