# Gutenberg 28K — Project Gutenberg Book Metadata

A structured dataset containing metadata for more than 28,000 books available through [Project Gutenberg](https://www.gutenberg.org/).

The dataset is intended for research, data analysis, natural language processing (NLP), information retrieval, recommendation systems, semantic search, and other machine learning or software projects.

This repository contains **book metadata, not the full text of the books**.

## Dataset Overview

| Field | Description |
|---|---|
| Records | 28,000+ books |
| Source | [Project Gutenberg](https://www.gutenberg.org/) |
| Format | JSON |
| Full book text | Not included |
| Authors | Names and birth/death years |
| Summaries | Book summaries provided in the source metadata |
| Subjects | Subject classifications |
| Bookshelves | Project Gutenberg bookshelf categories |
| Languages | Available languages |
| Copyright | Copyright status provided by the source |
| Formats | Links to available ebook formats and resources |
| Download count | Recorded Project Gutenberg download count |

## Dataset Structure

The dataset is provided as:

```text
complete_gutenberg_catalog.json
```

The root of the file is a JSON array containing individual book records.

A typical record has the following structure:

```json
{
  "id": 11,
  "title": "Alice's Adventures in Wonderland",
  "authors": [
    {
      "name": "Carroll, Lewis",
      "birth_year": 1832,
      "death_year": 1898
    }
  ],
  "summaries": [
    "Alice's Adventures in Wonderland by Lewis Carroll..."
  ],
  "editors": [],
  "translators": [],
  "subjects": [
    "Alice (Fictitious character from Carroll) -- Juvenile fiction",
    "Children's stories",
    "Fantasy fiction"
  ],
  "bookshelves": [
    "Category: British Literature",
    "Category: Classics of Literature"
  ],
  "languages": [
    "en"
  ],
  "copyright": false,
  "media_type": "Text",
  "formats": {
    "text/html": "https://www.gutenberg.org/ebooks/11.html.images",
    "application/epub+zip": "https://www.gutenberg.org/ebooks/11.epub3.images",
    "text/plain; charset=utf-8": "https://www.gutenberg.org/ebooks/11.txt.utf-8"
  },
  "download_count": 69528
}
```

## Fields

### `id`

The Project Gutenberg ebook identifier.

### `title`

The title of the ebook.

### `authors`

A list of authors associated with the work. Author records may contain:

- `name`
- `birth_year`
- `death_year`

### `summaries`

Available descriptions or summaries of the book.

Some summaries in the source metadata are automatically generated.

### `editors`

Editors associated with the work, when available.

### `translators`

Translators associated with the work, when available.

### `subjects`

Subject classifications associated with the book.

### `bookshelves`

Project Gutenberg bookshelf and category information.

### `languages`

Languages in which the ebook is available, represented using language codes such as `en`.

### `copyright`

Copyright status reported in the source metadata.

This field should not be interpreted as a universal legal determination of copyright status. Copyright laws vary by jurisdiction.

### `media_type`

The media type associated with the work.

### `formats`

URLs for resources and ebook formats associated with the book, such as HTML, EPUB, plain text, RDF, and cover images.

### `download_count`

The download count reported by Project Gutenberg.

## Usage

### Load the dataset with Python

```python
import json

with open("complete_gutenberg_catalog.json", "r", encoding="utf-8") as file:
    books = json.load(file)

print(f"Total books: {len(books)}")
```

### Search by title

```python
query = "alice"

results = [
    book for book in books
    if query.lower() in book["title"].lower()
]

for book in results:
    print(book["id"], book["title"])
```

### Search by author

```python
query = "Carroll"

results = [
    book
    for book in books
    if any(query.lower() in author["name"].lower()
           for author in book.get("authors", []))
]

for book in results:
    print(book["title"])
```

### Find the most downloaded books

```python
popular_books = sorted(
    books,
    key=lambda book: book.get("download_count", 0),
    reverse=True
)

for book in popular_books[:10]:
    print(book["title"], book.get("download_count", 0))
```

## Potential Applications

The dataset can be used as a metadata source for:

- Book search and discovery
- Recommendation systems
- Semantic search
- Natural language processing
- Information retrieval
- RAG and retrieval experiments
- Book classification
- Author and subject analysis
- Data visualization
- Machine learning experiments
- Educational and research projects

Because the dataset does not contain the full text of the books, applications requiring complete book content should retrieve the relevant resource from the original source where appropriate.

## Data Source

The metadata is sourced from [Project Gutenberg](https://www.gutenberg.org/), a digital library providing access to thousands of ebooks.

Project Gutenberg:

- Website: https://www.gutenberg.org/
- About: https://www.gutenberg.org/about/
- Catalog: https://www.gutenberg.org/ebooks/
- Terms of Use: https://www.gutenberg.org/policy/terms_of_use.html
- Copyright guidance: https://www.gutenberg.org/policy/license.html

The `formats` field in each record provides links to resources associated with individual Project Gutenberg ebooks.

## Provenance

This repository is a derived collection of Project Gutenberg book metadata.

The metadata was collected and consolidated into a single JSON dataset for easier use in data analysis, research, and software projects.

The dataset may contain information that changes over time, such as download counts and available formats. It should therefore be considered a snapshot of the source data rather than a continuously synchronized catalog.

## Copyright and Licensing

This repository does not claim ownership of the underlying Project Gutenberg works.

The copyright status of an individual work depends on the work, jurisdiction, and applicable law. The `copyright` field included in this dataset reflects information available in the source metadata and should not be treated as legal advice.

Users are responsible for determining whether a particular work or resource may legally be accessed, used, modified, or redistributed in their jurisdiction.

For Project Gutenberg's current policies and terms, consult the official:

- [Terms of Use](https://www.gutenberg.org/policy/terms_of_use.html)
- [License and Trademark Information](https://www.gutenberg.org/policy/license.html)

## Limitations

The dataset is provided as a convenience and may contain:

- Missing author information
- Missing summaries
- Missing subjects or bookshelf classifications
- Incomplete translator or editor information
- Metadata inconsistencies
- Historical download counts
- URLs that may change or become unavailable

No guarantee is made regarding the completeness or accuracy of the metadata.

## Contributing

Contributions are welcome.

If you find incorrect or incomplete metadata, please open an issue with:

1. The affected Project Gutenberg ebook ID
2. The field containing the issue
3. The expected or corrected value
4. A reference to the corresponding Project Gutenberg page, where possible

Pull requests that improve the dataset, documentation, validation, or processing tools are also welcome.

## Citation

If you use this dataset in a research project, publication, or application, please cite this repository and acknowledge Project Gutenberg as the original source of the metadata.

Example:

```text
Gutenberg 28K — Project Gutenberg Book Metadata.
Derived from metadata provided by Project Gutenberg.
```

## Disclaimer

This repository is an independent dataset derived from Project Gutenberg metadata.

It is not an official Project Gutenberg repository and is not affiliated with or endorsed by the Project Gutenberg Literary Archive Foundation.

For authoritative information about an individual ebook, consult its corresponding page on [Project Gutenberg](https://www.gutenberg.org/).

---

## License

No separate license is asserted for the underlying Project Gutenberg metadata or works by this repository.

If you intend to add original code, documentation, or other original material to this repository, consider adding an appropriate open-source license for those contributions.
