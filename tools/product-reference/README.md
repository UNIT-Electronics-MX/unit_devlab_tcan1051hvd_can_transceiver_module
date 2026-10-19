# Product reference build

The product reference source is maintained in Markdown under `chapters/`. Document
metadata and chapter order are defined in `book.yml`.

## Updating the contents menu

Edit the `##` chapter headings and `###` section headings in `chapters/`.
The HTML/PDF contents menu is generated from those headings, with links to
each section. For example:

```markdown
### **5.1 Getting Started with Arduino IDE** {.section-page}
```

Keep section numbers in order when adding or moving headings. The
`{.section-page}` marker is a heading class; it is omitted from the visible
contents text. The Markdown/DOCX contents list is also generated from the
same headings during the build.

## Local build

Requirements:

- Pandoc
- WeasyPrint

Run from the repository root:

```bash
./tools/product-reference/build.sh
```

Generated files are written to `build/product-reference/`:

```text
unit_product_reference_v_1_0_0_ue0085_tcan1051hvd_can_transceiver_module.md
unit_product_reference_v_1_0_0_ue0085_tcan1051hvd_can_transceiver_module.docx
unit_product_reference_v_1_0_0_ue0085_tcan1051hvd_can_transceiver_module.html
unit_product_reference_v_1_0_0_ue0085_tcan1051hvd_can_transceiver_module.pdf
```
