#Citations for code:
#Pillow documentation: https://pillow.readthedocs.io/en/stable/reference/index.html
#Regexone: https://regexone.com/
#Simple API in Python tutorial on YouTube: https://www.youtube.com/watch?v=hpc5jyVpUpw&ab_channel=VideoLab
#os.walk suggestion: https://stackoverflow.com/questions/1724693/find-a-file-in-python
#Being able to utilize ImageChops.difference() and ImageStat.Stat() from PIL documentation to calculate difference percentage: https://github.com/victordomingos/optimize-images/blob/master/optimize_images/img_dynamic_quality.py
#To check http:// https:// regex match: https://stackoverflow.com/questions/4643142/regex-to-test-if-string-begins-with-http-or-https

from PIL import Image, ImageStat, ImageChops
import requests
from io import BytesIO
import re 
import os

api_key = 'A2jsd23kasjd92183Kkuiajd'

pattern = re.compile("^https?://(.*)") #Pattern to identify website image URLs by matching an http:// or https:// with the input

headers = {"Authorization": api_key } #Utilizes the variable "headers" for authentication using the api_key

firstim = str(input("What is the link (url or name.jpg) to the first image? ")) #Initializes the process of asking the user for the first input 
if pattern.match(firstim): #Checks if the input matches the format of a website URL
  firstim_resp = requests.get(firstim, headers = headers) #Makes an API request to the website the image is found on (I tested using "Open image in new tab" in Google Images)
  image1 = Image.open(BytesIO(firstim_resp.content)) #Assigns a variable that holds the content of the image
else:
  for root, dirs, files in os.walk(".", topdown=False): #Searches in all directories and files for the first image if the input is not a URL
   for name in files: 
       if name == firstim:
           route = os.path.join(root, name) #If a file is found with the name of the input, the path of the image is saved to a variable
   with open(route, 'rb') as fi:
    image1 = Image.open(BytesIO(fi.read())) #Opens the pathing of the image file and reads the contents of the image, assigning it to a variable

secondim = str(input("What is the link (url or name.jpg) to the second image? ")) #Initializes the process of asking the user for the second input 
if pattern.match(secondim): #Checks if the second input matches the pattern for that of a website URL
  secondim_resp = requests.get(secondim,  headers = headers) #Makes an API request to get the the image
  image2 = Image.open(BytesIO(secondim_resp.content)) #Assigns the contents of the image to a variable
else:
  for root, dirs, files in os.walk(".", topdown=False): #Searches all directories for an image file with the name of the second input
   for name in files:
       if name == secondim:
           sroute = os.path.join(root, name) #After checking all files, if a file is found with the name of the second input, a variable is assigned to the pathing of the image
  with open(sroute, 'rb') as si:
    image2 = Image.open(BytesIO(si.read())) #Opens the file pathing for the second image and assigns a variable to the image read
    
Difference_In_Images = ImageChops.difference(image1, image2) #Utilize the ImageChops module in PIL to find the pixel-by-pixel differences between the two images found
Stats_Of_Dif = ImageStat.Stat(Difference_In_Images) #Retrieves the statistics for the differences of the two images
Ratio = sum(Stats_Of_Dif.mean) / (len(Stats_Of_Dif.mean) * 255) #Uses the method of summing up the average pixel level in each band of the images and divdes them by the quantity 255 (range of light for pixels) * the length of the means 
print("\nThere is a " + str(Ratio * 100) + "% difference between the images.") #Multiplies the Ratio by 100 to get the percentage difference, prints it out
