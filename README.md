import requests
from bs4 import BeautifulSoup
import random

def get_random_picture(url):
    # Send a GET request to the specified URL
    response = requests.get(url)
    
    # Check if the request was successful
    if response.status_code == 200:
        # Parse the HTML content of the webpage
        soup = BeautifulSoup(response.content, 'html.parser')
        
        # Find all image tags
        img_tags = soup.find_all('img')
        
        # Extract the src attribute from each image tag
        image_sources = [img['src'] for img in img_tags]
        
        # Filter out image sources that are empty or None
        image_sources = [src for src in image_sources if src]
        
        # Select a random image source from the list
        random_image_source = random.choice(image_sources)
        
        # Print the selected image source
        print("Random Image Source:", random_image_source)
        
        # Return the selected image source
        return random_image_source
    else:
        # If the request was not successful, print an error message
        print("Error: Failed to fetch URL:", url)
        return None

# Example usage:
url = "https://www.flickr.com/search/?text=tractor"
random_picture_url = get_random_picture(url)
