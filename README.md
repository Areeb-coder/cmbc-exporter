# Cambridge Battlecode Research Exporter v2.0

A Chrome extension for exporting Cambridge Battlecode leaderboard
information and team match-history data into Excel-compatible workbooks.

## Installation

1.  Download and unzip the extension archive.
2.  Open `chrome://extensions` in Google Chrome.
3.  Enable **Developer mode**.
4.  Select **Load unpacked**.
5.  Choose the extracted `cambridge-battlecode-suite` folder --- the
    folder that contains `manifest.json`.
6.  Open the relevant Cambridge Battlecode page:
    -   **Leaderboard export:**
        <https://2026a.battlecode.co.uk/game/ladder>
    -   **Match export:** your team's completed match-history page.
7.  Open the extension, choose the export mode, configure the available
    filters or limits, and select **Scan and export Excel**.

Keep the relevant Battlecode page open and allow it to finish loading
while the extension scans.

## Features

### Leaderboard export

-   Scans the leaderboard up to the rank limit selected in the
    extension.
-   Exports the displayed rank and team name.
-   Exports the member count and up to four member names when those
    names are exposed by the page.
-   Leaves unused member columns blank for teams with fewer than four
    members.
-   Does not invent names when the page does not expose a readable name.

The leaderboard workbook uses these columns:

1.  Rank
2.  Team name
3.  Number of team members
4.  First team member
5.  Second team member
6.  Third team member
7.  Fourth team member

### Match-history export

-   Filters match-history records by team and, optionally, bot version
    and opponent.
-   Scrolls the loaded match history to collect additional rendered
    records.
-   Exports match details when those details are present in the page,
    including:
    -   Match ID and match URL
    -   Team and bot version
    -   Opponent
    -   Ranked or unranked classification
    -   Win, loss, or draw result
    -   Our side and both scores
    -   Elo values and displayed Elo changes, when available
    -   Relative time and the original displayed match-row text
-   Separates ranked and unranked matches and losses.
-   Builds opponent-level statistics and a performance dashboard.

### Match workbook sheets

The match export can include:

-   **Dashboard** --- overall, ranked, unranked, and additional
    performance statistics.
-   **All Matches** --- collected match records.
-   **All Losses** --- all collected losses.
-   **Ranked Matches** --- ranked match records.
-   **Unranked Matches** --- unranked match records.
-   **Ranked Losses** --- ranked losses.
-   **Unranked Losses** --- unranked losses.
-   **Opponent Analytics** --- match counts, wins, losses, draws,
    ranked/unranked counts, scores, win rate, and net score by opponent.

## Export format

The extension exports Excel 2003 XML workbooks (`.xls`) containing
multiple worksheets.

These files are XML Spreadsheet 2003 documents. They are **not** binary
`.xls` files or `.xlsx` workbooks. Excel may display a file-format or
compatibility warning when opening them. If prompted, confirm that you
want to open the file.

## Important limitations and data accuracy

-   **Page-dependent:** Extraction depends on the current Cambridge
    Battlecode website structure (DOM), the page being loaded, and the
    browser session's access.
-   **Not live-verified:** The extension has not been verified against
    every authenticated leaderboard or match-history state. Check
    exported rows against the website before relying on them.
-   **Rendered records only:** The extension can collect only records
    that become available to the page while it scrolls. Infinite
    scrolling, virtualized lists, delayed loading, or pagination may
    limit coverage.
-   **Member names:** Some member names may be available only through
    avatar tooltips or profile popups. If the page does not expose a
    readable name to the extension, that cell may be blank. The
    extension must not guess or substitute a label such as "View
    Profile" for a person's name.
-   **Match parsing assumptions:** The match parser follows the supplied
    v153 console script's assumptions about score order and how the
    team's side is identified. Confirm a sample of exported matches
    against the website, especially opponent names, side, scores, and
    result.
-   **Match identifiers:** Match IDs and URLs are extracted only when
    they are present in accessible page links or row attributes. Missing
    values remain blank. A detected ID is not proof that it identifies
    the intended match; open and verify the corresponding match link.
-   **No hidden or private data:** The extension exports only
    information exposed to the browser session. It does not retrieve
    private source code, hidden member names, or matches that the
    account cannot access.
-   **Partial exports:** If the page stops loading, the session expires,
    or the website changes its layout, the workbook may contain fewer
    records than the selected limit or fewer matches than exist.

## Recommended checks

After each export:

1.  Compare the first, middle, and last exported leaderboard ranks with
    the live ladder.
2.  Check teams with one, two, and three members to confirm that member
    counts and blank cells are correct.
3.  Compare several match rows with their match pages, including at
    least one ranked win, ranked loss, unranked win, and unranked loss
    where available.
4.  Verify opponent names, scores, match type, IDs, and URLs before
    using the workbook for analysis.
5.  If records are missing or misidentified, capture the relevant page
    state and extension error so the page-specific extraction logic can
    be adjusted.

## Privacy and responsible use

Use the extension only with your own browser session and information you
are authorized to access. It does not bypass access controls or grant
access to private competition data.
