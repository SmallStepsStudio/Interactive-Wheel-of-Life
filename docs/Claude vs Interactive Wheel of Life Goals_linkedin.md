<!-- SPDX-FileCopyrightText: Copyright (c) 2026 Madison Nicole Goodwin https://github.com/NicoleDev021 -->  
<!-- SPDX-FileCopyrightText: Copyright (c) 2026 Small Steps Studio LLC smallsteps.studio -->  

![Wheel of Life filled in](https://raw.githubusercontent.com/SmallStepsStudio/Interactive-Wheel-of-Life/main/docs/wheel-of-life-filled.png)

# Claude vs Interactive Wheel of Life Goals

**Madison Nicole Goodwin**
Software • Data • Analytics Engineer | SQL • R • Python • Docker • CI/CD | Identity & Access Management

*July 1, 2026*

[smallstepsstudio.github.io/Interactive-Wheel-of-Life](https://smallstepsstudio.github.io/Interactive-Wheel-of-Life/)

---

I built a Wheel of Life tool this week. Not for a job search post, just something I could finish in an afternoon and give away for free. That's actually why it's one plain HTML file. No login, no server, no framework to install. You open the file and it works, on any computer, even offline.

The tool itself is a self assessment wheel with 8 life categories arranged around a circle. Each category has its own ring of 10 segments you click through to rate it, so the wheel fills in as you go and you end up with a quick visual of which areas of your life are strong and which are neglected. You can rename any category, pick your own colors or choose from six built in palettes including a colorblind safe one, and there's a goal list underneath tied to the same categories. When you're done you save it and it exports as a new file you can reopen later with everything you filled in still there.

![Interactive Wheel of Life](https://raw.githubusercontent.com/SmallStepsStudio/Interactive-Wheel-of-Life/main/docs/image.png)

The version worth talking about is what it took to get the label rendering right, because it's the clearest example of what working with Claude actually looks like on something that isn't a straightforward build.

The category names need to curve around the circle instead of sitting flat. First attempt had uneven spacing between the top and bottom halves. Fixed the radius, which fixed that and caused a new problem, labels overlapping into the next wedge. Fixed the angle, which surfaced a third symptom in a different spot.

At that point patching each symptom wasn't going to work. The actual issue was that making the bottom half of labels read left to right instead of backwards meant reversing the direction the arc gets drawn, and that reversal flips which side of the arc the letters render on. Three different visual bugs, one root cause. The fix was switching to a text alignment property that centers text on its path regardless of which direction the arc runs, so the direction reversal stopped mattering.

That's the kind of bug you don't catch by accepting the first plausible looking fix from Claude. I kept asking whether a change actually solved the underlying thing or just moved the symptom somewhere else. Later in the same session, a custom color feature had a rule preventing colors from landing too close to the wheel's separator line. I asked whether the automatically generated muted variant of a color could land in that same excluded zone even when the original color didn't. It could. That question caught a real gap before it shipped.

Two companion planner pages came out of the same build. Not finished yet, more to come.
