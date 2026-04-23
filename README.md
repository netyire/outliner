-----

# 📑 Outliner

**Transforming Static PDFs into Mobile-Ready Structured Content**

This guide outlines a comprehensive workflow that leverages the Gemini CLI to coordinate specialized processing agents. By passing your documents through these tailored scripts, you can seamlessly convert rigid, static PDFs into dynamic, mobile-optimized outlines.

-----

### **Phase 1: Document Segmentation**

The first step is breaking your source material down into manageable chapters using the Gemini CLI. Choose the specific agent below that best matches your document's original format.

| Document Type | Recommended Agent | Description & Execution |
| :--- | :--- | :--- |
| **Standard Digital Books** | `SplitMimo.md` | Automatically identifies chapter breaks by analyzing the Table of Contents (TOC) and font size variations. Built on Xiaomi's Mimoclaw (Mimo-V2) logic.<br><br>**Command:** `Execute SplitMimo.md on input.pdf` |
| **Scanned Spreads** | `SplitPhotoDouble.md` | Perfect for two-page scans (e.g., from CamScanner). It intelligently handles overlapping page boundaries and verifies content coverage.<br><br>**Command:** `Execute SplitPhotoDouble.md on input.pdf` |
| **Custom Ranges** | `Split.md` | Designed for manual page targeting. It cleans up filenames and automatically pulls metadata (like Title and Author) to generate appropriate folder names.<br><br>**Command:** `Execute Split.md on input.pdf` |

-----

### **Phase 2: Data Extraction & Structuring**

Once your document is split, the next step is extracting the core information. Upload your newly divided chapter PDFs to either DeepSeek (Expert Mode) or Gemini 3.1 Pro (highly recommended if your document contains complex equations or embedded images).

You will need to attach two specific gateway files to guide the extraction process:

  * `Outliner.md` (Handles the structural framework)
  * `OutlinerAdditionalRequirements.md` (Manages formatting and mathematical elements)

> **Primary Command:** \> `"Apply md to the pdf, output always in code block"`

*Alternative Automation:* You can also run `Outline.md` directly within the Gemini-CLI to process the split chapters automatically. While this minimizes manual input, be aware that the per-step processing time is noticeably slower.

> **Automated Command:** \> `"Apply Outline.md to <Target books>."`

-----

### **Phase 3: Content Refinement & Workspace Organization**

Head back to the Gemini CLI to build out your directory structure and elevate the quality of your extracted text.

**1. Initialize the Workspace**
Set up your foundational file structure to mirror your chapters.

> `"Create empty placeholder .md files for [Target books] in the /MarkDown directory, named exactly after the split chapter PDFs."`

**2. Clarify and Simplify**
If the source material is overly dense, use the `RewriteClearly.md` agent. This script simplifies the vocabulary and shifts the text into the active voice, optimizing it for a standard P6 reading comprehension level.

> `"Execute RewriteClearly.md on <Target books>'s Markdown files."`

**3. Bridge Informational Gaps**
Use `AnswerQuestions.md` to run a deep contextual search on your content. This step replaces any empty placeholders with comprehensive, substantive answers.

> `"Execute AnswerQuestions.md on <Target book>'s Markdown files."`

**4. Optimize for Discovery**
Finally, make your outlines highly scannable by running `UpdateTags.md`. This generates concise "What's this chapter about?" summaries and embeds relevant keyword blocks.

> `"Execute UpdateTags.md to regenerate chapter headers and tags for <Target books>."`

-----

### **Phase 4: Mobile HTML Compilation**

With your Markdown files refined and fully fleshed out, it's time to compile them into their final, mobile-friendly state.

> **Command:** \> `"Execute ConvertMDtoHTML.md on all unprocessed md books."`

-----

### **Phase 5: Environment Maintenance**

To prevent workflow bottlenecks in the future, routinely sync your documentation and agent directories with your latest scripts.

> **Command:** \> `"Execute UpdateREADMEandAGENTS.md"`

Quick start video: https://sourceforge.net/projects/sourceforge2342026/files/Quick%20Start%20Screencast.tar.zst/download
