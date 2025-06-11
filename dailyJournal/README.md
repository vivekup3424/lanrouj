## Journal for me to write things on this everyday.

### Instrutions for adding image
Here’s a clear step-by-step guide to link or embed an image from Google Drive using Markdown or HTML: 

### **To Embed an Image Using Markdown:**

1. **Ensure the Image is Public:**
   - Go to Google Drive and open the file.
   - Click on the "Share" button.
   - Set sharing to "Anyone with the link" and ensure it’s set to "Viewer."

2. **Get the Direct Image URL:**
   - Google Drive doesn’t provide a straightforward direct URL for Markdown. Instead, use a workaround to show a preview image.

   **Markdown Syntax for Image Link:**
   ```markdown
   [![Image Preview](https://drive.google.com/uc?id=11x-0hDstht0lVcV1MpbPNq-b8gnL6l42)](https://drive.google.com/file/d/11x-0hDstht0lVcV1MpbPNq-b8gnL6l42/view?usp=sharing)
   ```
 jlajkc kj
   - `https://drive.google.com/uc?id=11x-0hDstht0lVcV1MpbPNq-b8gnL6l42` is used to display the image preview.
   - `https://drive.google.com/file/d/11x-0hDstht0lVcV1MpbPNq-b8gnL6l42/view?usp=sharing` is the link to view the file.

3. **Add the Markdown to Your Document:**
   Paste the above Markdown code into your document where you want the image to appear.

### **To Embed an Image Using HTML (If Markdown Doesn’t Work):**

1. **Ensure the Image is Public:**
   - Same as above, ensure the image is shared publicly.

2. **Use the Embed URL:**
   Convert the Google Drive preview link for embedding.

   **HTML Embed Code:**
   ```html
   <iframe src="https://drive.google.com/file/d/11x-0hDstht0lVcV1MpbPNq-b8gnL6l42/preview" width="640" height="480" allow="autoplay"></iframe>
   ```

3. **Add the HTML to Your Document:**
   - If your documentation platform supports HTML, paste this code where you want the image to appear.

### **Summary:**

- **Markdown**: Use the provided Markdown link for image previews.
- **HTML**: Use the `<iframe>` tag for embedding if Markdown is not supported or if you need to display the image in its full size.

Choose the method that fits your documentation platform's capabilities.
