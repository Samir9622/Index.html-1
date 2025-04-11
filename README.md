<div class="navigation">
  <a href="/Tools">Home</a> | 
  <a href="/index.html-2">Tool Version 1</a> | 
  <a href="/Tools-index.html-2">Tool Version 2</a>
</div>
# Index.html
<!DOCTYPE html>

 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Image Compression Tool</title>
  <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-9354903383"
          crossorigin="anonymous"></script>
  <style>
</head>
<body>
  <div class="container">
    <h1>Image Compression Tool</h1>
    <!-- AdSense Bottom Placement -->
    <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-9055111364"
            crossorigin="anonymous"></script>
    <!-- Rest of the body content remains the same --> <style>
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

  <h1>Image Compressor</h1>ad-container {
  max-width: 1200px;
  padding: 0 20px;
  margin: 0 auto;
}

ins.adsbygoogle {
  border-radius: 8px;
  overflow: hidden;
}

  <div id="drop-area">
    <p>Drag & Drop an image here</p>
    <p>or</p>
    <label class="btn" for="fileElem">Select File</label>
    <input type="file" id="fileElem" accept="image/*">
  </div>

  <div id="preview"></div></section></header>

<!-- Top Ad -->
<div class="ad-container" style="margin: 20px auto; text-align: center;">
  <ins class="adsbygoogle"
       style="display:block"
       data-ad-client="ca-app-pub-8773480799818158"
       data-ad-slot="9354903383"
       data-ad-format="auto"
       data-full-width-responsive="true"></ins>
  <script>(adsbygoogle = window.adsbygoogle || []).push({});</script>
</div>

<section class="hero">



</section>

<!-- Bottom Ad -->
<div class="ad-container" style="margin: 40px auto; text-align: center;">
  <ins class="adsbygoogle"
       style="display:block"
       data-ad-client="ca-app-pub-8773480799818158"
       data-ad-slot="9055111364"
       data-ad-format="auto"
       data-full-width-responsive="true"></ins>
  <script>(adsbygoogle = window.adsbygoogle || []).push({});</script>
</div>

<footer><footer>

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
