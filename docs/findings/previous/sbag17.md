See findings and complete materials from the meeting on [Zenodo](https://zenodo.org/records/21705238){ target="_blank" }.

<div id="finding-pdf">Loading PDF preview…</div>

<script>
{
  const container = document.getElementById("finding-pdf");

  const recordId = "21705238";
  const filename = "Findings from SBAG 17_Jun12-14_2017.pdf";

  // Encoding matters for spaces, #, ?, parentheses, and other characters.
  const pdfUrl =
    `https://zenodo.org/api/records/${recordId}/files/` +
    `${encodeURIComponent(filename)}/content`;

  console.log("Requesting Zenodo PDF:", pdfUrl);

  fetch(pdfUrl)
    .then(async response => {
      console.log("Zenodo response:", {
        status: response.status,
        statusText: response.statusText,
        type: response.type,
        url: response.url,
        redirected: response.redirected,
        contentType: response.headers.get("content-type")
      });

      if (!response.ok) {
        throw new Error(
          `Zenodo returned ${response.status} ${response.statusText}`
        );
      }

      return response.arrayBuffer();
    })
    .then(bytes => {
      console.log(`Received ${bytes.byteLength} bytes`);

      const blob = new Blob([bytes], { type: "application/pdf" });
      const objectUrl = URL.createObjectURL(blob);

      const iframe = document.createElement("iframe");
      iframe.src = objectUrl;
      iframe.title = filename;
      iframe.style.width = "100%";
      iframe.style.height = "80vh";
      iframe.style.minHeight = "600px";
      iframe.style.border = "1px solid #ddd";

      container.replaceChildren(iframe);
    })
    .catch(error => {
      console.error("PDF preview failure:", error);
      container.textContent =
        `The PDF preview could not be loaded: ${error.message}`;
    });
}
</script>