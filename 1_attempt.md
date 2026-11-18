Snapshot code (attempt-before-AI): [ADD HASH AFTER COMMIT]

Data: teaching_prices_clean_week2.csv, my Week 2 cleaned file (2_work.ipynb loads it in Part 0). 96 rows, 4 items x 2 cities x 12 weeks (1 Jan to 19 Mar 2026). 3 prices are missing and flagged: Pulse C City 2 on 1 Jan (blank), Staple A City 2 on 15 Jan (was "1,250"), Sweetener D City 1 on 22 Jan (was 9999).

Step 1: Statistics for each item

Code: groupby("item")["price"].agg(["count", "mean", "median", ...]) and first vs last date by item and city.

Oil B: 24 prices. Mean 324.83, median 324.0 (gap 0.83). City 1: 298.0 on 1 Jan, 344.0 on 19 Mar, +15.44%. Pulse C: 23 prices. Mean 205.91, median 206.0 (gap -0.09). City 1: 200.0 on 1 Jan, 207.5 on 19 Mar, +3.75%. Staple A: 23 prices. Mean 111.26, median 112.5 (gap -1.24). City 1: 101.0 on 1 Jan, 114.5 on 19 Mar, +13.37%. Sweetener D: 23 prices. Mean 167.15, median 167.5 (gap -0.35). City 1: 149.0 on 1 Jan, 178.5 on 19 Mar, +19.80%.

I used City 1 for the percent change, because Pulse C City 2 has no price on 1 Jan. City 1 is fair to use: City 2 is exactly 6 PKR more than City 1 on all 45 dates where both have a price. So the PKR change is the same in both cities. The percent is a little lower in City 2 (for example Staple A 12.62%), because it starts from a higher price.

Which statistic I would report, and why:

Oil B: Report the first-to-last change (+46 PKR, +15.4%). Mean and median are almost equal, so either one is fine for the usual price. But Oil B went up in every week, so a 12-week average hides the rise.

Pulse C: Report the median (206) and say the change is small. It moves back and forth between 200, 202.5 and 205. First-to-last is +3.75%, but the last week jumped to 207.5. First 4 weeks vs last 4 weeks is only +1.96% (mean) or +2.72% (median).

Staple A: Report the change, using the first 4 weeks vs the last 4 weeks (+11.7% mean, +11.1% median), next to first-to-last (+13.4%). It goes down 1.5 PKR in 5 of 11 weeks, including the last week. So first-to-last depends on the end date: to 12 Mar it is +14.85%, to 19 Mar it is +13.37%.

Sweetener D: Report the first-to-last change (+29.5 PKR, +19.8%), the biggest of the 4 items. For the usual price, use the median (167.5), because the raw file had a 9999 for this item.

General rule: for the usual price, use the median, since it is safe against bad values and is the same as the mean in clean data. For "did it go up", use neither. Use a change between start and end.

Step 2: With and without a flagged value

Item: Staple A. Flagged value: "1,250" on 15 Jan, City 2 (set to missing in Week 2). Code: mean() and median() on Staple A prices, with 1250 added back and without.

Without 1,250: 23 prices. Mean 111.26, median 112.5. With 1,250: 24 prices. Mean 158.71, median 112.5.

The mean moved by 47.45 PKR. The median did not move at all. Why: the mean adds every price and divides by the count, so one price that is about 1,139 PKR too high adds 1,138.74 / 24 = 47.45 to the mean. 158.71 is higher than every real Staple A price (the highest is 122), so it is not a typical price. The median only looks at the middle of the sorted list. 1,250 goes to the top of the list, and the middle stays at 112.5. Same test on Sweetener D with 9999: the mean goes from 167.15 to 576.81, and the median only from 167.5 to 167.75.

Step 3: Referee's note (draft)

Did the staple really go up?

(O) In this teaching data, Staple A cost 101 PKR per kg in City 1 on 1 January and 114.5 PKR on 19 March, a rise of 13.5 PKR or 13.4%. (O) City 2 shows the same 13.5 PKR rise, from 107 to 120.5 PKR (12.6%). (O) Over the 12 weeks, the mean price of Staple A was 111.26 PKR and the median was 112.5 PKR. (O) These two averages are only 1.24 PKR apart, so in the cleaned data the mean and the median tell the same story. (O) Neither average shows whether the price went up, because each one squeezes all 12 weeks into one number. (O) The rise was not smooth: the price fell by 1.5 PKR in 5 of the 11 weeks, including the last week. (O) Comparing the first 4 weeks with the last 4 weeks, which smooths out these dips, the mean rose 11.7% and the median 11.1%. (O) In the raw file, one Staple A price was typed as "1,250"; with that value left in, the mean jumps to 158.71 PKR, while the median stays at 112.5. (E) A possible explanation for the argument is that the neighbour quoting the mean used figures that still had a bad value like this in them. (C) So the neighbour quoting the mean is wrong because his average is pulled up by a typo. (O) Verdict: yes, the staple went up, by about 11% to 13% depending on which weeks are compared. (O) This is illustrative teaching data for 2 cities and 12 weeks, not PBS observations, so it cannot tell us about real prices.

Step 4: Expected result before asking AI

I expect the AI to agree on the numbers (they can be recomputed). I expect it to add reasons for the price changes that are not in the data, such as costs or demand, because the file has only date, item, city and price.
