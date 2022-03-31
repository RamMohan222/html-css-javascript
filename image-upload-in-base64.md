# image-upload-in-base64
Image upload in base64 format

## Image to base64
```js
import fs from 'fs';

const imageAsBase64 = fs.readFileSync('/path/to/file.jpg', {encoding: 'base64'});
```

## base64 to image
```js
import fs from 'fs';

const imageAsBase64 = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgA';
// Remove header
const base64Image = imageAsBase64.split(';base64,').pop();
fs.writeFile('image.png', base64Image, {encoding: 'base64'}, (err) => {
    console.log('File created');
});
// Don’t forget the {encoding: 'base64'}
```
