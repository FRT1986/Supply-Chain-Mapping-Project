# SCM Category Mapping

An interactive version of the category mapping template. Value Analysis owners, the inventory planning
groups, the 17 inventory planners and the 10 buyers who cover those rows today are all mapped in. The
only thing left to fill in is which purchasing group each inventory group belongs to.

Everything is in `index.html` — one file, no build step, no server, no dependencies to install.

## Put it on GitHub Pages

1. Create a repository (private is fine — Pages works on private repos for GitHub Team and Enterprise;
   on a free account the repo must be public for Pages to serve it).
2. Upload `index.html` and this README to the root of the `main` branch.
3. Go to **Settings → Pages**. Under **Source** choose *Deploy from a branch*, pick `main` and `/ (root)`, save.
4. Wait about a minute. The site appears at `https://<your-org>.github.io/<repo-name>/`.

To change the data later, regenerate `index.html` and commit over it. Pages redeploys on push.

## How people use it

- Pick a purchasing group on each row. **Set all** on a category header does the whole category at once.
- The bar across the top shows how the 20,855 stock items are splitting between groups as you go.
- Each group panel shows **who buys for those rows today**, so you can see which buyers already cluster
  together before deciding the shape of the group.
- Name each group and add its buyers on the right. A buyer can only sit in one group — adding them to a
  second removes them from the first.
- Search matches category, inventory group, planner and buyer names.
- **Export CSV** opens in Excel with every row, its planner, its current buyer, the PR value band, the
  assignment, the group name and the group's buyers.

## Where the work is saved — read this before rolling it out

Work saves automatically, but **in that person's browser only** (`localStorage`). It is not shared, and it
does not sync. Two people opening the page will not see each other's assignments, and clearing browser
data loses the work.

For a first pass by one person, that is fine. To share:

- **Save file** writes `mapping.json`. Send it on, or commit it to the repo.
- **Load file** reads it back on any machine.

That gives you a version history if you commit each round, but it is still one editor at a time.

If you need several people editing at once, a static Pages site cannot do it — that needs somewhere
central to write to. Realistic options, cheapest first: keep the workbook as the shared master and use
this page for individual working sessions; put the file on SharePoint or Google Sheets where co-editing
is built in; or, if it justifies the effort, back this page with a small database.

## Regenerating the data

The page has the data baked into a `<script id="seed">` block near the bottom. It came from:

- `Planners___Buyers_Structure.xlsx` — the inventory group structure, 17 planners, 10 buyers, value bands
- `Inventory_Planning_Groups.xlsx` — item counts behind each group, 20,855 stock items
- `Stock_and_Non-Stock_PR_approvers-_VA_team_2026.xlsx` — Value Analysis owner per category
- `Staff_list_Section_wise.xlsx` — the 76 names in the buyer picker

Seven rows carry a planner but no buyer, including CSSD General and CSSD Orthopaedic — the two largest
categories in the file at 7,642 and 7,437 items. Those cells are left empty rather than guessed.

The eight rows marked in amber are classes 61, 81, 82, 83, 85, 86, 87 and 98, which do not appear in the
planning file. They still need a purchasing group, so they each get a row. Hovering the `!` marker on any
row shows what needs deciding about it.
