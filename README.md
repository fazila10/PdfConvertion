# PdfConvertion

**Before the code installation:**
```
pip3 install PIL
pip3 install pytesseract
pip3 install pdf2image
sudo apt-get install tesseract-ocr
```
**Code:**
```
from PIL import Image
import pytesseract
import sys
from pdf2image import convert_from_path
import os

PDF_file = "new.pdf"							//opens
pages = convert_from_path(PDF_file, 500)				//counter pages to stores images
image_counter = 1
for page in pages:
    filename = "page_"+str(image_counter)+".jpg"			//save each page
    page.save(filename, 'JPEG')
    image_counter = image_counter + 1
filelimit = image_counter-1
outfile = "out_text.txt"						//create output file
f = open(outfile, "a")							//opens in append mode
for i in range(1, filelimit + 1):
    filename = "page_"+str(i)+".jpg"					
    text = str(((pytesseract.image_to_string(Image.open(filename)))))
    text = text.replace('-\n', '') 
    f.write(text)							//writes in file
f.close()
```


**ERRORS:**
To change from jovyan to root:  (https://github.com/jupyter/docker-stacks/issues/408) 	//TO USE SUDO
docker exec -it -u root container_id bash   //no password required

Password issue:
tried url pasting multiple times.

Unable to locate package tesseract-ocr(https://github.com/codenvy/codenvy/issues/1068)
	->sudo apt-get update
	->sudo apt-get install tesseract-ocr 		//doesnt work if executed first.

to find number of pages(https://github.com/Belval/pdf2image/issues/25)
	->sudo apt-get install -y poppler-utils
Get path:(https://linuxize.com/post/python-get-change-current-working-directory/#:~:text=To%20find%20the%20current%20working,chdir(path)%20.)
```
import os
os.getcwd()
```
