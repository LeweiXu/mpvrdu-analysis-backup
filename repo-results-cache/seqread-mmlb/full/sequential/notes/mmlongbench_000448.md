## Turn 1 — document page 7 (rank 1 of 20)

Fig. 3: Extending our multimodal retriever to zero-shot recognition on object detection datasets such as LVIS [14] and V3Det [48]. Compared to the classification datasets, we apply the additional pre-processing techniques such as cropping and resizing to extract the image embeddings.

The figure shows a diagram with two main parts: (a) Pre-process and (b) Embedding & Retrieve.

In part (a) Pre-process:
- An input image is shown with three bounding boxes labeled bbox1, bbox2, and bbox3.
- Each bounding box is cropped and resized.
- The cropped images are then fed into a visual encoder.

In part (b) Embedding & Retrieve:
- The cropped images are embedded into a memory index.
- The memory index is labeled "Memory M" and contains entries like:
  - bbox1: carnation, bouquet, flower arrangement
  - bbox2: pepper, milk, subshaker, chopping board
  - bbox3: flowerpot, vase, glass, drink, container
- The system retrieves top-k categories based on similarity.

## Turn 2 — document page 21 (rank 2 of 20)

## Fig. 7: GPT4V Example for Stanford Cars and FGVC Aircraft

This figure presents two examples of the RAR (Retrieving And Ranking Augmented MLLMs) pipeline applied to zero-shot recognition.

**Left Panel (Stanford Cars):**
- Input: An image of a red car.
- Prompt: "Please play the role of a classification expert, and sort the provided categories from high to low according to the top 5 similarity with the input image. Here are the optional categories: ['2012 Aston Martin V8 Vantage Convertible', '2012 Aston Martin Virage Coupe', '2012 Aston Martin Virage Convertible', '2012 Audi TTS Coupe', '2012 Aston Martin V8 Vantage Coupe']"
- Output Ranking:
  1. 2012 Aston Martin V8 Vantage Coupe
  2. 2012 Aston Martin Virage Coupe
  3. 2012 Aston Martin V8 Vantage Convertible
  4. 2012 Audi TTS Coupe
  5. 2012 Aston Martin Virage Convertible
- Reasoning: The car is an Aston Martin, resembling the Vantage model line. It is a coupe, not a convertible, so coupes are ranked higher. The Audi TTS Coupe, while also a coupe, is from a different manufacturer and has distinct styling cues.

**Right Panel (FGVC Aircraft):**
- Input: An image of an aircraft.
- Prompt: "Please play the role of a classification expert, and sort the provided categories from high to low according to the top 5 similarity with the input image. Here are the optional categories: ['737-800', '757-300', '767-200', 'A340-300', 'MD-90']"
- Output Ranking:
  1. 757-300
  2. 767-200
  3. MD-90
  4. 737-800
  5. A340-300
- Reasoning: The aircraft is a Boeing 757, identifiable by its long fuselage, narrow-body, and characteristic nose shape. The -300 series has an extended fuselage, matching the aircraft. The 767-200 and MD-90 have some similarities but differ in design elements. The 737-800 is shorter with a different wing design. The A340-300 is a wide-body with four engines, making it distinct.

The figure also includes a caption explaining that green indicates ground truth and blue indicates characteristics analyzed by GPT-4V.

## Turn 3 — document page 13 (rank 3 of 20)

## Fig. 5: Visualization of the ranking examples for zero-shot object recognition on LVIS [14] validation set.

The figure displays two example images from the LVIS validation set, each with a corresponding "Retrieved" and "Re-ranked" section.

**Top Example:**
- **Image:** Shows a black object that appears to be a pair of shoes or a similar item.
- **Retrieved (Original predictions):** A list of retrieved object categories including: `['earring', 'peanut', 'mail_shoe', 'earring', 'scrabbing_brush']`.
- **Re-ranked (MLLM-selected):** The final selected label is `earring`.

**Bottom Example:**
- **Image:** Shows a person wearing a white shirt and holding a tennis racket.
- **Retrieved (Original predictions):** A list of retrieved object categories including: `['glove', 'podo_shirt', 'short_pants']`.
- **Re-ranked (MLLM-selected):** The final selected label is `short_pants`.

The figure caption explains that the CLIP&K-NN approach provides an extensive list of object predictions, but the most accurate label might not always be top-1. The RAR method uses MLLMs to select the correct class names accurately.

## Turn 4 — document page 6 (rank 4 of 20)

## Fig. 2: Pipeline of RAR

This figure illustrates the overall pipeline of the RAR (Retrieving And Ranking Augmented MLLMs) method, divided into two main parts: (a) Multimodal Retriever and (b) Retrieving & Ranking.

In part (a) Multimodal Retriever:
- An input image is processed to extract image embeddings.
- These embeddings are stored in an external memory M.
- An index system (using HNSW algorithm) is used to facilitate fast retrieval.

In part (b) Retrieving & Ranking:
- For inference, top-k categories are retrieved from memory M.
- These retrieved categories are then refined by MLLMs through a ranking process to produce the final prediction.

The figure also includes a diagram showing the flow: Image → Embeddings → Memory M → Retrieved Top-k Categories → Ranking → Final Prediction.

## Turn 5 — document page 9 (rank 5 of 20)

This page discusses the experimental setup for the RAR method, including datasets and implementation details. It mentions the LVIS dataset (164,000 images, 1,203 categories) and V3Det dataset (13,204 categories). It specifies that for retrieval, k=5 top-k results are used, except k=4 in the 4-shot few-shot setting. The page also describes using a frozen CLIP ViT B/16 model and the HNSW algorithm for retrieval. However, this page does not contain any figure or diagram showing bounding boxes or object detection results.

## Turn 6 — document page 12 (rank 6 of 20)

This page contains Tables 3 and 4 showing zero-shot object recognition results on LVIS and V3Det datasets, respectively. It also includes text discussing performance comparisons, particularly highlighting the RAR method's advantage for rare classes and its effectiveness on V3Det. The page references Fig. 5 for qualitative results but does not contain the figure itself. There is no mention of bounding boxes or any visual content showing object detection results on this page.
