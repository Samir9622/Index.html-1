# Index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Image Compressor</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
      background-color: #f4f4f4;
    }

    h1 {
      margin-bottom: 20px;
    }

    #drop-area {
      border: 2px dashed #ccc;
      border-radius: 10px;
      padding: 30px;
      background: white;
      cursor: pointer;
      transition: background 0.3s;
    }

    #drop-area:hover {
      background: #f0f0f0;
    }

    #fileElem {
      display: none;
    }

    .btn {
      display: inline-block;
      margin-top: 15px;
      padding: 10px 20px;
      background: #28a745;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
    }

    #preview img {
      max-width: 100%;
      margin-top: 10px;
    }

    #preview {
      margin-top: 30px;
    }
  </style>
</head>
<body>

  <h1>Image Compressor</h1>

  <div id="drop-area">
    <p>Drag & Drop an image here</p>
    <p>or</p>
    <label class="btn" for="fileElem">Select File</label>
    <input type="file" id="fileElem" accept="image/*">
  </div>

  <div id="preview"></div>

  <script>
    const dropArea = document.getElementById("drop-area");
    const fileInput = document.getElementById("fileElem");
    const preview = document.getElementById("preview");

    ["dragenter", "dragover", "dragleave", "drop"].forEach(eventName => {
      dropArea.addEventListener(eventName, e => {
        e.preventDefault();
        e.stopPropagation();
      });
    });

    dropArea.addEventListener("drop", handleDrop, false);
    fileInput.addEventListener("change", handleFiles, false);

    function handleDrop(e) {
      const dt = e.dataTransfer;
      const files = dt.files;
      handleFiles({ target: { files } });
    }

    function handleFiles(e) {
      const files = e.target.files;
      if (!files.length) return;

      const file = files[0];
      if (!file.type.startsWith("image/")) {
        alert("Please upload an image file.");
        return;
      }

      const reader = new FileReader();
      reader.onload = function(event) {
        const img = new Image();
        img.src = event.target.result;

        img.onload = function() {
          const canvas = document.createElement("canvas");
          const scale = 0.5; // Compress to 50%
          canvas.width = img.width * scale;
          canvas.height = img.height * scale;
          const ctx = canvas.getContext("2d");
          ctx.drawImage(img, 0, 0, canvas.width, canvas.height);

          canvas.toBlob(blob => {
            const compressedUrl = URL.createObjectURL(blob);
            preview.innerHTML = `<h3>Compressed Image Preview:</h3><img src="${compressedUrl}" alt="Compressed Image">`;
          }, "image/jpeg", 0.7); // Adjust quality (0.1–1)
        };
      };
      reader.readAsDataURL(file);
    }
  </script>

</body>
</html>
