Write a new blog post for this sport science and biomedical engineering blog.

**Topic:** $ARGUMENTS

Work through the steps below in order. At every **[WAIT FOR APPROVAL]** checkpoint, stop completely and do not proceed until the user explicitly says to continue.

---

## Step 1 — Draft a PubMed search strategy [WAIT FOR APPROVAL]

Propose a PubMed search strategy. Present it with:

- **Query string** — a complete, valid PubMed query using MeSH terms (`[MeSH Terms]`), title/abstract keywords (`[tiab]`), Boolean operators (AND, OR, NOT), and any useful field tags
- **Filters** — article types to prioritise (systematic reviews, meta-analyses, RCTs); language (English); suggested publication date range
- **Estimated scope** — rough estimate of how many results to expect

Stop here. Ask the user to approve, modify, or reject the strategy. Do not run any searches yet.

---

## Step 2 — Search PubMed and select articles [WAIT FOR APPROVAL]

Once the strategy is approved, run the search using the NCBI E-utilities API (no API key needed). Use Bash tool to execute these curl calls.

**Search — retrieve up to 80 PMIDs:**
```bash
curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term=QUERY_URL_ENCODED&retmax=80&retmode=json"
```

**Fetch metadata and abstracts in MEDLINE text format:**
```bash
curl -s -X POST "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi" \
  -d "db=pubmed&id=PMID1,PMID2,...&rettype=medline&retmode=text"
```

The MEDLINE format returns fields like `TI` (title), `AU` (authors), `AB` (abstract), `TA` (journal), `DP` (date), `AID` (DOI). Read all abstracts and select the **8–12 most relevant** papers.

Present the selected articles as a numbered list: title, first author et al., journal, year, PMID, and a one-sentence note on why it is relevant.

Stop here. Ask the user to approve the list. The user may remove articles or ask for replacements before you continue.

---

## Step 3 — Write the blog post

After the article list is approved, write the post. Match the style of the existing posts on this site — read `posts/recovery/index.html` or `posts/hrv/index.html` for reference on tone, length, and structure:

- Flowing, evidence-based paragraphs — scientific but accessible to an educated general audience
- No unnecessary jargon; explain technical terms when they are essential
- **No em dashes** (—) used as sentence separators; rephrase those as separate sentences or use commas instead
- **No inline citations** — do not mention author names or years inside the body text
- Cover the topic thoroughly but keep the writing concise — cut anything that does not add meaning
- Length should match the topic: a focused topic warrants a shorter post, a complex one warrants a longer one; do not pad or artificially constrain
- A **References** section at the end, formatted exactly like the existing posts:
  `Author(s). Title. Journal. Year;volume(issue):pages. doi: ...`

---

## Step 4 — Create the files

1. Choose a short, lowercase, hyphenated slug from the topic (e.g. `vo2max`, `sleep`, `tendon-stiffness`)

2. Create the directory `posts/{slug}/`

3. Create `posts/{slug}/index.html` using this exact template structure — fill in the post title, date (today's date formatted as `DD Mon YYYY`, e.g. `03 Jun 2026`), and body content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Marck+Script&family=Open+Sans:wght@300&display=swap" rel="stylesheet">
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="../../style.css">
  <title>Paavo Nyländen</title>
</head>
<body>
  <header class="otsikko">
    <h1>Sport Science & Engineering</h1>
    <p>By Paavo Nyländen</p>
  </header>

  <div class="navigointi"><a class="back-link" href="../../index.html">&#8592; Blog</a></div>

  <div class="blogiteksti">
    <h1>POST TITLE</h1>
    <p>DD Mon YYYY</p>

    <!-- paragraphs go here -->

    <h2>References</h2>
    <div class="lahteet">
      <!-- references go here, each in its own <p> -->
    </div>
  </div>

  <footer class="alatunniste">
    <p>CONTACT</p>
    <p>LinkedIn: <a href="https://www.linkedin.com/in/paavonylanden/">Paavo Nyländen</a></p>
  </footer>
</body>
</html>
```

4. Add a new card at the **top** of the post grid in `index.html` (inside `.blogikirjoitukset`, before the first existing card), using `images/placeholder.png` and today's date:

```html
<div class="blogikirjoitus">
  <a href="posts/{slug}/index.html">
    <div class="blogi-ikkuna">
      <img class="blogikuva" src="images/placeholder.png" alt="{Topic}">
      <h3>{Post title}</h3>
      <p>DD Mon YYYY</p>
    </div>
  </a>
</div>
```
