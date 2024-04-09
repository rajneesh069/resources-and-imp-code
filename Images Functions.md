# Images.tsx function explanations :-

### 1. Handle Image Drop Function :-
```typescript

 const handleImageDrop = (e: DragEvent<HTMLDivElement>) => {
    e.preventDefault();
    const files = e.dataTransfer.files;
    const filesArray = Array.from(files);
    if (files && files.length >= 1) {
      const validFiles: string[] = [];
      filesArray.forEach((file) => {
        const reader = new FileReader();
        reader.onload = () => {
          const base64String = reader.result as string;
          const image = new Image();
          image.src = base64String;
          image.onload = () => {
            if (
              image.height <= 1000 &&
              image.width <= 1000 &&
              file.size <= maxFileSizeInMB
            ) {
              validFiles.push(base64String);
            } else {
              if (file.size > maxFileSizeInMB) {
                alert("Please select an image with size less than 1MB");
              } else if (image.height > 1000 || image.width > 1000) {
                alert(
                  "Please select an image with dimensions less than 1000x1000."
                );
              }
            }
            setSelectedImages((prevImages) => [...prevImages, ...validFiles]);
            setValue("images", [...selectedImages, ...validFiles], {
              shouldDirty: true,
              shouldTouch: true,
            });
          };
        };
        reader.readAsDataURL(file);
      });
    }
  };

  ```

### Explanation :-
1. `e.preventDefault();`: This prevents the default behavior of the browser when a file is dropped onto a webpage, which is typically to open the file or navigate to it.

2. `const files = e.dataTransfer.files;`: This retrieves the files that were dropped onto the webpage from the `dataTransfer` property of the `DragEvent`.

3. `const filesArray = Array.from(files);`: This converts the `FileList` object into an array so that it can be easily iterated over.

4. `if (files && files.length >= 1) {`: This checks if any files were dropped onto the webpage.

5. `const validFiles: string[] = [];`: This initializes an array to store the valid base64 strings of the dropped images.

6. `filesArray.forEach((file) => { ... });`: This iterates over each file that was dropped.

7. `const reader = new FileReader();`: This creates a new `FileReader` object, which is used to read the contents of the dropped file.

8. `reader.onload = () => { ... };`: This sets up an event handler to be called when the file reading operation is completed.

9. `const base64String = reader.result as string;`: Inside the `onload` event handler, this retrieves the result of the file reading operation as a base64-encoded string.

10. `const image = new Image();`: This creates a new `Image` object, which is used to load and manipulate images in JavaScript.

11. `image.src = base64String;`: This sets the source of the image to the base64-encoded string obtained from the dropped file. Setting the `src` property triggers the loading of the image.

12. `image.onload = () => { ... };`: This sets up an event handler to be called when the image has finished loading.

13. Inside the `onload` event handler for the image:
    - It performs checks on the dimensions and size of the image.
    - If the image passes the checks, its base64 string is added to the `validFiles` array.
    - If the image fails the checks, an alert is displayed to the user.

14. `reader.readAsDataURL(file);`: This initiates the reading of the dropped file as a data URL, which represents the file's data as a base64-encoded string.

15. After all files have been processed, the valid base64 strings are added to the `selectedLogoFiles` array and set as the value of `logoImages` using the `setValue` function. The `shouldDirty` and `shouldTouch` options are provided to indicate that the form field has been modified and touched.

