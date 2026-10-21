Hi, I'm Yufeiyang (Fei). I study cyberspace security at Sun Yat-sen University and live in Shenzhen.

Most of my open-source time goes into AI evaluation tools. I keep running into the same kind of bug there: everything runs fine and you get a number, but the number is wrong. A judge model fails to answer and that counts as a 0. A missing field gets quietly skipped, and the tool still prints "all good". These are the bugs I like chasing.

I'm also an [Area Triager for TruLens](https://github.com/truera/trulens/blob/main/MAINTAINERS.md#area-triagers), covering feedback functions and metrics.

Some merged PRs I like:

- **TruLens [#2834](https://github.com/truera/trulens/pull/2834)**: when the judge couldn't produce a score, its `-1` placeholder was averaged in with the real scores. So a supported claim plus one failed call averaged out to 0.0.
- **Inspect Evals [#2132](https://github.com/UKGovernmentBEIS/inspect_evals/pull/2132)**: calibration error was computed after the epochs were already merged, so with several epochs a fully wrong attempt could still report 0.0. It now works per attempt.
- **PyRIT [#2467](https://github.com/microsoft/PyRIT/pull/2467)**: I was cleaning up a sentinel value in the GCG optimizer and wrote a new sentinel of my own. The maintainer caught it in review, and it became an explicit flag.
- **Soup [#911](https://github.com/MakazhanAlpamys/Soup/pull/911)**: a config check said "every setting is read" when two were silently dropped. Besides adding the two fields, the PR changed that sentence so it only claims what was actually checked.
- **Opik [#8195](https://github.com/comet-ml/opik/pull/8195)**: the output being graded could break out of the judge prompt. The first version got changes requested; the second got merged.

[All merged PRs](https://github.com/search?q=author%3Afeiiiiii5+is%3Apr+is%3Amerged+is%3Apublic+-user%3Afeiiiiii5&type=pullrequests)

How I work: I use AI coding agents a lot. I run several of them under rules I set and keep adjusting: read the repo's contributing guide and AI policy first, write a test that fails before the fix, and stay out of projects that don't want agent PRs. I pick the direction and talk to the maintainers. Maintainers decide what gets merged.

If one of my PRs is noisy, wrong, or just not something you want, close it or tell me. I'd rather know.

Most repos on this account are forks for upstream PRs.
