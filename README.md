
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Downtik - TikTok Downloader</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f7f7f7;
      color: #333;
      margin: 0; padding: 0;
    }
    header {
      background: #ff2c55;
      color: white;
      padding: 30px 0;
      text-align: center;
    }
    header h1 {
      margin: 0;
      font-size: 36px;
    }
    .container {
      max-width: 600px;
      margin: 40px auto;
      background: white;
      padding: 30px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    input[type="text"] {
      width: 100%;
      padding: 15px;
      font-size: 16px;
      margin-bottom: 20px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      width: 100%;
      background: #ff2c55;
      color: white;
      font-size: 18px;
      padding: 14px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background: #e02649;
    }
    .result {
      margin-top: 30px;
      text-align: center;
      display: none;
    }
    .result video {
      max-width: 100%;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
  </style>
</head>
<body>
<header>
<h1>Downtik - TikTok Downloader</h1>
</header>
<div class="container">
  <input type="text" id="videoUrl" placeholder="Paste TikTok video link here..." />
  <button onclick="downloadVideo()">Download</button>
  <div class="result" id="result">
    <h3>Preview:</h3>
    <video id="videoPreview" controls></video><br/><br/>
    <a id="downloadLink" href="#" download>Download Video</a>
  </div>
</div>
<script>
  async function downloadVideo() {
    const url = document.getElementById('videoUrl').value.trim();
    if (!url.includes("tiktok.com")) {
      alert("Please enter a valid TikTok URL.");
      return;
    }
    try {
      const res = await fetch('https://api.tikmate.app/api/lookup?url=' + encodeURIComponent(url));
      if (!res.ok) throw new Error('Failed to fetch video info');
      const data = await res.json();
      const videoUrl = data.download.no_watermark[0];
      document.getElementById('videoPreview').src = videoUrl;
      document.getElementById('downloadLink').href = videoUrl;
      document.getElementById('result').style.display = 'block';
    } catch {
      alert('Failed to fetch video. Try again later.');
    }
  }
</script>
</body>
</html>