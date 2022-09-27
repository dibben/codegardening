---

title: "A Visit to FUGAKU"
subtitle: ""
summary: "A visiting to the FUGAKU supercomputer at the RIKEN center for computational science in Kobe"
authors: ["dibben"]
tags: ["HPC", "FUGAKU"]
categories: []
date:  2022-09-27T09:33:38.974Z
lastmod:  2022-09-27T09:33:38.974Z
featured: false
draft: false
type: post
math:
  enable: true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

---


I attended my first in-person meeting for a long time yesterday. The 186th High Performance Computing Research Meeting (第186回ハイパフォーマンスコンピューティング研究発表会) held at the [RIKEN center for computational science](https://www.r-ccs.riken.jp/).
It was a small event (30 people in a large room) and as this is Japan _everyone_ wore a mask. 

This is also the home of FUGAKU and there was a chance to see it after the event. Until May this year FUGAKU was the fastest supercomputer in the world. 

{{< figure src="fugaku-1.jpg" >}}

We have had some discussions with Fujitsu about porting our software to the FUGAKU. It uses an extended ARM processor, the A64FX. This means that standard compilers will work but to get good performance you need to update your code to take advantage of the vector functions. The main problem is that 3rd party libraries also need ARM versions and they are not always available. 


## COVID simulations

FUGAKU came online just as COVID started so they used it for some COVID research to look at the effect of masks and ventilation. Because of the power of the machine they could do the simulations quickly.

They have a description of the results on the [RIKEN site](https://www.r-ccs.riken.jp/en/fugaku/research/covid-19/msg-en/)

There are also videos on YouTube.

{{< youtube -arizwuZWCM >}}

Their conclusion: "Wear a Mask & Ventilate". 


The energy crisis is affecting FUGAKU as well. The machine uses something like 20 MW at full power. Because of the high cost of energy now they have taken 10,000 nodes offline to reduce the energy consumption. 

Interestingly the current status, including energy consuption is open with an [online dashboard](https://status.fugaku.r-ccs.riken.jp/d/fugaku/0-operation-status-of-fugaku?orgId=1)

{{< figure src="fugaku-2.jpg" >}}
