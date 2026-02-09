# Starting from Scratch

Detailed guidance on beginning a new design without getting overwhelmed or making premature decisions.

---

## Start with a Feature, Not a Layout

Don't begin designing an app by working on the shell (navigation, sidebars, etc.). Start with a piece of actual functionality.

**The Problem:**
When most people think about "designing the app," they're thinking about the shell — top nav or sidebar, content container or full-width, where the logo goes. An "app" is actually a collection of features. Before you've designed a few features, you don't even have the information you need to make a decision about how the navigation should work.

**The Solution:**
Start with actual functionality. For a flight booking service, start with "searching for a flight" — departure city, destination, dates, and a search button. You might not even need navigation chrome. It worked for Google.

---

## Detail Comes Later

In the earliest stages of designing a new feature, don't get hung up on low-level decisions like typefaces, shadows, and icons.

**Design in Low Fidelity First:**
That stuff will all matter eventually, but it doesn't matter right now. If you have trouble ignoring details in high fidelity, try designing on paper using a thick Sharpie — obsessing over details just isn't possible.

**Hold the Color:**
Even when ready to refine in higher fidelity, resist introducing color right away. By designing in grayscale, you're forced to use spacing, contrast, and size to do all of the heavy lifting. You'll end up with a clearer interface with a strong hierarchy that's easy to enhance with color later.

**Don't Over-Invest:**
The whole point of low-fidelity is to move fast. Sketches and wireframes are disposable — users can't do anything with static mockups. Use them to explore ideas, and leave them behind when you've made a decision.

---

## Don't Design Too Much

You don't need to design every single feature before moving to implementation; in fact, it's better if you don't.

**Work in Cycles:**
1. Design a simple version of the next feature
2. Build it
3. Discover edge cases in real use
4. Fix them
5. Repeat

Build the real thing as early as possible so your imagination doesn't have to do all the heavy lifting.

**Be a Pessimist:**
Don't imply functionality you aren't ready to build. A comment system with no attachments is better than no comment system at all. When designing a new feature, expect it to be hard to build. Design the smallest useful version you can ship.

---

## Choose a Personality

Every design communicates something. Decide intentionally.

**Font Choice:**
| Goal | Typeface |
|------|----------|
| Elegant or classic | Serif typeface |
| Playful | Rounded sans serif |
| Plain / neutral | Neutral sans serif |

**Color Psychology:**
- Blue = safe and familiar
- Gold = expensive and sophisticated
- Pink = fun and not so serious

**Border Radius:**
| Radius | Feel |
|--------|------|
| Small (`rounded-sm`) | Neutral |
| Large (`rounded-xl`, `rounded-full`) | Playful |
| None (`rounded-none`) | Serious, formal |

**Important:** Stay consistent. Mixing square corners with rounded corners almost always looks worse than sticking with one or the other.

**Language:**
Words are everywhere in a UI. "Your account" vs "Hey there!" — choosing the right words is just as important as choosing the right color or typeface.

**Finding Your Direction:**
Look at other sites used by the people you want to reach. If they are mostly "serious business," maybe that's how your site should look too. Just don't borrow too much from direct competitors.

---

## Limit Your Choices

When designing without constraints, decision-making is torture — there's always more than one right choice.

**Define Systems in Advance:**
- Don't reach for the color picker every time — choose from a set of 8-10 shades picked ahead of time
- Don't tweak font size one pixel at a time — define a restrictive type scale in advance

**Design by Process of Elimination:**
With a constrained set of values, pick one, try the values on either side, and keep the best. Far fewer "right" choices to agonize over.

**Systematize Everything:**
- Font size, weight, line height
- Color palette
- Margin, padding
- Width, height
- Box shadows, border radius, border width
- Opacity

Look for opportunities to introduce new systems as you make new decisions, and try to avoid making the same minor decision twice.
