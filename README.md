# 1GFG Employee Deduction Statement Generator

A single-page browser tool that turns a census export (.xlsx or .csv) into
branded PDF Employee Deduction Statements, one per company, plus a
Needs Review PDF for rows with missing pricing data.

Runs entirely client-side — no backend, no data ever leaves the browser.

## Deploy

This is a static site with one file (`index.html`). Any static host works:

- **Vercel**: import this repo as a new project. Framework preset: "Other".
  No build command, no output directory override needed.
- **Netlify**: drag the repo folder onto app.netlify.com/drop, or connect
  the repo the same way as Vercel.
- **GitHub Pages**: enable Pages on this repo, source = root of main branch.

## Required input columns

Company, First Name, Last Name, Status, Employee ID, SIMERP, FGP,
FGP Amount, Policy Provider, Eligible Policy

(Column order and sheet name don't matter — headers are matched
case/spacing-insensitively.)

## Rollup logic

- **Virtual** = every row's SIMERP price, summed
- **In-Person** = FGP Amount for rows tagged MEC or MEC+, summed
- **Wholelife** = Eligible Policy amount, summed
- Companies with "test" in the name are skipped entirely
- Rows missing SIMERP or FGP are excluded from totals and listed in the
  Needs Review PDF instead (a missing Employee ID alone does not exclude
  a row)

## Customizing branding

Search for `BRAND_HEX` and `COMPANY_INFO` near the top of the `<script>`
block in `index.html` to change the accent color, company name, address,
or contact info shown on every statement.
