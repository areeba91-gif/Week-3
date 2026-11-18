What I asked AI (Interpretation Auditor):

"Here is a statistics table of weekly prices for 4 items in 2 cities, 1 Jan to 19 Mar 2026. It is illustrative teaching data. Interpret it for a newsroom note on whether the staple's price really went up."

Oil B: 24 prices. Mean 324.83, median 324.0, min 298.0, max 350.0. City 1 first 298.0, last 344.0, change 15.44%.
Pulse C: 23 prices. Mean 205.91, median 206.0, min 200.0, max 213.5. City 1 first 200.0, last 207.5, change 3.75%.
Staple A: 23 prices. Mean 111.26, median 112.5, min 99.5, max 122.0. City 1 first 101.0, last 114.5, change 13.37%.
Sweetener D: 23 prices. Mean 167.15, median 167.5, min 149.0, max 184.5. City 1 first 149.0, last 178.5, change 19.80%.

I did not replace my note with the AI's text.

AI's interpretation, with every sentence highlighted (green, amber, red):

S1. Oil B is the most expensive item, with a mean of 324.83 PKR per kg and a median of 324.0.
S2. For every item the mean and the median are within about 1.5 PKR of each other, so the prices are roughly symmetric with no major outliers.
S3. Sweetener D had the largest increase, about 19 to 20% from the first week to the last.
S4. Pulse C was the most stable, rising only about 3.75%.
S5. Staple A rose about 13% over the period, so yes, the staple's price clearly went up.
S6. The rise in Oil B is likely driven by higher global edible oil prices and a weaker rupee.
S7. Sweetener D's increase may reflect seasonal demand ahead of Ramadan.
S8. City 2 is consistently more expensive than City 1, probably because of higher transport costs.
S9. Because the mean and the median agree, the neighbour quoting the mean and the neighbour quoting the median are both right.
S10. Households in both cities are therefore paying noticeably more for basic food than at the start of the year.
S11. Staple A rose steadily every week.
S12. Overall, this points to broad food inflation in Pakistan in early 2026.

Colour key:
GREEN = I can recompute it.
AMBER = an explanation.
RED = a causal claim, or uses data I was not shown.

Count: 7 green, 1 amber, 3 red, and S8 is half green, half amber (12 sentences).

Audit:

Every number was recomputed in 2_work.ipynb, Part 3 (Cells 15 to 22).

S1: Oil B most expensive, mean 324.83, median 324.0
Colour: GREEN
How I checked: Cell 15: stats sorted by mean.
Decision: ACCEPTED. Matches.

S2: Mean and median within about 1.5 PKR, no major outliers
Colour: GREEN
How I checked: Cell 16: largest mean minus median gap is 1.24.
Decision: ACCEPTED, with a note: only true after cleaning. In the raw file the 9999 and 1,250 were outliers.

S3: Sweetener D largest increase, about 19 to 20%
Colour: GREEN
How I checked: Cell 17: 19.80% City 1, 19.03% City 2.
Decision: ACCEPTED.

S4: Pulse C most stable, about 3.75%
Colour: GREEN
How I checked: Cell 17: 3.75% City 1.
Decision: ACCEPTED, with a note: City 2 cannot be computed (no price on 1 Jan).

S5: Staple A rose about 13%, so it "clearly" went up
Colour: GREEN
How I checked: Cell 17: 13.37% City 1, 12.62% City 2. Cell 20: weekly prices.
Decision: MODIFIED. 13% is right, but "clearly" is too strong. It fell in 5 of 11 weeks. First 4 vs last 4 weeks is 11.1 to 11.7%.

S6: Oil B rise driven by global oil prices and a weaker rupee
Colour: RED
How I checked: Cell 22: columns are date, item, city, price, unit, data_label, flag. No oil import or exchange rate data.
Decision: REJECTED. Causal claim with data not shown.

S7: Sweetener D may reflect demand before Ramadan
Colour: AMBER
How I checked: Cell 22: no demand or season column.
Decision: REJECTED for the note. It says "may", but I cannot test it with this file.

S8: City 2 always more expensive, probably transport costs
Colour: GREEN + AMBER
How I checked: Cell 18: City 2 minus City 1 on all 45 pairs is always exactly +6.
Decision: First half ACCEPTED. "Transport costs" REJECTED, no cost data. A gap of exactly 6 every week looks like how the teaching file was built.

S9: Both neighbours right because mean and median agree
Colour: GREEN
How I checked: Cell 19: Staple A mean 111.26, median 112.5.
Decision: MODIFIED. Both are right about the usual price, but neither shows whether it went up. That needs a start-to-end change.

S10: Households pay noticeably more for basic food
Colour: RED
How I checked: Cell 21: no household, quantity or spending columns. data_label says teaching data.
Decision: REJECTED. Data not shown.

S11: Staple A rose steadily every week
Colour: GREEN
How I checked: Cell 20: down 1.5 on 8 Jan, 29 Jan, 12 Feb, 5 Mar, 19 Mar.
Decision: REJECTED. Recomputed and wrong. It went down in 5 of 11 weeks.

S12: Broad food inflation in Pakistan in early 2026
Colour: RED
How I checked: Cell 21: data_label is "ILLUSTRATIVE TEACHING DATA - NOT ACTUAL PBS OBSERVATIONS". 4 items, 2 cities, 12 weeks.
Decision: REJECTED. Not real data, and 4 items cannot show "broad" inflation.

Result: 4 accepted, 1 accepted in part, 2 modified, 5 rejected.
All the AI's numbers were right. The problems were in the words around them: "clearly", "steadily", "households", "Pakistan", and the reasons for the price changes.

Confused Classmate (transcript excerpt):

I asked the AI: "Play a classmate who believes the mean is always the typical price. Keep asking 'but why?' until you understand. Use our Staple A numbers."

Classmate: The mean of Staple A with the 1,250 is 158.71. The mean uses every number, so isn't that the most complete typical price?

Me: It uses every number, including the wrong one. Every real Staple A price in the file is between 99.5 and 122. 158.71 is higher than all of them. A "typical" price that no week ever had is not typical.

Classmate: But why can one number move it that much? It is only 1 price out of 24.

Me: The mean adds all 24 prices and divides by 24. The 1,250 is 1,138.74 more than the old mean of 111.26. Shared across 24 prices, that is 1,138.74 / 24 = 47.45 PKR added to the mean. That is exactly how much the mean moved in my notebook.

Classmate: But why doesn't the median move then? Isn't it ignoring the data?

Me: The median sorts the prices and takes the middle. 1,250 goes to the top of the list, so the middle stays at 112.5. It does not ignore 1,250. It counts it as "one more high price", but not as "1,250 high".

Classmate: Okay. So the median is always the better one?

Me: No. In the cleaned file the mean is 111.26 and the median is 112.5, almost the same. The mean is fine when there are no extreme values. The median is safer when a bad or extreme value might still be in the data.

Classmate: So if both are about 112, the neighbours are both right that the staple went up?

Me: That is a different question. Both are averages of all 12 weeks. They tell you the usual price, not whether it rose. For that I compare the start and the end: 101 to 114.5 in City 1, or the first 4 weeks against the last 4 weeks, 105 to 117.25.

Classmate: Oh. So "what is the typical price" and "did it go up" need different numbers.

(I stopped here. The classmate stopped asking why the mean is typical and moved to a new question, so the confusion was fixed.)

Reflection: Where did my first draft say more than the data allowed?

1. My (C) sentence: "the neighbour quoting the mean is wrong because his average is pulled up by a typo."
I never saw the neighbours' numbers. In the cleaned data the mean (111.26) is not wrong at all. This should have stayed as the (E) sentence before it, labelled as a possible explanation, and the (C) sentence should be cut.

2. My verdict: "yes, the staple went up."
This is true only for this teaching file, 2 cities and 12 weeks. I put the limit in the last sentence, but the verdict should carry it too: "In this teaching data, the staple went up by about 11 to 13%."

3. The size of the rise depends on the dates.
First-to-last is 13.37% to 19 Mar, but 14.85% to 12 Mar, because the last week was a down week. Giving one exact number would say more than the data allows. Giving a range is more honest.

The AI went further than my draft (S6, S10, S12). It gave reasons and talked about households and Pakistan, with no data on any of these. My draft did the same thing on a smaller scale, in sentence 1.

What I learned:

The mean and the median only disagree when there is an extreme value. In the cleaned data they are 1.24 PKR apart, so the neighbours' argument is about the wrong thing.
The real question, "did it go up", needs a change from start to end, not an average.
A number can be correct and the sentence around it still wrong (S5 "clearly", S11 "steadily").
