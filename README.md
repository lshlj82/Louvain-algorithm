# The Louvain Algorithm, Step by Step
**단계별로 보는 루뱅 알고리즘**

An interactive web demo showing how the Louvain algorithm for community detection works. It is a supplement to demo 11, [Network communities](https://lshlj82.github.io/network-community/), in the [interactive demos](https://lshlj82.github.io/netsci-course-GNU/) for *Network Science* (네트워크 과학) in the Department of Physics, Gyeongsang National University.

Created by **Claude Opus 5.5**, based on the lecture slides by **Prof. Sang Hoon Lee**.
이상훈 교수의 강의 슬라이드를 바탕으로 Claude Opus 5.5가 만들었습니다.

**Live page:** https://lshlj82.github.io/Louvain-algorithm/ (English) · https://lshlj82.github.io/Louvain-algorithm/ko.html (한국어)

## Files

| File | Description |
| --- | --- |
| `index.html` | English page |
| `ko.html` | Korean page (한국어) |
| `README.md` | This file |

The two pages share identical code and differ only in the language they display. Each one is a single self-contained HTML file with no build step and no libraries; the only external request is to Google Fonts (IBM Plex Sans and Fraunces for Latin text, and Noto Serif KR for Korean, as on the course page), with system fonts as the fallback.

## What's inside

1. **Two steps, repeated.** The algorithm as described on the slide: start from singletons, then repeat modularity optimization (move each node to the neighboring community with the largest Δ*Q*, sweep after sweep, until no move helps) and community aggregation (turn each community into a supernode with a self-loop). Modularity is always computed on the original network.
2. **The example from the paper.** The 16-node, 28-link network of Fig. 1 in Blondel *et al.* (2008). You can step through one node visit at a time, finish a sweep, finish a pass, or play it automatically. A table shows *k*<sub>*i*,*C*</sub>, Σ<sub>tot</sub> and Δ*Q* for every candidate community of the visited node. Visiting the nodes in the order 0, 1, 2, … reproduces the figure exactly: four communities after the 1st pass (self-loops 14, 4, 16, 2; links 4, 1, 1, 1, 3; *Q* = 0.3463) and two after the 2nd (self-loops 26, 24; link 3; *Q* = 0.3922). A random visiting order reaches the same answer about 85% of the time. A switch shows the self-loops either as ΣA<sub>ij</sub> inside the group, as in the paper's figure (14), or as the number of internal links, as in the textbook (7).
3. **Stochasticity: the order of visits.** Zachary's karate club, run with a new random order each time, singly or 500 at once, with a histogram of the final *Q* values. Unweighted runs give the slide's 0.4156 and 0.4188 (and 0.4198, 0.4151, …). With the edge weights of NetworkX's `karate_club_graph()`, runs give 0.4439 as on the slide, and 0.4449.
4. **In code.** `nx.community.louvain_communities`, the `community` (python-louvain) module used in the textbook, and GenLouvain.

## Notes on the model

- The algorithm is the standard Louvain method: Δ*Q* = *k*<sub>*i*,*C*</sub>/*m* − Σ<sub>tot</sub>*k*<sub>*i*</sub>/(2*m*<sup>2</sup>) after removing node *i* from its community, a move only when another community gives a strictly larger gain, and ties broken by the smaller community label. The run stops when a pass moves nothing.
- The karate-club edge weights are those distributed with NetworkX. The frequencies of the different answers depend on how the random order is drawn, so they will not match NetworkX run for run, but the set of answers is the same.
- The pages support light and dark mode (the choice is shared with the other course demos), adapt to phone screens, and slow automatic playback for visitors who have reduced motion turned on.

## Running it

Open `index.html` directly in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/
```

To publish with GitHub Pages, go to **Settings → Pages**, choose **Deploy from a branch**, and select `main` and the root folder.

## References

- V. D. Blondel, J.-L. Guillaume, R. Lambiotte, and E. Lefebvre, "Fast unfolding of communities in large networks," *J. Stat. Mech.* (2008) P10008.
- F. Menczer, S. Fortunato, and C. A. Davis, *A First Course in Network Science* (Cambridge University Press, 2020). 한국어판 『네트워크 분석』 (에이콘출판사, 2022).
- W. W. Zachary, "An information flow model for conflict and fission in small groups," *J. Anthropol. Res.* **33**, 452 (1977).
- Prof. Sang Hoon Lee, lecture slides for Network Science (이상훈 교수, 네트워크 과학 강의 슬라이드).
