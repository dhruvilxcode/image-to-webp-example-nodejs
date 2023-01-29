# image to webp example


Convert Image (JPG/PNG) to WebP for good compression and better performance. Resulting in faster website load.

[https://www.npmjs.com/package/image-to-webp](https://www.npmjs.com/package/image-to-webp)

### Installation

```bash
npm install
```

### Code Example

```javascript
const fs = require("fs");
const express = require("express");
const formidable = require("formidable");
const { imageToWebp } = require("image-to-webp");

const app = express();

app.post("/upload", async (req, res) => {
    const form = formidable({ multiples: false });
    form.parse(req, async (err, fields, files) => {
        if (err) {
          next(err);
          return;
        }


        const image = files.image.filepath;
        console.log(image);

        const webpImage = await imageToWebp(image, 30);
        console.log(webpImage);

        // now you can copy this file to public directory or simply upload to your cloud storage provider like AWS S3 / Cloudinary / Google Cloud Storage
        fs.copyFileSync(webpImage, "./public/images/myimg.webp");

        res.json({ image, webpImage });
    });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on the ${PORT}`);
});

```

