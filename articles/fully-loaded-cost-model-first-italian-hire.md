# How to Build a Fully Loaded Cost Model for Your First Italian Hire

> A step-by-step spreadsheet method for US controllers to model the true cost of a first hire in Italy, from gross pay to employer contributions and insurance.



A US offer letter names a salary. An Italian payroll names a cost. The gap between them is where budgets break. This guide gives you the spreadsheet logic to close that gap. A controller can build it in an afternoon.

## Start with the right mental model

In Italy, the gross salary is not what the company pays in total. The employer owes contributions on top of it. The employee also has contributions withheld from the gross. Those are different flows. Keep them in separate blocks of your sheet, or you will double count or miss something.

Think of the model as layers. Each layer sits on the one below it.

## Layer 1: the inputs tab

Create a tab called Inputs. Put every assumption there and nowhere else. Formulas elsewhere should only point to these cells.

You need:

- Gross annual salary in euros.
- The applicable national collective agreement (CCNL) for the role.
- The INAIL risk classification for the job.
- The EUR/USD rate you use for budgeting.
- The start date, so you can prorate the first year.

Add a column next to each input for source and date. If a number has no source, mark it red. This habit saves you at audit time.

## Layer 2: the contribution base

Create a tab called Contributions. The first cell is the taxable base for social security. For a simple salaried role, this starts from gross pay. Your CCNL may define what counts and what does not, so check it before you lock the base.

The pension line (called IVS in the Italian system) is the clearest example of the two-flow logic.

- Employer IVS: 23.81% of the taxable base.
- Employee IVS: 9.19% of the taxable base.

The employer share is a real cost on top of gross. Build it as `= base * employer_rate`. The employee share is withheld from the gross. It reduces net pay. It does not increase your cost. Build it as a separate line and exclude it from the total employer cost.

These rates come from secondary sources. Treat them as working values. Before you finalize a budget, confirm them against the current INPS circulars. Store the confirmation date in the source column.

IVS is not the only employer contribution. Other INPS items can apply depending on the sector, company size and contract type. Create a row for each and leave the rate empty until you have confirmed it. An empty cell is better than a guess, because it shows up as an open item.

## Layer 3: workplace injury insurance

Add an INAIL block below the contributions. INAIL is the national workplace injury insurer. The premium depends on the risk classification of the job, not on your company's home country or industry.

The tariffs currently in force are the 2019 ones (DI 27/02/2019). The way they are applied was changed by a ministerial decree dated 02/04/2026 and published on 03/06/2026. So do not copy a rate from an old article and assume it holds. Build the row with two cells: the rate and the application rule. Fill both from the current INAIL source for your classification.

For a desk role the premium is usually small compared with pension contributions. Even so, keep the line. A small line that is missing is still an error.

## Layer 4: the items outside payroll

A fully loaded model includes more than contributions. Add these as separate rows, each with its own status column:

- Severance accrual (TFR). Italy requires employers to set this aside during employment. Model it as an accrual, not as a cost that appears only at exit.
- Additional monthly pay periods required by the CCNL. Many agreements call for more than twelve payments a year. Check yours and reflect it in the annual gross.
- Paid leave and holiday cost. Model the cost of absence coverage if the role needs it.
- Benefits such as meal vouchers or supplementary health cover, if the CCNL or your policy includes them.
- Equipment, software and workspace.
- One-time costs: onboarding, local payroll setup and any relocation.

Not every row needs a number on day one. Every row needs an owner and a status: confirmed, estimated or open.

## Layer 5: the total and the checks

On a Summary tab, add up gross salary, employer contributions, INAIL and the accruals. That is your annual employer cost in euros. Convert to dollars with the rate from Inputs.

Then add three checks.

- Ratio check: total cost divided by gross salary. This is your loading factor. Compare it with the factor you saw in other quotes. If it differs a lot, find the reason row by row.
- Open items count: a cell that counts rows still marked open. The budget is not final until it reads zero.
- Sensitivity: change gross salary and the exchange rate and see what moves. The contribution lines scale with pay. The exchange rate moves everything.

## Keep it auditable

Use one formula per row, copied down. Avoid hard-coded numbers inside formulas. Log the date you last checked each rate. When a rule changes, as the INAIL application rules did, you will know which cells to revisit.

## What to do next

Build the Inputs tab first. Then fill the pension line, since it is the most certain part. Leave unconfirmed items open and visible. A model with honest gaps beats a model with confident guesses.

When your sheet is ready, try our cost calculator and compare it with your own numbers.

{{< compare-table compact="true" >}}


---
Source: https://hiringitaly.com/articles/fully-loaded-cost-model-first-italian-hire.html · 2026-10-27
