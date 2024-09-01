The above preporcessing is done with taking care of the things discussed below.
**Preprocessing and Cleaning Steps for Legal Documents**

1. **Download and Extract Metadata**:
   - **Download PDFs**: Access and download the judgment reports from the Indian Kanoon website (or any other publicly available websites).
   - **Extract Metadata**: Extract and save metadata such as details about judges, appellants, respondents, case document types (e.g., civil, criminal), appeal numbers, and reportability status into a separate sheet (with the help of regular expression matching the pattern).

2. **Text Extraction and Initial Cleanup**:
   - **Remove URLs**: Delete all URLs present in the text (especially in the footer).
   - **Remove Unnecessary Characters**: Eliminate non-alphanumeric characters that do not contribute to the content's meaning.
   - **UTF-8 Encoding**: Ensure the text is correctly encoded in UTF-8, removing any non-UTF-8 characters.
   - **Remove Page Numbers**: Strip out page numbers from the text.
   - **Filter Short Cases**: Discard cases where the token length is less than 100, as they may not be substantial enough for analysis.

3. **Metadata and Special Cases Removal**:
   - **Remove Unwanted Tokens**: Delete specific tokens such as “wp253.21.odtwp253.21.odt”, "J U D G E M E N T", "R E P O R T A B L E", "Uploaded", and "Downloaded" etc.
   - **Remove Redundant New Lines**: Consolidate redundant new lines to ensure a clean text flow.
   - **Remove Pre-keyword Text**: Exclude all text preceding keywords like "ORDER" or "JUDGMENT" to focus on relevant content.

4. **Header and Footer Removal**:
   - **Remove Footer Text**: Strip out footer text, including website links.
   - **Identify and Remove Headers**:
     - Find the line with the maximum overlap with the filename.
     - Remove this identified header line based on its similarity to the filename.
     - (This approach assumes that the header line in the PDF is similar or identical to the filename, which is why the overlap with the filename is used as a criterion to identify the header.)
     - Example: header in pdf is "A.M. Mohan vs The State Rep By Sho on 20 March, 2024" and file name is "A_M_Mohan_vs_The_State_Rep_By_Sho_on_20_March_2024".

5. **Handle Abbreviations**:
   - **Compile Abbreviation List**: Identify and list unique abbreviations (e.g., U.S.A., Ph.D., CEO, Inc., Ltd., Co., Mr., Dr., Ms.).
   - **Adjust Sentence Detection**:
     - Avoid treating abbreviations as sentence boundaries.
     - Traverse the document to identify abbreviations and prevent incorrect sentence segmentation.

6. **Final Cleanup**:
   - **Ensure Sentence Completeness**: Reassess sentence boundaries, considering unique abbreviations to avoid false sentence breaks.
   - **Maintain Grammatical Structure**: Avoid stemming and lemmatization to preserve the grammatical structure and meaning of sentences.

Following these steps, one can effectively preprocess and clean legal documents extracted from PDFs, ensuring that metadata is properly handled and the text is formatted for further analysis.
