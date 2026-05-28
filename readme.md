# Finding Planets Around Kepler-90

This project uses Python and a library called `lightkurve` to look for planets outside our solar system (exoplanets). We look at a star called **Kepler-90** and check its brightness over time to see if any planets are blocking its light.

---

## How the Code Works

1. **Get the Data:** The code downloads data from the Kepler Space Telescope. It stitches different chunks of data together into one long timeline.
2. **Clean Up the Noise:** Stars naturally change brightness, and space telescopes sometimes take blurry pictures. The code smooths out these slow changes and removes weird data errors so we can see the real picture.
3. **Look for Patterns:** When a planet passes in front of a star, it blocks a tiny bit of light. This creates a dip in brightness. The code searches for these dips to guess how long a planet takes to go around the star (its orbital period).
4. **Make a Chart:** The code lines up all the dips on top of each other to show a clean chart of the planet blocking the light.

---

## What We Found

* **The Code's Guess:** The planet goes around the star every **15.79 days**.
* **The Real Answer:** NASA says the closest planet here (Kepler-90i) actually takes **14.45 days**.

### Why is there a difference?

Our simple search missed the exact target by about a day and a half. Here is why:

* **Too Many Planets:** Kepler-90 is a crowded home. It has 8 planets pulling on each other and crossing the star at different times. Their signals get mixed up.
* **Math Confusion:** The code found a repeating pattern, but it likely got confused by the patterns of the other planets nearby and locked onto the wrong loop.
* **It's a Hard Problem:** Scientists actually needed advanced AI and machine learning back in 2017 to find Kepler-90i because its signal was too weak for a simple tool like this one to get perfectly right.

---

## How to Run It

### 1. Install the tools
You need Python and a few libraries. Open your terminal and run:

```bash
pip install lightkurve numpy matplotlib