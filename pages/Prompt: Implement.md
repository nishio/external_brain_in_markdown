
しっかりコメントを書けばいいという話を聞いて、むしろプロンプトではなくコメントに書くのを試した

prompt

```
Implement
```
...
```
```

python

```
def upload_images_to_gyazo(directory, ext="jpg"):
    """
    Uploads all images in the given directory to Gyazo.
    
    Args:
    - directory (str): The directory containing the images to upload.
    
    Returns:
    None
    """
    # Get all image files in the directory
    image_files = [f for f in os.listdir(directory) if f.endswith(f".{ext}")]
    print(f"In {directory}, Num images: {len(image_files)}")

    # Sort the image files by index
    # Images may be `page-99.jpg` and `page-100.jpg`, so we need to sort by the page number.
    # Page number is continuous number before the last period.


    # Upload each image to Gyazo
    # Each upload returns a JSON object with the URL to the uploaded image.
    # We want to store them in a local JSON file for later use.
    # Save after each API call so that we don't lose data if the script crashes.
    for image_file in image_files[:3]:

        ret = upload_one_image_to_gyazo(image_file, directory)
```


[result](https://chat.openai.com/share/b03d8b09-41b9-4f1b-bc28-edfa00325878)
