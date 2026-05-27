# Image Assets for ReADL Project Page

Place the following images extracted from the paper PDF in this directory:

## Required Images

| Filename | Source | Description |
|----------|--------|-------------|
| `framework.png` | Figure 2 in paper | Overall ReADL framework overview |
| `token_attention.png` | Figure 1 in paper | Token-to-patch attention visualization ("Key Insight") |
| `qualitative_comparison.png` | Figure 6 in paper/supp | Comparison with GPT-4.1, Triad, AnomalyGPT, EIAD |
| `consistency_reward.png` | Figure 5 in supp | Impact of consistency reward (Qwen2.5-VL-7B vs +R1 vs +CGRO) |
| `token_selection.png` | Figure 4 in paper | Token selection visualization (all tokens, SI, ST, SI+ST) |
| `failure_cases.png` | Figure 7 in supp | Failure case analysis |
| `main_results.png` | Table 1 in paper | Main results comparison table |
| `ablation_main.png` | Table 2 in paper | ReAL + CGRO ablation study table |
| `ablation_token.png` | Table 3 in paper | Token selection ablation table |

## Tips for Extracting from PDF

Using PyMuPDF (fitz):

```python
import fitz
doc = fitz.open("paper.pdf")
page = doc[page_num]  # 0-indexed
pix = page.get_pixmap(dpi=300)
pix.save("output.png")
```

Or extract all images:
```python
import fitz
doc = fitz.open("paper.pdf")
for i, page in enumerate(doc):
    for img in page.get_images(full=True):
        xref = img[0]
        base = doc.extract_image(xref)
        with open(f"image_{i}_{xref}.{base['ext']}", "wb") as f:
            f.write(base["image"])
```
